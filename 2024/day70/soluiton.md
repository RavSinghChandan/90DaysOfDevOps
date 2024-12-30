# Day 70 - Terraform Modules

## Introduction
Modules in Terraform are containers for multiple resources that can be used together. They enable reusability, consistency, and a modular approach in Infrastructure as Code (IaC). A module can call other modules, simplifying the inclusion of resources into configurations.

---

## Steps to Use Modules in Terraform

### Step 1: Create Resource Configuration
Define your resource in a `.tf` file with parameters for reusability. Below is an example of an AWS EC2 instance configuration:

```hcl
# Creating an AWS EC2 Instance
resource "aws_instance" "server-instance" {
  instance_count          = var.number_of_instances
  ami                    = var.ami
  instance_type          = var.instance_type
  subnet_id              = var.subnet_id
  vpc_security_group_ids = var.security_group

  tags = {
    Name = var.instance_name
  }
}
# Variables for Server Module
variable "number_of_instances" {
  description = "Number of Instances to Create"
  type        = number
  default     = 1
}

variable "instance_name" {
  description = "Instance Name"
}

variable "ami" {
  description = "AMI ID"
  default     = "ami-xxxx"
}

variable "instance_type" {
  description = "Instance Type"
}

variable "subnet_id" {
  description = "Subnet ID"
}

variable "security_group" {
  description = "Security Group"
  type        = list(any)
}
# Output for Server Module
output "server_id" {
  description = "Server ID"
  value       = aws_instance.server-instance.id
}
module "server" {
  source             = "./server-module"
  number_of_instances = 2
  instance_name       = "MyServer"
  ami                = "ami-0abc123"
  instance_type      = "t2.micro"
  subnet_id          = "subnet-0abc123"
  security_group     = ["sg-0abc123"]
}
