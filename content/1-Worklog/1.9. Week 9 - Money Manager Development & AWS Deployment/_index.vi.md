---
title: "Tuần 9 - Phát triển Dự án cuối khóa & Triển khai AWS"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
url: "/vi/1-worklog/1.9-week9/"
---

### Chủ đề tuần

Phát triển các tính năng cốt lõi của Money Manager và triển khai lên AWS theo kiến trúc đã thiết kế

### Mục tiêu tuần

* Phát triển các tính năng chính của Money Manager (backend + frontend).
* Triển khai lên AWS theo kiến trúc multi-AZ đã thiết kế ở tuần 8.

### Lịch làm việc

| Ngày | Thứ | Mô tả công việc | Lab / Dự án |
| :--- | :--- | :--- | :--- |
| 15/06/2026 | Thứ 2 | Xem lại mã nguồn và ưu tiên thứ tự triển khai các module. Đảm bảo môi trường phát triển ổn định (Spring Boot backend, React frontend). Xem xét quy trình build & deploy trước khi bắt đầu phát triển tính năng mới. | [Dự án cuối khóa](#) |
| 16/06/2026 | Thứ 3 | Phát triển các API nghiệp vụ cốt lõi: quản lý thu nhập/chi tiêu, ngân sách, hũ tiết kiệm. Kiểm tra entity mapping, mối quan hệ giữa các bảng và luồng truy xuất dữ liệu. Kiểm thử cục bộ để đảm bảo API hoạt động chính xác với MySQL. | [Dự án cuối khóa](#) |
| 17/06/2026 | Thứ 4 | Hoàn thiện các tính năng xác thực: JWT token + Google OAuth2. Phát triển các API phân quyền người dùng (Free/Premium). Cập nhật tài liệu kỹ thuật và tài liệu API. | [Dự án cuối khóa](#) |
| 18/06/2026 | Thứ 5 | Triển khai Spring Boot backend lên EC2 trong Private Subnet. Cấu hình ALB trong Public Subnet để điều tuyến lưu lượng đến EC2. Thiết lập Auto Scaling Group cho EC2 Web API để tự động mở rộng/thu hẹp dựa trên tải. | [Dự án cuối khóa](#) |
| 19/06/2026 | Thứ 6 | Cấu hình RDS MySQL multi-AZ. Cấu hình ElastiCache Redis để lưu cache và quản lý session. Kiểm tra kết nối từ EC2. | [Dự án cuối khóa](#) |

### Kết quả mong đợi

* Các API nghiệp vụ cốt lõi đi vào hoạt động ổn định (quản lý thu nhập/chi tiêu, xác thực, phân quyền).
* Backend được triển khai thành công lên EC2 với ALB + Auto Scaling Group.
* Cấu hình và kết nối thành công RDS MySQL và ElastiCache Redis.

### Tài liệu tham khảo Tuần 9

* [Dự án cuối khóa - Money Manager (Spring Boot + React JS + React Native Expo)](#)
* Các dịch vụ AWS: EC2 ASG, ALB, RDS MySQL, ElastiCache Redis



