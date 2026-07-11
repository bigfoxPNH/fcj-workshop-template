---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# XÂY DỰNG CÁC ỨNG DỤNG TIÊU TỐN NHIỀU BỘ NHỚ DỄ DÀNG HƠN VỚI AWS LAMBDA MANAGED INSTANCES

## AWS Lambda Managed Instances là gì?
Tính năng này cho phép bạn chạy các hàm AWS Lambda trên các phiên bản Amazon EC2 do bạn tự chọn (bao gồm các phiên bản tối ưu hóa bộ nhớ hoặc Graviton4). Bước đột phá là nó cung cấp bộ nhớ RAM lên tới 32 GB — cao gấp 3 lần so với giới hạn trước đây của Lambda. Toàn bộ vòng đời cơ sở hạ tầng (cấp phát, mở rộng quy mô, vá lỗi...) đều được AWS quản lý hoàn toàn.

## Các điểm nổi bật & Lợi ích cốt lõi
- **Thực thi đồng thời nhiều yêu cầu (Multi-concurrent invocations):** Một môi trường thực thi duy nhất có thể xử lý đồng thời nhiều yêu cầu, tối đa hóa hiệu suất cho các ứng dụng nặng về I/O.
- **Mở rộng quy mô động không có độ trễ (Dynamic scaling with no latency):** Hệ thống tự động mở rộng quy mô dựa trên mức sử dụng CPU mà không gặp phải tình trạng khởi động nguội (cold start).
- **Lựa chọn phần cứng linh hoạt (Flexible hardware selection):** Các nhà phát triển có thể chọn các dòng phiên bản tối ưu hóa tính toán (C), đa dụng (M), hoặc tối ưu hóa bộ nhớ (R) và điều chỉnh tỷ lệ RAM trên CPU khi cần.
- **Tiết kiệm chi phí (Cost savings):** Bằng cách sử dụng giá EC2, doanh nghiệp có thể áp dụng Savings Plans để giảm chi phí lên tới 33% so với giá Lambda tiêu chuẩn cho các khối lượng công việc có thể dự đoán trước.

## Các trường hợp sử dụng lý tưởng
Giải pháp này cực kỳ hiệu quả trong các hệ thống yêu cầu tải lượng lớn dữ liệu vào bộ nhớ:
- **Phân tích trong bộ nhớ (In-Memory Analytics):** Tải hàng gigabyte dữ liệu cho các truy vấn với độ trễ tính bằng mili giây.
- **Chạy các mô hình học máy (Running Machine Learning Models):** Giữ các mô hình AI trực tiếp trong RAM để suy luận nhanh chóng mà không cần trả phí cho một endpoint chuyên dụng (như Amazon SageMaker).
- **Tìm kiếm ngữ nghĩa (Semantic Search):** Duy trì các chỉ mục vector (vector indexes) trực tiếp trong bộ nhớ cho các truy vấn ngôn ngữ tự nhiên mà không cần Cơ sở dữ liệu Vector bên ngoài.
- **Tính toán khoa học & Xử lý đồ thị (Scientific Computing & Graph Processing):** Tối ưu hóa cho các thuật toán phức tạp cần quét toàn bộ các bộ dữ liệu lớn cùng một lúc.

## Ví dụ thực tế: Phân tích khách hàng hỗ trợ bởi AI (Real-World Example: AI-Powered Customer Analytics)
Trong bài viết, AWS trình bày việc xây dựng một hệ thống phân tích khách hàng. Hệ thống này tải 1 triệu bản ghi (định dạng Parquet từ S3) và mô hình tìm kiếm FastEmbed trực tiếp vào bộ nhớ trong quá trình khởi tạo hàm. Tổng dung lượng bộ nhớ sử dụng xấp xỉ 14 GB RAM (điều không thể thực hiện với Lambda truyền thống). Kết quả là một ứng dụng Serverless có thể phân tích xu hướng và tìm kiếm thông tin khách hàng trong thời gian thực (dưới một giây) mà đội ngũ IT không cần quản lý bất kỳ máy chủ EC2 nào.

![AI-Powered Customer Analytics](/images/3-BlogsPosted/customer_analytics.png)

## Kết luận
Xây dựng các ứng dụng tiêu tốn nhiều bộ nhớ giờ đây không còn đồng nghĩa với việc từ bỏ mô hình Serverless. AWS Lambda Managed Instances là sự kết hợp hoàn hảo giữa sức mạnh phần cứng của Amazon EC2 cùng sự đơn giản và tự động hóa của AWS Lambda. Đây là bước đệm tuyệt vời cho các dự án Phân tích Dữ liệu và AI/ML.

*Bài viết gốc: Building memory-intensive apps with AWS Lambda Managed Instances*