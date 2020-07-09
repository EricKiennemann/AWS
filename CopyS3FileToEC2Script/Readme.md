# Use a UderData Field at EC2 creation to install a webserver and copy php file from a S3 bucket.

## Step 1) create the « non public » S3 bucket and copy the php file on this S3 bucket

![](.//media/image1.png)

![](.//media/image2.png)

![](.//media/image3.png)

## Step 2) Create a Role to authorize the EC2 to access the S3 Bucket

This role has full access to S3 bucket

![](.//media/image4.png)

## Step 3) prepare the script that will install the Apache Webserver and copy the php file from S3 bucket

For a ubuntu Linux

\#\!/bin/bash

\#install apache server and php

apt-get -y update

apt-get -y install apache2

apt -y install php libapache2-mod-php

systemctl restart apache2.service

\# install the amazon CLI client that enabl scipt command with Amazon
services

apt -y install awscli

\# command to copy a file from amazon S3 bucket to local EC2

aws s3 cp s3://s20bucketforuserdata/amazons3.php
/var/www/html/amazons3.php

## Step 4) create the EC2 instance

![](.//media/image5.png)

Add « IAM Role » create at step 3

![](.//media/image6.png)

And « User data » script prepared at step 3

## Step 5) Check that the php page can be accessed from internet

![](.//media/image7.png)
