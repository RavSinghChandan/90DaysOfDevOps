# Day 59: Ansible Project 🔥

Ansible playbooks are amazing, as you learned yesterday.  
What if you deploy a simple web app using Ansible? Sounds like a good project, right?  

---

## **Task-01**

### **Step-by-Step Guide**

---

### 1. **Create 3 EC2 Instances**
1. Log in to your AWS Management Console.  
2. Launch three EC2 instances:  
   - Use the same key pair for all instances.  
   - Choose Ubuntu as the OS for simplicity.  

Alternatively, use the AWS CLI:  
```bash
aws ec2 run-instances --image-id ami-12345678 --count 3 --instance-type t2.micro --key-name your-key-name --security-group-ids sg-12345678 --subnet-id subnet-12345678
ssh -i your-key.pem ubuntu@your-host-ip
sudo apt update
sudo apt install ansible -y
scp -i your-key.pem your-key.pem ubuntu@your-host-ip:/home/ubuntu/.ssh
chmod 600 /home/ubuntu/.ssh/your-key.pem
sudo vim /etc/ansible/hosts
[webservers]
ec2-instance-1-ip ansible_ssh_private_key_file=/home/ubuntu/.ssh/your-key.pem ansible_user=ubuntu
ec2-instance-2-ip ansible_ssh_private_key_file=/home/ubuntu/.ssh/your-key.pem ansible_user=ubuntu
ec2-instance-3-ip ansible_ssh_private_key_file=/home/ubuntu/.ssh/your-key.pem ansible_user=ubuntu
