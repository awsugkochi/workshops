# Hosting a Static HTML Page in S3 with CloudFront CDN

## Agenda:

### **Introduction:**
- Welcome and Overview of the Workshop
- Importance of Serverless Hosting with AWS
- Brief Introduction to AWS S3 and CloudFront

### **Part 1: Setting up S3 Bucket:**
1. **Overview of S3 and AWS Console:**
   - Introduction to S3's capabilities and AWS Console navigation
2. **Creating an S3 Bucket for Static Website Hosting:**
   - Steps to create and configure the bucket for hosting
3. **Uploading the HTML files to the S3 Bucket:**
   - Process of adding your website files to the bucket
4. **Configuring Bucket Policy for Public Access:**
   - Setting permissions to allow the public to view your site

### **Part 2: Setting up CloudFront Distribution:**
5. **Introduction to CloudFront:**
   - Basics of what CloudFront does and why it's beneficial
6. **Creating a CloudFront Distribution for the S3 Bucket:**
   - Steps to link CloudFront to your S3 bucket for faster content delivery
7. **Configuring CloudFront with Custom Domain (Optional):**
   - Using your own domain instead of the default CloudFront domain
8. **Setting up SSL with AWS Certificate Manager (Optional):**
   - Securing your site with HTTPS

### **Part 3: Access and Test:**
9. **Accessing the Static Website via CloudFront URL:**
   - Viewing your live site
10. **Testing the Latency and Speed using Different Regions:**
   - Verifying the performance benefits of CloudFront

### **Part 4: Q&A and Closing:**
- Open floor for questions and discussion
- Recap of key learnings
- Sharing additional resources for further learning

## Workshop Guidelines:

### **Part 1: Setting up S3 Bucket:**

#### 1. Login to AWS Console:
   - Open your web browser and go to the [AWS Management Console](https://aws.amazon.com/).
   - Sign in with your AWS account credentials.

#### 2. Navigate to S3:
   - In the AWS Management Console, navigate to the "Services" dropdown and select "S3".

#### 3. Create S3 Bucket:
   - Click on the "Create bucket" button.
   - Name your bucket and select a region.
   - Under "Bucket settings for Block Public Access", uncheck all options to allow public access (ensure you understand the security implications).
   - Review settings and create the bucket.

#### 4. Enable Static Website Hosting:
   - Navigate to the created bucket > Properties > Static website hosting.
   - Enable it and provide the index and error documents (usually `index.html` and `error.html`).

#### 5. Upload HTML Files:
   - Go to the 'Objects' tab and click 'Upload'.
   - Drag and drop or select your static HTML files and upload them.

#### 6. Configure Bucket Policy:
   - Under the 'Permissions' tab, click on 'Bucket Policy'.
   - Add the following policy to make the bucket contents publicly readable. Make sure to replace `YOUR_BUCKET_NAME` with the actual name of your S3 bucket:

```json

        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Sid": "PublicReadGetObject",
                    "Effect": "Allow",
                    "Principal": "*",
                    "Action": "s3:GetObject",
                    "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
                }
            ]
        }
```
### **Part 2: Setting up CloudFront Distribution:**

#### 7. Navigate to CloudFront:
   - In the AWS Management Console, navigate to the "Services" dropdown and select "CloudFront".

#### 8. Create Distribution:
   - Click on "Create Distribution" and then select "Web".
   - In the "Origin Settings", select the S3 bucket you created.
   - Configure other settings as per your requirements.
   - Click on "Create Distribution".

#### 9. Configure SSL (Optional):
   - If you have a custom domain, you can set up SSL.
   - Request a certificate in AWS Certificate Manager.
   - Once validated, assign it to the CloudFront distribution.

### **Part 3: Access and Test:**

#### 10. Access Website:
   - Once the CloudFront distribution is deployed, you can access your static website using the CloudFront URL or your custom domain if configured.
