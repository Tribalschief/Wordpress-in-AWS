 Launch an EC2 Instance
Log in to AWS and go to the EC2 Dashboard.
Click “Launch Instance” to start the setup.
Select an Amazon Machine Image (AMI) (e.g., Amazon Linux 2).
Choose an instance type (t2.micro for Free Tier eligibility).
Configure instance settings like network, security groups, and storage.
Click “Launch”, select an SSH key pair, and deploy the instance.


Install Apache Web Server on EC2
Connect to your EC2 instance via SSH:

ssh -i /path/to/your/key.pem ec2-user@your-instance-ip
Update the instance and install Apache:

sudo su
yum update -y // can be yum or apt
yum install httpd -y
Start and enable the Apache service:

service httpd start
chkconfig httpd on
Verify that Apache is running by accessing your EC2 public IP in a browser

Download and Configure WordPress
Navigate to the Apache web directory:

cd /var/www/html/
Download and extract WordPress:

 yum install wget -y
 wget https://wordpress.org/latest.tar.gz
 tar -xzf latest.tar.gz
 mv wordpress/* .
 rm -rf wordpress latest.tar.gz

Set Up AWS RDS MySQL Database
Go to the AWS RDS Dashboard and create a new MySQL database.
Choose the Free Tier instance type.
Set up database credentials (DB name, username, and password).
Note down the RDS endpoint after the database is created.


Connect WordPress to the RDS Database
Navigate to the WordPress directory on EC2:

cd /var/www/html/
Rename the WordPress config file:

mv wp-config-sample.php wp-config.php
sudo nano wp-config.php
Update the file with your database credentials:

define( 'DB_NAME', 'wordpress_db' );
define( 'DB_USER', 'your_database_username' );
define( 'DB_PASSWORD', 'your_database_password' );
define( 'DB_HOST', 'your_rds_endpoint' );
Save and close the file.

Complete WordPress Installation
Open your browser and enter your EC2 public IP.
Follow the WordPress setup wizard.
Configure your site title, admin account, and settings.
Click Install, and your WordPress site is live!