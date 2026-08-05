TÀI LIỆU CHI TIẾT SỰ KIỆN: AWS FCAJ AGENT FORGE - DEEPDIVE
I. TỔNG QUAN SỰ KIỆN & NGỮ CẢNH CHUYÊN MÔN
	Tên sự kiện: AWS FCAJ Agent Forge - Deepdive.
	Đơn vị tổ chức: AWS Study Group.
	Diễn giả: Anh Nghĩa (Phụ trách phần Lý thuyết & Kiến trúc) và Hải Anh (Phụ trách phần Hands-on Lab).
	Cấp độ kiến thức: L300 (Advanced Level) — Dành cho Kỹ sư AI, Cloud Architect và Developer muốn đưa các ứng dụng Generative AI từ dạng thử nghiệm (Proof of Concept - PoC) lên môi trường triển khai thực tế (Production-ready).
	Bối cảnh nội dung: Bài giảng chuẩn từ AWS đóng gói khoảng 350 slide giảng dạy trong 1 ngày, tập trung giải quyết các rào cản lớn khi đưa AI Agent vào doanh nghiệp: Performance (Hiệu năng), Scalability (Khả năng mở rộng), Security (Bảo mật) và Governance (Quản trị).
II. LỘ TRÌNH ĐÀO TẠO KHÓA HỌC (AGENDA 3 NGÀY)
	Ngày 1: Nền tảng Agentic AI & Bedrock Agent Core (Runtime, Gateway, Identity)
	Tìm hiểu khái niệm Agentic AI, mức độ tự chủ, giao thức kết nối mới (MCP, A2A).
	Chi tiết môi trường thực thi Amazon Bedrock Agent Core Runtime, công nghệ cách ly Firecracker MicroVM.
	Lớp bảo mật định danh Identity và Cổng kết nối Gateway.
	Thực hành: Cài đặt Kiro IDE, cấu hình Steering Rules và Deploy Agent đầu tiên qua AgentCore CLI.
	Ngày 2: Memory Management, Observability & Guardrails
	Quản lý bộ nhớ ngắn hạn (Short-term) và dài hạn (Long-term) cho từng Session/User.
	Giám sát hệ thống (Observability), ghi nhận log/metrics trên Amazon CloudWatch.
	Thiết lập rào cản an toàn (Guardrails) chống Prompt Injection và lộ dữ liệu.
	Ngày 3: Enterprise Use Cases & Best Practices
	Kiến trúc tích hợp Agent cho ngân hàng, thương mại điện tử, chăm sóc khách hàng.
	Tối ưu hóa chi phí, quy trình Rollout/Rollback và xây dựng hệ thống hoàn chỉnh.
III. NỘI DUNG LÝ THUYẾT CHI TIẾT (DAY 1)
1. Triết lý Agentic AI & Dải Mức độ Tự chủ (Spectrum of Autonomy)
	Khái niệm Agentic AI: Lớp phần mềm thông minh có tính tự chủ (Autonomous). Khác với LLM thông thường chỉ dự đoán token tiếp theo, Agentic AI có khả năng: Lập luận (Reasoning) → Lập kế hoạch (Planning) → Thực thi các tác vụ phức tạp theo từng bước (Execute multi-step tasks).
	Các cấp độ tự chủ (Spectrum of Autonomy):
	Simple Assistant: Hỏi - đáp cơ bản dựa trên LLM.
	Deterministic Workflow: Luồng công việc được thiết lập cố định bởi Developer. Agent đi theo danh sách chỉ dẫn có sẵn, luôn có sự can thiệp của con người (Human-in-the-loop).
	Fully Autonomous Multi-Agent Systems: Các Agent tự liên kết, phân chia nhiệm vụ cho nhau, tự xử lý các tác vụ ngầm kéo dài (Long-running background jobs) và tổng hợp kết quả trả về cho người dùng.
2. Cấu trúc Nền tảng của một AI Agent (Basic Agent Architecture)
Một Agent tiêu chuẩn trên môi trường Production bao gồm 5 thành phần cốt lõi:
	Brain (Bộ não): Các Large Language Model (LLM) đóng vai trò xử lý ngôn ngữ và lập luận. Các họ mô hình phổ biến: Anthropic Claude (Haiku cho tốc độ/chi phí thấp, Sonnet cho tác vụ phức tạp, Opus cho lập trình/kỹ thuật nâng cao), Amazon Nova, Google Gemini.
	System Prompt & Role: Định hình nhân dạng, nhiệm vụ và giới hạn hành vi cho Agent.
	Knowledge Base / Context: Dữ liệu nội bộ doanh nghiệp (RAG, Vector Database, File hệ thống).
	Tools / Actions: Khả năng tương tác với thế giới bên ngoài (gửi email qua Gmail API, truy vấn CSDL, gọi Webhook).
	Memory & Observability: Lưu trữ ngữ cảnh hội thoại và giám sát trạng thái hoạt động thực tế trên Production.
