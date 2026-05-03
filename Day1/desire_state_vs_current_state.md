What is Desired State?

The Desired State refers to the configuration you define in your Terraform code. This is the blueprint or specification of the infrastructure you want to create or manage. For example, when defining an EC2 instance, you specify attributes such as:

AMI (Amazon Machine Image): The image you want to use to launch the EC2 instance.
Instance Type: The size of the EC2 instance, such as t2.micro.
Tags: Metadata to categorize the instance.
In this case, your Terraform configuration might look something like this:

resource "aws_instance" "my_instance" {
  ami = "ami-12345678"
  instance_type = "t2.micro"
  tags = {
    Name = "MyInstance"
  }
 }

This code represents the Desired State of your infrastructure. It defines that you want an EC2 instance with a specific AMI, a t2.micro instance type, and a tag for identification.

How Does Terraform Handle the Desired State?

Once you’ve written your Terraform configuration, you can apply it using the Terraform commands. The key commands for managing Terraform configurations are:

terraform plan: This command shows the actions Terraform will take to reach the desired state.
terraform apply: This command actually applies the changes, creating or updating resources to match the desired state.
When you run terraform apply for the first time, Terraform compares the Desired State (the configuration you wrote) with the Current State (the resources that currently exist in your cloud environment). If the current state is empty (i.e., no resources are yet created), Terraform will create the resources as defined in your code.

What is Current State?

The Current State is a snapshot of the existing resources in your cloud provider, as tracked by Terraform. This state is stored in a state file, which Terraform uses to keep track of the resources it manages.

The state file records the actual infrastructure details, including resource attributes such as the instance type, AMI, and tags.
This allows Terraform to compare the current state with the desired state in future operations and make decisions about creating, updating, or destroying resources.

First-Time Execution: Creating Resources

Let’s walk through what happens the first time you execute your Terraform configuration.

Initial State: The state file is empty since no resources have been created yet.
Applying Configuration: You run terraform apply, and Terraform communicates with the AWS API to create the resources as defined in your configuration.
Resource Creation: For example, an EC2 instance is created using the specified AMI, instance type, and tags. Terraform then records this new EC2 instance in the state file.
After the resource is created, the state file is updated to reflect the Current State, which now includes details of the EC2 instance.

Comparing Desired State and Current State

On subsequent runs of your Terraform configuration, Terraform will compare the Desired State (your Terraform code) to the Current State (the state recorded in the state file). This comparison allows Terraform to determine if any actions are necessary.

No Change: If the desired state and current state are the same (e.g., the EC2 instance type and AMI are identical), Terraform will not make any changes.
Change Detected: If there’s a difference between the desired state and the current state (e.g., you change the instance type from t2.micro to t2.medium), Terraform will initiate the necessary updates.

Updating Resources: Changing the Desired State

Now, let’s assume there’s a change in your requirements. You want to upgrade the EC2 instance from a t2.micro to a t2.medium. Here’s how you can update the desired state and apply the change:

Modify Configuration: Update the instance type in the Terraform code:
resource "aws_instance" "my_instance" {
  ami = "ami-12345678"
  instance_type = "t2.medium" # Updated from t2.micro to t2.medium
  tags = {
    Name = "MyUpdatedInstance"
  }
 }
2. Apply the Update: Run terraform plan to preview the changes, followed by terraform apply to apply them.

3. Terraform’s Response: Terraform compares the Desired State (with the t2.medium instance) and the Current State (which still has the t2.micro instance), detects the difference, and updates the EC2 instance.

Terraform interacts with AWS to update the EC2 instance type from t2.micro to t2.medium instead of creating a new instance. It ensures that the infrastructure is aligned with the new desired state.

Managing the State File

The state file is critical in Terraform’s operations because it tracks the current state of all resources. Terraform uses this file to compare the desired and current states in each run.

State File Location: The state file is typically stored locally or remotely (e.g., in an S3 bucket) for collaborative environments.
Sensitive Data: The state file contains sensitive information like resource IDs and secret keys, so it should be stored securely.
Why is Desired State vs. Current State Important?

Consistency: Terraform ensures that your infrastructure always matches the desired state as defined in your code.
Automation: By managing resources based on the desired state, Terraform automates infrastructure updates, ensuring that resources are created, modified, or destroyed as necessary.
Idempotency: Terraform only makes changes if there’s a difference between the desired and current states, ensuring that you don’t accidentally create or destroy resources without intending to.