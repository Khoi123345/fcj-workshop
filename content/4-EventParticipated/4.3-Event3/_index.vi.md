---
title: "AWS FCAJ Agent Forge - Deepdive"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài thu hoạch: "AWS FCAJ Agent Forge - Deepdive"

### Mục Đích Của Sự Kiện

- Trang bị kiến thức chuyên sâu cấp độ **L300 (Advanced Level)** giúp Kỹ sư AI, Cloud Architect và Developer chuyển đổi các ứng dụng Generative AI từ dạng thử nghiệm (Proof of Concept - PoC) lên môi trường triển khai thực tế (Production-ready).
- Giải quyết 4 rào cản cốt lõi khi đưa AI Agent vào doanh nghiệp: **Performance** (Hiệu năng), **Scalability** (Khả năng mở rộng), **Security** (Bảo mật) và **Governance** (Quản trị).
- Đi sâu vào kiến trúc Agentic AI, hệ sinh thái Amazon Bedrock Agent Core (Runtime, Identity, Gateway) và các giao thức kết nối hiện đại (MCP, A2A).
- Hướng dẫn thực hành phương pháp **Vibe Coding** với **Kiro IDE**, cấu hình Steering Rules và khởi tạo/triển khai con Agent đầu tiên trên môi trường Serverless của AWS chỉ với 3 dòng lệnh `agentcore CLI`.

### Danh Sách Diễn Giả

- **Anh Nghĩa** – Speaker (Phụ trách phần Lý thuyết & Kiến trúc)
- **Hải Anh** – Speaker (Phụ trách phần Thực hành Hands-on Lab)
- **AWS Study Group** – Đơn vị tổ chức (Host)

---

### Nội Dung Nổi Bật

#### 1. Triết lý Agentic AI & Dải Mức độ Tự chủ (Spectrum of Autonomy)
- **Khái niệm Agentic AI:** Khác với mô hình LLM thông thường chỉ dự đoán token tiếp theo, Agentic AI là lớp phần mềm thông minh có tính tự chủ (Autonomous), có khả năng thực hiện chuỗi quy trình: **Lập luận (Reasoning) → Lập kế hoạch (Planning) → Thực thi (Execute)** các tác vụ phức tạp theo nhiều bước.
- **Dải mức độ tự chủ (Spectrum of Autonomy):**
  - *Simple Assistant:* Mô hình hỏi - đáp cơ bản dựa trên LLM.
  - *Deterministic Workflow:* Luồng công việc cố định do lập trình viên định nghĩa, luôn có sự can thiệp và kiểm soát của con người (Human-in-the-loop).
  - *Fully Autonomous Multi-Agent Systems:* Hệ thống các Agent tự liên kết, phân chia nhiệm vụ, tự xử lý các tác vụ tính toán ngầm kéo dài (Long-running background jobs) và tổng hợp kết quả trả về cho người dùng.

#### 2. Cấu trúc Nền tảng của một AI Agent (Basic Agent Architecture)
- **5 Thành phần cốt lõi của Agent trên Production:**
  - **Brain (Bộ não):** Các Large Language Model (LLM) đóng vai trò lập luận. Phổ biến như Anthropic Claude (Haiku tối ưu tốc độ/chi phí, Sonnet cho tác vụ phức tạp, Opus cho lập trình nâng cao), Amazon Nova, hoặc Google Gemini.
  - **System Prompt & Role:** Định hình nhân dạng, nhiệm vụ và thiết lập các giới hạn hành vi cho Agent.
  - **Knowledge Base / Context:** Dữ liệu nội bộ doanh nghiệp kết nối qua RAG, Vector Database hoặc hệ thống File.
  - **Tools / Actions:** Khả năng giao tiếp với thế giới bên ngoài (gửi mail qua Gmail API, truy vấn CSDL, gọi Webhook).
  - **Memory & Observability:** Lưu trữ ngữ cảnh phiên làm việc (Short-term/Long-term Memory) và giám sát trạng thái hoạt động thực tế trên CloudWatch.

#### 3. Giao thức Kết nối Mới & Framework Phát triển
- **Sự chuyển dịch Giao thức (Protocols):**
  - Chuyển từ HTTP REST API truyền thống sang 2 giao thức tiêu chuẩn mới dành riêng cho kỷ nguyên AI Agent:
    - **MCP (Model Context Protocol):** Giao thức chuẩn hóa giúp Agent giao tiếp và gọi các Tool/Plugin bên ngoài.
    - **A2A (Agent-to-Agent):** Giao thức cho phép các Agent trao đổi dữ liệu và phối hợp phân chia công việc trực tiếp với nhau.
- **Framework AWS Strands SDK:** Bộ Open-source SDK do AWS phát triển dành riêng cho việc xây dựng Agent trên AWS Cloud, tối ưu hóa hiệu năng vượt trội so với LangChain hay LangGraph khi chạy trên hạ tầng AWS.
- **Design Pattern:** Sử dụng **Factory Design Pattern** để khởi tạo Agent nhanh chóng bằng cách đóng gói 3 yếu tố: `Model + System Prompt + Tools`.

