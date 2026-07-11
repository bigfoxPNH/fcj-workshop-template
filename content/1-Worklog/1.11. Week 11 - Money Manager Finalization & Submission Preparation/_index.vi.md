---
title: "Tuần 11 - Hoàn thiện Dự án cuối khóa & Chuẩn bị Báo cáo"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
url: "/vi/1-worklog/1.11-week11/"
---

### Chủ đề tuần

Hoàn thiện sản phẩm Money Manager, tối ưu hóa giao diện UI/UX, thiết lập giám sát (monitoring) và chuẩn bị nộp bài báo cáo

### Mục tiêu tuần

* Tối ưu hóa UI/UX cho cả Web và Mobile, chạy kiểm thử E2E (End-to-End).
* Thiết lập hệ thống giám sát, chuẩn bị tài liệu kỹ thuật và chạy thử nghiệm demo để nộp bài.

### Lịch làm việc

| Ngày | Thứ | Mô tả công việc | Lab / Dự án |
| :--- | :--- | :--- | :--- |
| 29/06/2026 | Thứ 2 | Đánh giá và tối ưu hóa UI/UX trên phiên bản React JS + Vite (Web) và React Native Expo (Mobile). Kiểm thử giao diện phản hồi (responsive) và đa nền tảng cho cả web và mobile. Chạy kiểm thử E2E cho các tính năng cốt lõi: đăng ký/đăng nhập, quản lý thu nhập/chi tiêu, chat AI Nova Money. | [Dự án cuối khóa](#) |
| 30/06/2026 | Thứ 3 | Hoàn thiện tài liệu triển khai hệ thống và hướng dẫn cài đặt cho Money Manager. Cấu hình Amazon CloudWatch: Logs, Metrics, Alarms cho ALB, EC2, RDS, Lambda, SQS. Chuẩn bị các script rollback và xác minh tính Sẵn sàng cao (High Availability) trên 2 Availability Zones. | [Dự án cuối khóa](#) |
| 01/07/2026 | Thứ 4 | Chuẩn bị nội dung trình bày slide và kịch bản demo cho Money Manager. Thực hành thuyết trình demo tính năng: quản lý thu nhập/chi tiêu, dự báo tài chính, trợ lý ảo Nova Money, quét hóa đơn bằng OCR. Hoàn thành tệp README và tài liệu dự án. | [Dự án cuối khóa](#) |
| 02/07/2026 | Thứ 5 | Kiểm tra tính năng lần cuối, đánh giá lại toàn bộ mã nguồn của Spring Boot backend và React frontend. Viết báo cáo chi tiết về kiến trúc: VPC multi-AZ, luồng đi của dữ liệu từ ALB -> EC2 -> RDS/ElastiCache/DynamoDB. Tạo kho lưu trữ (repository) cuối cùng và cập nhật mã nguồn lên. | [Dự án cuối khóa](#) |
| 03/07/2026 | Thứ 6 | Xác minh luồng bất đồng bộ: SQS -> EC2 Worker -> Lambda (Xuất báo cáo/Hóa đơn) -> S3. Xác minh luồng thông báo: Amazon SNS gửi email cảnh báo khi ngân sách vượt hạn mức hoặc gói đăng ký sắp hết hạn. Sao lưu dữ liệu RDS MySQL, tạo snapshot cho môi trường và gửi liên kết repository cho giảng viên hướng dẫn. | [Dự án cuối khóa](#) |

### Kết quả mong đợi

* Giao diện UI/UX được tối ưu hoàn thiện, vượt qua các bài kiểm thử E2E cho các tính năng cốt lõi.
* Hệ thống giám sát CloudWatch hoạt động ổn định, sẵn sàng các script rollback.
* Chuẩn bị đầy đủ tài liệu, slide thuyết trình và video/kịch bản demo.

### Tài liệu tham khảo Tuần 11

* [Dự án cuối khóa - Money Manager (Spring Boot + React JS + React Native Expo)](#)
* Các dịch vụ AWS: CloudWatch, SNS, SQS, Lambda, S3, RDS MySQL backup/snapshot



