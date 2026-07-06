---
title: "Week 10 - Security, Testing & AWS Service Integration"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
url: "/1-worklog/1.10-week10/"
---

### Weekly Topic

Complete security hardening, integrate remaining AWS services, and run tests for Money Manager

### Weekly Goals

* Configure comprehensive system security (IAM, Cloudflare, JWT/OAuth2).
* Integrate async services (SQS, Lambda) and run full tests.

### Work Schedule

| Date | Day | Task Description | Lab / Project |
| :--- | :--- | :--- | :--- |
| 22/06/2026 | Mon | Configure IAM Roles & Policies for EC2 Web API, Lambda, S3 in the Money Manager project. Review and complete application security: JWT authentication, Google OAuth2 on Spring Boot. Set up Cloudflare WAF, Rate Limit and Turnstile anti-bot for the domain. | [Final Project](#) |
| 23/06/2026 | Tue | Implement async flow: configure SQS + Dead-Letter Queue for background jobs. Set up EC2 Worker to consume messages from SQS. Invoke Lambda to generate Excel reports and render PDF invoices. Configure S3 bucket to store output files (reports, invoices). | [Final Project](#) |
| 24/06/2026 | Wed | Write unit tests and integration tests for core business APIs (income/expense, budget, savings jars). Test the async end-to-end flow: SQS -> EC2 Worker -> Lambda -> S3. Run load tests and optimize performance: connection pool, cache hit rate, query optimization. | [Final Project](#) |
| 25/06/2026 | Thu | Prepare Money Manager system architecture documentation on AWS. Describe processing flows in detail: core business, AI chat (DynamoDB), async (SQS/Lambda), notification (SNS). Start building presentation slides. | [Final Project](#) |
| 26/06/2026 | Fri | Test PayOS integration (QR payment) and Brevo SMTP (send OTP emails, reports) through NAT Gateway. Optimize AWS costs: review RDS MySQL, ElastiCache, EC2 ASG, Lambda usage. Summarize progress and plan for the final week. | [Final Project](#) |

### Expected Results

* System security complete (IAM, Cloudflare WAF, JWT/OAuth2).
* Async flow operational: SQS -> EC2 Worker -> Lambda -> S3.
* Sufficient test coverage for core APIs and critical processing flows.

### Week 10 References

* [Final Project - Money Manager (Spring Boot + React JS + React Native Expo)](#)
* AWS services: IAM, SQS + DLQ, Lambda, S3, SNS, CloudWatch
* External services: Cloudflare WAF, PayOS, Brevo SMTP

