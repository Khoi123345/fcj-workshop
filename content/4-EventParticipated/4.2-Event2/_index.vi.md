---
title: "FCAJ Community Day - June 2026"
date: 2026-06-27
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch: "FCAJ Community Day - June 2026"

### Mục Đích Của Sự Kiện

- Định hướng nghề nghiệp trong lĩnh vực Điện toán đám mây (Cloud) và giới thiệu về Cloud Thinker.
- Khám phá công nghệ Trợ lý giọng nói AI (Voice AI Agent), các mô hình kiến trúc và ứng dụng thực tế trong doanh nghiệp Việt Nam đối với ngôn ngữ ít tài nguyên như tiếng Việt.
- Giới thiệu các Trợ lý DevOps AI (DevOps AI Agent, như AWS DevOps Guru, Amazon Q Developer) giúp tự động hóa quá trình xử lý sự cố và tìm nguyên nhân gốc rễ (RCA).
- Tìm hiểu vai trò của Generative AI (như Amazon Q Business) trong quản trị nguồn nhân lực (HR), tự động hóa việc viết JD, lọc CV và đánh giá ứng viên.
- Thiết lập kết nối bảo mật cho Amazon Q Business sử dụng Private MCP Server nhằm hạn chế rủi ro an ninh mạng.

### Danh Sách Diễn Giả

- **Steve Trần** – Founder của Cloud Thinker, cựu Solution Architect tại AWS
- **Danh Hoàng Hiếu Nghị** – AI Engineer tại Renova Cloud, AWS Community Builder
- **Anh Kiệt** – AWS Study Builder
- **Anh Trung Đỗ** – CEO của R AI
- **Chị Bảo** – Cloud Engineer tại Cloud Kinetic
- **Anh Nguyên Nguyễn** – Cloud Engineer tại Cloud Kinetic
- **Anh Trường** – Solution Architect tại Noventic
- **Chị Minh Anh** – Solution Architect tại Noventic
- **Bạn Toàn Nguyễn** – AWS Security Builder

---

### Nội Dung Nổi Bật

#### 1. Định hướng nghề nghiệp với Cloud & Giới thiệu về Cloud Thinker (anh Steve Trần)
- **Hành trình sự nghiệp:** Diễn giả chia sẻ hành trình từ năm 19 tuổi khi bỏ học đại học để đi làm bảo trì server vật lý cho các Contact Center. Sau đó, anh tự học Cloud (từng trượt chứng chỉ Azure 3-4 lần trước khi chuyển sang AWS). Trong vòng 4 năm từ một kỹ sư hạ tầng bình thường, anh đã trở thành Solution Architect tại AWS nhờ dự đoán đúng xu hướng bùng nổ Cloud thời kỳ Covid-19.
- **Thách thức thời đại AI:** Diễn giả cảnh báo về việc các doanh nghiệp đang giảm tuyển dụng vị trí Developer/Cloud Junior và chuyển sang dùng công nghệ AI phối hợp với Senior. Anh khuyên sinh viên nên đi thực tập, trải nghiệm doanh nghiệp sớm.
- **Sản phẩm Cloud Thinker:** Giải quyết bài toán giảm độ phức tạp (Complexities) và nợ công nghệ (Technical Debt) khi hệ thống của doanh nghiệp phình to.
- **Kiến trúc Multi-Agent:** Giải thích lý do chọn mô hình Multi-Agent (nhiều AI Agent chuyên biệt) thay vì Single Agent nhằm tối ưu hóa chi phí xử lý văn cảnh (Context), quản lý quyền truy cập theo vai trò (RBAC) và vận hành trên nhiều môi trường phức tạp cùng lúc mà không lo bị ảo giác (Hallucination).

