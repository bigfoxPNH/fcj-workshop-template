---
title : "Implementation Steps"
date : 2024-01-01 
weight : 3 
chapter : false
pre : " <b> 5.3. </b> "
---
### Detailed Implementation Steps

#### Step 1: Setting up an isolated private VPC
The process of building an isolated network environment to place the entire Backend processing flow into a secure zone:

Initialize a custom VPC named **GymPro-VPC** with an IP CIDR block of `10.0.0.0/16` as the primary private network range.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/vpc-list.png" alt="VPC List" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> VPC list displaying the custom VPC with CIDR 10.0.0.0/16

Divide the subnet ranges into isolated tiers: Public Subnets (housing components exposed to the public Internet) and Private Subnets (hosting internal network interfaces of compute services to completely isolate their IPs from the Internet Gateway). The system is evenly distributed across two Availability Zones (us-east-1a and us-east-1b) to ensure redundancy.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/subnet-list.png" alt="Subnet List" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> List of Subnets distributed across Public and Private tiers

Configure the corresponding Route Tables: The Public Subnet routes directly to the Internet Gateway; the Private Subnet establishes an internal routing range with the NAT Gateway set to None to prevent continuous monthly account credit consumption.

#### Step 2: Deploying the Serverless Backend with AWS Lambda

Initialize a Serverless compute function named **GymPro_Get_Upload_URL** running on the Node.js environment. This function handles intensive business logic: receiving the file name sent from the Flutter App, performing secure digital signing, and generating a short-lived S3 Presigned URL (with a lifespan limited to 5 minutes) to grant image upload permissions to members.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/lambda-source.png" alt="Lambda Source Code Configuration" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Source code configuration interface of the GymPro_Get_Upload_URL Lambda function integrated with API Gateway on the AWS Console

Configure the network connection for the Lambda function: Navigate to the Configuration tab -> select VPC -> Connect the Lambda function directly to the GymPro-VPC.

Accurately select the 2 Private Subnets (GymPro-VPC-subnet-private1-... and GymPro-VPC-subnet-private2-...) to force Lambda to run entirely within the secure internal network partition. Assign the VPC's default Security Group to the Lambda function to manage Inbound/Outbound rules.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/lambda-vpc.png" alt="Lambda VPC Configuration" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Configuration for allocating the Lambda function to run within the GymPro-VPC internal network environment and Private Subnets on the AWS Console

#### Step 3: Configuring system permissions on AWS IAM

When configuring Lambda to be placed in Private Subnets, the system initially throws a permission error because Lambda does not yet have the authority to create internal virtual network interfaces.

To resolve this, access the IAM service -> Roles -> Accurately select the current execution Role of the function (GymPro_Get_Upload_URL-role-...).

Click the Add permissions button -> Attach policies -> Search for and select the standard AWS managed policy: AWSLambdaVPCAccessExecutionRole.

Confirm the permission assignment to grant Lambda full privileges to create and manage Elastic Network Interfaces (ENIs) for accessing the VPC network range.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/iam-role.png" alt="IAM Role Assignment" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Interface for assigning the AWSLambdaVPCAccessExecutionRole policy to the Lambda function's IAM Role on the AWS Console

#### Step 4: Setting up Amazon S3 Security and Gateway VPC Endpoint
Establish a private network connection to optimize costs and protect the large data storage repository:

Initialize an Amazon S3 Bucket named **gympro-storage-s3** in completely private mode (Block Public Access) and enable default Server-Side Encryption (SSE-S3) to store all member avatars and fitness check-in photos.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/s3-files.png" alt="S3 Files Management" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Interface for managing member image files stored inside the gympro-storage-s3 Bucket on the AWS Console

On the VPC Console management page, create a Gateway VPC Endpoint for S3 (service name: com.amazonaws.us-east-1.s3) and assign it directly to the Route Tables of the Private Subnets within the GymPro-VPC.

The new route entry automatically added by the system will direct all code generation requests and communications from the internal Lambda function to Amazon S3 through AWS's internal backbone network instead of routing out to the Internet. This mechanism cuts 100% of the network bandwidth costs for S3 and accelerates file transfer speeds.

Configure a strict S3 Bucket Policy to protect resources: Absolutely deny all structural read/write access requests from the external Internet, and only accept valid interaction requests that pass through the newly created Gateway VPC Endpoint of the system.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/s3-security.png" alt="S3 Block Public Access" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Activation status of the Block Public Access feature securing the S3 data storage on the AWS Console

#### Step 5: Configuring the monitoring system with Amazon CloudWatch & SNS
Set up an automatic monitoring "eye" to track all Backend error logs:

The business Lambda function automatically pushes all detailed operational logs to the Amazon CloudWatch Log Groups service in real-time.

Set up a custom Metric Filter named **EC2ErrorFilter** (or **LambdaErrorFilter**) on the project's Log Group to scan through the log streams and count the frequency of capitalized error keywords like "ERROR" or "Exception".

Initialize a CloudWatch Alarm connected directly to the filter's metric. Configure a highly sensitive alert threshold: Transition to an emergency alarm state (ALARM) as soon as the number of errors is >= 1 within a 5-minute monitoring period.

Link the Alarm with the Amazon SNS (Simple Notification Service) "siren". When the alarm state triggers, SNS will automatically compose a Backend system error notification and fire off a real-time emergency email to the developer's administrative Gmail inbox (phamquangtrung4504@gmail.com).

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/cloudwatch-logs.png" alt="CloudWatch Log Groups Management" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Interface for managing CloudWatch Log Groups to monitor Serverless system operational logs on the AWS Console