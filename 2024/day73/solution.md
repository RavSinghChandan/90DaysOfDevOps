# Setting up Grafana on AWS EC2

This guide will help you set up Grafana on an AWS EC2 instance step by step.

---

## **Step 1: Launch an EC2 Instance**

1. Log in to your AWS Management Console.
2. Navigate to **EC2 Dashboard** and click on **Launch Instance**.
3. Configure your instance:
   - **Choose an Amazon Machine Image (AMI):** Select a Linux-based AMI (e.g., Ubuntu 20.04 LTS).
   - **Instance Type:** Choose an instance type like `t2.micro` (sufficient for basic Grafana setup).
   - **Configure Key Pair:** Create or use an existing key pair to access your instance securely.
   - **Security Group:** Add inbound rules to allow HTTP (port 80), HTTPS (port 443), and SSH (port 22).

4. Launch the instance and note down the **public IP address**.

---

## **Step 2: Connect to the EC2 Instance**

1. Open a terminal and connect to your EC2 instance using SSH:

   ```bash
   ssh -i /path/to/key.pem ubuntu@<public-ip>
   ```

2. Update the system packages:

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

## **Step 3: Install Grafana**

1. Add the Grafana APT repository:

   ```bash
   sudo apt-get install -y software-properties-common
   wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
   echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
   ```

2. Update the package list and install Grafana:

   ```bash
   sudo apt update
   sudo apt install -y grafana
   ```

3. Start and enable the Grafana service:

   ```bash
   sudo systemctl start grafana-server
   sudo systemctl enable grafana-server
   ```

---

## **Step 4: Configure Security Group for Grafana**

1. Go to the EC2 Dashboard in AWS.
2. Select your instance, click on **Security Groups**, and edit the inbound rules.
3. Add the following rule:
   - **Type:** Custom TCP Rule
   - **Protocol:** TCP
   - **Port Range:** 3000
   - **Source:** Anywhere (or specify a range for restricted access)

---

## **Step 5: Access Grafana**

1. Open a web browser and navigate to:

   ```
   http://<public-ip>:3000
   ```

2. Log in using the default credentials:
   - **Username:** admin
   - **Password:** admin

3. Change the password when prompted.

---

## **Step 6: Finalize and Start Using Grafana**

- Add data sources like Prometheus, MySQL, or others.
- Create dashboards to visualize your data.

---

## **Troubleshooting**

1. If Grafana doesn't start, check the service status:

   ```bash
   sudo systemctl status grafana-server
   ```

2. Review logs for more details:

   ```bash
   sudo journalctl -u grafana-server
   ```

---

Your Grafana setup on AWS EC2 is now complete! 🎉
