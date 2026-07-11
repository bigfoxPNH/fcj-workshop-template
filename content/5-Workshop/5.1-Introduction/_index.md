---
title : "Introduction"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---


### Deploy infrastructure and secure connection to Amazon S3

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.1-Introduction/architecture1.png" alt="Overall Architecture" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
  <div style="font-weight: bold; margin-top: 8px; color: #555;">Figure 1. Overall architecture of the network infrastructure and AWS service integration.</div>
</div>

<br>

### Overview

This practical lab fully documents the process of building, configuring, and testing the cloud infrastructure for the Smart Gym Management and Operation System (GymPro) project.

The configuration focuses on implementing a Serverless model and multi-layered security, including:
* Establishing an isolated private network (Amazon VPC).
* Deploying the AWS Lambda Backend configuration to handle Serverless business logic.
* Configuring a Gateway VPC Endpoint routed to Amazon S3 to optimize network transmission, ensure absolute protection of members' check-in and avatar image data from leakage risks over the public Internet, and completely eliminate NAT Gateway data processing costs.
* Assigning strict access control policies via AWS IAM and S3 Bucket Policies.

Through this practical implementation, the system has adopted and strictly adhered to the AWS Well-Architected Framework design standards, focusing on two core pillars: Security and Cost Optimization.