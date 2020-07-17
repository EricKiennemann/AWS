### THIS CODE IS WORKING BUT STILL IN PROGRESS
  import os
  
  import subprocess
  
  import boto3
  
  import webbrowser
  
  from time import time
# create the EC2 ressource for the authorized region, here us-east-1
ec2 = boto3.resource('ec2',region_name='us-east-1')

# prepare the user_data script that will, install the jupyter notebook on the server
user_data = '''#!/bin/bash

sudo apt -y update

sudo apt -y install python3-pip python3-dev

sudo -H pip3 install --upgrade pip

sudo -H pip3 install virtualenv

pip install jupyter'''

# launch the EC2 instance with the following parameters
# ImageId = ubuntu linux

instance = ec2.create_instances(ImageId='ami-0ac80df6eff0e70b5', MinCount=1, MaxCount=1, \
                                KeyName='S20KEYPAIR2EK', SecurityGroupIds=['sg-03ce1dd2567031e9d'], UserData=user_data, \
                                InstanceType='t2.micro', SubnetId='subnet-0e7d6b8d0b33abad9')

# Get the instanceId of the created instance
instanceId = instance[0].instance_id

# Start a wait loop to wait for the end of the installation of the instance
start = now = time()

instanceStatus = ''

Ok = False

while (now - start < 100) and (Ok == False):

try:
# get theinstance status to see if the installation is finished
        status = ec2.meta.client.describe_instance_status(InstanceIds=[instanceId])['InstanceStatuses']
   
   except:
   
   pass
   
   try:
   
   instanceStatus = status[0]['SystemStatus']['Status']
   
   except:
   
   pass
   
   if instanceStatus == 'ok':

Ok = True

now = time()

# get the public dns name of the instance
ec2c = boto3.client('ec2',region_name='us-east-1')

response = ec2c.describe_instances(InstanceIds=[instance[0].instance_id])

dns = response['Reservations'][0]['Instances'][0]['PublicDnsName']

user_dns = 'ubuntu@' + dns

# Wait 60s before trying to connect to the instance (To be improved)
start = now = time()

while (now - start < 60):

now = time()

print('after wait')

# Connect with ssh : Create a SSH local port forward to port 8889
# and Run Jupyter notebook server on the EC2 at port 8889
ssh = subprocess.Popen(['C:\\temp\\ssh.exe','-i','C:\\Users/erick/.ssh/S20KEYPAIR2EK.pem', 
                        '-o', 'StrictHostKeyChecking no',
                        '-L', '8889:localhost:8889',
                        user_dns, 'jupyter notebook --no-browser --port 8889'], shell=False, 
                       stdin=subprocess.PIPE,
                       stdout=subprocess.PIPE,
                       stderr=subprocess.PIPE)

url= "'"
# Start a wait loop to wait for the start of the Jupyter Notebook server
start = now = time()
Ok = False
while (now - start < 10) and (Ok == False):
# get the connection token from the Jupyter Notebook Server
        ssh = subprocess.Popen(['C:\\temp\\ssh.exe','-i','C:\\Users/erick/.ssh/S20KEYPAIR2EK.pem', 
                        '-o', 'StrictHostKeyChecking no',
                        '-L', '8889:localhost:8889',
                        user_dns, 'jupyter notebook list'], shell=False, 
                       stdin=subprocess.PIPE,
                       stdout=subprocess.PIPE,
                       stderr=subprocess.PIPE)

        std_data = ssh.communicate()
        try:
# Build the url with token to be able to launch Jupyter Notebook on local PC
            liste1 = str(std_data[0]).split(' ')
            liste2 = liste1[2].split('\\n')
            url = liste2[1]
        except:
            pass
        if url != "'":
            Ok = True
        now = time()
# launch a local webserver with Jupyter Notebook client
webbrowser.open(url, new=2)

