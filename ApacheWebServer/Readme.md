# Create an Apache Web server to make available a php page

## Step 1) Create an instance with « AMI Amazon Linux » machine

## Step 2) Associate an Elastic Ip adress to this machine

This allow not to have a fix public IP adress even after start/stop of
the machine

  - Create the Elastic IP adress

![](.//media/image1.png)

  - Associate this IP adress to the created instance

![](.//media/image2.png)

[  
The created public IP adresse is :
34.224.150.252](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#ElasticIpDetails:PublicIp=34.224.150.252)

## Step 3) Install apach web server

To do this I have followed the documention :
<https://docs.aws.amazon.com/fr_fr/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateWebServer.html>

**sudo yum update -y**

![](.//media/image3.png)

**sudo yum install -y httpd24 php56 php56-mysqlnd**

![](.//media/image4.png)

**sudo service httpd start**

![](.//media/image5.png)

Try to access from the internet to test the Start of the Apache server

![](.//media/image6.png)

Command to make the Apache server start automatically

**sudo chkconfig httpd on**

Add the group www at my EC2 instance

**sudo groupadd www**

Add the user ec2-user at my EC2 instance

**sudo usermod -a -G www ec2-user**

Disconnect / Reconnect after this so that security information are taken
in account

Check that the new group is affected with command « groups »

![](.//media/image7.png)

Change the owner of the repositary /var/www to www

**sudo chgrp -R www /var/www**

Modify autorisations of /var/www and of its sub repertory

**sudo chmod 2775 /var/www**

**find /var/www -type d -exec sudo chmod 2775 {} +**

**find /var/www -type f -exec sudo chmod 0664 {} +**

The setup is finished, now we will add the web page

## Step 4) Prepare the web page 

Go the the web server folder

**cd /var/www/html**

create the file myip.php with nano text editor

I have found several solution on the following link to get the ip : I
have choosen the first one

<https://stackoverflow.com/questions/7909362/how-do-i-get-the-external-ip-of-my-server-using-php>

The result in the nano editor

![](.//media/image8.png)

The web page :

![](.//media/image9.png)
