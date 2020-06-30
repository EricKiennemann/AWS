# Create an Amazon RDS database using mySql. Access to it with WorkbenchMysql and do database operation on it

## Step 1) create the mySqlSql with RDS

![](.//media/image1.png)

![](.//media/image2.png)

**Choose the already created VPC**

![](.//media/image3.png)

**For the goal of this exercice the database is created « accessible by
public internet »**

(this could be improved later for more security)

![](.//media/image4.png)

**A dedicated Security Group is created**

![](.//media/image5.png)

At validation of the creation Amazon return the above message : some
changes has to be done in the subnet

## Step 2) Subnet modifications

A new subnet is created attached to the same VPC but belonging to a
second AZ

![](.//media/image6.png)

## Step 3) The VPC need to be modified

At the validation step of the database Amazon ask to activate the
« modifiy domain name » option to be activated at the VPC level in
order to allow the database to be access from internet

![](.//media/image7.png)

## Step 4) Update The security group attached to the database

New inbound rules must be added in order to allow mysql protocol on port
3306 to be accessed from internet

![](.//media/image8.png)

## Step 5) Get the connection parameters

When the database is created, Amazon provides it’s « termination point »
that we will use as an input to connect to the database

![](.//media/image9.png)

## Step 6) Download and install the tool « Workbench mysql » to be able to connect to the database

Download the tool at the following adresse :
<https://dev.mysql.com/downloads/workbench/>

## Step 7) connect to the database from a local PC

The adress of the database given by Amazon has to be filled in the cell
« hostname »

![](.//media/image10.png)

## Step 8) Create the schema and the table

The connection is done.

  - Then first create a schema

![](.//media/image11.png)

![](.//media/image12.png)

  - Create a table in this schema

![](.//media/image13.png)

  - And finally fill this table with some data

![](.//media/image14.png)
