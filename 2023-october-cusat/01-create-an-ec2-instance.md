# Create EC2 Instance with Ubuntu 22.04 in Mumbai Region with Public IP

## 1. Login to AWS Console
   - Open your web browser and go to the [AWS Management Console](https://aws.amazon.com/).
   - Sign in with your AWS account credentials.

## 2. Navigate to EC2 Dashboard
   - In the AWS Management Console, navigate to the "Services" dropdown and select "EC2" under the "Compute" section.

## 3. Choose Region
   - In the top-right corner of the console, select the region as "Asia Pacific (Mumbai)".

## 4. Launch Instance
   - Click on the "Instances" link in the left sidebar.
   - Click the "Launch Instance" button.

## 5. Choose AMI
   - In the "Choose an Amazon Machine Image (AMI)" step, select "Ubuntu" as the operating system.
   - Choose the version as "Ubuntu Server 22.04 LTS" from the list.

## 6. Choose Instance Type
   - Select the desired instance type based on your requirements. For example, choose a t2.micro instance for a free-tier eligible instance.

## 7. Configure Instance
   - In the "Configure Instance" step, you can leave the default settings.
   - Scroll down to the "Advanced Details" section if needed, but for a basic setup, you can proceed with the default options.

## 8. Add Storage
   - Specify the amount of storage you want for your instance. The default is usually fine for testing purposes.

## 9. Add Tags (Optional)
   - You can add tags for better organization if needed. This step is optional.

## 10. Configure Security Group
   - In the "Configure Security Group" step, create a new security group or choose an existing one.
   - Make sure to add a rule to allow inbound traffic on SSH (port 22) so that you can connect to your instance.

## 11. Review and Launch
   - Review your configuration settings and click the "Launch" button.

## 12. Select Key Pair
   - Choose an existing key pair or create a new one. This key pair is essential for SSH access to your instance.

## 13. Launch Instance
   - Click the "Launch Instances" button.

## 14. View Instances
   - In the EC2 dashboard, click on "Instances" in the left sidebar to view the list of instances.
   - Wait for your new instance to enter the "running" state.

## 15. Connect to Instance
   - Once the instance is running, select it in the list and click the "Connect" button.
   - Follow the instructions to connect via SSH. For example, you can use the following command:
     ```bash
     ssh -i your-key.pem ubuntu@your-instance-ip
     ```
     Replace `your-key.pem` with the path to your private key file and `your-instance-ip` with the public IP address of your instance.