#### 2. Giọng nói của AI (Voice AI Agent) & Ứng dụng thực tế (anh Hiếu Nghị, anh Kiệt & anh Trung Đỗ)
- **Tổng quan về Voice AI:** Giới thiệu về hai dạng kiến trúc hệ thống Voice (Speech-to-Speech trực tiếp và mô hình kết hợp 3 bước: Speech-to-Text → LLM xử lý → Text-to-Speech).
- **Demo thực tế:** Thực hiện Live Demo một Voice Agent nói tiếng Anh được build trên hạ tầng AWS Bedrock, tích hợp Knowledge Base để trả lời thông tin về sản phẩm MacBook của Apple.
- **Bài toán Voice AI cho tiếng Việt (Enterprise):** Tiếng Việt là ngôn ngữ ít tài nguyên (low-resource). R AI áp dụng kiến trúc 3 bước (STT → LLM → TTS) cho các ngân hàng như VPBank, VIB để kiểm soát nội dung trả lời real-time và thực hiện cuộc gọi công cụ (Tool calling) như khóa thẻ.
- **Các tính năng nâng cao cho tiếng Việt:**
  - **Streaming:** Xử lý luồng âm thanh dạng Stream để giảm latency.
  - **Nhận diện giới tính:** Tự động nhận diện giới tính để xưng hô anh/chị chính xác.
  - **Ngắt lời tự nhiên (Interruption Handling):** Train model nhận biết ngữ cảnh dừng nghỉ để ngắt lời tự nhiên.
  - **Chuyển giao cho con người:** Kết hợp hệ thống chuyển giao mượt mà cho tổng đài viên là con người khi AI gặp ca khó.
  - **Xử lý giọng vùng miền (Accent):** Giải quyết giọng nói vùng miền bằng cách đưa 10-20% dữ liệu vùng miền vào tập train.

#### 3. DevOps AI Agent (chị Bảo & anh Nguyên Nguyễn)
- **Vấn đề của phương pháp DevOps truyền thống:** Khi hệ thống gặp sự cố (Incident), kỹ sư mất nhiều thời gian tìm log/trace ở nhiều nơi rải rác, bị ngắt quãng liên tục, dẫn đến thời gian khắc phục (MTTR) bị kéo dài.
- **Giải pháp DevOps AI Agent:** Tự động hóa quá trình học ngữ cảnh hệ thống qua "Agent Space" (vùng chứa logic phân quyền tài nguyên dựa trên Tag) để vẽ ra sơ đồ cấu trúc (Topology).
- **Cách tính phí:** Công cụ tính phí dựa trên thời gian thực thi tác vụ (khoảng 0.083 USD/giây) chứ không tính theo lượng Token.
- **Quy trình 4 bước xử lý sự cố:**
  1. Phân loại/Trích xuất dữ liệu khi có alert.
  2. Điều tra tìm nguyên nhân gốc rễ (Root Cause Analysis - RCA).
  3. Đề xuất phương án xử lý (Mitigation Plan - Agent chỉ khuyến nghị chứ không tự áp dụng để đảm bảo an toàn).
  4. Đề xuất cải thiện hệ thống lâu dài.
- **Live Demo:** Mô phỏng cuộc tấn công Mock DDoS (1000 request/giây) vào một ứng dụng E-commerce chạy trên ECS. DevOps Agent tự động quét, tìm ra nguyên nhân và xuất ra các dòng lệnh cụ thể. Kỹ sư chỉ cần copy-paste vào terminal để tắt các task ECS độc hại, đưa ứng dụng hoạt động bình thường trở lại.
- **Case Studies thực tế:** Đưa ra ví dụ từ các khách hàng lớn giúp giảm thời gian xử lý sự cố từ hàng tiếng/hàng tuần xuống còn vài phút/vài ngày (như Đại học WGU giảm 77% MTTR).

