---
title: "FCAJ - Agentic AI Build Week"
date: 2026-07-25
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài thu hoạch: "FCAJ - Agentic AI Build Week & Agent Forge"

### Mục Đích Của Sự Kiện

- Hiểu rõ sự dịch chuyển từ việc hỏi - đáp LLM đơn thuần sang hệ thống Agentic AI có tính tự chủ (`Tự lập luận → Lập kế hoạch → Thực thi`).
- Nắm vững 5 thành phần kiến trúc Production của một AI Agent trên AWS Cloud: Bộ não (LLM), System Prompt, Bộ nhớ & Ngữ cảnh, Công cụ (Tools) và Giám sát (Observability).
- Tìm hiểu các giao thức kết nối hiện đại (Model Context Protocol - MCP và Agent-to-Agent - A2A) giúp chuẩn hóa việc giao tiếp giữa Agent với các công cụ và các Agent khác.
- Đi sâu vào hạ tầng Amazon Bedrock Agent Core với các tính năng bảo mật doanh nghiệp: cách ly Firecracker MicroVM, Workload Access Token (WAT) và Cổng kiểm soát Human-in-the-Loop (HITL).
- Thực hành phương pháp Vibe Coding trên Kiro IDE cấu hình Steering Rules và triển khai AI Agent lên Cloud qua bộ lệnh `agentcore CLI`.

### Danh Sách Diễn Giả

- **Anh Nghĩa** – Diễn giả chính (Phụ trách phần Lý thuyết Kiến trúc L300 & Agent Core Topology)
- **Anh Hải Anh** – Diễn giả thực hành (Phụ trách phần Demo Vibe Coding với Kiro IDE & AgentCore CLI)
- **AWS Study Group** – Đơn vị tổ chức (Host)

---

### Nội Dung Nổi Bật

#### 1. Triết lý Agentic AI & Dải mức độ tự chủ (anh Nghĩa)
- **Vượt xa LLM truyền thống:** Khác với các mô hình LLM thông thường chỉ dự đoán từ tiếp theo, Agentic AI là lớp phần mềm có khả năng tự chủ vận hành theo chu trình: **Tự lập luận → Lập kế hoạch → Thực thi tác vụ**.
- **Dải mức độ tự chủ (Spectrum of Autonomy):** Phân loại thành dải 4 cấp độ:
  - *Simple Assistant:* Giao diện hỏi - đáp 1 lượt cơ bản.
  - *Deterministic Workflow:* Luồng công việc cố định do lập trình viên định nghĩa có sự giám sát của con người.
  - *Human-in-the-Loop Workflow:* Agent tự chủ lập kế hoạch nhưng các hành động quan trọng bắt buộc có sự phê duyệt của con người.
  - *Fully Autonomous Multi-Agent Systems:* Các Agent chuyên biệt tự phối hợp và xử lý các tác vụ ngầm kéo dài.

#### 2. Kiến trúc 5 lớp Production của một AI Agent (anh Nghĩa)
- **Bóc tách thành phần Agent:** Để xây dựng một AI Agent vững chắc trên Production, hệ thống cần bóc tách rõ ràng 5 yếu tố:
  1. *Bộ não (Brain / LLM):* Các mô hình ngôn ngữ lớn như Anthropic Claude 3.5 Sonnet, Claude 3 Haiku hoặc Amazon Nova.
  2. *System Prompt & Steering Rules:* Định hình nhân dạng, giới hạn vai trò và cấu trúc dữ liệu đầu ra.
  3. *Bộ nhớ & Ngữ cảnh (Knowledge Base / Context):* Tích hợp dữ liệu nội bộ qua RAG và CSDL Vector (như OpenSearch Serverless).
  4. *Công cụ thực thi (Tools & Action Invocation):* Kết nối với bên ngoài (truy vấn SQL, gọi REST Webhook, Gmail API).
  5. *Giám sát & Lưu vết (Memory & Observability):* Lưu giữ ngữ cảnh bộ nhớ và theo dõi nhật ký hoạt động trên Amazon CloudWatch.

