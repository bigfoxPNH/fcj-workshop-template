---
title: "Event 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# BÀI THU HOẠCH: BÀI BÁO CÁO SỰ KIỆN 2

### Mục Tiêu Sự Kiện

* Phát triển tư duy xây dựng các sản phẩm thực tế.
* Chia sẻ kinh nghiệm thực tế từ các cuộc thi Hackathon.
* Nâng cao nhận thức về an toàn thông tin và tính tuân thủ.
* Tối ưu hóa chi phí vận hành hạ tầng và hệ thống Cloud.
* Khuyến khích giao tiếp tự tin và tư duy phản biện.
* Hiểu rõ bản chất của công nghệ để thiết kế các hệ thống bền vững.

### Danh Sách Diễn Giả

* **Mr. Tính Trương** - Platform Engineer at GoTyme
* **Mr. Phạm Nguyễn Hải Anh** - G-AsiaPacific Vietnam, AWS Community Builder
* **Mr. Thịnh** - DevOps/Cloud Engineer at FCAJ
* **UTMorpho** - LotusHacks 2026 Team
* **Mr. Đức Đào** - Solution Architect at Kinetics
* **Ms. Cát Vy** - Senior Business Systems Analyst at VPBank

### Nội Dung Nổi Bật

#### Xu Hướng Thị Trường Lao Động & Yêu Cầu Mới Đối Với Nhân Sự IT
* **Thực tế giai đoạn chuyển giao:** Cuộc đua đầu tư hạ tầng AI toàn cầu giữa các gã khổng lồ công nghệ tạo ra áp lực tối ưu hóa chi phí trong ngắn hạn, khiến thị trường việc làm (đặc biệt là các vị trí Thực tập sinh/Fresher) trở nên cạnh tranh hơn bao giờ hết (tỷ lệ chọi thực tế tại các doanh nghiệp có thể lên tới 1:50).
* **Làn sóng việc làm mới:** Sự bùng nổ của AI làm giảm chi phí tạo ra phần mềm, dẫn đến nhu cầu tăng vọt về bảo trì, vận hành và mở rộng hệ thống. Các vai trò mới như Platform Engineering (Kỹ thuật nền tảng) và Off-Platform Engineering xuất hiện để xử lý các hệ thống doanh nghiệp.
* **3 vũ khí bắt buộc phải trang bị:**
  * **Nền tảng kỹ thuật vững chắc:** Bằng đại học vẫn là một 必要条件 (điều kiện cần thiết - bộ lọc CV) đối với các tổ chức lớn.
  * **Kiến thức chuyên môn thực tế (Domain/Case study):** Phải hiểu mô hình vận hành của ngành mục tiêu (ví dụ: Tài chính - Ngân hàng).
  * **Sản phẩm thực tế (Tư duy sản phẩm):** Thay vì chỉ các bài tập demo, ứng viên phải sở hữu các sản phẩm thực tế để thuyết phục nhà tuyển dụng.

#### Làm Chủ Bối Cảnh Trong Giao Tiếp AI
* **Vấn đề "Internet Buffet":** Thói quen thu thập mọi prompt, plugin và quy tắc template từ internet rồi sử dụng tất cả chúng trong một phiên chat làm loãng bối cảnh của AI, gây ra việc chuyển đổi bối cảnh liên tục dẫn đến sự nhầm lẫn và mã nguồn nhiều lỗi.
* **Xây dựng bối cảnh đúng và đủ:** Khi viết prompt cho AI, hãy cung cấp rõ ràng: Mục tiêu (Goal), Cấp độ vai trò/Hình mẫu (Role/Persona level), Định dạng mong muốn (Desired Format), và đặc biệt chỉ bao gồm các tài liệu/quy tắc cụ thể của dự án/doanh nghiệp (kiến thức chung AI đã có sẵn).
* **Bản chất của Temperature = 0:** Khi giảm temperature xuống 0, LLM sẽ chuyển sang Greedy Decoding (Giải mã tham lam - Argmax) — luôn chọn token có xác suất cao nhất. Tuy nhiên, do các kỹ thuật làm tròn thập phân của GPU và gom cụm prompt để tối ưu hóa chi phí của các nhà cung cấp API (Tối ưu hóa suy luận), kết quả giữa các lần chạy vẫn có thể khác nhau (Tính ngẫu nhiên).
* **Chiến lược giảm thiểu:** Đối với các hệ thống Production ổn định, hãy bao bọc các dịch vụ hạ nguồn để xử lý các lỗi định dạng, cân nhắc tự host các mô hình cục bộ để kiểm soát toàn bộ, hoặc sử dụng cơ chế multi-Agent song song để bỏ phiếu cho kết quả có sự đồng thuận cao nhất.

#### Kinh Nghiệm Phát Triển Sản Phẩm AI Thực Tế (Case Study Hackathon)
* **Dự án "UTMorpho" (Giải nhất Hackathon):** Minh chứng thực tế về việc xây dựng ứng dụng AI Editor tự động tạo giao diện người dùng và cho phép chỉnh sửa kéo thả trực tiếp trên giao diện đó từ các bản phác thảo hoặc hình ảnh trong vòng 36 giờ.
* **Kiến trúc Multi-Agent cộng tác:** Dự án sử dụng cấu trúc phân tầng gồm 3 Agent chuyên biệt:
  * **Agent 1 (Vision Agent):** Đọc và phân tích các hình ảnh đầu vào thành các tệp JSON.
  * **Agent 2 (Layout Agent):** Nhận JSON để tính toán kích thước, bố cục và CSS.
  * **Agent 3 (Design Agent):** Tạo mã nguồn HTML/CSS hoàn chỉnh.
