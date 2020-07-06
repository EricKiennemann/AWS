# Create a second Apache Web server and configure Application Load Balancer (ALB)

## Step 1) Create an instance with « ubuntu » machine

## Step 2) Associate an Elastic Ip adress to this machine

Same as for first Apache Web Server instance

## Step 3) Install apach web server

For the second server I try with an ubuntu instance and with a newer
version of apache server

Its fix public IP adress is :
[18.213.203.114](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#ElasticIpDetails:PublicIp=18.213.203.114)

The ssh connection is a bit different since the user for ubuntu
distribution is « ubuntu » and nomore ec2

sudo ssh -i "S20KEYPAIRWEB.pem" <ubuntu@18.213.203.114>

### Instruction to install Apache web server

sudo apt-get update

sudo apt-get install apache2

![](.//media/image1.png)

Install php

sudo apt install php libapache2-mod-php

sudo systemctl restart apache2.service

## Step 4) Prepare the php web file

Same as for the first server

![](.//media/image2.png)

## Step 5) Install Application Load Balancer

![](.//media/image3.png)

  - Select the Elastic Load balancer

![](.//media/image4.png)

  - Configure it on http for current VPC and subnet

![](.//media/image5.png)

  - Configure the security group to authorize http and https

![](.//media/image6.png)

  - Configure a Target Group based on instance name

![](.//media/image7.png)

  - Add the instances name to the target group and check the « healthy »
    status

> ![](.//media/image8.png)

  - The Application load balancer can be access at the adress below

> ![](.//media/image9.png)

<http://s20albek-1766160242.us-east-1.elb.amazonaws.com/myip.php>

![](.//media/image10.png)

![](.//media/image11.png)