#### 4. Amazon Bedrock Agent Core - Runtime Environment
- **Serverless Managed Runtime:** Môi trường Managed Serverless giúp triển khai và vận hành Agent an toàn, dễ mở rộng theo mô hình Pay-as-you-go.
- **Công nghệ cách ly Firecracker MicroVM:**
  - Mỗi phiên làm việc (User Session) của Agent chạy trên một MicroVM hoàn toàn độc lập.
  - Tách biệt tuyệt đối về phần cứng (Compute), bộ nhớ (Memory) và hệ thống tệp (File System), đảm bảo không xảy ra rò rỉ dữ liệu giữa các người dùng (User Data Isolation).
- **Phương thức Deploy:** Đóng gói linh hoạt qua Mã nguồn Strands Template, Docker Container Image trên Amazon ECR, hoặc file ZIP nén trên Amazon S3.
- **Tính năng quản lý Endpoint & Strategy:**
  - Thiết lập Endpoint ARN đi kèm quản lý Alias (`default`, `prod`, `v1`, `v2`).
  - Hỗ trợ triển khai **Canary Rollout** (chuyển dần 5% - 10% traffic sang bản mới) và **Rollback** tức thì khi gặp lỗi.
- **Async Jobs & Bidirectional Streaming:**
  - *Async & Long-running Jobs:* Phân tách các tác vụ tìm kiếm/phân tích phức tạp cho các Agent ngầm xử lý ở Background.
  - *Bidirectional Streaming:* Hỗ trợ truyền dữ liệu luồng 2 chiều real-time cho các ứng dụng Đa thức (Multi-modal) bao gồm cả Voice/Audio và Text (như Voice Mode hoặc Google Live API).

#### 5. Lớp Bảo mật & Định danh (Identity Layer)
- **Quản trị Authentication & Authorization Inbound & Outbound:**
  - **Luồng bảo mật 5 bước:**
    1. *Inbound:* Client gửi yêu cầu kèm JWT Token hoặc AWS Cognito Credential.
    2. *Token Exchange:* Agent Core chuyển đổi JWT thành **WAT (Workload Access Token)** - kết hợp quyền hạn của User và Agent để không làm lộ JWT gốc của User.
    3. *Outbound Exchange:* Chuyển đổi WAT sang Credential tương ứng của Tool (OAuth Token, API Key).
    4. *Token Vault:* Lưu trữ các Token trong kho khóa mã hóa an toàn.
    5. *Execution:* Trả kết quả an toàn về cho người dùng.
  - **Hỗ trợ đa dạng chuẩn:** Basic Login, OAuth 2-legged, OAuth 3-legged (SSO) và tích hợp sẵn AWS Cognito.

#### 6. Cổng Kết Nối Doanh Nghiệp (Gateway Layer)
- **Lớp Middleware trung gian:** Giải quyết bài toán quản trị khi mở rộng lên hàng trăm Agent kết nối với hàng nghìn Tool/MCP Server.
- **Các tính năng nổi bật:**
  - **Human-in-the-Loop (HITL):** Cho phép Quản trị viên phê duyệt (Approve) hoặc từ chối (Deny) các hành động vượt ngưỡng Policy (ví dụ: yêu cầu hoàn tiền ≤ 100$ tự động xử lý, >100$ phải chuyển Admin duyệt).
  - **Semantic Tool Search:** Tự động tìm kiếm và định tuyến Agent đến đúng Tool dựa trên Vector Indexing mà không cần Hard-code API.
  - **Interceptors / Hooks:** Bộ lọc an toàn tự động loại bỏ thông tin nhạy cảm và dữ liệu định danh cá nhân (PII) ở cả 2 chiều Inbound/Outbound.
  - **Diverse Targets & Enterprise Topology:** Hỗ trợ Lambda, REST API, API Gateway, MCP Server Target; kết nối hệ thống On-Premises qua AWS PrivateLink và NAT Gateway.

#### 7. Thực Hành Hands-on Labs: Build & Deploy AI Agents
- **Lab 1: Kiro and Its Features**
  - **Setup môi trường:** Lựa chọn cài đặt *Local Kiro IDE* (cấu hình `aws configure` region `ap-southeast-1`) hoặc sử dụng *AWS Hosted Remote Desktop (Amazon DCV)* có sẵn toàn bộ công cụ Kiro, Python, AWS CLI, AgentCore CLI.
  - **Cấu hình Kiro Steering:** Thiết lập file quy tắc `.kiro/steering.md` để định hướng AI trong Kiro tuân thủ chuẩn AWS Strands SDK, quy tắc đặt tên biến và xử lý ngoại lệ. Kiểm thử sinh code tự động qua **Vibe Coding**.
