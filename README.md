# Website Deployment on AWS EC2 Using Apache Web Server

This project demonstrates how to deploy a simple static website on an AWS EC2 instance using the Apache web server. The following instructions will guide you through the entire process, from uploading your website files to GitHub to accessing your site through a public IP.

## Prerequisites

- AWS account with access to EC2.
- Basic knowledge of Git and SSH.
- A simple static website (HTML, CSS, JS files).

## Steps to Deploy

### 1. **Upload Website to GitHub**

1. Navigate to the project folder on your local system.
2. Initialize a Git repository:
   ```bash
   git init
   ```
3. Add all files to the staging area:
   ```bash
   git add .
   ```
4. Commit the changes:
   ```bash
   git commit -m "Initial commit"
   ```
5. Create a new repository on GitHub and add it as a remote:
   ```bash
   git remote add origin <repository-url>
   ```
6. Push the files to GitHub:
   ```bash
   git push -u origin main
   ```

### 2. **Launch EC2 Instance on AWS**

1. Log in to the AWS Management Console and navigate to EC2.
2. Click on "Launch Instance" and configure the following:
   - **OS**: Red Hat Linux or Amazon Linux.
   - **Instance Type**: t2.micro (Free Tier eligible).
   - **Key Pair**: Create and download a key pair for SSH authentication.
   - **Security Groups**:
     - Allow SSH (only from your IP for better security).
     - Allow HTTP traffic.

3. Launch the instance.

### 3. **Connect to EC2 Instance**

1. Open a terminal and navigate to the directory containing your downloaded `.pem` key file.
2. Change permissions of the key file:
   ```bash
   chmod 400 <key.pem>
   ```
3. Connect to the instance via SSH:
   ```bash
   ssh -i <key.pem> ec2-user@<public-ip>
   ```

### 4. **Install Required Software**

1. Update the system:
   ```bash
   sudo yum update -y
   ```
2. Install Git:
   ```bash
   sudo yum install git -y
   ```

### 5. **Clone Repository to EC2**

1. Clone your GitHub repository:
   ```bash
   git clone <repository-url>
   ```
2. Navigate to the cloned folder.

### 6. **Install Apache Web Server**

1. Install Apache:
   ```bash
   sudo yum install httpd -y
   ```
2. Move website files to the default web root:
   ```bash
   sudo cp -r * /var/www/html/
   ```

3. Start the Apache web server:
   ```bash
   sudo systemctl start httpd
   ```

### 7. **Access the Website**

1. Copy the public IP of the EC2 instance.
2. Open a browser and navigate to `http://<public-ip>`.

### 8. **Troubleshooting**

- If the website doesn’t load, ensure the Apache server is running:
  ```bash
  sudo systemctl status httpd
  ```
- Make sure HTTP traffic is allowed in your security group settings.

## Additional Notes

- **HTTPS**: This demo uses HTTP, but HTTPS can be configured for better security.
- **IAM**: Use Identity and Access Management (IAM) to control access permissions if needed.

## License

This project is for educational purposes. Feel free to modify and expand it as needed.

---

For any questions or issues, feel free to raise an issue in the GitHub repository or contact me on LinkedIn!