#### 3. Giao thức kết nối thế hệ mới (MCP & A2A) & Framework AWS Strands (anh Nghĩa)
- **Model Context Protocol (MCP):** Giao thức chuẩn hóa mới thay thế REST API cho việc kết nối giữa AI Agent và các công cụ/plugin bên ngoài.
- **Agent-to-Agent (A2A) Protocol:** Chuẩn giao tiếp cho phép các Agent chuyên biệt tự trao đổi dữ liệu và phân công nhiệm vụ trực tiếp cho nhau.
- **AWS Strands SDK & Factory Pattern:** Áp dụng bộ Open-source Strands SDK và Factory Design Pattern để khởi tạo Agent gọn gàng (`Agent = Model + System Prompt + Tools`).

#### 4. Hạ tầng Amazon Bedrock Agent Core & Bảo mật Enterprise (anh Nghĩa)
- **Công nghệ cách ly Firecracker MicroVM:** Bedrock Agent Core vận hành mỗi phiên làm việc của người dùng trên một Firecracker MicroVM riêng biệt, đảm bảo cách ly tuyệt đối và 100% không rò rỉ dữ liệu giữa các phiên (Zero Tenant Leakage).
- **Luồng bảo mật 5 bước với Workload Access Token (WAT):**
  1. *Yêu cầu đầu vào:* Client gửi request kèm JWT Token hoặc Cognito Credential.
  2. *Đổi Token:* Agent Core chuyển đổi JWT của User thành Workload Access Token (WAT).
  3. *Ủy quyền công cụ:* WAT được đổi sang Token tương ứng của Tool lưu trong kho khóa mã hóa Token Vault.
  4. *Thực thi an toàn:* Tool thực thi mà không bao giờ làm lộ JWT gốc của người dùng.
  5. *Trả kết quả:* Trả dữ liệu đã qua bộ lọc về cho Client.
- **Enterprise Gateway & HITL:** Đóng vai trò lớp Middleware trung gian. Ví dụ: yêu cầu hoàn tiền dưới 100$ được Agent tự động xử lý, nhưng trên 100$ sẽ kích hoạt luồng chuyển quản trị viên phê duyệt.

#### 5. Thực hành Vibe Coding với Kiro IDE & agentcore CLI (anh Hải Anh)
- **Kiro IDE & Steering Rules:** Cấu hình file quy tắc `.kiro/steering.md` để định hướng AI trợ lý trong Kiro IDE tự động sinh code C# và Python tuân thủ chuẩn kiến trúc AWS Strands SDK.
- **Quy trình 3 lệnh triển khai siêu tốc:**
  1. `agentcore init my-first-agent` — Tự động khởi tạo cấu trúc thư mục chuẩn (`agent.py`, `config.yaml`, `requirements.txt`).
  2. `agentcore configure --model anthropic.claude-3-5-sonnet` — Liên kết bộ não LLM và thiết lập System Prompt.
  3. `agentcore deploy --env dev` — Đóng gói và đưa Agent lên môi trường Firecracker MicroVM của Bedrock Agent Core chỉ trong vài giây.

---

### Những Gì Học Được

#### Tư duy thiết kế
- **Vòng lặp Agentic tự chủ:** Chuyển đổi tư duy từ tương tác hỏi - đáp tĩnh sang xây dựng luồng vận hành tự chủ: Tự lập luận → Lập kế hoạch → Thực thi.
- **Bảo mật cách ly phiên:** Tận dụng hạ tầng Firecracker MicroVM để tạo môi trường tính toán riêng biệt cho từng người dùng, ngăn chặn rò rỉ dữ liệu.
- **Quản trị Human-in-the-Loop:** Thiết lập các chính sách phê duyệt của con người tại lớp Gateway đối với các hành động tài chính hoặc hạ tầng rủi ro cao.

