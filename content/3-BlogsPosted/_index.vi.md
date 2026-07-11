---
title: "Các bài blogs đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---
Trang này liệt kê và giới thiệu các bài blog chúng tôi đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj).

### [Blog 1 - Xây dựng các ứng dụng tiêu tốn nhiều bộ nhớ dễ dàng hơn với AWS Lambda Managed Instances](3.1-Blog1/)
Các ứng dụng hiện đại ngày càng đòi hỏi dung lượng bộ nhớ lớn để xử lý dữ liệu lớn, thực hiện các phân tích phức tạp hoặc chạy các mô hình Học máy (ML). Để giải quyết thách thức này, AWS đã giới thiệu AWS Lambda Managed Instances — một giải pháp vượt qua các giới hạn bộ nhớ của Lambda tiêu chuẩn trong khi vẫn giữ nguyên tính tiện lợi hoàn toàn của kiến trúc Serverless.

### [Blog 2 - Next-Gen OpenSearch Serverless: Vector Search Scale-to-Zero cho các ứng dụng AI Agent](3.2-Blog2/)
Các ứng dụng AI agent có mô hình lưu lượng truy cập rất đặc thù: một agent có thể kích hoạt hàng trăm truy vấn vector trong một lần suy luận tác vụ duy nhất, sau đó không hoạt động trong nhiều giờ. Với cơ sở hạ tầng tìm kiếm truyền thống, bạn vẫn phải trả tiền cho phần dung lượng không sử dụng trong những khoảng thời gian nhàn rỗi đó. Vào ngày 28 tháng 5 năm 2026, AWS đã công bố thế hệ tiếp theo của Amazon OpenSearch Serverless (gọi là NextGen) — một công cụ tìm kiếm và vector được thiết kế lại từ đầu để phục vụ chính xác loại khối lượng công việc khó dự đoán này.

### [Blog 3 - Xây dựng các quy trình làm việc nhiều bước đáng tin cậy với AWS Lambda Durable Functions](3.3-Blog3/)
Các ứng dụng hiện đại thường cần xử lý các quy trình tuần tự nhiều bước — chẳng hạn như xử lý đơn hàng, làm quen với người dùng mới hoặc điều phối các quy trình làm việc AI gọi các Mô hình Ngôn ngữ lớn (LLM) và các công cụ bên ngoài nhiều lần. Trước đây, để hoàn thành việc này trên AWS Lambda, các nhà phát triển phải ghép nối Step Functions, SQS và DynamoDB để quản lý trạng thái, dẫn đến cơ sở hạ tầng phức tạp. Tại re:Invent 2025, AWS đã giới thiệu AWS Lambda Durable Functions — cho phép bạn viết toàn bộ quy trình làm việc dưới dạng mã tuần tự trong một hàm Lambda duy nhất trong khi vẫn duy trì khả năng chịu lỗi và tạm dừng lâu dài.