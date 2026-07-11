---
title : "Các bước triển khai"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---
### Các bước triển khai chi tiết

#### Bước 1: Thiết lập VPC riêng biệt, cô lập (Isolated Private VPC)
Quá trình xây dựng môi trường mạng cô lập để đặt toàn bộ luồng xử lý Backend vào một vùng an toàn:

Khởi tạo một VPC tùy chỉnh có tên là **GymPro-VPC** với khối IP CIDR là `10.0.0.0/16` làm dải mạng riêng chính.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/vpc-list.png" alt="Danh sách VPC" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Danh sách VPC hiển thị VPC tùy chỉnh với CIDR 10.0.0.0/16

Chia các dải mạng con (subnets) thành các phân tầng cô lập: Public Subnets (chứa các thành phần tiếp xúc với Internet công cộng) và Private Subnets (chứa các giao diện mạng nội bộ của các dịch vụ tính toán để cô lập hoàn toàn IP của chúng khỏi Internet Gateway). Hệ thống được phân bổ đều trên hai Availability Zones (us-east-1a và us-east-1b) để đảm bảo tính dự phòng.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/subnet-list.png" alt="Danh sách Subnet" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Danh sách các Subnet được phân bổ trên các phân tầng Public và Private

Cấu hình các Route Table tương ứng: Public Subnet định tuyến trực tiếp đến Internet Gateway; Private Subnet thiết lập dải định tuyến nội bộ với NAT Gateway được đặt thành None để tránh tiêu tốn chi phí duy trì tài khoản hàng tháng.

#### Bước 2: Triển khai Serverless Backend với AWS Lambda

Khởi tạo một hàm tính toán Serverless có tên là **GymPro_Get_Upload_URL** chạy trên môi trường Node.js. Hàm này xử lý các logic nghiệp vụ quan trọng: nhận tên tệp được gửi từ Flutter App, thực hiện ký số bảo mật và tạo một S3 Presigned URL ngắn hạn (thời gian sống giới hạn trong 5 phút) để cấp quyền tải ảnh lên cho các thành viên.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/lambda-source.png" alt="Cấu hình mã nguồn Lambda" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Giao diện cấu hình mã nguồn của hàm Lambda GymPro_Get_Upload_URL tích hợp với API Gateway trên AWS Console

Cấu hình kết nối mạng cho hàm Lambda: Di chuyển đến tab Configuration -> chọn VPC -> Kết nối trực tiếp hàm Lambda với GymPro-VPC.

Lựa chọn chính xác 2 Private Subnets (GymPro-VPC-subnet-private1-... và GymPro-VPC-subnet-private2-...) để bắt buộc Lambda phải chạy hoàn toàn trong phân vùng mạng nội bộ an toàn. Gán Security Group mặc định của VPC cho hàm Lambda để quản lý các quy tắc Inbound/Outbound.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/lambda-vpc.png" alt="Cấu hình Lambda VPC" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Cấu hình phân bổ hàm Lambda chạy trong môi trường mạng nội bộ GymPro-VPC và các Private Subnet trên AWS Console

#### Bước 3: Cấu hình quyền truy cập hệ thống trên AWS IAM

Khi cấu hình Lambda được đặt trong Private Subnet, hệ thống ban đầu sẽ báo lỗi phân quyền vì Lambda chưa có quyền tạo các giao diện mạng ảo nội bộ.

Để giải quyết vấn đề này, hãy truy cập dịch vụ IAM -> Roles -> Chọn chính xác Role thực thi hiện tại của hàm (GymPro_Get_Upload_URL-role-...).

Nhấp vào nút Add permissions -> Attach policies -> Tìm kiếm và chọn policy do AWS quản lý: AWSLambdaVPCAccessExecutionRole.

