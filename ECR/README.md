CloudFormation Template: AWS CodeBuild Scheduled ECR Sync

Description

This CloudFormation template automates the process of pulling Amazon Linux images (amazonlinux:2, amazonlinux:2023, and amazonlinux:latest) from Docker Hub and pushing them to an existing AWS Elastic Container Registry (ECR) repository. The synchronization occurs on a weekly schedule using AWS CodeBuild and EventBridge.

Key Benefits

Automated Image Synchronization – Ensures that Amazon Linux images in your ECR repository remain updated without manual intervention.

Parameterized IAM Role Support – Allows the use of an existing IAM role, making the template flexible across different environments.

Cost-Effective Execution – The process runs only once a week, minimizing compute and networking costs.

Security Best Practices – Uses AWS IAM roles and least-privilege policies for secure access to AWS resources.

Fully Managed AWS Services – Leverages AWS CodeBuild, EventBridge, and ECR, reducing the need for additional infrastructure.

Scalable and Maintainable – Easily extendable for additional image repositories or modified scheduling requirements.

Deployment Instructions

1. Replace parameters with your values and deploy the CloudFormation stack:

aws cloudformation create-stack --stack-name AmazonLinuxECRSync \
  --template-body file://amazonlinux-ecr-sync.yml \
  --parameters ParameterKey=ExistingECRRepoName,ParameterValue=<your-existing-ecr-repo-name> \
               ParameterKey=ExistingServiceRoleARN,ParameterValue=<your-service-role-arn> \
  --capabilities CAPABILITY_NAMED_IAM

2. Verify the deployment in AWS Console:

AWS ECR → Confirm that images are updated.

AWS CodeBuild → Locate the AmazonLinuxECRSync project and review build logs.

AWS EventBridge → Ensure the AmazonLinuxECRSyncSchedule rule is enabled and running as expected.

CloudFormation Template Location

The full CloudFormation template is stored in the amazonlinux-ecr-sync.yml file within the project repository. It defines the AWS CodeBuild project, IAM role integration, and EventBridge scheduling to automate the image synchronization process.

This document serves as a reference guide for understanding the functionality and benefits of the template while keeping the YAML file as the primary source for deployment.
