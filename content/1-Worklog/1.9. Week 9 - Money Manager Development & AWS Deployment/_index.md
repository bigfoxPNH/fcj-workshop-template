---
title: "Week 9 - Final Project Development & AWS Deployment"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
url: "/1-worklog/1.9-week9/"
---

### Weekly Topic

Develop core features of Money Manager and deploy to AWS following the designed architecture

### Weekly Goals

* Develop the main features of Money Manager (backend + frontend).
* Deploy to AWS following the multi-AZ architecture designed in week 8.

### Work Schedule

| Date | Day | Task Description | Lab / Project |
| :--- | :--- | :--- | :--- |
| 15/06/2026 | Mon | Review the source code and prioritize module deployment order. Ensure the dev environment is stable (Spring Boot backend, React frontend). Review the build & deploy process before starting new feature development. | [Final Project](#) |
| 16/06/2026 | Tue | Develop core business APIs: income/expense management, budget, savings jars. Check entity mappings, table relationships and data access flows. Test locally and ensure APIs work correctly with MySQL. | [Final Project](#) |
| 17/06/2026 | Wed | Complete authentication features: JWT token + Google OAuth2. Develop APIs for subscription-based authorization (Free/Premium). Update technical documentation and API docs. | [Final Project](#) |
| 18/06/2026 | Thu | Deploy Spring Boot backend to EC2 in Private Subnet. Configure ALB in Public Subnet to route traffic to EC2. Set up Auto Scaling Group for EC2 Web API to auto-scale based on load. | [Final Project](#) |
| 19/06/2026 | Fri | Configure RDS MySQL multi-AZ. Configure ElastiCache Redis for caching and session management. Test connectivity from EC2. | [Final Project](#) |

### Expected Results

* Core business APIs are operational (income/expense management, authentication, authorization).
* Backend deployed on EC2 with ALB + Auto Scaling Group.
* RDS MySQL and ElastiCache Redis configured and connected successfully.

### Week 9 References

* [Final Project - Money Manager (Spring Boot + React JS + React Native Expo)](#)
* AWS services: EC2 ASG, ALB, RDS MySQL, ElastiCache Redis

