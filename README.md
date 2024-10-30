# Project-1-AWS
**Deploying a Multi-Tier Website Using AWS EC2**

Description:
Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing
capacity in the Amazon Web Services (AWS) cloud. Using Amazon EC2
eliminates your need to invest in hardware up front so you can develop and
deploy applications faster. You can use Amazon EC2 to launch as many or as
few virtual servers as you need, configure security and networking, and manage
storage. Amazon EC2 enables you to scale up or down to handle changes in
requirements or spikes in popularity, reducing your need to forecast traffic.
Problem Statement:
Company ABC wants to move their product to AWS. They have the following
things set up right now:
1. MySQL DB
2. Website (PHP)
The company wants high availability on this product, therefore wants Auto
Scaling to be enabled on this website.
Steps To Solve:
1. Launch an EC2 Instance
2. Enable Auto Scaling on these instances (minimum 2)
3. Create an RDS Instance
4. Create Database & Table in RDS instance:
a. Database name: intel
b. Table name: data
c. Database password: intel123
5. Change hostname in website
6. Allow traffic from EC2 to RDS instance
7. Allow all-traffic to EC2 instance







**Solution:**


1.	Create a ec2 instance – t2.micro, OS-Ubuntu
2.	Install apache web server – sudo apt install apache2 –y
3.	Create Goto /var/www/html – remove index.html file – sudo rm index.html
4.	Create a file index.php – sudo nano index.php 
5.	Paste the php code to file
6.	Goto RDS in console and create a mysql database
7.	Create database – standard create – MySQL – Template – free tier – DB instance identifier – give name [aws-project] – give admin name and password 
8.	Database configuration – t3.micro
9.	Uncheck storage autoscaling – select - Don’t connect to an EC2 compute resource
10.	Additional database name – intel
11.	Uncheck backup 
12.	Uncheck encryption
13.	Create database
14.	Install php and mysql in ec2 instance
15.	Add dependencies : sudo add-apt-repository ppa:ondrej/php
16.	Add dependencies : sudo apt install php5.6 mysql-client php5.6-mysqli
17.	Open index.php file in – cd /var/www/html index.php
18.	In index.php file - in server name remove and paste the endpoint of rds
19.	With following – 
$username = "admin";
$password = "admin1234";
$db = "intel";
20.	Connect with ec2 also - mysql -h aws-project-rds.cb62c60mgybe.us-east-1.rds.amazonaws.com -u admin -padmin1234
21.	See the databases – show databases;
22.	Use table - use intel;
23.	create table - create table data(firstname varchar(15), email varchar(25));
24.	See data in table - select * from data;
25.	For AutoScaling - Create AMI of instance
26.	Go to launch template using the AMI 
27.	Create launch template – give name – select created AMI – t2.micro – keypair – security group – default – create
28.	Create autoscaling group – create autoscaling group – name – select launch template create – next – select all six default AZ’s – next – 
29.	Attach a new load balancer – Application load balancer - internet facing
30.	Listeners and routing – create a target group – Health check = 60s – next

Insert data
![image](https://github.com/user-attachments/assets/987ecdf4-7536-4df4-a001-d341a1a2494e)

Using autoscaling -dns
![image](https://github.com/user-attachments/assets/63548434-5b2a-435a-8d5d-dbe027a29327)

Database - mysql
![image](https://github.com/user-attachments/assets/7aa2c372-011d-48c4-8800-02f862222a6e)