#### Kiến trúc kỹ thuật
- **Chuẩn hóa Giao thức AI:** Nắm vững giao thức MCP và A2A để kết nối linh hoạt các công cụ và điều phối các Agent đa nhiệm.
- **Bảo mật định danh WAT:** Bảo vệ thông tin đăng nhập của người dùng khi ủy quyền cho Agent gọi dịch vụ bên ngoài thông qua Workload Access Token (WAT).
- **Mô hình Agent Factory:** Áp dụng Factory Design Pattern để đóng gói Mô hình LLM, System Prompt và Tools thành các module độc lập.

#### Chiến lược tích hợp AI
- **Phương pháp Vibe Coding:** Sử dụng file Steering Rules (`.kiro/steering.md`) để định hướng trợ lý AI lập trình theo đúng chuẩn kiến trúc Cloud.
- **Triển khai Serverless siêu tốc:** Tận dụng bộ công cụ CLI (`agentcore CLI`) để quản lý và triển khai hạ tầng Agent nhanh chóng.

---

### Ứng Dụng Vào Công Việc

- **Tích hợp Bedrock Story Service:** Sử dụng API Amazon Bedrock Runtime trong Backend .NET 8 AWS Lambda để sinh kịch bản phiêu lưu ngẫu nhiên cho game.
- **Ràng buộc cấu trúc đầu ra:** Áp dụng quy tắc Steering trên System Prompt để ép AI trả về dữ liệu JSON chuẩn, phục vụ deserialize mượt mà sang C# DTOs.
- **Xử lý gọi API bất đồng bộ:** Sử dụng async/await trong `ApiClient` của Unity để xử lý dữ liệu AI sinh ra mà không gây đơ giao diện game.
- **Thiết lập bộ đệm Timeout:** Cấu hình cơ chế fallback và xử lý timeout 5 giây khi gọi dịch vụ AI để đảm bảo trải nghiệm chơi game liên tục.
- **Chuẩn hóa quy trình viết code:** Sử dụng Steering Rules trong IDE để đồng bộ phong cách viết code và cấu trúc dự án trong Monorepo C#.

---

### Trải nghiệm trong event

Tham gia sự kiện **FCAJ - Agentic AI Build Week & Agent Forge** đã mang lại cho tôi những kiến thức chuyên môn vô cùng thực tế và giá trị về việc đưa AI Agent lên môi trường Production.

- **Bài giảng L300 chuyên sâu:** Phần trình bày của anh Nghĩa về Bedrock Agent Core, Firecracker MicroVM và bảo mật WAT giúp tôi giải tỏa nhiều thắc mắc về an toàn dữ liệu AI.
- **Thực hành Vibe Coding trực quan:** Phần demo của anh Hải Anh với Kiro IDE và `agentcore CLI` cho thấy tốc độ xây dựng và triển khai một AI Agent Serverless mượt mà như thế nào.
- **Giá trị trực tiếp cho đồ án:** Kiến thức về định dạng Prompt và tích hợp Bedrock API đã giúp tôi hoàn thiện kiến trúc cho dự án **AI Dungeon RPG**.
- **Môi trường giao lưu cởi mở:** Buổi sự kiện là cơ hội tuyệt vời để kết nối với các Cloud Architect, kỹ sư AI và các bạn học viên trong cộng đồng AWS.

#### Một số hình ảnh khi tham gia sự kiện

![FCAJ Agentic AI Build Week](hinh-anh-sk-3/event3.png)


> Sự kiện FCAJ Agentic AI Build Week & Agent Forge là một cột mốc học hỏi quan trọng trong kỳ thực tập, trang bị cho tôi tư duy thiết kế kiến trúc chuẩn Production và các công cụ hiện đại để xây dựng các ứng dụng AI Agent vững chắc trên AWS Cloud.
