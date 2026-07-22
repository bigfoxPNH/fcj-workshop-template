---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# PROPOSAL

## GymPro – Hệ thống quản lý phòng gym thông minh trên AWS
### Giải pháp toàn diện cho hoạt động vận hành phòng gym với kiến trúc AWS Serverless & Cloud-Native

### 1. Tóm tắt điều hành
GymPro là một hệ thống quản lý và vận hành phòng gym thông minh được xây dựng trên kiến trúc Cloud-Native và Serverless hiện đại trên Amazon Web Services (AWS). Từ góc độ kỹ thuật, ứng dụng phía máy khách được phát triển bằng Flutter (Đa nền tảng), trong khi cơ sở hạ tầng backend hoạt động hoàn toàn trên các dịch vụ đám mây thế hệ mới của AWS tích hợp với cơ sở dữ liệu thời gian thực Firebase Firestore. Tác giả và quản trị viên chính của hệ thống là phamquangtrung4504@gmail.com.

### 2. Mục tiêu
Với GymPro, mục tiêu cốt lõi không chỉ đơn thuần là số hóa các quy trình quản lý mà còn hướng tới việc tối ưu hóa toàn bộ cơ sở hạ tầng:
- Giảm thiểu tối đa chi phí vận hành phần cứng thông qua mô hình Serverless.
- Tự động mở rộng quy mô theo lượng truy cập đồng thời của các thành viên.
- Tối ưu hóa bảo mật dữ liệu với mạng riêng ảo và các quy tắc bảo mật nghiêm ngặt.
- Nâng cao trải nghiệm người dùng thông qua trợ lý AI (Google Gemini API) được tích hợp trực tiếp vào ứng dụng, đóng vai trò như một huấn luyện viên cá nhân thông minh để cung cấp lời khuyên về dinh dưỡng và luyện tập.

### 3. Tuyên bố vấn đề
- **Tình trạng hiện tại:** Các phòng gym truyền thống thường gặp khó khăn trong việc quản lý thành viên tập trung, bảo mật dữ liệu thẻ thành viên và tối ưu hóa chi phí bảo trì máy chủ trong những thời điểm lưu lượng truy cập biến động mạnh.
- **Giải pháp:** GymPro tận dụng kiến trúc Serverless trên AWS để loại bỏ hoàn toàn việc bảo trì máy chủ vật lý. Danh tính người dùng được quản lý thông qua AWS Cognito, dữ liệu được lưu trữ trong Firebase Firestore và tất cả các tính toán backend (ví dụ: cấp quyền tải lên) được xử lý an toàn bởi AWS Lambda ẩn trong một VPC.
- **Lợi ích:** Mang lại một hệ thống có tính sẵn sàng cao, được bảo mật nghiêm ngặt với chi phí vận hành ban đầu gần như bằng không, cung cấp trải nghiệm hiện đại cho các thành viên.

### 4. Kiến trúc hệ thống
Toàn bộ cơ sở hạ tầng backend được triển khai trên AWS trong mạng nội bộ Amazon VPC (subnet 10.0.0.0/16), được chia thành Public và Private Subnet trên 2 Availability Zones (AZs).

**Công nghệ sử dụng:**
- **Client App:** Flutter (Ứng dụng di động đa nền tảng).
- **Cơ sở dữ liệu:** Firebase Firestore (Cơ sở dữ liệu NoSQL).
- **Trí tuệ nhân tạo:** Google Gemini API.

**Các dịch vụ AWS cốt lõi:**
- **AWS Cognito (User Pool & Roles):** Quản lý định danh (Đăng ký/Đăng nhập/Đăng xuất), mã hóa bảo mật và gửi mã OTP qua hệ thống thoại/email.
- **Amazon S3:** Kho lưu trữ dung lượng cao tập trung tất cả ảnh đại diện (Avatar) và ảnh check-in luyện tập.
- **AWS Lambda:** Xử lý các tính toán backend Serverless, chứa các hàm nghiệp vụ độc lập (chẳng hạn như GymPro_Get_Upload_URL).
- **Amazon VPC:** Cơ sở hạ tầng mạng cô lập giúp ẩn hoàn toàn các hàm Lambda tính toán nặng bên trong Private Subnet, cách ly nghiêm ngặt chúng khỏi Internet công cộng.
- **Amazon CloudWatch:** Radar giám sát thu thập nhật ký vận hành và quét từ khóa 'ERROR' bằng Metric Filters.
- **Amazon SNS:** Hệ thống cảnh báo tự động liên kết với CloudWatch để gửi cảnh báo khẩn cấp đến Gmail.

![Kiến trúc hệ thống](/images/2-Proposal/architecture1.png?classes=shadow)