- **Lab 2: Build & Deploy AI Agents với AgentCore CLI (3 Lệnh chính)**
  - *Bước 1 (Khởi tạo dự án):* `agentcore init my-first-agent` → Tự động sinh cấu trúc thư mục chuẩn gồm `agent.py`, `config.yaml`, `requirements.txt`.
  - *Bước 2 (Cấu hình Runtime):* `agentcore configure --model anthropic.claude-3-5-sonnet --prompt "You are a helpful AWS assistant."` → Liên kết bộ não LLM và System Prompt.
  - *Bước 3 (Triển khai & Invoke):* `agentcore deploy --env dev` → Đóng gói lên Bedrock AgentCore Runtime (MicroVM) và chạy `agentcore invoke --prompt "..."` để nhận luồng kết quả Streaming Response real-time.

---

### Những Gì Học Được

#### Tư duy thiết kế
- **Chuyển đổi từ PoC sang Production:** Nắm vững 4 trụ cột quan trọng (Performance, Scalability, Security, Governance) khi xây dựng các ứng dụng GenAI thực tế.
- **Cách ly dữ liệu người dùng:** Áp dụng công nghệ Firecracker MicroVM để tạo môi trường tính toán riêng biệt tuyệt đối cho từng phiên làm việc.
- **Bảo mật phân quyền WAT:** Sử dụng Workload Access Token (WAT) để bảo mật thông tin định danh của người dùng khi ủy quyền cho Agent gọi dịch vụ bên ngoài.

#### Kiến trúc kỹ thuật
- **Chuẩn hóa Giao thức AI:** Hiểu rõ tầm quan trọng của MCP và A2A trong việc kết nối các công cụ và các Agent đa nhiệm.
- **Kiến trúc Bedrock Agent Core:** Làm chủ 3 thành phần cốt lõi: **Runtime** (Serverless microVM), **Identity** (Xác thực & Ủy quyền), và **Gateway** (Middleware & HITL).
- **Lập trình theo phương pháp Vibe Coding:** Tận dụng Kiro IDE và Steering Rules để định hướng AI trợ lý viết code chuẩn kiến trúc Cloud.

#### Vận hành & Triển khai
- **Chiến lược triển khai Canary:** Sử dụng Alias ARN trên Bedrock Agent Core để triển khai thử nghiệm 5-10% traffic và sẵn sàng Rollback khi gặp lỗi.
- **Human-in-the-Loop:** Tích hợp cơ chế can thiệp của con người vào Cổng Gateway nhằm kiểm soát các rủi ro vận hành doanh nghiệp.

---

### Ứng Dụng Vào Công Việc

- **Xây dựng Agent với AWS Strands SDK:** Áp dụng bộ khung mã nguồn mở Strands và Factory Design Pattern để thiết kế các Agent có tính đóng gói cao.
- **Thiết lập Steering Rules cho dự án:** Tạo các file quy tắc `.kiro/steering.md` trong IDE để chuẩn hóa mã nguồn khi làm việc nhóm cùng AI.
- **Tối ưu hóa quy trình triển khai với AgentCore CLI:** Đóng gói và đưa ứng dụng Agent lên AWS Cloud một cách nhanh chóng thông qua bộ 3 lệnh CLI (`agentcore init`, `agentcore configure`, `agentcore deploy`).
- **Tăng cường an toàn dữ liệu:** Cấu hình Bedrock Gateway Interceptors để tự động lọc dữ liệu nhạy cảm PII và thiết lập AWS PrivateLink bảo mật kết nối nội bộ.

---

### Trải nghiệm trong event

Tham gia buổi **AWS FCAJ Agent Forge - Deepdive** đã mang lại cho tôi những trải nghiệm vô cùng quý giá và kiến thức thực tiễn vượt trội về lĩnh vực Agentic AI.

- **Bài giảng L300 vô cùng cô đọng:** Anh Nghĩa đã hệ thống hóa lượng kiến thức khổng lồ (hơn 350 slide) thành các mô hình kiến trúc rất dễ tiếp thu, làm rõ lộ trình đưa AI Agent từ giai đoạn thử nghiệm lên môi trường doanh nghiệp.
- **Trực quan với phương pháp Vibe Coding:** Phần hướng dẫn thực hành của anh Hải Anh với Kiro IDE và AgentCore CLI đã giúp tôi trải nghiệm cách khởi tạo, cấu hình và triển khai một AI Agent lên hạ tầng Serverless AWS chỉ trong vài phút.
- **Giải tỏa rào cản bảo mật:** Sự kết hợp giữa Firecracker MicroVM, Workload Access Token (WAT) và Cổng kết nối Gateway giúp tôi hoàn toàn tự tin về tính an toàn và khả năng quản trị khi đưa AI vào hệ thống thực tế.

#### Một số hình ảnh khi tham gia sự kiện
![AWS FCAJ Agent Forge - Deepdive](hinh-anh-sk-3/IMG_20260801_091335.webp)
![AWS FCAJ Agent Forge - Deepdive](hinh-anh-sk-3/IMG_20260801_110623.webp)

> Sự kiện AWS FCAJ Agent Forge - Deepdive là một cột mốc quan trọng, giúp tôi định hình rõ nét tư duy thiết kế kiến trúc Agentic AI chuyên nghiệp, sẵn sàng làm chủ công nghệ Bedrock Agent Core và áp dụng các công cụ hiện đại để xây dựng các giải pháp Cloud-native AI vững chắc cho doanh nghiệp.
