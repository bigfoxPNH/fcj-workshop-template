---
title : "Prerequiste"
date : 2024-01-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---
### Preparation Steps

#### Account and Access (AWS IAM & CLI)
The system requires an active AWS account with IAM administrator privileges. To comply with the Principle of Least Privilege, the author does not use the main Root account but instead creates a secondary developer account named **GymPro-Developer** to assign permissions and retrieve security keys for connecting from the workstation through the following steps:

* **Step 1 (Configuration on AWS Console):** Log in to the AWS Management Console using the administrator account, and navigate to the **IAM (Identity and Access Management)** service -> **Users** -> Select the user **GymPro-Developer**. Navigate to the **Security credentials** tab, locate the **Access keys** section, and select **Create access key**. Choose **Command Line Interface (CLI)** as the use case, agree to the terms, and confirm for the system to generate the key pair: **Access Key ID** and **Secret Access Key**. Download the `.csv` file containing this security key information.

* **Step 2 (Configuration on the local workstation):** Open Terminal or PowerShell on your personal computer and run the following command:

```bash
aws configure
```

Enter the Access Key ID and Secret Access Key generated in Step 1. Set the Default region name to `us-east-1` (N. Virginia - the default deployment region for the GymPro project) and the Default output format to `json`. The configuration is automatically saved in the user's home directory (`~/.aws/` on Linux/macOS or `%USERPROFILE%\.aws\` on Windows).

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.2-Prerequisite/iam-credentials.png" alt="IAM Security Credentials" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> The IAM Security credentials tab with the Access keys section is used to create CLI connection keys.

#### Local Workstation Environment
* Ensure that the workstation has successfully installed the **Node.js** environment (version 20 or higher) for writing and packaging the source code for the Lambda Backend functions, along with the **Flutter** mobile app development environment (Dart SDK).
* The workstation must maintain a stable internet connection to fetch dependency packages (`@aws-sdk/client-s3`, `@aws-sdk/s3-request-presigner` for Node.js, and the `http` library for Flutter).

#### Infrastructure Region Selection
Select the AWS network infrastructure region in **N. Virginia (us-east-1)** as the default deployment region to ensure maximum compatibility for all AWS services used in the architecture, while simultaneously optimizing Serverless infrastructure costs for the personal project.