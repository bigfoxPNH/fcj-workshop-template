---
title: "Tuần 10 - Bảo mật, Kiểm thử & Tích hợp Dịch vụ AWS"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
url: "/vi/1-worklog/1.10-week10/"
---

### Chủ đề tuần

Hoàn thiện tối ưu bảo mật (security hardening), tích hợp các dịch vụ AWS còn lại và chạy thử nghiệm hệ thống Money Manager

### Mục tiêu tuần

* Cấu hình bảo mật hệ thống toàn diện (IAM, Cloudflare, JWT/OAuth2).
* Tích hợp các dịch vụ xử lý bất đồng bộ (SQS, Lambda) và chạy thử nghiệm toàn bộ hệ thống.

### Lịch làm việc

| Ngày | Thứ | Mô tả công việc | Lab / Dự án |
| :--- | :--- | :--- | :--- |
| 22/06/2026 | Thứ 2 | Cấu hình IAM Roles & Policies cho EC2 Web API, Lambda, S3 trong dự án Money Manager. Đánh giá và hoàn thiện bảo mật ứng dụng: xác thực JWT, Google OAuth2 trên Spring Boot. Thiết lập Cloudflare WAF, giới hạn tần suất (Rate Limit) và Turnstile anti-bot cho tên miền. | [Dự án cuối khóa](#) |
| 23/06/2026 | Thứ 3 | Triển khai luồng bất đồng bộ: cấu hình SQS + Dead-Letter Queue cho các tác vụ nền. Thiết lập EC2 Worker để tiêu thụ thông điệp từ SQS. Kích hoạt Lambda để tạo báo cáo Excel và render hóa đơn PDF. Cấu hình S3 bucket để lưu trữ tệp đầu ra (báo cáo, hóa đơn). | [Dự án cuối khóa](#) |
| 24/06/2026 | Thứ 4 | Viết kiểm thử đơn vị (unit tests) và kiểm thử tích hợp (integration tests) cho các API nghiệp vụ cốt lõi (thu nhập/chi tiêu, ngân sách, hũ tiết kiệm). Kiểm thử luồng bất đồng bộ end-to-end: SQS -> EC2 Worker -> Lambda -> S3. Chạy kiểm thử tải (load tests) và tối ưu hiệu năng: connection pool, tỷ lệ trúng cache, tối ưu hóa câu lệnh truy vấn. | [Dự án cuối khóa](#) |
| 25/06/2026 | Thứ 5 | Chuẩn bị tài liệu kiến trúc hệ thống Money Manager trên AWS. Mô tả chi tiết các luồng xử lý: nghiệp vụ cốt lõi, chat AI (DynamoDB), bất đồng bộ (SQS/Lambda), thông báo (SNS). Bắt đầu làm slide thuyết trình. | [Dự án cuối khóa](#) |
| 26/06/2026 | Thứ 6 | Kiểm thử tích hợp cổng thanh toán PayOS (thanh toán qua mã QR) và Brevo SMTP (gửi email OTP, báo cáo) qua NAT Gateway. Tối ưu chi phí AWS: đánh giá mức độ sử dụng RDS MySQL, ElastiCache, EC2 ASG, Lambda. Tổng kết tiến độ và lập kế hoạch cho tuần cuối cùng. | [Dự án cuối khóa](#) |

### Kết quả mong đợi

* Hoàn thành bảo mật hệ thống (IAM, Cloudflare WAF, JWT/OAuth2).
* Luồng bất đồng bộ hoạt động ổn định: SQS -> EC2 Worker -> Lambda -> S3.
* Đạt tỷ lệ bao phủ kiểm thử (test coverage) đầy đủ cho các API cốt lõi và luồng xử lý quan trọng.

### Tài liệu tham khảo Tuần 10

* [Dự án cuối khóa - Money Manager (Spring Boot + React JS + React Native Expo)](#)
* Các dịch vụ AWS: IAM, SQS + DLQ, Lambda, S3, SNS, CloudWatch
* Dịch vụ bên ngoài: Cloudflare WAF, PayOS, Brevo SMTP



