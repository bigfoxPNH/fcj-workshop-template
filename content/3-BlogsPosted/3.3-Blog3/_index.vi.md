---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# XÂY DỰNG CÁC QUY TRÌNH LÀM VIỆC NHIỀU BƯỚC ĐÁNG TIN CẬY VỚI AWS LAMBDA DURABLE FUNCTIONS

## Durable Functions là gì?
Durable Functions là các hàm Lambda thông thường được kích hoạt tính năng "durable execution" (thực thi bền bỉ). Tính năng này mở rộng mô hình lập trình của Lambda với hai tính năng nguyên bản mới — "steps" (các bước) và "waits" (chờ đợi) — cho phép tự động lưu điểm kiểm tra (checkpointing), khôi phục sau lỗi và tạm dừng thực thi tối đa một năm mà không phát sinh chi phí tính toán trong thời gian nhàn rỗi. Bạn không cần quản lý thêm cơ sở hạ tầng hoặc viết mã quản lý trạng thái và xử lý lỗi tùy chỉnh.

Cơ chế kỹ thuật cốt lõi là checkpoint và replay (lưu điểm kiểm tra và phát lại): khi xảy ra lỗi, Lambda sẽ chạy lại hàm từ đầu nhưng bỏ qua các bước đã hoàn thành (đã có checkpoint) và tái sử dụng kết quả đã lưu, đảm bảo không bị mất tiến trình.

## Các vấn đề với Lambda truyền thống
Với Lambda tiêu chuẩn, mã của bạn chạy từ đầu đến cuối trong một lượt thực thi duy nhất và hoàn toàn không lưu trạng thái (stateless). Điều này tạo ra ba hạn chế lớn khi xây dựng các quy trình làm việc phức tạp:
- **Mất trạng thái khi gặp lỗi:** Nếu xảy ra lỗi ở bất kỳ bước nào, toàn bộ hàm phải chạy lại từ đầu; tất cả trạng thái phải được lưu thủ công vào DynamoDB hoặc S3.
- **Giới hạn thời gian:** Một lần thực thi bị giới hạn tối đa 15 phút, không phù hợp cho các tiến trình chạy lâu dài hoặc các tiến trình yêu cầu phê duyệt từ con người.
- **Xử lý tính không đổi (idempotency) thủ công:** Các nhà phát triển phải tự bảo vệ chống lại các lượt thực thi trùng lặp và tự xây dựng các chiến lược triển khai an sau.

## Cách hoạt động: Checkpoint & Replay
Durable Functions giải quyết các vấn đề này bằng hai tính năng nguyên bản cốt lõi trong bộ Durable Execution SDK mã nguồn mở:
- **Step – context.step():** Bao bọc một khối logic nghiệp vụ để tự động lưu checkpoint và thử lại. Một khi bước đó hoàn thành, nó sẽ được bỏ qua trong các lượt phát lại (replays) tiếp theo.
- **Wait – context.wait() / callback:** Tạm dừng thực thi trong một khoảng thời gian hoặc cho đến khi nhận được tín hiệu từ bên ngoài (ví dụ: sự phê duyệt của con người). Trong thời gian chờ, hàm được tạm dừng và không phát sinh phí tính toán, sau đó tự động tiếp tục chạy.

Sơ đồ kiến trúc bên dưới minh họa một quy trình làm việc AI sử dụng Durable Functions: client gọi qua API Gateway đến một hàm Lambda (được bật durable execution); hàm sử dụng step() để gọi Bedrock (LLM) và lưu kết quả vào DynamoDB — mỗi bước đều được tự động lưu checkpoint; sử dụng wait() / callback để tạm dừng chờ con người phê duyệt rồi tiếp tục; trạng thái thực thi được gửi đến EventBridge và CloudWatch để giám sát.

