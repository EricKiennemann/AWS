# Launch an EC2 instance from a Python code, using UserData to build an Apache web server

## Step 1) Install library boto3 to be able to communicate with amazon

Just install with pip command : « pip install boto3 »

## Step 2) Setup the credential, so that the communication can be achieved

![](.//media/image1.png)

I have choosen to put the credential information in a file in
« \~/.aws/credentials »

## Step 3) Write the Python code to launche the EC2 instance

![](.//media/image2.png)

## Step 4) Check that the web site is up and running and that the php web page has been copied from AWS S3 bucket

![](.//media/image3.png)

![](.//media/image4.png)
