---
title : "Kết quả thử nghiệm & Thực nghiệm"
date : 2024-01-01 
weight : 4 
chapter : false
pre : " <b> 5.4. </b> "
---
### Kết quả Thử nghiệm & Thực nghiệm
Sau khi hoàn tất cấu hình cơ sở hạ tầng, tác giả đã tiến hành thử nghiệm thực tế từ đầu đến cuối (end-to-end) để đánh giá tính ổn định và chính xác của toàn bộ giải pháp:

#### Thử nghiệm Luồng Đăng ký / Xác thực (AWS Cognito)

Thực hiện đăng ký tài khoản thành viên mới trên giao diện ứng dụng di động GymPro.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Test Results & Experimentation/cognito-register.png" alt="Luồng Đăng ký Cognito" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Hình ảnh chức năng tạo tài khoản và xác thực Cognito

Hệ thống AWS Cognito ghi nhận chính xác người dùng mới và tự động gửi mã kích hoạt OTP về email cá nhân của thành viên. Người dùng nhập mã thành công và trạng thái tài khoản chuyển sang Verified.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Test Results & Experimentation/cognito-users.png" alt="Quản trị Người dùng Cognito" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Giao diện quản lý danh sách tài khoản thành viên và trạng thái xác thực trên AWS Cognito User Pool

#### Thử nghiệm Luồng Tải ảnh Bảo mật qua S3 Presigned URL

Thành viên truy cập tính năng "Cập nhật ảnh đại diện" trên Flutter App, chọn tệp hình ảnh từ thiết bị và nhấn lưu.

Ứng dụng di động lập tức gửi yêu cầu chạy ngầm (background request) tới API Gateway để kích hoạt hàm AWS Lambda đang ẩn mình an toàn trong Private Subnet của VPC.

Hàm Lambda thực thi mượt mà, gọi qua S3 Gateway Endpoint nội bộ để yêu cầu Amazon S3 cấp một đường liên kết mã hóa tạm thời (Presigned URL) có hiệu lực trong 5 phút và trả về cho ứng dụng di động.

Sau khi nhận được liên kết, Flutter App tự động kích hoạt một yêu cầu HTTP PUT để đẩy trực tiếp các byte dữ liệu của tệp ảnh vào Amazon S3 Bucket gympro-storage-s3.

Truy cập S3 Console, tác giả xác nhận tệp ảnh đã được đặt đúng thư mục lưu trữ với định dạng và dung lượng chính xác, chứng minh luồng kết nối bảo mật nội bộ đã hoạt động thành công 100%.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Test Results & Experimentation/s3-upload.png" alt="Tải ảnh lên S3 Thành công" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Hình ảnh chức năng tải ảnh lên hệ thống S3

#### Thử nghiệm Hệ thống Giám sát Lỗi CloudWatch & SNS

Tác giả cố tình chỉnh sửa một đoạn mã nguồn nhỏ trong ứng dụng để gửi yêu cầu sai định dạng, bắt buộc hàm Lambda Backend phải ném ra lỗi hệ thống (system error).

Ngay khi lỗi xảy ra, CloudWatch Log Groups lập tức ghi nhận nhật ký (logs). Bộ lọc chỉ số (Metric Filter) phát hiện từ khóa "ERROR" và đẩy chỉ số trên biểu đồ vượt quá ngưỡng cấu hình.

Hệ thống kích hoạt trạng thái ALARM của CloudWatch Alarm. Trong khoảng 30 giây, một email cảnh báo khẩn cấp từ Amazon SNS được gửi trực tiếp tới hộp thư Gmail quản trị của nhà phát triển (phamquangtrung4504@gmail.com), chứng minh hệ thống cảnh báo lỗi chủ động hoạt động hoàn toàn chính xác theo thiết kế.
