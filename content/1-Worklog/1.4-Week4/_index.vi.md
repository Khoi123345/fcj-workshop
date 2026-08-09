---
title: "Nhật ký công việc Tuần 4"
date: 2026-07-13
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu Tuần 4:

* Tìm hiểu lập trình Backend Serverless với .NET 8 trên dịch vụ AWS Lambda.
* Nghiên cứu dịch vụ Amazon Bedrock Runtime API và kỹ thuật viết Prompt cho mô hình Claude LLM.
* Viết thử nghiệm hàm .NET 8 Lambda thực hiện gọi API Amazon Bedrock sinh nội dung tự động.
* Đánh giá chất lượng sinh câu chuyện phiêu lưu và các lựa chọn rẽ nhánh cho game RPG.

### Nhiệm vụ thực hiện trong tuần:

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ 2 | - Tìm hiểu kiến trúc AWS Lambda cho runtime C# .NET 8 <br> - Đọc tài liệu `Amazon.Lambda.Core` & `Amazon.Lambda.APIGatewayEvents` | 13/07/2026 | 13/07/2026 | AWS Lambda C# Docs |
| Thứ 3 | - Nghiên cứu dịch vụ Amazon Bedrock và các mô hình ngôn ngữ lớn Claude LLM <br> - Tìm hiểu quyền IAM `bedrock:InvokeModel` cần thiết để gọi Bedrock | 14/07/2026 | 14/07/2026 | Amazon Bedrock Developer Guide |
| Thứ 4 | - Cài đặt thư viện `AWSSDK.BedrockRuntime` vào dự án .NET 8 Backend <br> - Thiết kế mẫu Prompt chuẩn để sinh ra ngữ cảnh ngục tối và 3 lựa chọn hành động | 15/07/2026 | 15/07/2026 | AWS SDK for .NET Docs |
| Thứ 5 | - Lập trình Service gọi Bedrock Runtime API trong C# <br> - Viết bộ parse đọc kết quả JSON từ AI thành đối tượng `StoryNodeResponse` DTO | 16/07/2026 | 16/07/2026 | Prompt Engineering Best Practices |
| Thứ 6 | - Chạy thử nghiệm hàm Lambda local gọi thành công Bedrock API <br> - Kiểm tra độ chuẩn xác của dữ liệu sinh ra đảm bảo không bị lỗi cấu trúc | 17/07/2026 | 17/07/2026 | AWS Mock Testing |

### Kết quả đạt được Tuần 4:

* Hiểu rõ cách thức hoạt động của Serverless .NET 8 trên AWS Lambda.
* Kết nối thành công dịch vụ Amazon Bedrock Runtime API từ ứng dụng C#.
* Tạo được các mẫu Prompt AI chất lượng, sinh ra kịch bản phiêu lưu RPG hấp dẫn kèm lựa chọn cho người chơi.
