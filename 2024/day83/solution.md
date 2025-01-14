# Comprehensive Guide to Deploying Web Applications

This file provides a step-by-step solution for deploying web applications using **Docker Swarm** and **Kubernetes**, covering the complete process for both orchestration tools.

---

## 🚀 Step 1: Clone the Application Repository

1. Choose the application to deploy (e.g., Netflix Clone or another web app). 
   - Netflix Clone: [GitHub Link](https://github.com/devandres-tech/Netflix-Clone)
   
2. Clone the repository using the following command:
   ```bash
   git clone <repository-link>
   ```

---

## 🐳 Step 2: Containerize the Application

1. Navigate to the project directory:
   ```bash
   cd <project-directory>
   ```
2. Create a `Dockerfile` to containerize the application. Example:
   ```dockerfile
   FROM node:14
   WORKDIR /app
   COPY package*.json ./
   RUN npm install
   COPY . .
   CMD ["npm", "start"]
   EXPOSE 3000
   ```
3. Build the Docker image:
   ```bash
   docker build -t <image-name>:<tag> .
   ```
4. Test the image locally:
   ```bash
   docker run -p 3000:3000 <image-name>:<tag>
   ```

---

## ⚙️ Step 3: Deploy with Docker Swarm

### Initialize Docker Swarm:
1. Start the Swarm mode:
   ```bash
   docker swarm init
   ```
2. Verify the Swarm status:
   ```bash
   docker info
   ```

### Deploy the Application:
1. Create a `docker-compose.yml` file for the Swarm deployment. Example:
   ```yaml
   version: "3.8"
   services:
     web:
       image: <image-name>:<tag>
       ports:
         - "80:3000"
       deploy:
         replicas: 3
         resources:
           limits:
             cpus: "0.5"
             memory: "512M"
         restart_policy:
           condition: on-failure
   ```
2. Deploy the stack:
   ```bash
   docker stack deploy -c docker-compose.yml <stack-name>
   ```
3. Monitor the deployment:
   ```bash
   docker service ls
   docker service ps <service-name>
   ```

---

## ☸️ Step 4: Deploy with Kubernetes

### Setup Kubernetes Cluster:
1. Install Kubernetes tools:
   ```bash
   sudo apt-get install kubectl minikube
   ```
2. Start a local Kubernetes cluster:
   ```bash
   minikube start
   ```
3. Verify the cluster status:
   ```bash
   kubectl cluster-info
   ```

### Deploy the Application:
1. Create Kubernetes manifests:
   - **Deployment** (`deployment.yaml`):
     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: web-deployment
     spec:
       replicas: 3
       selector:
         matchLabels:
           app: web
       template:
         metadata:
           labels:
             app: web
         spec:
           containers:
           - name: web
             image: <image-name>:<tag>
             ports:
             - containerPort: 3000
     ```
   - **Service** (`service.yaml`):
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: web-service
     spec:
       type: NodePort
       selector:
         app: web
       ports:
       - protocol: TCP
         port: 80
         targetPort: 3000
         nodePort: 30080
     ```
2. Apply the manifests:
   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```
3. Verify the deployment:
   ```bash
   kubectl get pods
   kubectl get services
   ```
4. Access the application:
   ```bash
   minikube service web-service
   ```

---

## 🛠️ Step 5: Monitor and Manage

- **Docker Swarm**:
  - Use `docker service ls` and `docker service ps` for service status.
  - Scale services:
    ```bash
    docker service scale <service-name>=<replica-count>
    ```

- **Kubernetes**:
  - View pod logs:
    ```bash
    kubectl logs <pod-name>
    ```
  - Scale deployments:
    ```bash
    kubectl scale deployment web-deployment --replicas=<count>
    ```

---

## 🎯 Summary

This guide provides all the steps to deploy a web application using Docker Swarm and Kubernetes. Both tools offer unique advantages for container orchestration, making them essential for production-grade deployments.

Happy Learning! 🚀
