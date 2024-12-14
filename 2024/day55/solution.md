# Day 55: Mastering Configuration Management with Ansible

## 🧐 *What’s this Ansible, bhaiyya?*

**Ansible** is an open-source automation tool that makes IT tasks like configuration management, application deployment, service orchestration, and provisioning a breeze. It's simple yet powerful—perfect for automating your DevOps workflows!

---

## 🎯 **Today's Task Overview**

1️⃣ **Install Ansible on AWS EC2 (Master Node)**  
2️⃣ **Learn About the Hosts File**  
3️⃣ **Set Up and Ping EC2 Instances Using Ansible**  

---

## 💻 **Solution Code**

### **Task-01: Installing Ansible on the Master Node**
Run these commands on your Master EC2 instance:
```bash
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```

### **Task-02: Editing the Hosts File**
Open the hosts file to define target nodes:
```bash
sudo nano /etc/ansible/hosts
```
Add the private IPs of your nodes:
```
[aws-nodes]
<PRIVATE_IP_NODE_1>
<PRIVATE_IP_NODE_2>
```
List inventory for verification:
```bash
ansible-inventory --list -y
```

### **Task-03: Setting Up and Pinging Nodes**

1️⃣ Launch two new EC2 instances (Nodes) using the same key pair as the Master.  

2️⃣ Copy the private key to the Master EC2 instance:
```bash
scp -i <YOUR_PRIVATE_KEY>.pem <YOUR_PRIVATE_KEY>.pem ubuntu@<MASTER_PRIVATE_IP>:/home/ubuntu/
```

3️⃣ Set proper permissions for the private key on the Master:
```bash
chmod 400 <YOUR_PRIVATE_KEY>.pem
```

4️⃣ Test connectivity to the nodes using Ansible:
```bash
ansible aws-nodes -m ping --private-key <YOUR_PRIVATE_KEY>.pem
```

---

## ✨ **Next Steps**
- Write a blog about your experience with screenshots and post it on LinkedIn.
- Share your learnings and inspire others to explore Ansible!

---

## Happy Learning! 😊