* **Những bài học xương máu từ thực tế:**
  * **Tránh cái bẫy nghĩ quá nhiều/quá nhiều tính năng:** Cắt bỏ các tính năng không cần thiết, chỉ tập trung tối ưu hóa Tính năng Cốt lõi (Core Feature) để kịp tiến độ.
  * **Giải quyết vấn đề của chính bạn:** Những ý tưởng tốt nhất không cần phải vĩ đại — hãy tìm những ý tưởng giải quyết các điểm đau đớn hàng ngày của đội ngũ phát triển.

#### Công Nghệ AI Agent & Ứng Dụng Phân Tích Dữ Liệu
* **Sự tiến hóa từ Chatbot lên Agent:** Không giống như các Chatbot truyền thống chỉ trả lời bằng văn bản, một AI Agent là một bộ não LLM được trang bị "cánh tay nối dài" — các Hành động/Hàm (thông qua các giao thức như MCP) để trực tiếp hành động: lên lịch họp, tạo dashboard, gửi email...
* **Ứng dụng Amazon Q Business / QuickSight (Demo):** Người dùng doanh nghiệp (Quản lý, CEO) không có kỹ năng kỹ thuật chỉ cần tải các tệp dữ liệu Excel thô lên ô chat, và AI Agent sẽ tự động phân tích và xây dựng các biểu đồ trực quan bằng tiếng Việt.
* **Tự động hóa cuộc họp:** Agent có thể tự động ghi chép âm thanh cuộc họp, tóm tắt các quyết định và tự động gửi các Bước tiếp theo (Next Steps) đến email của từng thành viên thông qua Microsoft Teams hoặc Outlook.

#### Mô Hình Giá Mới & Nền Tảng Bảo Mật CloudFront CDN
* **Mô hình giá cố định (Flat-rate Pricing):** AWS ra mắt các gói CDN cố định (Free, Pro, Business, Premium) thay vì mô hình Pay-as-you-go truyền thống. Điều này giải quyết hoàn toàn nỗi sợ "đột biến hóa đơn" khi hệ thống đối mặt với các cuộc tấn công DDoS hoặc lưu lượng truy cập tăng đột biến. Vượt quá giới hạn sẽ chỉ bị giới hạn băng thông mà không phải trả thêm phí.
* **Mạng nội bộ siêu tốc (AWS Backbone):** Với gần 700 PoP được kết nối trực tiếp với các ISP lớn, lưu lượng truy cập từ CDN đến máy chủ gốc (Origin) sẽ đi qua mạng cáp quang nội bộ của AWS, bỏ qua internet công cộng và ngăn ngừa nghẽn mạng khi đứt cáp quang biển.
* **Bảo mật nâng cao tại vùng biên (Edge):**
  * **Chặn các cuộc tấn công DDoS quy mô lớn** tại máy chủ Edge ở quốc gia xuất phát của Botnet, ngăn lưu lượng độc hại tiếp cận máy chủ gốc.
  * **Áp dụng thư viện mã hóa S2N** để chống giải mã bằng máy tính lượng tử và Mutual TLS (mTLS) yêu cầu xác thực chứng chỉ từ cả hai phía (Client & Server), áp dụng mạnh mẽ cho ngành Tài chính.
* **Tính năng VPC Origin:** Tạo một đường hầm ẩn che giấu hoàn toàn máy chủ gốc trong Private Subnet khỏi Internet, chỉ cho phép CloudFront truy cập trực tiếp.

#### Kiến Trúc Multi-Agent Cấp Doanh Nghiệp
* **Bài toán thực tế:** Thiết kế hệ thống Multi-Agent để đánh giá điểm tín dụng cho các doanh nghiệp Khởi nghiệp Việt Nam — những đối tượng thường bị các mô hình ngân hàng truyền thống từ chối do thiếu báo cáo tài chính 3 năm hoặc tài sản thế chấp.
* **Phân rã chuyên môn hóa doanh nghiệp:** Hệ thống được thiết kế như một Hội đồng Tín dụng bao gồm một Host (Điều phối - Orchestrator) điều phối các Sub-Agent chuyên biệt: **Financial Analyst** (xử lý dòng tiền), **Market Analyst** (quét thị phần TAM/SAM/SOM), **Team Evaluator** (quét uy tín của nhà sáng lập trên LinkedIn/Facebook), và **Risk Assessor** (đánh giá rủi ro).
* **Rào cản Bảo mật & Tuân thủ:** Ở các doanh nghiệp lớn, bảo mật luôn đi trước công nghệ. Các công cụ AI không thể được cắm vào một cách tùy tiện do rủi ro rò rỉ dữ liệu (vector tấn công MCP). Mọi quy trình kết quả do AI tạo ra đều phải có sự xem xét của con người (Human-in-the-loop) và dấu vết kiểm toán (Audit trails), vì trước pháp luật, con người chịu trách nhiệm cuối cùng — không phải AI.

#### Một số hình ảnh khi tham gia sự kiện
* Thêm các hình ảnh của các bạn tại đây

![Hình ảnh Sự kiện 2](/images/4-EventParticipated/event2.png?width=30%&classes=shadow) ![Hình ảnh Sự kiện 2.1](/images/4-EventParticipated/event2.1.png?width=30%&classes=shadow) ![Hình ảnh Sự kiện 2.2](/images/4-EventParticipated/event2.2.png?width=30%&classes=shadow)