#### 4. Vai trò của AI trong Quản trị Nguồn nhân lực (HR & Talent Acquisition) (anh Trường & chị Minh Anh)
- **Khó khăn của bộ phận HR hiện tại:** Lọc CV thủ công dễ bỏ sót nhân tài, tốn thời gian on-boarding (Time to hire kéo dài 1-2 tháng), đánh giá ứng viên mang tính cảm tính, rủi ro bảo mật dữ liệu khi đẩy CV ứng viên lên các AI Public.
- **Giải pháp Amazon Q Business:** Đây là một AI Chat Agent dành cho Enterprise cho phép kết nối đa nền tảng (Microsoft Sharepoint, OneDrive, Google Drive, Gmail, Jira, GitHub, S3...) để gom dữ liệu rời rạc. Khả năng lưu ngữ cảnh vào bộ nhớ riêng giúp tiết kiệm lượng token tiêu thụ.
- **Live Demo quy trình HR tự động:**
  - Tạo một Skill chuyên biệt mang tên "HR Talent Review Assistant" từ các file hướng dẫn định dạng Markdown.
  - AI tự động viết Job Description (JD) cho vị trí Junior Cloud Engineer dựa trên các template có sẵn.
  - Giao việc cho AI tự động quét (OCR) toàn bộ các file CV có trong thư mục, đối chiếu với JD để phân loại ứng viên theo các mức độ (Strong, Good, Low, Very Low) kèm lý do chi tiết.
  - Tự động xuất ra một file báo cáo Talent Review dạng HTML trực quan chấm điểm theo khung tiêu chí năng lực (Technical, Problem Solving, Communication) và gợi ý khung lương phù hợp cho từng người.

#### 5. Thiết lập Bảo mật cho Amazon Q Business với Private MCP Server (anh Toàn Nguyễn & anh Hiếu Nghị)
- **Rủi ro bảo mật:** Thông thường các AI Agent kết nối với các hệ thống bên thứ ba (MCP Server) qua Internet Public, dễ gặp rủi ro bị tấn công từ chối dịch vụ (DoS) hoặc tấn công đứng giữa (Man-in-the-middle).
- **Giải pháp Private Connection:** Ứng dụng tính năng AWS VPC Connection để đưa luồng kết nối của Amazon Q vào trong mạng nội bộ (Private Subnet). Sử dụng cơ chế phân giải DNS nội bộ của Route 53 Resolver, định tuyến qua Application Load Balancer (ALB) tích hợp chứng chỉ bảo mật ACM. Toàn bộ dữ liệu truy vấn từ AI Agent đến các API bên thứ ba (như Zalo, WhatsApp, Slack...) không hề đi qua Internet Public.
- **Demo kỹ thuật:** Thực hiện kiểm tra câu lệnh truy vấn từ Amazon Q, cho thấy hệ thống chặn hoàn toàn các truy cập từ Public IP nhưng vẫn cho phép AI lấy thông tin Real-time về latency và các dịch vụ đang chạy trong mạng nội bộ một cách bảo mật.
- **Chi phí vận hành hệ thống bảo mật:** Chi phí thiết lập mạng Private này dao động khoảng từ 250 - 350 USD/tháng (bao gồm chi phí cố định cho Route 53 Resolver khoảng 180 USD, ALB 32 USD, tiền hạ tầng EC2 và chi phí Data Transfer In/Out thực tế).

---

### Những Gì Học Được

#### Tư duy thiết kế
- **Hệ thống Multi-Agent:** Việc phân rã các tác vụ phức tạp thành nhiều AI Agent chuyên biệt giúp quản lý ngữ cảnh tốt hơn và hạn chế tình trạng ảo giác (hallucination) của AI.
- **Bảo mật AI doanh nghiệp:** Các tích hợp AI cho môi trường Enterprise cần ưu tiên kết nối mạng Private qua VPC để đảm bảo dữ liệu nhạy cảm không đi qua internet công cộng.
- **Quản trị quyền hạn (Agent Spaces):** Thiết lập không gian Agent riêng biệt và áp dụng quy tắc Tag tài nguyên giúp phân quyền chặt chẽ cho AI Agent.

