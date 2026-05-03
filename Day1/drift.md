Detecting and Managing Drift with Terraform:

Drift happens when your infrastructure no longer matches what’s defined in your Terraform configuration. This usually occurs because of manual changes, other automation tools, or unexpected failures.

1. The Role of State
Terraform keeps a state file (terraform.tfstate) that maps your configuration to real resources.
It stores metadata, dependencies, and cached attributes.
State can be local or remote (remote is recommended for teams).
Commands like terraform show and terraform state show let you inspect it.

2. Detecting Drift
terraform refresh updates the state file with the actual status of resources. It doesn’t change infrastructure, only the state.
terraform plan compares desired configuration with current state and shows what changes Terraform would make.
Example: 
If a tag was changed manually, Terraform will plan to update it back.
If a resource was deleted, Terraform will plan to recreate it.
If an immutable attribute (like an AMI ID) changed, Terraform will destroy and recreate the resource.

3. Managing Drift
Terraform provides lifecycle options to control how drift is handled:

prevent_destroy: Protects critical resources from accidental deletion.
ignore_changes: Ignores specific attributes so Terraform doesn’t try to fix them (use carefully).
create_before_destroy: Ensures new resources are created before old ones are destroyed, avoiding downtime.

4. Best Practices
Always run terraform plan before apply to preview drift corrections.
Use remote state backends for consistency in teams.
Apply lifecycle flags thoughtfully — they can prevent unwanted changes but may also hide important drift.
Combine lifecycle protections with review processes for critical infrastructure.