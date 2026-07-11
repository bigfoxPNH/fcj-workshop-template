---
title : "Test Results & Experimentation"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---
### Testing & Experimental Results
After completing the infrastructure configuration, the author conducted practical end-to-end testing to evaluate the stability and correctness of the entire solution:

#### Testing the Registration / Authentication Flow (AWS Cognito)

Performed the registration of a new member account on the GymPro mobile app interface.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Test Results & Experimentation/cognito-register.png" alt="Cognito Registration Flow" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Image of the account creation and Cognito authentication function

The AWS Cognito system accurately recorded the new user and automatically sent an OTP activation code to the member's personal email. The user successfully entered the code, and the account status transitioned to Verified.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Test Results & Experimentation/cognito-users.png" alt="Cognito Users Management" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Management interface of the member account list and authentication status on the AWS Cognito User Pool

#### Testing the Secure Image Upload Flow via S3 Presigned URL

The member accessed the "Update Avatar" feature on the Flutter App, selected an image file from their device, and clicked save.

The mobile application immediately sent a background request to the API Gateway, triggering the AWS Lambda function safely hidden within the VPC's Private Subnet.

The Lambda function executed smoothly, calling the internal S3 Gateway Endpoint to request Amazon S3 to issue a temporary encrypted link (Presigned URL) valid for 5 minutes, which was then returned to the mobile app.

Upon receiving the link, the Flutter App automatically triggered an HTTP PUT request to push the image file's data bytes directly into the Amazon S3 Bucket gympro-storage-s3.

Accessing the S3 Console, the author confirmed that the image file was properly placed in the storage directory with the exact format and size, proving that the internal secure connection flow operated with 100% success.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Test Results & Experimentation/s3-upload.png" alt="S3 Image Upload Success" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Image of the image upload function to the S3 system

#### Testing the CloudWatch & SNS Error Monitoring System

The author intentionally modified a small snippet of source code in the app to send an invalidly formatted request, forcing the Backend Lambda function to silently throw a system error.

As soon as the error occurred, CloudWatch Log Groups immediately recorded the logs. The Metric Filter detected the keyword "ERROR" and pushed the metric on the graph beyond the configured threshold.

The system triggered the ALARM state of the CloudWatch Alarm. Within approximately 30 seconds, an urgent notification email from Amazon SNS was directly dispatched to the administrator's Gmail inbox (phamquangtrung4504@gmail.com), proving that the proactive error warning radar operates exactly as designed.
