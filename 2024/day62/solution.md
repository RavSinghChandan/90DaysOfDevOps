# Day 62 - Terraform and Docker 🔥

Terraform requires specifying the provider in the automation script. For Docker, you can use the following code in your `main.tf` file:

---

## Terraform Block

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.21.0"
    }
  }
}
provider "docker" {}
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "tutorial"
  ports {
    internal = 80
    external = 80
  }
}
sudo apt-get install docker.io  
sudo docker ps  
sudo chown $USER /var/run/docker.sock  
