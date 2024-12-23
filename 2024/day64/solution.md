# Day 64 - Terraform with AWS

Provisioning on AWS is quite easy and straightforward with Terraform.

---

## Prerequisites

### AWS CLI Installed

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

### AWS IAM User

IAM (Identity and Access Management) AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

**In order to connect your AWS account and Terraform, you need the access keys and secret access keys exported to your machine.**

```bash
export AWS_ACCESS_KEY_ID=<access key>
export AWS_SECRET_ACCESS_KEY=<secret access key>
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
resource "aws_instance" "aws_ec2_test" {
  count = 4
  ami = "ami-08c40ec9ead489470"
  instance_type = "t2.micro"
  tags = {
    Name = "TerraformTestServerInstance"
  }
}

This `.md` file includes all the information in the correct order with clear sections and formatting.
