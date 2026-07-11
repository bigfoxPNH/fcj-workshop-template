---
title: "Week 8 - AWS Well-Architected, AWS SAM & Architecture Design"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
url: "/1-worklog/1.8-week8/"
---

### Weekly Topic

Learn AWS Well-Architected Framework, AWS SAM, and apply them to Money Manager architecture design

### Weekly Goals

* Understand the 5 pillars of the AWS Well-Architected Framework.
* Design the AWS architecture for the Money Manager project based on best practices.

### Work Schedule

| Date | Day | Task Description | Lab / Project |
| :--- | :--- | :--- | :--- |
| 08/06/2026 | Mon | Learn about the AWS Well-Architected Framework and its 5 main pillars. Practice AWS SAM - trial deploy a simple serverless application. Start drafting the AWS architecture for Money Manager (VPC, EC2, RDS, ElastiCache). | [Well-Architected Labs](https://wellarchitectedlabs.com/) |
| 09/06/2026 | Tue | Dive deeper into Well-Architected principles and real-world trade-offs. Continue AWS SAM practice with serverless deployment flow. Design VPC layout: Public Subnet (ALB, NAT Gateway), Private Subnet (EC2, RDS, ElastiCache). | [Well-Architected Labs](https://wellarchitectedlabs.com/) |
| 10/06/2026 | Wed | Review design decisions through the lens of the 5 pillars. Learn more about AWS SAM and serverless deployment patterns. Design async flow: SQS -> EC2 Worker -> Lambda -> S3 for report export and invoice rendering. | [Well-Architected Labs](https://wellarchitectedlabs.com/) |
| 11/06/2026 | Thu | Review Reliability, Security and Cost Optimization in the Money Manager architecture. Practice packaging and deploying serverless with AWS SAM. Design AI chat flow: DynamoDB stores conversation history for Nova Money. | [Well-Architected Labs](https://wellarchitectedlabs.com/) |
| 12/06/2026 | Fri | Summarize the 5 pillars and their impact on the Money Manager architecture. Complete basic AWS SAM practice. Finalize the proposed architecture: multi-AZ, ALB + EC2 ASG, RDS MySQL, ElastiCache HA, SQS -> Lambda. | [Well-Architected Labs](https://wellarchitectedlabs.com/) |

### Expected Results

* Understand the 5 pillars of the AWS Well-Architected Framework and how to apply them.
* Gain hands-on experience with AWS SAM.
* Finalize the AWS architecture for Money Manager: multi-AZ VPC, ALB, EC2 ASG, RDS MySQL, ElastiCache, DynamoDB, SQS, Lambda, S3, SNS, CloudWatch.

### Week 8 References

* [Well-Architected Labs](https://wellarchitectedlabs.com/)
* 5 pillars: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization

