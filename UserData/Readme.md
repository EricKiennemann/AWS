# Use UderData Field a EC2 creation to install a webserver

## Step 1) Prepare the script for installing the Apacheweb server and create a php page

For a ubuntu Linux

\#\!/bin/bash

apt-get -y update

apt-get -y install apache2

apt -y install php libapache2-mod-php

systemctl restart apache2.service

cd /var/www/html

echo "\<html\>" \>\> myip.php

echo "\<body\>" \>\> myip.php

echo "\<h1\> Access to an Apache Web Server on AWS done with UserData
script\</h1\>" \>\> myip.php

echo "\<?php" \>\> myip.php

echo " \\$externalContent =
file\_get\_contents('http://checkip.dyndns.com/');" \>\> myip.php

echo " preg\_match('/Current IP Address: \\\[?(\[:.0-9a-fA-F\]+)\\\]?/',
\\$externalContent, \\$m);" \>\> myip.php

echo " \\$externalIp = \\$m\[1\];" \>\> myip.php

echo " echo \\"\<p\> My Public IP is : \\",\\$externalIp" \>\> myip.php

echo "?\>" \>\> myip.php

echo "\</body\>" \>\> myip.php

echo "\</html\>" \>\> myip.php

## Step 2) Put this script when creating the EC2 instance in the UserData

![](.//media/image1.png)

## Step 3) Test the access to the web page

![](.//media/image2.png)