Xác nhận gán quyền để cấp cho Lambda đầy đủ các đặc quyền tạo và quản lý Elastic Network Interfaces (ENIs) nhằm truy cập dải mạng VPC.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/iam-role.png" alt="Gán IAM Role" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Giao diện gán policy AWSLambdaVPCAccessExecutionRole cho IAM Role của hàm Lambda trên AWS Console

#### Bước 4: Thiết lập Bảo mật Amazon S3 và Gateway VPC Endpoint
Thiết lập kết nối mạng riêng để tối ưu hóa chi phí và bảo vệ kho lưu trữ dữ liệu lớn:

Khởi tạo một Amazon S3 Bucket có tên là **gympro-storage-s3** ở chế độ hoàn toàn riêng tư (Block Public Access) và bật mặc định Server-Side Encryption (SSE-S3) để lưu trữ tất cả ảnh đại diện của thành viên và ảnh check-in tập luyện.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/s3-files.png" alt="Quản lý tệp S3" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Giao diện quản lý các tệp hình ảnh thành viên được lưu trữ bên trong Bucket gympro-storage-s3 trên AWS Console

Trên trang quản lý VPC Console, tạo một Gateway VPC Endpoint cho S3 (tên dịch vụ: com.amazonaws.us-east-1.s3) và gán trực tiếp vào các Route Table của các Private Subnet trong GymPro-VPC.

Bản ghi định tuyến mới tự động được hệ thống thêm vào sẽ hướng tất cả các yêu cầu và giao tiếp từ hàm Lambda nội bộ đến Amazon S3 thông qua mạng xương sống nội bộ của AWS thay vì định tuyến ra ngoài Internet. Cơ chế này giúp cắt giảm 100% chi phí băng thông mạng cho S3 và tăng tốc độ truyền tải tệp.

Cấu hình S3 Bucket Policy nghiêm ngặt để bảo vệ tài nguyên: Từ chối tuyệt đối tất cả các yêu cầu truy cập đọc/ghi từ Internet bên ngoài và chỉ chấp nhận các yêu cầu tương tác hợp lệ đi qua Gateway VPC Endpoint mới được tạo của hệ thống.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/s3-security.png" alt="S3 Block Public Access" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Trạng thái kích hoạt của tính năng Block Public Access bảo vệ kho lưu trữ dữ liệu S3 trên AWS Console

#### Bước 5: Cấu hình hệ thống giám sát với Amazon CloudWatch & SNS
Thiết lập "mắt thần" giám sát tự động để theo dõi tất cả các nhật ký lỗi Backend:

Hàm Lambda nghiệp vụ tự động đẩy tất cả nhật ký vận hành chi tiết vào dịch vụ Amazon CloudWatch Log Groups trong thời gian thực.

Thiết lập một Metric Filter tùy chỉnh có tên là **EC2ErrorFilter** (hoặc **LambdaErrorFilter**) trên Log Group của dự án để quét qua luồng nhật ký và đếm tần suất của các từ khóa lỗi viết hoa như "ERROR" hoặc "Exception".

Khởi tạo một CloudWatch Alarm kết nối trực tiếp với chỉ số (metric) của bộ lọc. Cấu hình ngưỡng cảnh báo nhạy bén: Chuyển sang trạng thái báo động khẩn cấp (ALARM) ngay khi số lượng lỗi >= 1 trong khoảng thời gian giám sát 5 phút.

Liên kết Alarm với dịch vụ Amazon SNS (Simple Notification Service). Khi trạng thái báo động kích hoạt, SNS sẽ tự động biên soạn thông báo lỗi hệ thống Backend và gửi email khẩn cấp theo thời gian thực tới hộp thư Gmail quản trị của nhà phát triển (phamquangtrung4504@gmail.com).

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Implementation Steps/cloudwatch-logs.png" alt="Quản lý CloudWatch Log Groups" style="width: 100%; max-width: 900px; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</div>

> [!NOTE]
> Giao diện quản lý CloudWatch Log Groups để giám sát nhật ký vận hành hệ thống Serverless trên AWS Console
