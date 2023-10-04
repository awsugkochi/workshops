# Create EC2 Instance, Configure LEMP Stack and Deploy Wordpress CMS


## Agenda:

### **Introduction:**
- Welcome and Overview of the Workshop
- Importance of Deploying WordPress on Cloud Servers
- Brief Introduction to AWS EC2, Nginx, PHP-FPM, and MySQL

### **Part 1: Server Provisioning:**
1. **Launch EC2 Instance:**
   - Overview of EC2 and AWS Console
   - Launching an EC2 instance with Ubuntu 22.04 LTS
   - Configuring Security Groups for SSH, HTTP, and HTTPS

2. **Connect to the EC2 Instance:**
   - SSH into the EC2 instance
   - Introduction to the command line on the server

### **Part 2: Software Installation:**
3. **Install Nginx, PHP-FPM, and MySQL:**
   - Bash commands to update packages and install Nginx
   - Installing PHP-FPM and required PHP extensions
   - Setting up MySQL Server for WordPress

### **Part 3: WordPress Deployment:**
4. **Download and Configure WordPress:**
   - Downloading the latest version of WordPress
   - Configuring Nginx to serve WordPress
   - Setting up a MySQL database for WordPress

5. **Test and Verify:**
   - Ensuring the WordPress website is functioning correctly
   - Troubleshooting common deployment issues

### **Part 4: Bonus - SSL Configuration:**
6. **Configure SSL with Let's Encrypt:**
   - Obtaining and configuring a free SSL certificate
   - Enabling HTTPS on the WordPress site

### **Part 5: Q&A and Closing:**
- Open floor for questions and discussion
- Recap of key learnings
- Sharing additional resources for further learning


## Workshop Guidelines


### **Part 1: Server Provisioning:**

#### 1. Login to AWS Console
   - Open your web browser and go to the [AWS Management Console](https://aws.amazon.com/).
   - Sign in with your AWS account credentials.

#### 2. Navigate to EC2 Dashboard
   - In the AWS Management Console, navigate to the "Services" dropdown and select "EC2" under the "Compute" section.

#### 3. Choose Region
   - In the top-right corner of the console, select the region as "Asia Pacific (Mumbai)".

#### 4. Launch Instance
   - Click on the "Instances" link in the left sidebar.
   - Click the "Launch Instance" button.

#### 5. Choose AMI
   - In the "Choose an Amazon Machine Image (AMI)" step, select "Ubuntu" as the operating system.
   - Choose the version as "Ubuntu Server 22.04 LTS" from the list.

#### 6. Choose Instance Type
   - Select the desired instance type based on your requirements. For example, choose a t2.micro instance for a free-tier eligible instance.

#### 7. Configure Instance
   - In the "Configure Instance" step, you can leave the default settings.
   - Scroll down to the "Advanced Details" section if needed, but for a basic setup, you can proceed with the default options.

#### 8. Add Storage
   - Specify the amount of storage you want for your instance. The default is usually fine for testing purposes.

#### 9. Add Tags (Optional)
   - You can add tags for better organization if needed. This step is optional.

#### 10. Configure Security Group
   - In the "Configure Security Group" step, create a new security group or choose an existing one.
   - Make sure to add a rule to allow inbound traffic on SSH (port 22) so that you can connect to your instance.

#### 11. Review and Launch
   - Review your configuration settings and click the "Launch" button.

#### 12. Select Key Pair
   - Choose an existing key pair or create a new one. This key pair is essential for SSH access to your instance.

#### 13. Launch Instance
   - Click the "Launch Instances" button.

#### 14. View Instances
   - In the EC2 dashboard, click on "Instances" in the left sidebar to view the list of instances.
   - Wait for your new instance to enter the "running" state.

#### 15. Connect to Instance
   - Once the instance is running, select it in the list and click the "Connect" button.
   - Follow the instructions to connect via SSH. For example, you can use the following command:
     ```bash
     ssh -i your-key.pem ubuntu@your-instance-ip
     ```
     Replace `your-key.pem` with the path to your private key file and `your-instance-ip` with the public IP address of your instance.


### **Part 2: Software Installation:**

#### 2.1 Install Nginx, PHP-FPM, and MySQL Server
   - Run the following commands on your EC2 instance to install Nginx, PHP-FPM, and MySQL Server:

     ```bash
     # Update package list
     sudo apt update

     # Install Nginx
     sudo apt install nginx

     # Install PHP and required extensions
     sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip

     # Install MySQL Server
     sudo apt install mysql-server
     ```

#### 2.2 Configure MySQL for WordPress
   - Set up a MySQL database and user for WordPress:

     ```bash
     # Access MySQL
     sudo mysql

     # Create a new database
     CREATE DATABASE wordpress;

     # Create a new user and grant privileges
     CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'your_password';
     GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress_user'@'localhost';
     FLUSH PRIVILEGES;

     # Exit MySQL
     EXIT;
     ```

### **Part 3: WordPress Deployment:**

##### 3.1 Install WordPress
   - Download and configure WordPress:

     ```bash
     # Download and extract WordPress
     cd /var/www/html
     sudo wget https://wordpress.org/latest.tar.gz
     sudo tar -xvzf latest.tar.gz
     sudo mv wordpress/* .
     sudo rm -rf wordpress latest.tar.gz

     # Set correct permissions
     sudo chown -R www-data:www-data /var/www/html
     sudo chmod -R 755 /var/www/html
     ```

#### 3.2 Configure Nginx for WordPress
   - Create an Nginx server block configuration for WordPress:

     ```bash
     # Create a new configuration file
     sudo nano /etc/nginx/sites-available/wordpress

     # Add the following configuration, replacing example.com with your domain or IP
     server {
         listen 80;
         server_name example.com;

         root /var/www/html;
         index index.php index.html index.htm;

         location / {
             try_files $uri $uri/ /index.php?$args;
         }

         location ~ \.php$ {
             include snippets/fastcgi-php.conf;
             fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
             fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
             include fastcgi_params;
         }

         location = /favicon.ico { log_not_found off; access_log off; }
         location = /robots.txt { log_not_found off; access_log off; }

         error_page 404 /index.php;
     }

     # Create a symbolic link to enable the site
     sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/

     # Test Nginx configuration
     sudo nginx -t

     # Reload Nginx
     sudo systemctl reload nginx
     ```

#### 3.3 Access WordPress via Public IP
   - Open your web browser and enter the public IP address of your instance.
   - Follow the on-screen instructions to complete the WordPress installation.

Now, you have successfully provisioned an EC2 instance and deployed WordPress with Nginx, PHP-FPM, and MySQL.