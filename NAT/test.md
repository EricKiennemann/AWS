**Enable ping to google.com from an instance in a private subnet**

**Install the instance on the private subnet**

\* the security group is modified to accept only ssh/22 from the public
subnet : 10.0.1.0/24

![](/media/image1.png){width="3.266949912510936in"
height="1.8501607611548556in"}

**Install the NAT instance on the public subnet**

\* create an instance : look in AMI friend for \"nat\" instance

\* create a security group, specific for NAT

\+ in this group add an inbound Rule for ICMP v4 (ping) : source : the
private subnet 10.0.2.0\\24

\* associate the NAT security group to this instance

\* Disabling source/destination checks : Select the NAT instance, choose
Actions, Networking, Change Source/Dest. Check

**adapt the table route of the private subnet :**

\* add a rule for destination = 0.0.0.0 to target = \"InstanceNAT\"

**connect with ssh to the instance on the private network to be able to
realize the ping**

\* find the private IP of the private instance : 10.0.2.25

\* send the private key from the local PC to the public instance (using
filezilla via sftp)

\* connect to public instance via putty

\* change the rights on the key file: chmod 400 S20KEYPAIR2EK.pem

\* connect to private instance with ssh : ssh -i \"S20KEYPAIR2EK.pem\"
ec2-user\@10.0.2.25

\* after accepting the key fingerprint, connected to the machine !

\* and \"ping www.google.com\"