## Các điểm nổi bật & Lợi ích cốt lõi
- **Khả năng chịu lỗi tự động:** SDK tự động xử lý lưu checkpoint, thử lại với cấu hình trì hoãn (backoff) tùy chọn và đảm bảo tính không đổi (chỉ một lần thực thi cho mỗi yêu cầu ngay cả khi có lượt thử lại từ thượng nguồn).
- **Tạm dừng tối đa một năm:** Lý tưởng cho các quy trình làm việc có sự tham gia của con người (human-in-the-loop), quy trình phê duyệt hoặc xử lý theo lịch trình — không tính phí tính toán khi nhàn rỗi.
- **Trải nghiệm Lambda quen thuộc:** Vẫn là một hàm Lambda với cùng một bộ xử lý sự kiện (event handler) và các tích hợp; chỉ cần bật tùy chọn "durable execution" khi tạo hàm.
- **Hỗ trợ đa ngôn ngữ:** SDK hỗ trợ JavaScript, TypeScript, Python và Java (Java đang trong bản Developer Preview, tương thích với Java 17+).

## Các trường hợp sử dụng lý tưởng
- **Quy trình làm việc AI nhiều bước (Multi-step AI workflows):** Điều phối các chuỗi gọi LLM, gọi công cụ và xử lý kết quả một cách an toàn ngay cả khi một cuộc gọi bị lỗi.
- **Xử lý đơn hàng & thanh toán:** Duy trì trạng thái giao dịch qua các lỗi với tính năng tự động thử lại; điều phối xác thực, kiểm tra gian lận và thanh toán qua nhiều nhà cung cấp.
- **Phê duyệt có sự tham gia của con người (Human-in-the-loop approvals):** Xem xét tài liệu, phê duyệt yêu cầu nghỉ phép — tạm dừng chờ quyết định của con người trước khi tiếp tục.
- **Tác vụ theo lịch trình / chạy lâu dài:** Quy trình tiếp nhận (onboarding) nhiều ngày, dùng thử gói đăng ký, thông báo trễ, xử lý hàng loạt theo khung thời gian.

## Ví dụ mã nguồn (Python)
Sau khi bật durable execution và thêm SDK, sử dụng `DurableContext` để bao bọc từng bước nghiệp vụ. Khái niệm cốt lõi là `context.step()` và `context.wait()`:

```python
def handler(event, context):
    # Step 1: call LLM - automatically checkpointed
    summary = context.step("summarize", lambda: call_llm(event))

    # Step 2: wait for human approval (free compute while waiting)
    decision = context.wait_for_callback("approval")

    # Step 3: only runs when approved - skips completed steps on replay
    if decision == "approved":
        context.step("persist", lambda: save_result(summary))
```

## Trạng thái phát hành
Lambda Durable Functions được công bố vào ngày 2 tháng 12 năm 2025 (re:Invent 2025), ban đầu khả dụng rộng rãi (GA) tại vùng US East (Ohio) với các runtime Python (3.13, 3.14) và Node.js (22, 24), sau đó mở rộng ra nhiều vùng khác. Có thể được bật thông qua Console, AWS CLI, SAM, CloudFormation, CDK hoặc SDK. Java SDK đã được ra mắt dưới dạng Developer Preview vào ngày 26 tháng 2 năm 2026.

![Release Status](/images/3-BlogsPosted/release_status_durable.png)

## Kết luận
AWS Lambda Durable Functions xóa nhòa ranh giới giữa sự đơn giản của Lambda và sự phức tạp của các hệ thống điều phối quy trình làm việc. Thay vì lắp ghép Step Functions, SQS và DynamoDB lại với nhau, bạn viết logic tuần tự trong một hàm duy nhất và để SDK lý thuyết việc lưu checkpoint, thử lại và tạm dừng. Đây là lựa chọn lý tưởng cho các quy trình làm việc AI nhiều bước, xử lý đơn hàng và quy trình phê duyệt có sự tham gia của con người.

## Tài liệu tham khảo
Build multi-step applications and AI workflows with AWS Lambda Durable Functions

Building fault-tolerant long-running applications with AWS Lambda Durable Functions

AWS Lambda Durable Functions

Lambda durable multi-step applications and AI workflows

Durable Execution SDK documentation