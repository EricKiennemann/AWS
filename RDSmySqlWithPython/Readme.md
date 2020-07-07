# Connect to the RDS Database from Python

It is possible to connect to a RDS Database using the library pymysql.

## Step 1) Connect to the database

Use the connect() function

**Password must be provided which is not a safe solution**

## Step 2) insert data in an existing table

Use the function execute() with an « Insert » sql statement as a
parameter

## Step 3) print data from a table

Use function execute() with a « Select » sql statement as a parameter

Loop on the result to get all rows returned by the sql statement

![](.//media/image1.png)
