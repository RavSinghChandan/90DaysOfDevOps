# Day 74 - Connecting EC2 with Grafana

## Overview

In this task, you will connect a Linux and a Windows EC2 instance to Grafana to monitor different components of the servers.

## Prerequisites

1. **Grafana Installed:** Ensure Grafana is set up locally or on a server.
2. **EC2 Instances:** One Linux and one Windows EC2 instance are launched and accessible.
3. **Access Permissions:** Appropriate IAM roles and security group configurations for accessing and monitoring EC2 instances.

---

## Steps

### 1. Install Node Exporter on Linux EC2 Instance

1. **SSH into the Linux instance:**
   ```bash
   ssh -i "your-key.pem" ec2-user@<Linux-EC2-IP>
   ```
2. **Download Node Exporter:**
   ```bash
   wget https://github.com/prometheus/node_exporter/releases/latest/download/node_exporter-linux-amd64.tar.gz
   ```
3. **Extract the package:**
   ```bash
   tar xvfz node_exporter-linux-amd64.tar.gz
   ```
4. **Run Node Exporter:**
   ```bash
   cd node_exporter-* && ./node_exporter &
   ```
5. **Verify Node Exporter is running:**
   Open `<Linux-EC2-IP>:9100/metrics` in a browser.

### 2. Install Windows Exporter on Windows EC2 Instance

1. **RDP into the Windows instance.**
2. **Download the Windows Exporter:**
   Visit [Windows Exporter](https://github.com/prometheus-community/windows_exporter/releases).
3. **Install the Windows Exporter:**
   Run the `.msi` installer and follow the instructions.
4. **Start the service:**
   Open **Services**, find **windows_exporter**, and start it.
5. **Verify Windows Exporter is running:**
   Open `<Windows-EC2-IP>:9182/metrics` in a browser.

### 3. Configure Grafana to Monitor EC2 Instances

1. **Log in to Grafana:**
   Open Grafana in your browser and log in.
2. **Add Prometheus Data Source:**
   - Go to **Configuration** > **Data Sources**.
   - Click **Add data source** and select **Prometheus**.
   - Enter the URL of your Prometheus server and save.
3. **Add Linux EC2 Node Exporter Dashboard:**
   - Go to **+ > Import**.
   - Use **Node Exporter Full Dashboard** (Dashboard ID: `1860`).
   - Link the data source and save.
4. **Add Windows EC2 Exporter Dashboard:**
   - Similarly, import a dashboard specific to Windows Exporter.
   - Link the data source and save.

### 4. Verify Metrics in Grafana

1. **Navigate to the Dashboards:**
   - Open the dashboards for Linux and Windows EC2 instances.
2. **Confirm Metrics:**
   - Ensure you can see CPU, memory, disk usage, and other metrics for both instances.

---

## Summary

You have successfully connected a Linux and a Windows EC2 instance to Grafana and are monitoring their metrics. Great job! 🎉
