# Terraform Meta-Arguments

Terraform meta-arguments are special configuration options that apply to all resources and modules, giving you control over resource creation, dependencies, scaling, and lifecycle behavior. The most important ones are count, for_each, depends_on, lifecycle, and provider.

## depends_on
The depends_on meta-argument in Terraform is used to explicitly declare that a resource or module depends on one or more other resources or modules, ensuring Terraform processes them in the correct order. Unlike normal references, it does not read or pass values; it only enforces execution order when Terraform cannot automatically infer the dependency. In short, it’s a way of telling Terraform: “Don’t touch this until those are finished.”

  resource "aws_instance" "example" {
    ami           = "ami-a1b2c3d4"
    instance_type = "t2.micro"
    depends_on = [
      aws_iam_role_policy.example
    ]
  }

## count
In Terraform, the count meta-argument is used to create multiple instances of a resource or module based on a numeric value. It acts like a loop counter: if you set count = 3, Terraform will create three identical resources, each indexed from 0 to 2. You can then reference them individually using resource_name[count.index]. This is especially useful for provisioning repeated infrastructure (like multiple servers, buckets, or subnets) without duplicating code. In short, count lets you scale resources up or down by simply changing a number.

Example 1: Multiple EC2 Instances

  resource "aws_instance" "server" {
    count = 4 
    ami = "ami-a1b2c3d4"
    instance_type = "t2.micro"
    tags = {
      Name = "Server ${count.index}"
    }
  }

Example 2: Conditional Resource Creation

  resource "aws_s3_bucket" "example" {
    count  = var.create_bucket ? 1 : 0
    bucket = "my-example-bucket"
  }

Example 3: Multiple Subnets

  resource "aws_subnet" "example" {
    count             = length(var.subnet_cidrs)
    vpc_id            = aws_vpc.main.id
    cidr_block        = var.subnet_cidrs[count.index]
    availability_zone = var.azs[count.index]
  }

Example 4: Modules with Count

  module "server" {
    count  = 2
    source = "./modules/ec2"
    name   = "server-${count.index}"
  }

Example 5: Data Resources with Count

  data "aws_ami" "ubuntu" {
    count       = 2
    most_recent = true
    owners      = ["099720109477"]
    filter {
      name   = "name"
      values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
    }
  }

## for_each
In Terraform, the for_each meta-argument is used to create multiple instances of a resource or module based on a map or set of strings, instead of just a number like count. Each instance is identified by a unique key, which makes it easier to manage and reference specific resources. Unlike count, which uses numeric indexes (0, 1, 2…), for_each lets you work with meaningful keys (like names or IDs), making configurations more readable and flexible.

Example 1: Using a Set of Strings

  resource "aws_s3_bucket" "example" {
    for_each = toset(["logs", "media", "backup"])
    bucket = "my-${each.key}-bucket"
  }

Example 2: Using a Map

  resource "aws_s3_bucket" "example" {
    for_each = {
      logs   = "logs-bucket"
      media  = "media-bucket"
      backup = "backup-bucket"
    }
    bucket = each.value
  }

## lifecycle
The lifecycle meta-argument in Terraform allows you to control the behavior of resources during creation, update, and deletion. It provides options to prevent accidental destruction, ignore changes to specific attributes, and manage resource replacement. The main lifecycle blocks are create_before_destroy, prevent_destroy, and ignore_changes.

Example 1: Preventing Resource Destruction

  resource "aws_s3_bucket" "example" {
    bucket = "my-important-bucket"
    lifecycle {
      prevent_destroy = true
    }
  }

Example 2: Ignoring Changes to Specific Attributes

  resource "aws_instance" "example" {
    ami           = "ami-a1b2c3d4"
    instance_type = "t2.micro"
    lifecycle {
      ignore_changes = [tags]
    }
  }

Example 3: Create Before Destroy

  resource "aws_instance" "example" {
    ami           = "ami-a1b2c3d4"
    instance_type = "t2.micro"
    lifecycle {
      create_before_destroy = true
    }
  }

## provider
The provider meta-argument in Terraform is used to specify which provider configuration a resource or module should use. This is particularly useful when you have multiple provider configurations (e.g., for different regions, accounts, or environments) and want to ensure that specific resources are created using the correct provider settings. By referencing the provider configuration, you can control where and how your resources are provisioned.

Example 1: Using a Specific Provider Configuration

  provider "aws" {
    alias  = "us_east"
    region = "us-east-1"
  }
  provider "aws" {
    alias  = "us_west"
    region = "us-west-2"
  }
  resource "aws_instance" "example" {
    provider      = aws.us_east
    ami           = "ami-a1b2c3d4"
    instance_type = "t2.micro"
  }

Example 2: Using a Provider in a Module

  module "example" {
    source   = "./modules/example"
    provider = aws.us_west
  }

## providers
In Terraform, the providers (plural) argument is used inside a module block to tell Terraform which provider configuration that module should use. By default, a child module inherits the parent’s default provider settings, but if you have defined multiple provider configurations (for example, AWS in different regions or accounts), you can override this behavior by passing the desired provider alias through the providers argument. This ensures that all resources inside that module are created using the specified provider configuration. In short, providers lets you control which provider a module uses, making it possible to reuse the same module across different regions, accounts, or even clouds without changing the module’s internal code.

Example 1: Using Providers in a Module

  provider "aws" {
    region = "us-west-1"
  }

  provider "aws" {
    alias  = "usw2"
    region = "us-west-2"
  }

  module "example" {
    source    = "./example"
    providers = {
      aws = aws.usw2
    }
  }



