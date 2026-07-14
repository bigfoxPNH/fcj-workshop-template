---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---
# GIỚI THIỆU

### Triển khai cơ sở hạ tầng và thiết lập kết nối an toàn với Amazon S3

<div style="text-align: center; margin: 20px 0;">

  ![Kiến trúc tổng thể](/images/5-Workshop/5.1-Introduction/architecture1.png?classes=shadow)

  <div style="font-weight: bold; margin-top: 8px; color: #555;">Hình 1. Kiến trúc tổng thể của cơ sở hạ tầng mạng và sự tích hợp dịch vụ AWS.</div>
</div>

<br>

### Giới thiệu Tổng quan

Bài thực hành này ghi lại đầy đủ quy trình xây dựng, cấu hình và thử nghiệm cơ sở hạ tầng đám mây cho dự án Hệ thống Quản lý và Vận hành Phòng tập thông minh (GymPro).

Cấu hình tập trung vào việc triển khai mô hình Serverless và bảo mật đa lớp, bao gồm:
* Thiết lập mạng riêng cô lập (Amazon VPC).
* Triển khai cấu hình Backend AWS Lambda để xử lý logic nghiệp vụ Serverless.
* Cấu hình một Gateway VPC Endpoint định tuyến đến Amazon S3 để tối ưu hóa truyền tải mạng, đảm bảo bảo vệ tuyệt đối dữ liệu hình ảnh check-in và ảnh đại diện của thành viên khỏi các nguy cơ rò rỉ trên Internet công cộng, đồng thời loại bỏ hoàn toàn chi phí xử lý dữ liệu của NAT Gateway.
* Phân quyền kiểm soát truy cập nghiêm ngặt thông qua AWS IAM và S3 Bucket Policies.

Thông qua việc triển khai thực tế này, hệ thống đã áp dụng và tuân thủ nghiêm ngặt các tiêu chuẩn thiết kế của Khung kiến trúc AWS Well-Architected, tập trung vào hai trụ cột cốt lõi: Bảo mật và Tối ưu hóa chi phí.
