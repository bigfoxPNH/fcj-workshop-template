---
title: "Tuần 8 - AWS Well-Architected, AWS SAM & Thiết kế Kiến trúc"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
url: "/vi/1-worklog/1.8-week8/"
---

### Chủ đề tuần

Tìm hiểu AWS Well-Architected Framework, AWS SAM, và áp dụng vào thiết kế kiến trúc Money Manager

### Mục tiêu tuần

* Hiểu 5 trụ cột của AWS Well-Architected Framework.
* Thiết kế kiến trúc AWS cho dự án Money Manager dựa trên các best practices.

### Lịch làm việc

| Ngày | Thứ | Mô tả công việc | Lab / Dự án |
| :--- | :--- | :--- | :--- |
| 08/06/2026 | Thứ 2 | Tìm hiểu về AWS Well-Architected Framework và 5 trụ cột chính. Thực hành AWS SAM - triển khai thử nghiệm một ứng dụng serverless đơn giản. Bắt đầu phác thảo kiến trúc AWS cho Money Manager (VPC, EC2, RDS, ElastiCache). | [Well-Architected Labs](https://wellarchitectedlabs.com/) |
| 09/06/2026 | Thứ 3 | Đi sâu vào các nguyên tắc Well-Architected và các đánh đổi (trade-offs) trong thực tế. Tiếp tục thực hành AWS SAM với luồng triển khai serverless. Thiết kế bố cục VPC: Public Subnet (ALB, NAT Gateway), Private Subnet (EC2, RDS, ElastiCache). | [Well-Architected Labs](https://wellarchitectedlabs.com/) |
| 10/06/2026 | Thứ 4 | Đánh giá các quyết định thiết kế dưới góc nhìn của 5 trụ cột. Tìm hiểu thêm về AWS SAM và các pattern triển khai serverless. Thiết kế luồng xử lý bất đồng bộ (async flow): SQS -> EC2 Worker -> Lambda -> S3 để xuất báo cáo và render hóa đơn. | [Well-Architected Labs](https://wellarchitectedlabs.com/) |
| 11/06/2026 | Thứ 5 | Đánh giá tính Độ tin cậy (Reliability), Bảo mật (Security) và Tối ưu hóa chi phí (Cost Optimization) trong kiến trúc Money Manager. Thực hành đóng gói và triển khai serverless với AWS SAM. Thiết kế luồng chat AI: sử dụng DynamoDB để lưu lịch sử hội thoại cho Nova Money. | [Well-Architected Labs](https://wellarchitectedlabs.com/) |
| 12/06/2026 | Thứ 6 | Tổng kết 5 trụ cột và tác động của chúng đối với kiến trúc Money Manager. Hoàn thành bài thực hành AWS SAM cơ bản. Hoàn thiện kiến trúc đề xuất: multi-AZ, ALB + EC2 ASG, RDS MySQL, ElastiCache HA, SQS -> Lambda. | [Well-Architected Labs](https://wellarchitectedlabs.com/) |

### Kết quả mong đợi

* Hiểu rõ 5 trụ cột của AWS Well-Architected Framework và cách áp dụng chúng.
* Tích lũy kinh nghiệm thực hành thực tế với AWS SAM.
* Hoàn thiện kiến trúc AWS cho Money Manager: multi-AZ VPC, ALB, EC2 ASG, RDS MySQL, ElastiCache, DynamoDB, SQS, Lambda, S3, SNS, CloudWatch.

### Tài liệu tham khảo Tuần 8

* [Well-Architected Labs](https://wellarchitectedlabs.com/)
* 5 trụ cột: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization



