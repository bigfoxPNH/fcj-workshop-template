---
title : "Clean up"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---
### Resource Cleanup
After concluding the experimental testing sessions for the graduation project defense, the author proceeded to clean up the test infrastructure to optimize resources and prevent unintended charges on the AWS account:

* **Delete S3 Objects**: Completely delete all test image and avatar files uploaded to the `gympro-storage-s3` bucket to free up monthly storage capacity.
* **Remove VPC Endpoints**: Access the VPC configuration, detach, and remove the Gateway VPC Endpoint from the Route Tables of the Private Subnets to restore the network configuration to its initial state.
* **Remove Alarms and Filters**: Delete the Metric Filter configurations and disable the monitoring Alarms on the Amazon CloudWatch service to halt the automated log scanning flow.
