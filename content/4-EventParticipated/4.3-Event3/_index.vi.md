---
title: "FCAJ - Agentic AI Build Week & Agent Forge"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài thu hoạch: "AWS FCAJ Agent Forge & Agentic AI Build Week"

### Tổng quan sự kiện

Ngày **01/08/2026**, em đã tham gia sự kiện chuyên đề **AWS FCAJ Agent Forge - Deepdive** do cộng đồng AWS Study Group tổ chức tại Tầng 26, Tòa nhà Bitexco (TP.HCM). Sự kiện tập trung vào các kiến trúc **Agentic AI cấp độ L300 (Advanced Level)**, giúp chuẩn hóa quy trình đưa các ứng dụng Generative AI từ dạng mô hình thử nghiệm (PoC) lên môi trường Production thực tế trên điện toán đám mây AWS.

Buổi chia sẻ đã thu hút đông đảo các Cloud Architect, AI Engineer và bạn trẻ yêu công nghệ cùng mổ xẻ 4 rào cản lớn nhất của doanh nghiệp hiện nay: **Hiệu năng (Performance), Khả năng mở rộng (Scalability), Bảo mật (Security) và Quản trị (Governance)**.

---

### Nội dung kỹ thuật trọng tâm

#### 1. Triết lý Agentic AI & Dải mức độ tự chủ
* **Vượt xa LLM truyền thống:** Thay vì chỉ dự đoán từ tiếp theo như các Chatbot thông thường, Agentic AI là thế hệ phần mềm có khả năng tự chủ lập luận, lập kế hoạch nhiều bước và chủ động gọi công cụ để thực thi tác vụ (`Reasoning → Planning → Execution`).
* **Dải mức độ tự chủ:** Đi từ trợ lý phản hồi đơn giản (Simple Assistant) đến các hệ thống Đa-Agent tự vận hành các tác vụ chạy ngầm kéo dài (Long-running background jobs).

#### 2. Kiến trúc 5 thành phần cốt lõi của AI Agent
* **Bộ não (Brain / LLM):** Sử dụng các mô hình ngôn ngữ tiên tiến như Anthropic Claude (Sonnet/Haiku) hoặc Amazon Nova để xử lý lập luận và viết code.
* **System Prompt & Quy tắc nhân dạng:** Định hình vai trò, phạm vi quyền hạn và giới hạn hành vi cho Agent.
* **Bộ nhớ & Ngữ cảnh (Knowledge & Context):** Kết nối dữ liệu nội bộ thông qua RAG và CSDL Vector.
* **Công cụ thực thi (Tools / Actions):** Cho phép Agent tương tác với bên ngoài (Gửi Email, truy vấn Database, gọi Webhook API).
* **Giám sát & Lưu trữ (Memory & Observability):** Lưu trữ ngữ cảnh phiên làm việc và theo dõi nhật ký hoạt động qua Amazon CloudWatch.

#### 3. Chuẩn hóa giao thức mới (MCP & A2A)
* **Model Context Protocol (MCP):** Giao thức chuẩn hóa giúp Agent giao tiếp và sử dụng các công cụ/plugin bên ngoài một cách nhất quán.
* **Agent-to-Agent (A2A) Protocol:** Giao thức cho phép các Agent tự trao đổi thông tin và phân chia công việc trực tiếp cho nhau.
* **AWS Strands SDK & Design Pattern:** Áp dụng **Factory Design Pattern** để đóng gói và khởi tạo Agent gọn gàng (`Model + System Prompt + Tools`).

#### 4. Hạ tầng Amazon Bedrock Agent Core & Bảo mật
* **Công nghệ cách ly Firecracker MicroVM:** Mỗi phiên làm việc của người dùng chạy trên một MicroVM độc lập hoàn toàn, đảm bảo không rò rỉ dữ liệu giữa các phiên (User Isolation).
* **Xác thực Workload Access Token (WAT):** Cơ chế chuyển đổi Token thông minh giúp bảo mật thông tin đăng nhập của người dùng khi Agent gọi API bên ngoài.
* **Enterprise Gateway & Human-in-the-Loop (HITL):** Lớp trung gian cho phép quản trị viên phê duyệt các hành động quan trọng trước khi Agent thực thi.

#### 5. Thực hành Vibe Coding & AgentCore CLI
* **Kiro IDE Steering Rules:** Cấu hình file `.kiro/steering.md` để định hướng AI trợ lý viết code C# và Python tuân thủ chuẩn kiến trúc Cloud của AWS.
* **Bộ 3 lệnh thần tốc với `agentcore CLI`:**
  1. `agentcore init my-agent` — Khởi tạo cấu trúc dự án chuẩn.
  2. `agentcore configure` — Cấu hình mô hình LLM và System Prompt.
  3. `agentcore deploy` — Triển khai nhanh chóng lên môi trường Serverless của AWS.

---

### Bài học cá nhân & Ứng dụng vào đồ án thực tập

Việc tham gia sự kiện mang lại giá trị rất lớn cho dự án **AI Dungeon RPG Adventure Game** mà em đang thực hiện:

* **Tích hợp sinh cốt truyện AI:** Áp dụng tư duy thiết kế Prompt và gọi API Bedrock Runtime để tạo ra các kịch bản phiêu lưu ngẫu nhiên cho Backend game.
* **Parse dữ liệu cấu trúc:** Hiểu cách ràng buộc dữ liệu đầu ra từ AI thành cấu trúc JSON chuẩn để parse trực tiếp về các DTOs C# trong dự án Unity.
* **Tư duy bảo mật & Xử lý lỗi:** Nắm rõ cách quản lý quyền truy cập API key và xử lý trường hợp timeout mượt mà khi gọi các mô hình AI.

#### Hình ảnh kỷ niệm tại sự kiện

![AWS FCAJ Agent Forge Event](hinh-anh-sk-3/IMG_20260801_091335.webp)
![Thực hành Vibe Coding](hinh-anh-sk-3/IMG_20260801_102453.webp)
![Giao lưu cộng đồng AWS](hinh-anh-sk-3/IMG_20260801_110623.webp)

> **Tổng kết:**
> Sự kiện AWS FCAJ Agent Forge đã mang đến cho em tư duy thiết kế kiến trúc AI Agent chuẩn Production. Đây là một trải nghiệm học hỏi tuyệt vời, giúp em tự tin hơn trong việc áp dụng công nghệ Cloud-native AI vào đồ án thực tập của mình!
