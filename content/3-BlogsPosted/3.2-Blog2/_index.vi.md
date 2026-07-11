---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# NEXT-GEN OPENSEARCH SERVERLESS: VECTOR SEARCH SCALE-TO-ZERO CHO CÁC ỨNG DỤNG AI AGENT

## OpenSearch Serverless NextGen là gì?
NextGen là kiến trúc mới của Amazon OpenSearch Serverless, một công cụ tìm kiếm và vector được quản lý hoàn toàn (fully managed). Cải tiến cốt lõi là nó phân tách hoàn toàn tính toán (compute) và lưu trữ (storage) thông qua một lớp lưu trữ dùng chung, cho phép dung lượng tính toán mở rộng độc lập với khối lượng dữ liệu. Điều này cho phép dịch vụ cấp phát tài nguyên trong vài giây và thu nhỏ về không (scale-to-zero) khi nhàn rỗi.

AWS đặt tên cho hai kiến trúc này là: các collection cũ hiện được gọi là Classic, trong khi kiến trúc mới là NextGen và là tùy chọn mặc định khi tạo các collection mới qua Console. Trong API/CLI, bạn chỉ định --generation NEXTGEN (hoặc --generation CLASSIC để giữ kiến trúc cũ).

## Các vấn đề với Kiến trúc Classic
Kiến trúc Serverless ban đầu luôn duy trì tối thiểu hai OpenSearch Compute Units (OCUs) chạy mọi lúc. Điều này hợp lý cho một công cụ tìm kiếm môi trường sản xuất (production) có lượng truy cập ổn định, nhưng lại lãng phí đối với các khối lượng công việc dạng agent:
- **Trả phí khi nhàn rỗi:** Tính toán luôn được phân bổ ở mức tối thiểu, vì vậy bạn vẫn bị tính phí ngay cả khi không có truy vấn nào.
- **Tính toán bị ràng buộc với lưu trữ:** Bạn không thể mở rộng quy mô tính toán độc lập mà không ảnh hưởng đến dữ liệu được lưu trữ.
- **Mở rộng quy mô chậm:** Cấp phát tài nguyên mất vài phút, gây khó khăn cho việc bắt kịp với lưu lượng truy cập tăng đột biến trong quy trình làm việc của agent.

## Cách NextGen hoạt động: Phân tách Compute & Storage
Thay đổi cơ bản của NextGen là tách biệt compute khỏi storage. Một lớp lưu trữ dùng chung mới được truy cập bởi cả các OCU lập chỉ mục (indexing) và các OCU tìm kiếm (search), cho phép các OCU mở rộng hoặc thu nhỏ bất kể khối lượng dữ liệu được lưu trữ. Bạn có thể có nhiều chỉ mục chứa dữ liệu mà không phát sinh chi phí tính toán khi không lập chỉ mục hoặc tìm kiếm.

Sơ đồ kiến trúc bên dưới minh họa cách NextGen phục vụ một AI agent: agent tạo các embedding thông qua Bedrock và ghi vào Indexing OCU; các truy vấn vector đi qua Search OCU. Cả Indexing OCU và Search OCU (lớp tính toán) mở rộng độc lập và chia sẻ một Lớp Lưu trữ Dùng chung (Shared Storage Layer) riêng biệt, cho phép scale-to-zero khi nhàn rỗi.

## Các điểm nổi bật & Lợi ích cốt lõi
- **Scale-to-zero thực sự:** Khi không có yêu cầu nào được gửi đến trong khoảng thời gian nhàn rỗi (10 phút), dịch vụ sẽ giải phóng compute và giảm OCU về 0 — việc tính phí tính toán sẽ dừng lại. Khi có lưu lượng truy cập trở lại, dung lượng sẽ khôi phục trong khoảng 10 giây.
- **Mở rộng quy mô nhanh hơn 20 lần:** Tài nguyên được tạo trong vài giây và dung lượng mở rộng nhanh hơn 20 lần so với thế hệ trước, xử lý được cả những quy trình làm việc bất định nhất của agent.
- **Tiết kiệm chi phí lên đến 60%:** Đối với các khối lượng công việc có thời gian nhàn rỗi lớn, kiến trúc mới giúp giảm chi phí hạ tầng lên tới 60% so với việc dự phòng cho mức tải đỉnh.
- **Tích hợp sẵn cho AI (AI-native integration):** Tích hợp sẵn với các nền tảng phát triển AI như Vercel và Kiro; một phần của OpenSearch Agent Skills để sử dụng trực tiếp trong Claude Code, Cursor, Codex thông qua các câu lệnh ngôn ngữ tự nhiên.

## Các trường hợp sử dụng lý tưởng
- **Vector backend cho AI agents:** Lưu trữ và truy vấn các vector embedding cho RAG và tìm kiếm ngữ nghĩa, chỉ trả phí khi agent thực sự thực hiện truy vấn.
- **Tìm kiếm ngữ nghĩa (Semantic Search):** Duy trì các chỉ mục vector cho các truy vấn ngôn ngữ tự nhiên thay vì tự vận hành Cơ sở dữ liệu Vector riêng.
- **Khối lượng công việc bất định (Unpredictable workloads):** Ví dụ, một nền tảng thương mại điện tử có lưu lượng truy cập tăng gấp 10 lần trong các đợt flash sale rồi giảm về 0 — mở rộng quy mô tức thì mà không cần dự phòng trước cho mức đỉnh.
- **Môi trường phát triển/thử nghiệm (Dev/test environments):** Tính năng Express Create giúp nhanh chóng xây dựng một collection với các policy mặc định, hữu ích cho việc thử nghiệm (môi trường sản xuất nên cấu hình mã hóa, mạng và quyền truy cập dữ liệu một cách có chủ đích).

## Trạng thái phát hành
Thế hệ mới của OpenSearch Serverless đã được công bố vào ngày 28 tháng 5 năm 2026 và đã khả dụng rộng rãi (GA). Tại thời điểm ra mắt, hai loại collection được hỗ trợ: tìm kiếm toàn văn (full-text search) và tìm kiếm vector (vector search). Các collection có thể được tạo qua Console, AWS SDK và AWS CLI; hỗ trợ AWS CloudFormation sẽ sớm được cập nhật. Lưu ý: 'lưu trữ dùng chung' vẫn phát sinh phí lưu trữ hàng tháng (GB-month) ngay cả khi compute ở mức 0, vì vậy các con số 20 lần và 60% là có điều kiện, gắn liền với các mốc cơ sở cụ thể và các khối lượng công việc có thời gian nhàn rỗi đáng kể.

![Release Status](/images/3-BlogsPosted/release_status.png)

## Kết luận
OpenSearch Serverless NextGen giải quyết trực tiếp thách thức về chi phí trong kỷ nguyên AI agent: lưu lượng truy cập đột biến rồi im lặng. Bằng cách tách biệt tính toán và lưu trữ để hỗ trợ scale-to-zero, nó cho phép triển khai các backend tìm kiếm và vector sẵn sàng cho production trong vài phút, chỉ trả phí cho lượng sử dụng thực tế. Đây là sự lựa chọn hoàn toàn phù hợp cho các kiến trúc RAG và tìm kiếm ngữ nghĩa mà không cần vận hành một Cơ sở dữ liệu Vector riêng biệt.

## Tài liệu tham khảo
Introducing the next generation of Amazon OpenSearch Serverless

The next generation of Amazon OpenSearch Serverless built from the ground up for agents

Amazon OpenSearch Serverless next generation generally available

Amazon OpenSearch Service pricing