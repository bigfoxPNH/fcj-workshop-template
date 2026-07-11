---
title: "Tuần 7 - Khởi động Dự án cuối khóa & Phân tích"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
url: "/vi/1-worklog/1.7-week7/"
---

### Chủ đề tuần

Khởi động dự án cuối khóa Money Manager - tìm hiểu mã nguồn, thiết lập môi trường và triển khai thử nghiệm lên AWS

### Mục tiêu tuần

* Hiểu cấu trúc mã nguồn và kiến trúc của dự án Money Manager.
* Thiết lập môi trường phát triển cục bộ và bắt đầu triển khai thử nghiệm các thành phần lên AWS.

### Lịch làm việc

| Ngày | Thứ | Mô tả công việc | Lab / Dự án |
| :--- | :--- | :--- | :--- |
| 01/06/2026 | Thứ 2 | Đọc tài liệu dự án Money Manager, phân tích cấu trúc thư mục và các module chính (Spring Boot backend, React Frontend, React Native mobile). Thiết lập môi trường phát triển: JDK 21, Maven, Node.js, Docker. Chạy thử Spring Boot backend và React frontend cục bộ; tìm hiểu luồng build & deploy. | [Dự án cuối khóa](#) |
| 02/06/2026 | Thứ 3 | Phân tích kiến trúc phân lớp (Controller -> Service -> Repository) của Spring Boot backend. Tìm hiểu về database schema, các lớp thực thể (entity), và cấu hình Spring Data JPA/Hibernate. Tìm hiểu cách backend kết nối với MySQL và cấu hình connection pooling. | [Dự án cuối khóa](#) |
| 03/06/2026 | Thứ 4 | Nghiên cứu các tính năng cốt lõi: đăng nhập (JWT + Google OAuth2), quản lý thu nhập/chi tiêu, ngân sách, hũ tiết kiệm. Tìm hiểu cách backend tương tác với cơ sở dữ liệu và các API endpoint. Bắt đầu viết ghi chú kỹ thuật và tài liệu kiến trúc. | [Dự án cuối khóa](#) |
| 04/06/2026 | Thứ 5 | Triển khai thử nghiệm Spring Boot backend lên AWS EC2. Cấu hình RDS MySQL và kết nối ứng dụng. Kiểm thử các API cơ bản và xử lý các lỗi ban đầu. | [Dự án cuối khóa](#) |
| 05/06/2026 | Thứ 6 | Tích hợp S3 để lưu trữ file (ảnh hóa đơn, báo cáo). Tìm hiểu cách thiết lập CloudFront để phân phối tài sản tĩnh (static assets). Kiểm thử hệ thống và đánh giá hiệu năng. | [Dự án cuối khóa](#) |

### Kết quả mong đợi

* Hiểu rõ kiến trúc Spring Boot và các luồng nghiệp vụ cốt lõi của Money Manager.
* Thiết lập thành công môi trường chạy cục bộ và triển khai thử nghiệm lên EC2.
* Xây dựng nền tảng kỹ thuật vững chắc cho các tuần phát triển tiếp theo.

### Tài liệu tham khảo Tuần 7

* [Dự án cuối khóa - Money Manager (Spring Boot + React JS + React Native Expo)](#)
* Các dịch vụ AWS: EC2, RDS MySQL, S3, CloudFront