**Các luồng dữ liệu chính:**
- **Luồng xác thực & đồng bộ hóa dữ liệu:** Người dùng nhập thông tin đăng nhập trên ứng dụng di động Flutter. Yêu cầu được gửi đến AWS Cognito User Pool để lấy các mã thông báo bảo mật (ID, Access Token). Sau đó, ứng dụng sử dụng ID Cognito làm khóa để xác thực với Firestore Security Rules nhằm đọc/ghi dữ liệu lịch sử tập luyện của thành viên.
- **Luồng tải ảnh an toàn qua VPC cô lập:** Ứng dụng yêu cầu quyền tải lên hình ảnh thông qua API Gateway. Yêu cầu được chuyển tiếp đến một hàm AWS Lambda ẩn trong Private Subnet. Hàm Lambda giao tiếp an toàn thông qua S3 Gateway Endpoint nội bộ để yêu cầu một S3 Presigned URL tạm thời từ Amazon S3. URL này được trả về để ứng dụng có thể tải trực tiếp các tệp ảnh nặng lên S3.
- **Luồng Radar giám sát lỗi chủ động:** Lambda tự động đẩy nhật ký lên CloudWatch Log Groups. Metric Filter quét từ khóa "ERROR" và cộng thêm 1 điểm nếu phát hiện. Nếu CloudWatch Alarm ghi nhận >= 1 lỗi trong chu kỳ 5 phút, hệ thống sẽ kích hoạt Amazon SNS (Topic: GymPro-Urgent-Alerts) để gửi email cảnh báo khẩn cấp đến phamquangtrung4504@gmail.com.

### 5. Triển khai kỹ thuật
Nhóm HTV chia sẻ các nhiệm vụ kỹ thuật để đáp ứng các tiêu chuẩn của dự án:
- **Phát triển Frontend:** Trung và Vũ chịu trách nhiệm phát triển giao diện người dùng bằng Flutter, đảm bảo trải nghiệm mượt mà trên cả iOS và Android.
- **Thiết kế Backend AWS:** Xây dựng cơ sở hạ tầng Serverless với AWS Lambda, cấu hình xác thực Cognito và thiết lập bảo mật mạng VPC.
- **Tích hợp AI & Cơ sở dữ liệu:** Khởi tạo Firebase Firestore với các Security Rules nghiêm ngặt và tích hợp Google Gemini API để nhúng logic tư vấn dinh dưỡng cho AI Chatbot.

### 6. Lộ trình triển khai
Lộ trình triển khai dự án tại HUTECH được chia thành các giai đoạn chính:
- **Tuần 1-3:** Khởi tạo kiến trúc mạng Amazon VPC (Subnets, AZs) và thiết lập AWS Cognito. Thực hiện cấu hình Firebase Firestore ban đầu.
- **Tuần 4-6:** Nhóm HTV lập trình giao diện Ứng dụng di động bằng Flutter và kết nối luồng xác thực đăng nhập.
- **Tuần 7-9:** Lập trình các hàm AWS Lambda cốt lõi (ví dụ: GymPro_Get_Upload_URL), cấu hình S3 Gateway Endpoint và hoàn thiện luồng tải ảnh bảo mật qua Presigned URL.
- **Tuần 10-12:** Tích hợp Google Gemini API cho tính năng AI Chatbot. Thiết lập Amazon CloudWatch và cấu hình cảnh báo Amazon SNS. Chạy thử nghiệm luồng lỗi và chuẩn bị cho buổi bảo vệ dự án cuối kỳ.

### 7. Ước tính chi phí
Kiến trúc Serverless mang lại lợi thế vượt trội về chi phí cho giai đoạn phát triển:
- **AWS Lambda & API Gateway:** Tính phí theo số lượng yêu cầu, dự kiến nằm hoàn toàn trong giới hạn Free Tier.
- **AWS Cognito:** Miễn phí cho 50.000 MAU (Người dùng hoạt động hàng tháng) đầu tiên.
- **Amazon S3:** Chi phí cực thấp (~0.025 USD/GB) để lưu trữ ảnh check-in.
- **Amazon VPC & CloudWatch:** Các tính năng cơ bản và Metric Filters nằm trong giới hạn của gói miễn phí.

### 8. Đánh giá rủi ro
- **Rủi ro lộ thông tin xác thực:** Rất thấp nhờ cơ chế cấp S3 Presigned URL thời hạn ngắn để tải ảnh lên thay vì để lộ thông tin xác thực tài khoản AWS gốc cho Phía máy khách.
- **Truy cập trái phép từ Internet công cộng:** Được ngăn chặn hoàn toàn do các hàm logic nghiệp vụ nặng được ẩn hoàn toàn bên trong Private Subnet của VPC.
- **Khôi phục sự cố hệ thống:** Với luồng Radar giám sát lỗi sử dụng CloudWatch và SNS, mọi lỗi phát sinh sẽ tự động được cảnh báo đến email của quản trị viên trong vòng 5 phút, đảm bảo phản hồi và giải quyết nhanh chóng.

### 9. Kết quả kỳ vọng
Xây dựng thành công một hệ thống quản lý phòng gym hiện đại, an toàn và tối ưu hóa tài nguyên. GymPro sẽ đóng vai trò là một minh chứng thực tế về việc áp dụng kiến trúc Serverless & Cloud-Native để giải quyết các vấn đề kinh doanh, tạo ra một hệ thống không cần bảo trì máy chủ vật lý, khả năng tự động mở rộng vô hạn và bảo mật dữ liệu tối đa cho các thành viên.