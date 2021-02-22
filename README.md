Credits & Source from: https://github.com/sendmail2krrish/eCommerce-site-using-Node-Express-js

# Dress4Win

## Phase -1:

### Create a custom VPC with three subnets, one in usa, asia and Europe. Create appropriate firewall rules.

### Launching one server for database and application
Launching Compute Engine Instance
1.	Provision a Google Compute Engine (GCE)
2.	SSH into the server. 
3. Switch as root user using 

    sudo -s
    
4. install following software

    apt update
    
    apt install mysql-server -y
    
    apt install git
    
    curl -sL https://deb.nodesource.com/setup_14.x -o nodesource_setup.sh 
    
    bash nodesource_setup.sh
    
    apt install -y nodejs
    
    npm install -g forever
    
5.	Logging to mysql using command

    sudo mysql -h 127.0.0.1 -uroot -p (press enter for password).
    
6.	Create a database named eCommerce using command.
    
    CREATE DATABASE eCommerce;
    
    show databases; (make sure eCommerce database exist)
    
    CREATE USER 'dress4win'@'localhost' IDENTIFIED BY 'root123';  (create new user)
    
    GRANT ALL PRIVILEGES ON * . * TO 'dress4win'@'localhost';
    
    exit
    
7.	git clone https://github.com/shalligoel/Dress4Win.git.  (download application code)

8.	Change directory to dress and then sql

     cd dress4win
     
     cd sql
     
9.	Create the table schema using command

    mysql -udress4win -proot123 < ecommerce.sql

10. mysql -udress4win -proot123

    use eCommerce;
    
    show tables; (check three tables exist in database)
    
    select count(*) from products;    (check some records exist in table)
    
    exit
    
11. cd .. (back to dress4win folder)

    pwd (make sure dress4win is current folder)
    
    npm install. (install packages)
    
12. Make sure node_modules folder exists.

13. change the database IP address in database/config.js file.  - host - localhost, username - dress4win, password - root123

14.  Now, run the Node JS app  using command

     node index.js
     
15. Use the external IP of app-server to access the Dress4Win App

16. Make sure application is running properly.


## Phase - 2

# Create a SQL instance and connect to your application

1. Create a cloud SQL instance with mysql as option with version 5.7 and password as root123.
	Create a private ip address for cloud-sql insance.
	As Authorized Networks, use your custom VPC.

2. Get the private ip-address of cloud sql instance.

3. connect to user from your vm by using the following command

   mysql -h <cloudsql_address> -uroot -proot123
   
   Follow the same commands as you did while setting mysql on the VM.
   
4. exit from mysql server.

5. login with dress4win as user.
   
   mysql -h <cloudsql_address> -udress4win -proot123
   
   use eCommerce;
   
   show tables;
   
   If everything seems fine, exit from mysql server.
   
6. Change the database IP address in database/config.js file.  - host - cloud-sql private ip address, username - dress4win, password - root123

7.  Now, run the Node JS app  using command

     node index.js
     
8. Use the external IP of app-server to access the Dress4Win App

9. Make sure application is running properly.
   
10. Stop VM. (Do not delete it)

11. Goto Disks page and select your disk.

12. Create an image from this disk and name it as dress4win-image.

13. Wait for the image to be built. It will take some time.

 # Phase - 3
 
 1. Create a new VM with image that you have created in phase-2.
 
 2. Use startup-script with following commands
 
    #! /bin/bash
    
    sudo -s 
    
    cd /home/yourid/dress4win
    
    sudo node index.js
    
 3. Create instance and wait for some time.
 
 4. Use the external IP of new vm to access the Dress4Win App

 5. Make sure application is running properly.
 
 Yes, now you are ready for next phases. Keep working.

 
 
 
 # Phase - 4

1. Create three instance template with following settings:

   name - dress4win-template-asia

   image - dress4win-image

   machine-type - f1-micro 

   startup script - #! /bin/bash

	sudo -s

	cd /home/yourid/dress4win

	node index.js

	network - dress4win-vpc

	Create one template  for one subnet.

2. Now, you have three instance templates in three different regions.

3. Create three instance groups based upon these templates.

   name - dress4win-instancegroup-asia

   location - multiple zones

   region - based upon subnets

   template - dress4win-template-asia

   Number of instances - 1

   Autoscaling mode - autoscale

   autoscaling metric - loadbalancing 

   min instance - 1

   max instance - 2

   health check

   create a new health check as dress4win-health and set

   Leave default settings for other parameters and click on create.
  
   Ignore warning and click on create.

   use one template for one group.

4. Now three instance groups are ready, one for each region.

5. Goto Compute Engine console, you will see three VM running. Wait for some time to settle down.

6. Click on external IP addresses on each VM. Check your application is running successfully.

7. You are ready for next phase.


# phase - 5
 
 ## Set up a global Load Balancer
 
 
 
 # Phase - 6
 
 ## Create a domain name and set for your application.


