# Summary

## [Project 1 - Jupyter Notebook on EC2 launch from Python Code](NAT/Readme.md)

Write Pyhon code to be able to AUTOMATICALLY :
* create an EC2 instance with Jupyter Notebook server installed on it
* connect to this Jupyter Notebook server from a local PC
* launch Jupyer Notebook on a webbrowser on the local PC

## [NAT](NAT/Readme.md)

Build public and private subnet and add a NAT instance on the public
subnet in order to be able to « connect » to the internet (ping
google.com) from the private subnet using the NAT instance

## [Amazon S3](Amazon%20S3/Readme.md)

Create an Amazon S3 bucket and use it to host a static web age

## [RDS MySql Database](RDSmySQLDatabase/Readme.md)

Create an Amazon RDS database using mySql. Access to it with
WorkbenchMysql and do database operation on it

## [RDS MySql Database - Python](RDSmySqlWithPython/Readme.md)

Acces to the RDS MySqlDatabase from Python and do database operation on
it

## [Apache Web Server](ApacheWebServer/Readme.md)

Install Apache Web Server and PHP and add a simple web page that print the public IP adress of the instance

## [Application Load Balancer](ApplicationLoadBalancerALB/Readme.md)

Install a second Apache Web Server on a different instance with the same web page. Add those two servers to an Application Load Balancer

## [User Data](UserData/Readme.md)

Launch an EC2 instance using the UserData functionality to install automatically an Apache server and create a.php file

## [Copy S3 File to EC2 using a  Script](CopyS3FileToEC2Script/Readme.md)

Launch an EC2 server using UserData functionnality : install a Apache web server and copy a S3 .php file to this instance 

## [Launch EC2 Instance with a Python code](LaunchEC2withPython/Readme.md)

Launch an EC2 server from a Python code : install a Apache web server and copy a S3 file to this instance using UserData functionnality
