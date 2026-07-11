---
title : "Các bước chuẩn bị"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---
### Các bước chuẩn bị

#### Tài khoản và Truy cập (AWS IAM & CLI)
Hệ thống yêu cầu một tài khoản AWS đang hoạt động với quyền quản trị viên IAM. Để tuân thủ Nguyên tắc Quyền hạn tối thiểu (Principle of Least Privilege), tác giả không sử dụng tài khoản Root chính mà thay vào đó tạo một tài khoản nhà phát triển phụ tên là **GymPro-Developer** để cấp quyền và lấy các khóa bảo mật nhằm kết nối từ máy trạm làm việc thông qua các bước sau:

* **Bước 1 (Cấu hình trên AWS Console):** Đăng nhập vào AWS Management Console bằng tài khoản quản trị viên và điều hướng đến dịch vụ **IAM (Identity and Access Management)** -> **Users (Người dùng)** -> Chọn người dùng **GymPro-Developer**. Di chuyển đến tab **Security credentials (Thông tin bảo mật)**, tìm đến phần **Access keys (Khóa truy cập)** và chọn **Create access key (Tạo khóa truy cập)**. Chọn **Command Line Interface (CLI)** làm trường hợp sử dụng (use case), đồng ý với các điều khoản và xác nhận để hệ thống tạo cặp khóa: **Access Key ID** và **Secret Access Key**. Tải xuống tệp `.csv` chứa thông tin khóa bảo mật này.

* **Bước 2 (Cấu hình trên máy trạm cục bộ):** Mở Terminal hoặc PowerShell trên máy tính cá nhân của bạn và chạy lệnh sau:

```bash
aws configure
```

Nhập Access Key ID và Secret Access Key đã được tạo ở Bước 1. Thiết lập Default region name thành `us-east-1` (N. Virginia - vùng triển khai mặc định của dự án GymPro) và Default output format thành `json`. Cấu hình này sẽ tự động được lưu trong thư mục người dùng (`~/.aws/` trên Linux/macOS hoặc `%USERPROFILE%\.aws\` trên Windows).

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.2-Prerequisite/iam-credentials.png" alt="Thông tin xác thực bảo mật IAM" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Tab IAM Security credentials với phần Access keys được sử dụng để tạo các khóa kết nối CLI.

#### Môi trường Máy trạm Cục bộ
* Đảm bảo máy trạm đã cài đặt thành công môi trường **Node.js** (phiên bản 20 trở lên) để viết và đóng gói mã nguồn cho các hàm Lambda Backend, cùng với môi trường phát triển ứng dụng di động **Flutter** (Dart SDK).
* Máy trạm phải duy trì kết nối Internet ổn định để tải các gói phụ thuộc (`@aws-sdk/client-s3`, `@aws-sdk/s3-request-presigner` cho Node.js và thư viện `http` cho Flutter).

#### Lựa chọn Vùng Cơ sở hạ tầng
Lựa chọn vùng cơ sở hạ tầng mạng AWS tại **N. Virginia (us-east-1)** làm vùng triển khai mặc định để đảm bảo khả năng tương thích tối đa cho tất cả các dịch vụ AWS được sử dụng trong kiến trúc, đồng thời tối ưu hóa chi phí hạ tầng Serverless cho dự án cá nhân.