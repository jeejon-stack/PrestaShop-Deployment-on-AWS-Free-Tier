# PrestaShop Deployment on AWS Free Tier
## Project Description: This project demonstrates the step-by-step deployment of the PrestaShop e-commerce platform on an AWS EC2 Ubuntu server using the AWS Free Tier.

## Tools and Technologies
- AWS EC2 (Free Tier)
- Ubuntu Server
- Apache2
- MySQL
- PHP
- PrestaShop
- SSH

## Architecture
User Browser → AWS EC2 (Ubuntu) → Apache → PHP → MySQL Database

## Step by Step Deployment

### Step 1 - Launch EC2 Instance
- Login to AWS Console
- Navigate to EC2
- Launch Ubuntu Server  22.04 instance
- Prestashop-server
-  t2.micro and create new key pair the download .pem file
- Allow inbound rules:
  - SSH (22) step ssh to my ip
  - HTTP (80)
  - HTTPS (443)
  - launch instance
### Step 2 - Connect to Server

- Download puttygen and putty
- Generate a private key the prestashop-key.pem file from EC2 then use the key to have access to putty
- Open puttygen
- load the .pem file downloaded and change to the dropdown to all files and open
- save the private key in .ppk
- On putty on the host name put the ipv4 public address from EC2 and navigate to connection, SSH, auth and credential, click on browse to navigate to private key generated then click open
- A terminal will display type ubuntu 

### Step 3 - update the system 

- sudo apt update && sudo apt upgrade -y

### Step 4 - Install Apache, MYSQL and extensions

- sudo apt install apache2 mysql-client php php-mysql php-curl php-gd php-intl php-xml php-zip unzip –y
- sudo systemctl enable apache2
  
### Step 5 - Creation of RDS database

- Go to aws console
- RDS
- Create Database
- MYSQL
- Prestashop.db
- Username  <admin>
- Password  <input password>
- db.t3.micro
- Public access <yes>
- Create database. Wait till is installed and show status says Available.
- Copy the RDS Endpoint.
- Allow EC2 to Access RDS
- Navigate to aws console, RDS, Security Groups. 
- Navigate to inbound and edit rules and add
- MySQL/Aurora
- Port: 3306
- Source: EC2 Security Group

### Step 6 - Download Prestashop

- On putty
- cd /var/www/html
- Sudo wget https://github.com/PrestaShop/PrestaShop/releases/8.1.5/download/prestashop_8.1.5.zip
- Sudo unzip prestashop.zip –d /var/www/html
- Sudo chown –R www-data:www-data /var/www/html
- Sudo chmod –R 755 /var/www/html
- Sudo systemctl restart apache2

### Step 7 - Prestashop open and configuration

- Open a browser 
- Search http://<your –EC2-public-IP>
- Prestashop installer will appear then set it up and configure the database 
- Database server <use the copied RDS endpoint>
- Database <prestasop>
- User<admin>
- Password<password created when setting up RDS>
- Test database connection 
- Install
- After install then verified public address
- http:// EC2 public address ip



