# Day 69 - Meta-Arguments in Terraform

## Steps to Follow:

1. **Install Terraform**  
   Ensure Terraform is installed on your system. If not, download it from the [official Terraform website](https://www.terraform.io/downloads).

2. **Set Up Your AWS Credentials**  
   - Configure your AWS credentials using the AWS CLI or by setting up an `~/.aws/credentials` file.

3. **Create a New Terraform Directory**  
   - Initialize a directory for Terraform code:  
     ```bash
     mkdir terraform-meta-arguments
     cd terraform-meta-arguments
     ```

4. **Write Terraform Code for `count`**  
   Create a file `main.tf` with the following code:

   ```hcl
   terraform {
     required_providers {
       aws = {
         source  = "hashicorp/aws"
         version = "~> 4.16"
       }
     }
     required_version = ">= 1.2.0"
   }

   provider "aws" {
     region = "us-east-1"
   }

   resource "aws_instance" "server" {
     count         = 4
     ami           = "ami-08c40ec9ead489470"
     instance_type = "t2.micro"
     tags = {
       Name = "Server ${count.index}"
     }
   }
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }
  required_version = ">= 1.2.0"
}

provider "aws" {
  region = "us-east-1"
}

locals {
  ami_ids = toset([
    "ami-0b0dcb5067f052a63",
    "ami-08c40ec9ead489470",
  ])
}

resource "aws_instance" "server" {
  for_each = local.ami_ids
  ami           = each.key
  instance_type = "t2.micro"
  tags = {
    Name = "Server ${each.key}"
  }
}
locals {
  ami_ids = {
    "linux"  = "ami-0b0dcb5067f052a63",
    "ubuntu" = "ami-08c40ec9ead489470",
  }
}

resource "aws_instance" "server" {
  for_each = local.ami_ids
  ami           = each.value
  instance_type = "t2.micro"
  tags = {
    Name = "Server ${each.key}"
  }
}
Apply the Configuration

Initialize the Terraform project:
bash
Copy code
terraform init
Validate the configuration:
bash
Copy code
terraform validate
Plan the changes:
bash
Copy code
terraform plan
Apply the changes:
bash
Copy code
terraform apply
Verify the Resources in AWS

Log in to your AWS Management Console and check the EC2 instances created by Terraform.
