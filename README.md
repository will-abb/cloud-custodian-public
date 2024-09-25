# Cloud Custodian Repository for User

This repository contains Cloud Custodian configurations and policies for managing AWS resources effectively and securely.

## Repository Structure

### Folders

- `configs`: Contains configuration files required for Cloud Custodian and AWS.
    - `aws_configs`: AWS Configurations
    - `c7_unified_permissions.json`: Permission requirements
    - `email.html.j2`: Jinja template for email notifications
    - `slack.j2`: Jinja template for Slack notifications

- `policies`: Contains policy definitions for Cloud Custodian.
    - `active_policies`: Policies that are actively running
    - `non_lambda_policies`: Policies that are not active and must be manually triggered

### Bitbucket Pipelines

The `bitbucket-pipelines.yml` file contains the CI/CD setup for executing Cloud Custodian policies. There are two main sequences:

1. `commonBuildAndTest`: This sequence installs necessary dependencies, sets up AWS credentials, and runs policies in dry-run mode.
2. `commonBuildAndDeployUser`: Similar to `commonBuildAndTest` but additionally executes the policies.

#### Manual Triggers

Manual triggers have been added to save on Bitbucket build minutes.

## How to Use

1. **Initialization**: Make sure to populate the AWS Config and credentials in the `configs` folder.
2. **Policy Management**: Add or update policies in the `policies/active_policies` or `policies/non_lambda_policies` folder as required.
3. **Pipeline Execution**: Execute the Bitbucket pipeline manually or as scheduled.

## Policy Descriptions

### Active Policies

- `CUSTODIAN_mailer.yml`: Configuration for the Custodian mailer
- `EC2_delete_unused_security_groups.yml`: Deletes unused security groups
- `EC2_notify_aged_instances_and_amis.yml`: Notifies about old instances and AMIs
- `EC2_notify_open_ssh_rdp_security_groups.yml`: Notifies if SSH or RDP is open to the world
- `EC2_notify_sg_open_to_world.yml`: Notifies if any security group is open to the world
- `IAM_notify_disable_inative_users.yml`: Notifies and disables inactive IAM users
- `IAM_root_login_detected.yml`: Detects and notifies of root account login
- `IAM_user_failed_login.yml`: Notifies on IAM user login failures
- `TEST_mailer_policy.yml`: Test policy for mailer

### Non-Active Policies

- `EC2_old_instance_report.yml`: Generates a report for old EC2 instances (Manual Trigger)
- `EC2_terminate_non_standard_region.yml`: Terminates instances that are not in standard regions (Manual Trigger)

```
