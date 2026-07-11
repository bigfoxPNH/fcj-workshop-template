---
title : "Difficulties & Development Direction"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---
### Challenges & Future Development

#### Challenges Encountered

* **Hidden network permission error (ENI)**: During the initial phase of deploying Lambda into the VPC subnet, due to an insufficient understanding of the infrastructure mechanisms, the author encountered a system permission denial error when saving the configuration. After carefully researching the troubleshooting documentation for the `CreateNetworkInterface` error in the AWS Knowledge Center, the author resolved the issue by appending the correct `AWSLambdaVPCAccessExecutionRole` managed policy in IAM.
* **Security policy conflict (Bucket Policy vs. Endpoint Policy)**: When configuring the security filter for the S3 storage, setting the S3 Bucket Policy to block all external traffic too early—before accurately configuring the service ARN of the VPC Endpoint—resulted in the internal Lambda function itself being denied access by the S3 service (Access Denied). The author had to trace back through CloudWatch logs and execute small test commands via the CLI to isolate the issue and rectify the configuration sequence.

#### Future Development Directions

* **Infrastructure as Code (IaC) Deployment**: Transitioning all manual configuration operations from the current Web Console interface (VPC, Subnets, Lambda, Endpoint, IAM, Bucket Policy) to centrally managed code using Terraform or AWS CloudFormation. This will facilitate easy packaging, Version Control, and the ability to reproduce the project's infrastructure with a single command.
* **Expanding the internal security network**: Integrating additional Gateway/Interface Endpoints for other dependent services in the architecture, such as AWS Cognito or Amazon DynamoDB. This will completely lock down all network traffic within the AWS internal backbone, upgrading the GymPro application to meet maximum enterprise security standards.
* **Building a centralized Dashboard**: Consolidating all discrete metrics from CloudWatch Alarms and Log Groups into a single monitoring interface (CloudWatch Dashboard). This will provide gym administrators with the most comprehensive and intuitive overview of the system's health during real-world operation.