# Day 52: Your CI/CD Pipeline on AWS - Part 3 🚀 ☁

On your journey of making a CI/CD pipeline on AWS with these tools, you completed AWS CodeCommit & CodeBuild.

Next few days you'll learn these tools/services:

- CodeDeploy
- CodePipeline
- S3

---

## What is CodeDeploy?

AWS CodeDeploy is a deployment service that automates application deployments to:

- Amazon EC2 instances
- On-premises instances
- Serverless Lambda functions
- Amazon ECS services

CodeDeploy can deploy application content that:
- Runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories.
- Deploys a serverless Lambda function.

You do not need to make changes to your existing code before you can use CodeDeploy.

---

## Solution

### Task-01: Deploy `index.html` file on EC2 using CodeDeploy

1. **Read about `Appspec.yaml` file**: The `Appspec.yaml` file defines the deployment actions. Here is a sample:
   ```yaml
   version: 0.0
   os: linux
   files:
     - source: /
       destination: /var/www/html
   hooks:
     BeforeInstall:
       - location: scripts/install_dependencies.sh
         timeout: 300
         runas: root
     ApplicationStart:
       - location: scripts/start_server.sh
         timeout: 300
         runas: root
   ```

2. **Deploy `index.html` on EC2**:
   - Create an `index.html` file with basic content:
     ```html
     <html>
     <head><title>Welcome</title></head>
     <body><h1>Hello from CodeDeploy!</h1></body>
     </html>
     ```
   - Install **nginx** on the EC2 instance:
     ```bash
     sudo yum update -y
     sudo yum install nginx -y
     sudo systemctl start nginx
     sudo systemctl enable nginx
     ```

3. **Set up the CodeDeploy agent**:
   - Install the CodeDeploy agent on the EC2 instance:
     ```bash
     sudo yum update -y
     sudo yum install ruby wget -y
     cd /home/ec2-user
     wget https://aws-codedeploy-region.s3.amazonaws.com/latest/install
     chmod +x ./install
     sudo ./install auto
     sudo systemctl start codedeploy-agent
     sudo systemctl enable codedeploy-agent
     ```
   - Replace `region` with your AWS region (e.g., `us-east-1`).

### Task-02: Complete the Deployment

1. **Add `Appspec.yaml` to the CodeCommit repository**:
   - Clone your CodeCommit repository:
     ```bash
     git clone https://git-codecommit.<region>.amazonaws.com/v1/repos/<repository-name>
     ```
   - Add the `Appspec.yaml` file to the repository:
     ```bash
     cd <repository-name>
     echo "<content of appspec.yaml>" > appspec.yaml
     git add appspec.yaml
     git commit -m "Added Appspec.yaml for CodeDeploy"
     git push origin main
     ```

2. **Configure and execute CodeDeploy**:
   - In the AWS Management Console, create a new deployment group in CodeDeploy.
   - Specify the EC2 instance as the deployment target.
   - Deploy the application from the CodeCommit repository.

---

## Additional Resources

For more details, watch [this video](https://youtu.be/IUF-pfbYGvg).

---

Happy Learning! 

[← Previous Day](../day51/README.md) | [Next Day →](../day53/README.md)
