# Day 44: Relational Database Service in AWS

---

## 🎯 Task Overview

Explore **Amazon Relational Database Service (Amazon RDS)**, a managed database service that simplifies the setup, operation, and scaling of databases in the cloud. 

---

## 🛠️ Task Steps

### 1. **Create a Free Tier RDS Instance**
- Navigate to the **Amazon RDS Console**.
- Select **MySQL** as the database engine.
- Choose the **Free Tier** option for your instance.
- Configure instance details, such as database name, username, and password.
- Launch the RDS instance.

---

### 2. **Create an EC2 Instance**
- Navigate to the **Amazon EC2 Console**.
- Launch an EC2 instance within the same VPC and region as the RDS instance.
- Use a **free tier-eligible Amazon Linux 2 AMI** for simplicity.
- Ensure your EC2 instance has access to the internet for package installations.

---

### 3. **Create an IAM Role with RDS Access**
- Go to the **IAM Console**.
- Create a new IAM role:
  - Select **AWS Service** as the trusted entity.
  - Choose **EC2** as the service.
- Attach a policy granting **AmazonRDSFullAccess** or a custom policy with specific permissions for your RDS instance.

---

### 4. **Attach the IAM Role to EC2**
- Navigate to the EC2 instance **Actions** menu.
- Select **Security** -> **Modify IAM Role**.
- Attach the IAM role created in the previous step.

---

### 5. **Install MySQL Client on EC2**
- SSH into your EC2 instance:
  ```bash
  ssh -i <your-key-file>.pem ec2-user@<EC2-public-IP>
