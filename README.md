Credits & Source from: https://github.com/sendmail2krrish/eCommerce-site-using-Node-Express-js

# Dress4Win

## Phase -1:

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
    curl -sL https://deb.nodesource.com/setup_14.x -o nodesource_setup.sh <br>
    bash nodesource_setup.sh<br>
    apt install -y nodejs<br>
    npm install -g forever<br>
    
5.	Logging to mysql using command

    mysql -h 127.0.0.1 -u root -p (press enter for password).
    
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
     
9.	Create the table schema using mysql -h 127.0.0.1 -u root -p < ecommerce.sql

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

     node index.js<br>
     
15. Use the external IP of app-server to access the Dress4Win App

16. Make sure application is running properly.


## Phase - 2

# Create a SQL instance and connect to your application

1. Create a cloud SQL instance with mysql as option with version 5.7 and password as root123.

2. Get the connection string of cloud sql instance.

3. connect to user from your vm by using the following command

   mysql -h <cloudsql_connectionstring> -uroot -proot123
   Follow the same commands as you did while setting mysql on the VM.
   
4. exit from mysql server.

5. login with dress4win as user.
   
   mysql -h <cloudsql_connectionstring> -udress4win -proot123
   use eCommerce;
   show tables;
   
   If everything seems fine, exit from mysql server.
   
6. Change the database IP address in database/config.js file.  - host - cloud-sql connection string, username - dress4win, password - root123

7.  Now, run the Node JS app  using command

     node index.js<br>
     
8. Use the external IP of app-server to access the Dress4Win App

9. Make sure application is running properly.
   
10. Stop VM.

11. Goto Disks page and select your disk.

12. Create an image from this disk and name it as dress4win-image.

13. Wait for the image to be built. It will take some time.

                        