#### Kiến trúc kỹ thuật
- **Pipeline Voice AI đa tầng:** Đối với các ngôn ngữ ít tài nguyên như tiếng Việt, kiến trúc kết hợp STT -> LLM -> TTS xử lý dạng Stream kết hợp với việc train dữ liệu vùng miền (accent) mang lại hiệu quả tốt nhất.
- **Vận hành hệ thống bằng AI (AIOps):** Kết hợp các công cụ monitor với DevOps Agent giúp phát hiện sự cố nhanh chóng, đề xuất mã lệnh chính xác để hạ thấp chỉ số MTTR (giảm đến 77%).
- **Kết nối dữ liệu phân tán:** Tận dụng Amazon Q Connectors để gom và index các nguồn dữ liệu rời rạc (Sharepoint, Drive, GitHub) dưới cơ chế bảo mật cao.

#### Chiến lược tích hợp AI
- **Mô hình "Human-in-the-loop":** Khi đưa AI vào các quy trình doanh nghiệp nhạy cảm (như tuyển dụng HR, can thiệp hạ tầng), AI chỉ nên giữ vai trò trợ lý đề xuất, quyết định thực thi cuối cùng vẫn thuộc về con người.
- **Ước lượng chi phí hạ tầng:** Cần tính toán đầy đủ các chi phí mạng ẩn (Route 53 Resolver endpoints, ALB) trước khi triển khai hệ thống mạng Private cho AI.

---

### Ứng Dụng Vào Công Việc

- **Tìm hiểu pipeline Voice AI:** Thực hành xây dựng các ứng dụng Trợ lý giọng nói (Voice Agent) đơn giản trên AWS Bedrock và tìm hiểu các phương pháp tối ưu độ trễ.
- **Ứng dụng các trợ lý DevOps:** Sử dụng các công cụ AI hỗ trợ code/DevOps (như Amazon Q Developer) trong công việc hàng ngày để tăng tốc sửa lỗi và tự động hóa các phân tích hệ thống.
- **Tự động hóa xử lý văn bản:** Thử nghiệm xây dựng các luồng RAG hoặc sử dụng Amazon Q Business để kết nối và truy vấn nhanh dữ liệu từ các kho tài liệu nội bộ.
- **Thiết kế kết nối bảo mật:** Thực hành cấu hình Private Subnet và Route 53 Resolver để bảo vệ dữ liệu truyền tải giữa các API nội bộ.
- **Phân rã kiến trúc Multi-Agent:** Khi phát triển ứng dụng với LLM, thử chia nhỏ bài toán thành nhiều agent chuyên trách để nâng cao độ chính xác và khả năng mở rộng.

---

### Trải nghiệm trong event

Tham gia buổi **FCAJ Community Day - June 2026** đã mang lại cho tôi những kiến thức chuyên môn vô cùng thực tế và giá trị về việc ứng dụng Generative AI trong doanh nghiệp.

- **Giải pháp thực tế ấn tượng:** Các buổi demo trực quan về cách ứng dụng AI trong tổng đài ngân hàng (VPBank, VIB) và tự động hóa nhân sự (HR) giúp tôi thấy rõ giá trị thực tế của AI.
- **Nâng cao tư duy an toàn thông tin:** Bài chia sẻ về Private MCP Server giúp tôi hiểu rõ tầm quan trọng và phương pháp bảo vệ dữ liệu doanh nghiệp khi tích hợp AI.
- **Câu chuyện truyền cảm hứng:** Hành trình tự học và đón đầu xu hướng đám mây của anh Steve Trần tiếp thêm động lực lớn cho tôi trong việc kiên trì tự học và định hướng sự nghiệp Cloud/AI.
- **Môi trường giao lưu cởi mở:** Buổi sự kiện là cơ hội tuyệt vời để kết nối với các anh chị đi trước, các kỹ sư và chuyên gia AWS/AI hàng đầu.

#### Một số hình ảnh khi tham gia sự kiện
![FCAJ Community Day - June 2026](hinh-anh-sk-2/IMG_20260627_101320.webp)


> Sự kiện FCAJ Community Day - June 2026 đã mang lại nguồn cảm hứng lớn, chứng minh rằng AI không còn là khái niệm tương lai mà đã trở thành công cụ thực tiễn len lỏi vào từng ngóc ngách của phát triển phần mềm, xử lý giọng nói, vận hành hệ thống và quản trị doanh nghiệp.
