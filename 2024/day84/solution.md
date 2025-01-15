# Project-5: Deploying a Netflix Clone on Kubernetes

## Project Description

This project involves deploying a Netflix clone web application on a Kubernetes cluster, leveraging container orchestration for simplified deployment and management. It includes the following steps:

1. Creating Docker images for the Netflix clone application and its dependencies.
2. Deploying these images on a Kubernetes cluster using Kubernetes manifests.
3. Utilizing Kubernetes tools such as the Kubernetes Dashboard and `kubectl` for monitoring and management.

### Benefits:
- High availability
- Scalability
- Automatic failover

This project demonstrates the capabilities of Kubernetes in managing containerized applications at scale.

---

## Task-01: Deploy a Netflix Clone

### Steps to Follow:

1. **Clone the Repository:**
   
   Clone the Netflix clone repository from GitHub:
   ```bash
   git clone https://github.com/devandres-tech/Netflix-Clone.git
   cd Netflix-Clone
   ```

2. **Read Reference Material:**

   Go through this [reference article](https://www.linkedin.com/posts/chetanrakhra_devops-project-share-activity-7034173810656296960-UjUw?utm_source=share&utm_medium=member_desktop) to understand how to deploy a Reddit clone and apply the same steps for the Netflix clone.

3. **Create Docker Images:**
   
   Build Docker images for the Netflix clone application:
   ```bash
   docker build -t netflix-clone:latest .
   ```

4. **Set Up a Kubernetes Cluster:**
   
   - Use a managed Kubernetes service (e.g., Google Kubernetes Engine, AWS EKS) or set up a local cluster with Minikube.
   - Verify your Kubernetes setup:
     ```bash
     kubectl cluster-info
     ```

5. **Create Kubernetes Manifests:**
   
   Define the necessary Kubernetes manifests (Deployment, Service, Ingress, etc.):
   
   - **Deployment:** Deploy the application pods.
   - **Service:** Expose the pods for external access.
   - **Ingress (Optional):** Configure an ingress for routing traffic.

   Example `deployment.yaml`:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: netflix-clone-deployment
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: netflix-clone
     template:
       metadata:
         labels:
           app: netflix-clone
       spec:
         containers:
         - name: netflix-clone
           image: netflix-clone:latest
           ports:
           - containerPort: 3000
   ```

6. **Deploy on Kubernetes:**
   
   Apply the manifests to deploy the application:
   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

7. **Monitor and Manage:**
   
   Use Kubernetes tools for monitoring and management:
   - Access the Kubernetes Dashboard.
   - Use `kubectl` commands to check pod and service status:
     ```bash
     kubectl get pods
     kubectl get services
     ```

---

## Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Kubernetes Dashboard Setup](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)

---

## Happy Learning!

Let me know your thoughts or if you face any challenges!
