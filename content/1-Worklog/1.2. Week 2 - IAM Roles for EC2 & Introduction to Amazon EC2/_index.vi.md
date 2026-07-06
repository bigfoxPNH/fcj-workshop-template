---
title: "Tuần 2 - Vai trò IAM cho EC2 & Giới thiệu về Amazon EC2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
url: "/vi/1-worklog/1.2-week2/"
---

> Lưu ý: Ngày 30/04 (Ngày Giải phóng miền Nam) và 01/05 (Ngày Quốc tế Lao động) là các ngày nghỉ lễ — tuần này chỉ có 3 ngày làm việc.

### Chủ đề tuần

Đánh giá IAM + Vai trò IAM cho EC2 + các thao tác cơ bản với Amazon EC2

### Mục tiêu tuần

* Xem lại và củng cố kiến thức về IAM & VPC từ Tuần 1.
* Tìm hiểu sâu về IAM Roles cho EC2 và các thao tác cơ bản với Amazon EC2.

### Lịch làm việc

| Ngày | Thứ | Mô tả công việc | Lab / Dự án |
| :--- | :--- | :--- | :--- |
| 27/04/2026 | Thứ 2 | Xem lại IAM bao gồm user, group, role, và policy. Xem lại các thành phần VPC như subnet, route table, Internet Gateway, và security group. Thiết lập Cảnh báo hóa đơn (Billing Alarm) $5 và xem xét chiến lược sử dụng credit AWS. | [Lab 000001](https://000001.awsstudygroup.com/vi/) / [Lab 000002](https://000002.awsstudygroup.com/vi/) / [Lab 000003](https://000003.awsstudygroup.com/vi/) |
| 28/04/2026 | Thứ 3 | Tìm hiểu về IAM Roles cho EC2 và mô hình Instance Profile. Truy cập S3 và DynamoDB từ EC2 mà không cần access key tĩnh. Xem xét quản trị chi phí IAM, bao gồm các hạn chế về region và loại instance. | [Lab 000048 - IAM Roles for EC2 (Instance Profile)](https://000048.awsstudygroup.com/vi/) |
| 29/04/2026 | Thứ 4 | Tạo VPC và security group cho cả Linux và Windows EC2. Khởi chạy Amazon Linux 2023 và Windows Server 2025. Kết nối qua SSH và RDP, đồng thời xem xét các khái niệm Key Pair, AMI, và loại instance. | [Lab 000004 - Introduction to Amazon EC2](https://000004.awsstudygroup.com/vi/) |

### Kết quả mong đợi

* Củng cố hiểu biết về IAM và VPC thông qua việc thực hành xem lại.
* Thiết lập các biện pháp kiểm soát chi phí cơ bản như Billing Alarm và giám sát credit.
* Hiểu cách IAM Roles cho EC2 thay thế các thông tin xác thực tĩnh (static credentials) khi truy cập các dịch vụ AWS.
* Khởi chạy và truy cập cả Linux EC2 và Windows EC2 với cấu hình mạng và bảo mật phù hợp.
* Nắm vững mối quan hệ giữa AMI, loại instance, key pair và security group trong quy trình triển khai EC2.

### Tài liệu tham khảo Tuần 2

* [Lab 000001 - Create your first AWS account](https://000001.awsstudygroup.com/vi/)
* [Lab 000002 - Access management with AWS IAM](https://000002.awsstudygroup.com/vi/)
* [Lab 000003 - Basic networking with Amazon VPC](https://000003.awsstudygroup.com/vi/)
* [Lab 000048 - IAM Roles for EC2 (Instance Profile)](https://000048.awsstudygroup.com/vi/)
* [Lab 000004 - Basic compute knowledge with Amazon EC2](https://000004.awsstudygroup.com/vi/)



