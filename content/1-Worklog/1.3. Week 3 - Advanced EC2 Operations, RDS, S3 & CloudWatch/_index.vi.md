---
title: "Tuần 3 - Thao tác EC2 nâng cao, RDS, S3 & CloudWatch"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
url: "/vi/1-worklog/1.3-week3/"
---

### Chủ đề tuần

Thao tác EC2 nâng cao + RDS + Hosting tĩnh trên S3 + Giám sát CloudWatch

### Mục tiêu tuần

* Hoàn thành các thao tác EC2 nâng cao: thay đổi kích thước, snapshot, custom AMI, triển khai ứng dụng.
* Tìm hiểu về Amazon RDS, hosting tĩnh trên Amazon S3, và giám sát CloudWatch.

### Lịch làm việc

| Ngày | Thứ | Mô tả công việc | Lab / Dự án |
| :--- | :--- | :--- | :--- |
| 04/05/2026 | Thứ 2 | Thay đổi loại instance EC2. <br> Tạo và quản lý EBS snapshot. <br> Tạo custom AMI và khởi chạy các instance từ đó. <br> Khôi phục quyền truy cập vào các instance Linux và Windows, sau đó hoàn thành phần nâng cao của Lab 000004. | [Lab 000004 - Introduction to Amazon EC2](https://000004.awsstudygroup.com/vi/) |
| 05/05/2026 | Thứ 3 | Cài đặt LAMP server và Node.js trên Amazon Linux 2023. <br> Triển khai ứng dụng Node.js trên EC2 cho cả Linux và Windows. <br> Xem xét AWS CLI cơ bản cho EC2, S3 và IAM; tạo cảnh báo AWS Budgets. <br> Hoàn thành các bài lab liên quan đến triển khai và chấm dứt (terminate) các instance EC2 vào cuối ngày. | [Lab 000004 - Introduction to Amazon EC2](https://000004.awsstudygroup.com/vi/) |
| 06/05/2026 | Thứ 4 | Tạo VPC và security group cho Amazon RDS. <br> Khởi chạy một instance quản trị RDS MySQL và triển khai ứng dụng kết nối tới đó. <br> Thực hành sao lưu và khôi phục với RDS snapshot. <br> Hoàn thành Lab 000005. | [Lab 000005 - Database fundamentals with Amazon RDS](https://000005.awsstudygroup.com/vi/) |
| 07/05/2026 | Thứ 5 | Tạo một S3 bucket và cấu hình truy cập công khai để hosting website tĩnh. <br> Tải lên các tệp HTML/CSS và cấu hình bucket policy với tính năng versioning. <br> Kiểm tra các pre-signed URL để kiểm soát truy cập. <br> Hoàn thành Lab 000057 và dọn dẹp tài nguyên vào cuối tuần. | [Lab 000057 - Static website hosting with Amazon S3](https://000057.awsstudygroup.com/vi/) |
| 08/05/2026 | Thứ 6 | Tìm hiểu các chỉ số (metrics) và dashboard của CloudWatch. <br> Thiết lập cảnh báo CPU > 80% với thông báo email qua SNS. <br> Cấu hình log group, Log Insights và CloudWatch Agent trên EC2. <br> Hoàn thành Lab 000036. | [Lab 000036 - Monitoring with Amazon CloudWatch](https://000036.awsstudygroup.com/vi/) |

### Kết quả mong đợi

* Làm chủ các thao tác EC2 nâng cao: thay đổi kích thước, snapshot, custom AMI, và khôi phục quyền truy cập.
* Triển khai khối lượng công việc ứng dụng trên EC2 và sử dụng AWS CLI cho các nhiệm vụ vận hành cơ bản.
* Khởi chạy và vận hành một instance quản trị Amazon RDS MySQL với thực hành sao lưu và khôi phục.
* Host một website tĩnh trên Amazon S3 với kiểm soát truy cập và versioning phù hợp.
* Cấu hình giám sát Amazon CloudWatch với cảnh báo, log và CloudWatch Agent.

### Tài liệu tham khảo Tuần 3

* [Lab 000004 - Basic compute knowledge with Amazon EC2](https://000004.awsstudygroup.com/vi/)
* [Lab 000005 - Database fundamentals with Amazon RDS](https://000005.awsstudygroup.com/vi/)
* [Lab 000057 - Static website hosting with Amazon S3](https://000057.awsstudygroup.com/vi/)
* [Lab 000036 - Monitoring with Amazon CloudWatch](https://000036.awsstudygroup.com/vi/)



