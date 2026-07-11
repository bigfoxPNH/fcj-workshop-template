---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---
### Dọn dẹp Tài nguyên
Sau khi kết thúc các phiên thử nghiệm thực nghiệm để bảo vệ đồ án tốt nghiệp, tác giả đã tiến hành dọn dẹp hạ tầng thử nghiệm nhằm tối ưu hóa tài nguyên và ngăn ngừa các khoản phí phát sinh ngoài ý muốn trên tài khoản AWS:

* **Xóa đối tượng S3**: Xóa hoàn toàn tất cả các tệp hình ảnh và ảnh đại diện thử nghiệm đã tải lên bucket `gympro-storage-s3` để giải phóng dung lượng lưu trữ hàng tháng.
* **Gỡ bỏ VPC Endpoints**: Truy cập cấu hình VPC, hủy liên kết và gỡ bỏ Gateway VPC Endpoint khỏi các Route Table của các Private Subnet để khôi phục cấu hình mạng về trạng thái ban đầu.
* **Gỡ bỏ Alarms và Filters**: Xóa các cấu hình Metric Filter và tắt các Alarm giám sát trên dịch vụ Amazon CloudWatch để dừng luồng quét nhật ký tự động.
