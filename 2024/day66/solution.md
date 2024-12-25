# Terraform Hands-on Project Solution - Day 66

## Task Overview

This hands-on project involves creating an AWS infrastructure using Terraform. Below is the solution with step-by-step instructions and Terraform code snippets for each requirement.

---

## 1. Initialize Terraform Project

1. Create a directory for your Terraform project and navigate to it:
   ```bash
   mkdir terraform_day66 && cd terraform_day66
   ```
2. Create a `main.tf` file for your Terraform configuration.

---

## 2. Define Providers

```hcl
provider "aws" {
  region = "us-east-1" # Update to your preferred region
}
```

---

## 3. Create a VPC

```hcl
resource "aws_vpc" "main" {
  cidr_block       = "10.0.0.0/16"
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name = "Day66-VPC"
  }
}
```

---

## 4. Create Subnets

### Public Subnet
```hcl
resource "aws_subnet" "public" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.1.0/24"
  map_public_ip_on_launch = true

  tags = {
    Name = "Day66-Public-Subnet"
  }
}
```

### Private Subnet
```hcl
resource "aws_subnet" "private" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.2.0/24"

  tags = {
    Name = "Day66-Private-Subnet"
  }
}
```

---

## 5. Create an Internet Gateway

```hcl
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "Day66-IGW"
  }
}
```

---

## 6. Create a Route Table and Associate with Public Subnet

### Route Table
```hcl
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }

  tags = {
    Name = "Day66-Public-Route-Table"
  }
}
```

### Route Table Association
```hcl
resource "aws_route_table_association" "public" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public.id
}
```

---

## 7. Launch an EC2 Instance in Public Subnet

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0557a15b87f6559cf"
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.public.id

  security_groups = [aws_security_group.web_sg.name]

  user_data = <<-EOF
    #!/bin/bash
    sudo yum update -y
    sudo yum install -y httpd
    sudo systemctl start httpd
    sudo systemctl enable httpd
    echo "<h1>Welcome to Terraform Day 66 Project</h1>" | sudo tee /var/www/html/index.html
  EOF

  tags = {
    Name = "Day66-Web-Instance"
  }
}
```

---

## 8. Create Security Group for EC2

```hcl
resource "aws_security_group" "web_sg" {
  name_prefix = "Day66-Web-SG"
  vpc_id      = aws_vpc.main.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "Day66-Web-Security-Group"
  }
}
```

---

## 9. Allocate and Associate an Elastic IP

```hcl
resource "aws_eip" "web_eip" {
  instance = aws_instance.web.id

tags = {
    Name = "Day66-EIP"
  }
}
```

---

## 10. Verify Hosted Website

After applying the configuration, copy the Elastic IP from the output and paste it into your browser to verify the hosted website.

---

## Apply Terraform Configuration

1. Initialize Terraform:
   ```bash
   terraform init
   ```
2. Validate the configuration:
   ```bash
   terraform validate
   ```
3. Plan the resources:
   ```bash
   terraform plan
   ```
4. Apply the configuration:
   ```bash
   terraform apply
   ```
5. Confirm by typing `yes` when prompted.

---

## Output Example

After successful execution, you should see:
- VPC, Subnets, IGW, Route Table, EC2 instance, and Elastic IP created.
- The website accessible via the Elastic IP.

---

### That’s it! You’ve successfully completed Day 66 of the Terraform hands-on project.

**Happy Terraforming!** 🚀
