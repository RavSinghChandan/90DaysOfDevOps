# Day 75 - Sending Docker Logs to Grafana

We have monitored 😉 that you are understanding and doing amazing with monitoring tools.👌  
Today, let's make it a bit more complex yet interesting 😍 by integrating Docker logs with Grafana. This task will not only enhance your monitoring skills but also add a **Project** 🔥 to your resume.

---

## Solution

### Prerequisites:
1. A Linux-based EC2 instance (Amazon Linux 2 or Ubuntu preferred).
2. Installed and configured Grafana with the Docker plugin enabled.
3. Basic understanding of Docker and Grafana.

---

## Steps to Complete the Task

### 1. Install Docker and Start the Docker Service
Use **User Data** to automate Docker installation during EC2 instance launch.  
Here's the User Data script:  
```bash
#!/bin/bash
sudo apt-get update -y
sudo apt-get install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
2. Launch Docker Containers
Create two Docker containers running a basic application like a Todo app:

bash
Copy code
# Pull the image for the app
docker pull kodekloud/simpletodo

# Run the first container
docker run -d --name todo_app_1 -p 8080:80 kodekloud/simpletodo

# Run the second container
docker run -d --name todo_app_2 -p 8081:80 kodekloud/simpletodo
3. Install and Configure the Docker Logging Driver
Enable the JSON logging driver to forward logs to a specific location or service:

Create a Docker configuration file:
bash
Copy code
sudo nano /etc/docker/daemon.json
Add the following configuration to enable JSON logging:
json
Copy code
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
Restart the Docker service to apply changes:
bash
Copy code
sudo systemctl restart docker
4. Integrate Docker with Grafana
Install Prometheus Node Exporter:

bash
Copy code
docker run -d --name prometheus -p 9090:9090 prom/prometheus
Enable Docker Monitoring with Prometheus:

bash
Copy code
docker run -d \
-p 3000:3000 \
--name grafana \
-e "GF_SECURITY_ADMIN_PASSWORD=admin" \
grafana/grafana
Connect Grafana to Prometheus:

Access Grafana UI via http://<your-ec2-instance-ip>:3000.
Login with default credentials (admin/admin).
Navigate to Settings > Data Sources > Add Data Source.
Select Prometheus and provide the endpoint http://<your-ec2-instance-ip>:9090.
Enable the Docker Plugin on Grafana:

In Grafana, go to the Plugins section and search for the Docker plugin.
Enable the plugin and configure it to read the logs from your Docker containers.
5. Visualize Logs on Grafana
Go to Grafana > Explore.
Select the Docker data source and query the logs.
You can filter logs based on container names (todo_app_1 or todo_app_2).