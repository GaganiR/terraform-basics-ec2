# Overview
Terraform project that launches an AWS EC2 instance. Breaking in to the world of Infrastructure as Code, using Terraform we can easily manage the resources in any cloud provider. These configuration files will be stored in version control systems like Git.
## Prerequisites
* Terraform installed >= 1.2.0
* AWS CLI installed and configured with valid credentials
* An AWS account
## Create a new directory
Create a new directory for the Terraform project, and navigate into it.
```
mkdir terraform-ec2-demo
cd terraform-ec2-demo
```
## Create main.tf file
Create main.tf file and add he following script to it.
```
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
  region  = "us-west-2"
}

resource "aws_instance" "app_server" {
  ami           = "ami-830c94e3"
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform_Demo"
  }
}
```
![main](https://github.com/user-attachments/assets/2d2698b1-1864-4974-8efb-98bf0a28321a)
This Terraform script (`main.tf`) sets up the following:

- **Initializes the AWS provider** with a specified version constraint.
- **Configures the AWS region** to `us-west-2`.
- **Creates a single EC2 instance** using a specific Amazon Machine Image (AMI) and instance type (`t2.micro`).
- **Adds a tag** to the instance for easy identification (`Name = Terraform_Demo`).
## Initialize the Terraform Project
Run the following command to initialize the project. This downloads the necessary provider plugins (e.g., AWS). It ensures everything is ready before creating infrastructure.
```
terraform init
```
![init](https://github.com/user-attachments/assets/2bc84190-4282-4120-8964-95e9ab0268ad)
## Preview the Infrastructure Changes
This command lets you review the changes before applying them (nothing is executed yet). It shows you what resources will be created, modified, or destroyed. 
```
terraform plan
```
![plan](https://github.com/user-attachments/assets/b955cb1a-7d0f-4504-bb35-3221d6b07dbe)
## Apply the Configuration
Executes the actions proposed in the plan. In our script, it will create an EC2 instance.
```
terraform apply
```
![apply](https://github.com/user-attachments/assets/31c12a3c-e476-4e83-8525-7bd870b0637c)
![ec2](https://github.com/user-attachments/assets/ef0234ff-64fc-4fa5-8b2f-7af2f3e82f0e)

## Destroy the Infrastructure 
Delete resources to avoid unexpected charges.
```
terraform destroy
```
![destroy](https://github.com/user-attachments/assets/a57e92e8-b540-49aa-be90-1f1bd5b2f7ed)

## Notes
* AMI ID ami-830c94e3 is specific to the us-west-2 region. Use a valid one for other regions.

* t2.micro is eligible for the AWS Free Tier.
