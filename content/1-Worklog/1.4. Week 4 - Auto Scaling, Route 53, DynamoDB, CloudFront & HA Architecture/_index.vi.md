---
title: "Tuần 4 - Auto Scaling, Route 53, DynamoDB, CloudFront & Kiến trúc HA"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
url: "/vi/1-worklog/1.4-week4/"
---

### Chủ đề tuần

Auto Scaling + Route 53 + DynamoDB + CloudFront + Kiến trúc độ khả dụng cao (HA)

### Mục tiêu tuần

* Tìm hiểu về EC2 Auto Scaling, Application Load Balancer, Route 53 DNS, DynamoDB, CloudFront, và kiến trúc độ khả dụng cao (HA).

### Lịch làm việc

| Ngày | Thứ | Mô tả công việc | Lab / Dự án |
| :--- | :--- | :--- | :--- |
| 11/05/2026 | Thứ 2 | Tạo launch template và Auto Scaling Group. Cấu hình chính sách target tracking scaling policy. Thiết lập Application Load Balancer với listener rules. Kiểm tra các hoạt động scale-out, scale-in và health check trong Lab 000006. | [Lab 000006 - Scaling applications with EC2 Auto Scaling](https://000006.awsstudygroup.com/vi/) |
| 12/05/2026 | Thứ 3 | Tìm hiểu về Route 53 hosted zones và các loại bản ghi phổ biến như A, CNAME, Alias. Cấu hình các chính sách routing cơ bản. Thiết lập mô hình hybrid DNS tích hợp với VPC. | [Lab 000010 - Hybrid DNS management with Amazon Route 53](https://000010.awsstudygroup.com/vi/) |
| 13/05/2026 | Thứ 4 | Tạo các bảng DynamoDB với thiết kế partition key và sort key. Thực hiện các thao tác CRUD qua console và CLI. Cấu hình Global Secondary Index và so sánh dung lượng on-demand vs provisioned. | [Lab 000060 - Basic NoSQL with Amazon DynamoDB](https://000060.awsstudygroup.com/vi/) |
| 14/05/2026 | Thứ 5 | Tìm hiểu CloudFront bao gồm distribution, origin và các cache behavior. Tích hợp CloudFront với website tĩnh trên S3. Cấu hình HTTPS với ACM và thực hiện cache invalidation. | [Lab 000094 - Content distribution with Amazon CloudFront](https://000094.awsstudygroup.com/vi/) |
| 15/05/2026 | Thứ 6 | Thiết kế kiến trúc Multi-AZ sử dụng ALB, EC2 và RDS. Cấu hình target group và listener rule. Triển khai RDS Multi-AZ và kiểm tra health check cùng với cơ chế failover. | [Lab 000101 - Building a High Availability web application](https://000101.awsstudygroup.com/vi/) |

### Kết quả mong đợi

* Hiểu cách thức hoạt động đồng bộ của EC2 Auto Scaling, ALB và các chính sách scaling trong một kiến trúc linh hoạt (elastic).
* Cấu hình các bản ghi Route 53 DNS và các chiến lược định tuyến cơ bản, bao gồm cả hybrid DNS.
* Thực hành thiết kế bảng DynamoDB, các thao tác CRUD, secondary index và mô hình dung lượng.
* Sử dụng CloudFront để phân phối nội dung từ S3 một cách an toàn qua HTTPS với quản lý bộ nhớ đệm (cache).
* Xây dựng và xác minh kiến trúc Multi-AZ với độ khả dụng cao sử dụng ALB, EC2 và RDS.

### Tài liệu tham khảo Tuần 4

* [Lab 000006 - Scaling applications with EC2 Auto Scaling](https://000006.awsstudygroup.com/vi/)
* [Lab 000010 - Hybrid DNS management with Amazon Route 53](https://000010.awsstudygroup.com/vi/)
* [Lab 000060 - Basic NoSQL with Amazon DynamoDB](https://000060.awsstudygroup.com/vi/)
* [Lab 000094 - Content distribution with Amazon CloudFront](https://000094.awsstudygroup.com/vi/)
* [Lab 000101 - Building a High Availability web application](https://000101.awsstudygroup.com/vi/)



