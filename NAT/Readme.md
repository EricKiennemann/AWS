# Enable ping to google.com from an instance in a private subnet

## Framework : 

We have two subnet :

  - Subnet 1 : which is public. One instance (I1) and connected to an
    internet gateway :

  - Subnet 2 : which is private. One instance (I2) and no connection to
    interner

## Step 1) be able to connect to I1 from a PC at home connected to the internet

Install « putty » software on the « home PC »

Setup the connection on putty to access to the instance I1. For this :

1)  Get the public ip adress of the I1 instance on AWS console

![](.//media/image1.png)

2)  Setup the connection on putty

![](.//media/image2.png)

3)  Convert the private key(\*.pem file) provided by AWS when creating
    the instance to a (\*.pkk file) accepted by putty. For this use the
    tool «PuttyGen » installed at the same time as putty

![](.//media/image3.png)

Load the « \*.pem » file and generate a « \*.pkk » file

![](.//media/image4.png)

4)  Setup putty with this \*.ppk key

![](.//media/image5.png)

5)  To improve security access to your I1 instance it is a good idea to
    restrict the access to your I1 by ssh to your « home PC » : for this
    go to your instance I1 in AWS console and change the « inbound
    rules » of the security group associated to your instance (I1)

Below, the SSH/TCP protocol has been modified to add a « source » which
is the « home PC » public IP adress.

At the same time I added a rule to authorize ping (ICMP v4) from this
home PC too

![](.//media/image6.png)

6)  Access from the « home PC » should now work using putty with ssh and
    ping also

![](.//media/image7.png)

## 

## Step 1bis) : connect directly from the Windows Subsystem Linux (WSL)

1)  Install WSL on the local PC

Procedure available at :
<https://docs.microsoft.com/fr-fr/windows/wsl/install-win10>

2)  Connect using wsl

<!-- end list -->

  - change the rights on the key file: chmod 400 S20KEYPAIREK.pem

  - connect to private instance with ssh : « sudo ssh -i
    "S20KEYPAIREK.pem" ec2-user@xxxxx

![](.//media/image8.png)

## Step 2) : Modify the instance (I2) on the private subnet

1)  the security group of instance (I1) is modified to accept only
    ssh/22 from the public subnet : 10.0.1.0/24

> ![](.//media/image9.png)

## Step 3) Install a « NAT instance » (N1) on the public subnet

1)  create an instance : look in AMI friend for "nat" instance

![](.//media/image10.png)

2)  create a security group, specific for this NAT instance (N1)

in this group add an inbound Rule for ICMP v4 (ping) : source : the
private subnet 10.0.2.0\\24

![](.//media/image11.png)

3)  associate the NAT security group to this instance

4)  Disabling source/destination checks : Select the NAT instance,
    choose Actions, Networking, Change Source/Dest. Check

![](.//media/image12.png)

5)  adapt the table route of the private subnet :

add a rule for destination = 0.0.0.0 to target = "InstanceNAT" (N1)

![](.//media/image13.png)

## Step 4) connect with ssh to instance I2 from instance I1

1)  send the private key from the local PC to the public instance I1
    (using « filezilla » tool via sftp)

> connection settings on « filezilla »
> 
> ![](.//media/image14.png)
> 
> You are then able to copy the \*.pem file from your local PC to the I1
> instance at user root level
> 
> ![](.//media/image15.png)
> 
> The \*. pem file can now be seen on the I1 instance :
> 
> ![](.//media/image16.png)

2)  Alternative to 1) : send the private key from the local PC to the
    public instance I1 (using WSL and SCP)

<!-- end list -->

  - From the « wsl » command line : sudo scp -i "S20KEYPAIREK.pem"
    S20KEYPAIREK2.pem <ec2-user@34.229.162.76>:.

<!-- end list -->

3)  connect with ssh from I1 to I2

<!-- end list -->

  - change the rights on the key file: chmod 400 S20KEYPAIR2EK.pem

  - connect to private instance with ssh : ssh -i "S20KEYPAIR2EK.pem"
    <ec2-user@10.0.2.25>

  - after accepting the key fingerprint, connected to the machine \!

<!-- end list -->

4)  "ping www.google.com"

![](.//media/image17.png)
