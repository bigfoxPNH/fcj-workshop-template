---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


## GymPro – Smart Gym Management System on AWS
### A comprehensive solution for gym operations with AWS Serverless & Cloud-Native architecture 

### 1. Executive Summary
GymPro is a smart gym management and operation system built on a modern Cloud-Native and Serverless architecture on Amazon Web Services (AWS). From a technical standpoint, the client-side application is developed using Flutter (Cross-platform), while the backend infrastructure operates entirely on next-generation AWS cloud services integrated with the Firebase Firestore real-time database. The system's author and primary administrator is phamquangtrung4504@gmail.com.

### 2. Objectives
With GymPro, the core objective goes beyond simply digitizing management processes; it aims for complete infrastructure optimization:
- Reduce hardware operational costs to the maximum through a Serverless model.
- Automatically scale according to the concurrent access volume of members.
- Optimize data security with a virtual private network and strict security rules.
- Enhance the user experience via an AI assistant (Google Gemini API) integrated directly into the App, acting as a smart personal trainer to provide nutrition and workout advice.

### 3. Problem Statement
- **Current Situation:** Traditional gyms often struggle with centralized member management, membership card data security, and optimizing server maintenance costs during times of highly fluctuating traffic.
- **Solution:** GymPro leverages a Serverless architecture on AWS to completely eliminate physical server maintenance. User identity is managed via AWS Cognito, data is stored in Firebase Firestore, and all backend computations (e.g., granting upload permissions) are securely processed by AWS Lambda hidden within a VPC.
- **Benefits:** Delivers a highly available, strictly secured system with near-zero initial operational costs, providing a modern experience for members.

### 4. System Architecture
The entire backend infrastructure is deployed on AWS within an internal Amazon VPC network (10.0.0.0/16 subnet), divided into Public and Private Subnets across 2 Availability Zones (AZs).

**Technologies used:**
- **Client App:** Flutter (Cross-platform Mobile App).
- **Database:** Firebase Firestore (NoSQL database).
- **AI:** Google Gemini API.

**Core AWS Services:**
- **AWS Cognito (User Pool & Roles):** Manages identity (Sign Up/Login/Logout), security encryption, and sends OTP codes via the voice/email system.
- **Amazon S3:** A high-capacity storage repository centralizing all Avatars and workout check-in photos.
- **AWS Lambda:** Handles Serverless backend computations, containing isolated business functions (such as GymPro_Get_Upload_URL).
- **Amazon VPC:** An isolated network infrastructure that completely hides heavy computing Lambda functions inside the Private Subnet, strictly isolating them from the public Internet.
- **Amazon CloudWatch:** The monitoring radar that collects operational logs and scans for the keyword 'ERROR' using Metric Filters.
- **Amazon SNS:** An automated alarm system linked with CloudWatch to send urgent alerts to Gmail.

![System Architecture](/images/2-Proposal/system_architecture.png)

**Core Data Flows:**
- **Authentication & Data Synchronization Flow:** Users enter their login information on the Flutter mobile app. The request is sent to the AWS Cognito User Pool to retrieve security tokens (ID, Access Token). The App then uses the Cognito ID as a key to verify against Firestore Security Rules to read/write the member's workout history data.
- **Secure Image Upload Flow via Isolated VPC:** The App requests permission to upload an image via API Gateway. The request is forwarded to an AWS Lambda function hidden within the Private Subnet. The Lambda function securely communicates through an internal S3 Gateway Endpoint to request a temporary S3 Presigned URL from Amazon S3. This URL is returned so the App can upload heavy image files directly to S3.
- **Proactive Error Monitoring Radar Flow:** Lambda automatically pushes logs to CloudWatch Log Groups. The Metric Filter scans for the word "ERROR" and adds 1 point if detected. If the CloudWatch Alarm records >= 1 error within a 5-minute cycle, the system triggers Amazon SNS (Topic: GymPro-Urgent-Alerts) to push an alert email to phamquangtrung4504@gmail.com.

### 5. Technical Implementation
The HTV group divides the technical tasks to meet the project standards:
- **Frontend Development:** Trung and Vũ are responsible for developing the user interface using Flutter, ensuring a smooth experience on both iOS and Android.
- **AWS Backend Design:** Building the Serverless infrastructure with AWS Lambda, configuring Cognito authentication, and setting up the VPC network security.
- **AI & Database Integration:** Initializing Firebase Firestore with strict Security Rules and integrating the Google Gemini API to embed nutrition advisory logic for the AI Chatbot.

### 6. Implementation Roadmap
The project implementation roadmap at HUTECH is divided into main phases:
- **Weeks 1-3:** Initialize the Amazon VPC network architecture (Subnets, AZs) and set up AWS Cognito. Perform initial Firebase Firestore configuration.
- **Weeks 4-6:** The HTV group codes the Mobile App interface using Flutter and connects the login authentication flow.
- **Weeks 7-9:** Program the core AWS Lambda functions (e.g., GymPro_Get_Upload_URL), configure the S3 Gateway Endpoint, and finalize the secure image upload flow via Presigned URL.
- **Weeks 10-12:** Integrate the Google Gemini API for the AI Chatbot feature. Set up Amazon CloudWatch and configure Amazon SNS alarms. Run error flow testing and prepare for the final project defense.

### 7. Cost Estimation
The Serverless architecture offers an outstanding cost advantage for the development phase:
- **AWS Lambda & API Gateway:** Charged per request, expected to fall entirely within the Free Tier limits.
- **AWS Cognito:** Free for the first 50,000 MAU (Monthly Active Users).
- **Amazon S3:** Extremely low cost (~$0.025/GB) for storing check-in photos.
- **Amazon VPC & CloudWatch:** Basic features and Metric Filters fall within free tier limits.

### 8. Risk Assessment
- **Risk of credential exposure:** Very low due to the mechanism of issuing short-lived S3 Presigned URLs for image uploads instead of exposing root AWS account credentials to the Client.
- **Unauthorized access from the Public Internet:** Completely prevented since heavy business logic functions are entirely hidden within the Private Subnet of the VPC.
- **System Incident Recovery:** With the Error Monitoring Radar flow using CloudWatch and SNS, any arising errors are automatically alerted to the administrator's email within 5 minutes, ensuring rapid response and resolution.

### 9. Expected Results
Successfully build a modern, secure, and resource-optimized gym management system. GymPro will serve as a practical demonstration of applying Serverless & Cloud-Native architecture to solve business problems, yielding a system that requires zero physical server maintenance, infinite auto-scaling capabilities, and maximum data security for members.