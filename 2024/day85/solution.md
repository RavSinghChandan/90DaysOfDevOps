# 🚀 Deploying a Node.js App on AWS ECS Fargate and ECR

## 📋 Project Description
In this project, we will deploy a Node.js application on **AWS ECS Fargate** using **AWS ECR**. The steps below outline the process from setting up the application to running it on ECS Fargate.

---

## 🛠️ Step-by-Step Solution

### 1. Clone the Node.js Application Repository
1. Open your terminal.
2. Clone the repository:
   ```bash
   git clone https://github.com/LondheShubham153/node-todo-cicd.git
   ```
3. Navigate to the project directory:
   ```bash
   cd node-todo-cicd
   ```

---

### 2. Build the Docker Image
1. Create a Docker image using the provided `Dockerfile`:
   ```bash
   docker build -t node-todo-app .
   ```

2. Verify the image:
   ```bash
   docker images
   ```

---

### 3. Set Up AWS CLI
1. Install the AWS CLI if not already installed:
   ```bash
   curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
   sudo installer -pkg AWSCLIV2.pkg -target /
   ```

2. Configure AWS CLI:
   ```bash
   aws configure
   ```
   Provide your **Access Key ID**, **Secret Access Key**, **Region**, and **Output format**.

---

### 4. Push the Image to AWS ECR
1. Authenticate Docker to your ECR:
   ```bash
   aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.<your-region>.amazonaws.com
   ```

2. Create a repository in ECR:
   ```bash
   aws ecr create-repository --repository-name node-todo-app
   ```

3. Tag the Docker image:
   ```bash
   docker tag node-todo-app:latest <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/node-todo-app:latest
   ```

4. Push the image to ECR:
   ```bash
   docker push <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/node-todo-app:latest
   ```

---

### 5. Set Up an ECS Cluster
1. Go to the **ECS Console** in AWS.
2. Create a new cluster:
   - Select "Networking only" (Fargate).
   - Provide a name for your cluster.
   - Click "Create."

---

### 6. Create a Task Definition
1. Go to the **Task Definitions** section.
2. Create a new task definition:
   - Select "Fargate" as the launch type.
   - Define the task role and execution role.
   - Add a container:
     - Image: `<your-account-id>.dkr.ecr.<your-region>.amazonaws.com/node-todo-app:latest`
     - Port: 3000

3. Save and create the task definition.

---

### 7. Deploy the Application
1. Navigate to your ECS cluster.
2. Click on "Create Service":
   - Launch type: Fargate
   - Task definition: Select the one created earlier.
   - Cluster: Select your cluster.
   - Service name: Provide a name.
   - Number of tasks: 1 (or more, based on requirement).

3. Configure the VPC and subnets for networking.
4. Click "Create Service."

---

### 8. Test the Application
1. Go to the **Service** section of your ECS cluster.
2. Note the public IP or DNS of the load balancer (if configured).
3. Access the application in your browser:
   ```
   http://<public-ip>:3000
   ```

---

### 🎉 Congratulations
Your Node.js application is now successfully deployed on AWS ECS Fargate and ECR! 🚀
