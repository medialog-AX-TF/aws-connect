# AWS Connect IaC Project

This project manages AWS Connect configurations using AWS CloudFormation.

## Directory Structure

- `iac/cloudformation/`: Contains AWS CloudFormation templates and parameter files.
  - `connect-resources.yaml`: The main CloudFormation template that defines AWS Connect resources like Queues, Hours of Operation, etc.
  - `parameters-dev.json`: The parameter file for the development environment. You should update the `ConnectInstanceArn` with your actual AWS Connect instance ARN.

## Prerequisites

- [AWS CLI](https://aws.amazon.com/cli/) installed and configured with appropriate permissions.
- An existing AWS Connect instance.

## Deployment

1.  **Update Parameters**:
    Open `iac/cloudformation/parameters-dev.json` and replace the placeholder value for `ConnectInstanceArn` with your actual instance ARN. You can find the ARN in the AWS Connect console.

2.  **Deploy the Stack**:
    Navigate to the `iac/cloudformation` directory and run the following AWS CLI command:

    ```bash
    aws cloudformation deploy \
      --template-file connect-resources.yaml \
      --stack-name connect-custom-resources \
      --parameter-overrides file://parameters-dev.json \
      --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM
    ```

This command will create a new CloudFormation stack named `connect-custom-resources` with the resources defined in the template.