3. Giao thức Kết nối Mới & Framework Phát triển
	Sự chuyển dịch Giao thức (Protocols):
	Trước năm 2023: Chuẩn HTTP REST API là giao thức kết nối chính giữa các ứng dụng.
	Kỷ nguyên AI Agent: Sử dụng 2 giao thức chuẩn hóa mới:
	MCP (Model Context Protocol): Giao thức chuẩn hóa giúp Agent giao tiếp và gọi các Tool/Plugin.
	A2A (Agent-to-Agent): Giao thức cho phép các Agent trao đổi và phân chia công việc trực tiếp với nhau.
	Framework Strands SDK: Bộ Open-source SDK do AWS phát triển dành riêng cho việc xây dựng Agent trên AWS Cloud, thay thế hoặc tối ưu hóa tốt hơn so với LangChain/LangGraph khi tích hợp vào hạ tầng AWS.
	Design Pattern: Sử dụng Factory Design Pattern để khởi tạo Agent nhanh chóng bằng cách đóng gói 3 thành phần: Model + System Prompt + Tools.
4. Amazon Bedrock Agent Core - Runtime Environment
Runtime là môi trường Serverless managed giúp triển khai và vận hành Agent an toàn, dễ mở rộng.
	Công nghệ Firecracker MicroVM:
	Mỗi phiên làm việc (User Session) của Agent được khởi chạy trong một MicroVM hoàn toàn độc lập.
	Mỗi MicroVM có tài nguyên phần cứng (Compute), bộ nhớ (Memory) và hệ thống tập tin (File System) riêng biệt, đảm bảo tính cách ly tuyệt đối (Completely Isolated), loại bỏ hoàn toàn nguy cơ rò rỉ dữ liệu giữa các người dùng.
	Phương thức Deploy:
	Sử dụng mã nguồn Strands Framework từ đầu.
	Đóng gói Container Docker Image qua Amazon ECR.
	Nén mã nguồn dạng ZIP đẩy lên Amazon S3.
	Tính năng quản lý Endpoint & Rollout Strategy:
	Khởi tạo Endpoint với tên tài nguyên ARN.
	Hỗ trợ gán Alias cho phiên bản (default, prod, v1, v2).
	Cho phép triển khai dạng Canary Rollout (chuyển dần 5% - 10% traffic sang phiên bản mới) và Rollback tức thì nếu phát sinh lỗi trên Production.
	Xử lý Tác vụ Bất đồng bộ & Truyền Luồng (Streaming):
	Async & Long-running Jobs: Phân tách các tác vụ tính toán/tìm kiếm phức tạp cho Asynchronous Agents chạy ngầm ở Background.
	Bidirectional Streaming: Hỗ trợ truyền luồng dữ liệu 2 chiều real-time cho ứng dụng Đa thức (Multi-modal) bao gồm cả Voice/Audio và Text (như chế độ Voice Mode hoặc Google Live API).
5. Lớp Bảo mật & Định danh (Identity Layer)
Lớp Identity quản trị toàn bộ quá trình Authentication (Xác thực) và Authorization (Phân quyền) Inbound & Outbound.
	Quy trình Xác thực 5 Bước:
	Inbound: Người dùng/Ứng dụng gửi yêu cầu kèm Credential (thường là JSON Web Token - JWT).
	Token Exchange: Agent Core tiếp nhận JWT và chuyển đổi thành WAT (Workload Access Token). WAT kết hợp quyền hạn của User và Agent nhưng không tiết lộ JWT gốc của User để đảm bảo Best Practice.
	Outbound Exchange:Chuyển đổi WAT sang OAuth Token hoặc API Key tương ứng với Tool cần gọi.
	Token Vault: Lưu trữ an toàn các Credential trong kho khóa mã hóa tích hợp trên Agent Core.
	Execution: Thực thi tác vụ tại Tool và trả kết quả an toàn về cho người dùng.
	Chuẩn Authentication hỗ trợ: Basic Login, OAuth 2-legged, OAuth 3-legged (Single Sign-On qua Google/Facebook/Cognito).
	Tích hợp AWS Cognito: Giúp phát hành JWT chuẩn hóa mà không cần tự xây dựng luồng Authen từ đầu.
