---
title : "Khó khăn & Hướng phát triển"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---
### Khó khăn & Hướng phát triển

#### Khó khăn Gặp phải

* **Lỗi phân quyền mạng ẩn (ENI)**: Trong giai đoạn đầu triển khai Lambda vào mạng con VPC, do chưa hiểu rõ cơ chế vận hành hạ tầng mạng, tác giả đã gặp lỗi hệ thống từ chối quyền truy cập mạng khi lưu cấu hình. Sau khi tìm hiểu tài liệu khắc phục lỗi `CreateNetworkInterface` tại AWS Knowledge Center, tác giả đã khắc phục được bằng cách gán thêm policy tiêu chuẩn `AWSLambdaVPCAccessExecutionRole` cho IAM Role của hàm Lambda.
* **Xung đột chính sách bảo mật (Bucket Policy vs. Endpoint Policy)**: Khi thiết lập bộ lọc bảo mật cho kho lưu trữ S3, việc cấu hình S3 Bucket Policy chặn mọi truy cập từ Internet bên ngoài quá sớm—trước khi gán chính xác ARN dịch vụ của VPC Endpoint—đã dẫn đến kết quả là chính hàm Lambda nội bộ cũng bị dịch vụ S3 từ chối kết nối (Access Denied). Tác giả đã phải lần vết nhật ký lỗi trên CloudWatch logs và thực thi các câu lệnh kiểm tra ngắn bằng CLI để xác định chính xác và điều chỉnh trình tự thiết lập.

#### Hướng phát triển Tương lai

* **Triển khai Hạ tầng dưới dạng mã nguồn (IaC)**: Chuyển dịch toàn bộ thao tác cấu hình thủ công bằng giao diện Web Console hiện tại (VPC, Subnets, Lambda, Endpoint, IAM, Bucket Policy) sang dạng mã nguồn quản lý tập trung bằng Terraform hoặc AWS CloudFormation. Việc này giúp dễ dàng đóng gói, kiểm soát phiên bản và tái lập hạ tầng dự án chỉ với một câu lệnh.
* **Mở rộng vùng mạng bảo mật nội bộ**: Tích hợp thêm các Gateway/Interface Endpoint cho các dịch vụ phụ thuộc khác trong kiến trúc như AWS Cognito hay Amazon DynamoDB. Điều này sẽ khóa hoàn toàn luồng dữ liệu bên trong mạng xương sống của AWS, nâng cấp ứng dụng GymPro đạt chuẩn bảo mật doanh nghiệp ở mức tối đa.
* **Xây dựng Dashboard giám sát tập trung**: Đồng bộ các chỉ số rời rạc từ CloudWatch Alarms và Log Groups vào một giao diện giám sát duy nhất (CloudWatch Dashboard). Việc này sẽ giúp người quản trị hệ thống phòng tập có cái nhìn trực quan và toàn diện nhất về sức khỏe hệ thống khi vận hành thực tế.