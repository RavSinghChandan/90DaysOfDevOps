# Day 63 - Terraform Variables

## Introduction

Terraform variables are a cornerstone of efficient and reusable configurations. Whether it’s the name of an instance, configurations, or dynamic content, variables help keep your code clean and organized.

## Declaring Variables

You can use a `variables.tf` file to hold all your variable definitions. Here’s an example:

```hcl
variable "filename" {
  default = "/home/ubuntu/terraform-tutorials/terraform-variables/demo-var.txt"
}

variable "content" {
  default = "This is coming from a variable which was updated"
}
```

These variables can then be accessed in `main.tf` using the `var` object. For example:

```hcl
resource "local_file" "devops" {
  filename = var.filename
  content  = var.content
}
```

## Task-01: Create a Local File

Use the above configuration to create a local file using Terraform.

## Data Types in Terraform

### Map Example

```hcl
variable "file_contents" {
  type = map
  default = {
    "statement1" = "this is cool"
    "statement2" = "this is cooler"
  }
}
```

### Task-02: Demonstrate List, Set, and Object Data Types

Below is an example of how to define and use List, Set, and Object data types:

#### List Example
```hcl
variable "example_list" {
  type = list
  default = ["item1", "item2", "item3"]
}

output "list_output" {
  value = var.example_list
}
```

#### Set Example
```hcl
variable "example_set" {
  type = set
  default = ["itemA", "itemB", "itemC"]
}

output "set_output" {
  value = var.example_set
}
```

#### Object Example
```hcl
variable "example_object" {
  type = object({
    name = string
    age  = number
  })
  default = {
    name = "TerraformUser"
    age  = 30
  }
}

output "object_output" {
  value = var.example_object
}
```

## Using `terraform refresh`

You can use `terraform refresh` to reload your state based on the configuration file and variables.

## Additional Resources

If Terraform seems tricky, check out this amazing **free Terraform course** to get started: [bit.ly/tws-terraform](https://bit.ly/tws-terraform)

## Happy Learning!

[← Previous Day](../day62/README.md) | [Next Day →](../day64/README.md)