6. Cổng Kết Nối Doanh Nghiệp (Gateway Layer)
Gateway đóng vai trò là lớp Middleware trung gian giúp quản trị kết nối khi hệ thống mở rộng lên hàng trăm Agent và hàng nghìn Tool/MCP Server.
	Các tính năng chính của Gateway:
	Human-in-the-Loop (HITL): Cho phép Quản trị viên (Admin) can thiệp phê duyệt (Approve) hoặc từ chối (Deny) các hành động nhạy cảm. Ví dụ: Quy định tự động hoàn tiền là ≤100$. Nếu khách hàng yêu cầu hoàn tiền 200$, Gateway sẽ chuyển yêu cầu đến Admin xem xét trường hợp ngoại lệ thay vì Agent tự quyết định hoặc từ chối cứng nhắc.
	Semantic Tool Search: Áp dụng Vector Indexing để Agent tự động tìm kiếm ngữ nghĩa và chọn ra Tool phù hợp nhất trong danh sách hàng nghìn Tool mà không cần Hard-code API.
	Interceptors / Hooks: Bộ lọc tự động chặn ở đầu vào (Inbound) và đầu ra (Outbound) để quét và loại bỏ các thông tin nhạy cảm hoặc dữ liệu định danh cá nhân (PII - Personally Identifiable Information).
	Các loại Target hỗ trợ: Lambda Target, REST API Target, API Gateway Target, MCP Server Target.
	Enterprise Topology: Kết nối an toàn giữa Agent trên AWS Cloud với hệ thống dữ liệu nội bộ (On-Premises) thông qua AWS PrivateLink và NAT Gateway.
IV. NỘI DUNG THỰC HÀNH CHI TIẾT (HANDS-ON LABS) cho buổi này
Lab 1: Kiro and Its Features
1.1. Thiết lập Môi trường (Workshop Setup)
Học viên được hướng dẫn chuẩn bị môi trường theo 1 trong 2 cách:
	Option 1 — Local Kiro Installation:
	Cài đặt phần mềm Kiro IDE trên máy cá nhân.
	Thiết lập AWS Credentials qua Terminal lệnh: aws configure (nhập Access Key, Secret Key, Region ap-southeast-1).
	Option 2 — AWS Hosted Event Remote Desktop (Amazon DCV):
	Truy cập vào máy chủ ảo do BTC cung cấp qua Amazon DCV Web Client.
	Môi trường đã tích hợp sẵn Kiro IDE, Python Runtime, AWS CLI và AgentCore CLI.
1.2. Cấu hình Kiro Steering (Set Up Steering)
	Khái niệm: Steering File trong Kiro là tập hợp các quy tắc định hướng (Directives) giúp AI Assistant trong Kiro hiểu ngữ cảnh phát triển phần mềm của dự án.
	Các bước thực hiện:
	Mở Kiro IDE, khởi tạo file cấu hình .kiro/steering.md (hoặc cấu hình Steering trong cài đặt).
	Khai báo quy chuẩn lập trình: Chỉ định Kiro phải tuân thủ AWS Strands SDK, quy tắc đặt tên biến, cấu trúc file Python và cách quản lý ngoại lệ (Exception Handling).
	Kiểm thử Steering: Ra lệnh bằng ngôn ngữ tự nhiên (Vibe Coding) để Kiro sinh mã nguồn Agent và kiểm tra xem mã nguồn sinh ra có tuân thủ đúng chuẩn Strands hay không.
Lab 2: Build & Deploy AI Agents with AgentCore CLI
2.1. Part 1: Your First Agent in 3 Commands
Mục tiêu là khởi tạo, đóng gói và triển khai thành công một AI Agent đơn giản lên môi trường Bedrock AgentCore Runtime chỉ với 3 câu lệnh CLI chính.
	Lệnh 1: Khởi tạo dự án (agentcore init)
	Thao tác: Mở Terminal và chạy lệnh:
Bash
agentcore init my-first-agent
	Giải thích: Lệnh này tự động sinh ra cấu trúc thư mục tiêu chuẩn bao gồm:
	agent.py: File chứa mã nguồn chính sử dụng Strands SDK.
	config.yaml: File cấu hình tài nguyên và thông số Agent.
	requirements.txt: Danh sách các thư viện phụ thuộc.
	Lệnh 2: Đóng gói & Cấu hình (agentcore build / agentcore configure)
	Thao tác: Chạy lệnh đóng gói cấu hình:
Bash
agentcore configure --model anthropic.claude-3-5-sonnet --prompt "You are a helpful AWS assistant."
	Giải thích: Lệnh thiết lập bộ não LLM cho Agent (ví dụ: Claude 3.5 Sonnet), khai báo System Prompt định hình vai trò và liên kết các hàm xử lý dữ liệu.
	Lệnh 3: Triển khai & Kiểm thử (agentcore deploy & agentcore invoke)
	Thao tác Triển khai:
Bash
agentcore deploy --env dev
AgentCore CLI sẽ đóng gói mã nguồn, khởi tạo môi trường container/MicroVM trên AWS Bedrock Agent Core và trả về ARN Endpoint.
	Thao tác Kiểm thử (Invoke):
Bash
agentcore invoke --prompt "Xin chào, bạn có thể giúp gì cho tôi?"
	Kết quả: Terminal nhận luồng dữ liệu trả về (Streaming Response) trực tiếp từ Agent đang chạy trên môi trường AWS Serverless.

