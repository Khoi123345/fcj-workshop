Dưới đây là nội dung chi tiết và cụ thể theo từng session (phiên chia sẻ) của sự kiện **FCAJ Community Day \- June 2026**:

### **Session 1: Định hướng nghề nghiệp với Cloud & Giới thiệu về Cloud Thinker**

* **Speaker:** Anh Steve Trần (Founder của Cloud Thinker, cựu Solution Architect tại AWS) \[[13:02](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=782)\].  
* **Nội dung chính:**  
  * **Hành trình sự nghiệp (Career Path):** Diễn giả chia sẻ hành trình từ năm 19 tuổi khi bỏ học đại học để đi làm bảo trì server vật lý cho các Contact Center \[[15:13](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=913)\]. Sau đó, anh tự học Cloud (từng trượt chứng chỉ Azure 3-4 lần trước khi chuyển sang AWS) \[[16:14](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=974)\]. Trong vòng 4 năm từ một kỹ sư hạ tầng bình thường, anh đã trở thành Solution Architect tại AWS nhờ dự đoán đúng xu hướng bùng nổ Cloud thời kỳ Covid \[[18:20](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=1100)\].  
  * **Thách thức thời đại AI:** Diễn giả cảnh báo về việc các doanh nghiệp đang giảm tuyển dụng vị trí Developer/Cloud Junior và chuyển sang dùng công nghệ AI phối hợp với Senior \[[19:34](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=1174)\]. Anh khuyên sinh viên nên đi thực tập, trải nghiệm doanh nghiệp sớm \[[20:43](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=1243)\].  
  * **Sản phẩm Cloud Thinker:** Giải quyết bài toán giảm độ phức tạp (Complexities) và nợ công nghệ (Technical Debt) khi hệ thống của doanh nghiệp phình to \[[22:03](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=1323)\].  
  * **Kiến trúc Multi-Agent:** Giải thích lý do chọn mô hình Multi-Agent (nhiều AI Agent chuyên biệt) thay vì Single Agent nhằm tối ưu hóa chi phí xử lý văn cảnh (Context), quản lý quyền truy cập (Role-based access control) \[[35:57](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=2157)\] và vận hành trên nhiều môi trường phức tạp cùng lúc mà không lo bị ảo giác (Hallucination) \[[39:06](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=2346)\].

### **Session 2: Giọng nói của AI (Voice AI Agent) & Ứng dụng thực tế**

* **Speakers:** Anh Hiếu Nghị (Renova Cloud), anh Kiệt (AWS Study Builder) và anh Trung Đỗ (CEO của R AI) \[[43:43](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=2623)\].  
* **Nội dung chính:**  
  * **Tổng quan về Voice AI:** Anh Nghị giới thiệu về hai dạng kiến trúc hệ thống Voice (Speech-to-Speech trực tiếp và mô hình kết hợp 3 bước: Speech-to-Text → LLM xử lý → Text-to-Speech) [[46:55](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=2815)].  
  * **Demo thực tế:** Diễn giả thực hiện Live Demo một Voice Agent nói tiếng Anh được build trên hạ tầng AWS Bedrock, tích hợp Knowledge Base để trả lời thông tin về sản phẩm MacBook của Apple [[50:12](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3012)].  
  * **Bài toán Voice AI cho tiếng Việt (Enterprise):** Anh Trung Đỗ phân tích tiếng Việt là ngôn ngữ ít tài nguyên (low-resource) [[52:52](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3172)], do đó R AI áp dụng kiến trúc 3 bước (STT → LLM → TTS) cho các ngân hàng như VPBank, VIB để kiểm soát nội dung trả lời real-time và thực hiện cuộc gọi công cụ (Tool calling) như khóa thẻ [[53:35](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3215)].  
  * **Các tính năng nâng cao cho tiếng Việt:** Hệ thống của R AI xử lý luồng âm thanh dạng Stream để giảm latency, tự động nhận diện giới tính (để xưng hô anh/chị chính xác) \[[56:58](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3418)\], train model nhận biết ngữ cảnh dừng nghỉ để ngắt lời tự nhiên (Interruption handling) \[[57:05](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3425)\], kết hợp hệ thống chuyển giao mượt mà cho tổng đài viên là con người khi AI gặp ca khó \[[58:44](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3524)\]. Xử lý giọng nói vùng miền (Accent) bằng cách đưa 10-20% dữ liệu vùng miền vào tập train \[[50:54](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3054)\].

### **Session 3: DevOps AI Agent (AWS DevOps Guru / Amazon Q Developer Agent)**

* **Speakers:** Chị Bảo và anh Nguyên Nguyễn (Cloud Engineers từ Cloud Kinetic) \[[01:03:35](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3815)\].  
* **Nội dung chính:**  
  * **Vấn đề của phương pháp DevOps truyền thống:** Khi hệ thống gặp sự cố (Incident), kỹ sư mất nhiều thời gian tìm log/trace ở nhiều nơi rải rác, bị ngắt quãng liên tục, dẫn đến thời gian khắc phục (MTTR) bị kéo dài \[[01:05:02](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=3902)\].  
  * **Giải pháp DevOps AI Agent:** Tự động hóa quá trình học ngữ cảnh hệ thống qua "Agent Space" (vùng chứa logic phân quyền tài nguyên dựa trên Tag) để vẽ ra sơ đồ cấu trúc (Topology) \[[01:07:47](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=4067)\].  
  * **Cách tính phí:** Công cụ tính phí dựa trên thời gian thực thi tác vụ (khoảng 0.083 USD/giây) chứ không tính theo lượng Token \[[01:12:00](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=4320)\].  
  * **Quy trình 4 bước xử lý sự cố:** 1\. Phân loại/Trích xuất dữ liệu khi có alert → 2\. Điều tra tìm nguyên nhân gốc rễ (Root Cause Analysis - RCA) → 3\. Đề xuất phương án xử lý (Mitigation Plan - Agent chỉ khuyến nghị chứ không tự áp dụng để đảm bảo an toàn) → 4\. Đề xuất cải thiện hệ thống lâu dài [[01:12:25](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=4345)].  
  * **Live Demo:** Mô phỏng cuộc tấn công Mock DDoS (1000 request/giây) vào một ứng dụng E-commerce chạy trên ECS \[[01:17:52](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=4672)\]. DevOps Agent tự động quét, tìm ra nguyên nhân và xuất ra các dòng lệnh cụ thể. Kỹ sư chỉ cần copy-paste vào terminal để tắt các task ECS độc hại, đưa ứng dụng hoạt động bình thường trở lại \[[01:20:50](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=4850)\].  
  * **Case Studies thực tế:** Đưa ra ví dụ từ các khách hàng lớn giúp giảm thời gian xử lý sự cố từ hàng tiếng/hàng tuần xuống còn vài phút/vài ngày (như Đại học WGU giảm 77% MTTR) \[[01:24:01](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=5041)\].

### **Session 4: Vai trò của AI trong Quản trị Nguồn nhân lực (HR & Talent Acquisition)**

* **Speakers:** Anh Trường và chị Minh Anh (Solution Architects từ Noventic) \[[01:31:51](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=5511)\].  
* **Nội dung chính:**  
  * **Khó khăn của bộ phận HR hiện tại:** Lọc CV thủ công dễ bỏ sót nhân tài, tốn thời gian on-boarding (Time to hire kéo dài 1-2 tháng), đánh giá ứng viên mang tính cảm tính, rủi ro bảo mật dữ liệu khi đẩy CV ứng viên lên các AI Public \[[01:45:27](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=6327)\].  
  * **Giải pháp Amazon Q Business (Amazon Quick):** Đây là một AI Chat Agent dành cho Enterprise cho phép kết nối đa nền tảng (Microsoft Sharepoint, OneDrive, Google Drive, Gmail, Jira, GitHub, S3...) để gom dữ liệu rời rạc \[[01:53:24](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=6804)\]. Khả năng lưu ngữ cảnh vào bộ nhớ riêng giúp tiết kiệm lượng token tiêu thụ \[[02:01:54](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=7314)\].  
  * **Live Demo quy trình HR tự động:**  
    * Tạo một Skill chuyên biệt mang tên "HR Talent Review Assistant" từ các file hướng dẫn định dạng Markdown \[[02:03:09](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=7389)\].  
    * AI tự động viết Job Description (JD) cho vị trí Junior Cloud Engineer dựa trên các template có sẵn \[[02:04:40](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=7480)\].  
    * Giao việc cho AI tự động quét (OCR) toàn bộ các file CV có trong thư mục, đối chiếu với JD để phân loại ứng viên theo các mức độ (Strong, Good, Low, Very Low) kèm lý do chi tiết \[[02:05:38](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=7538)\].  
    * Tự động xuất ra một file báo cáo Talent Review dạng HTML trực quan chấm điểm theo khung tiêu chí năng lực (Technical, Problem Solving, Communication) \[[02:07:04](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=7624)\] và gợi ý khung lương phù hợp cho từng người \[[02:08:34](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=7714)\].

### **Session 5: Thiết lập Bảo mật cho Amazon Q Business với Private MCP Server**

* **Speakers:** Bạn Toàn Nguyễn (AWS Security Builder) và anh Hiếu Nghị (Renova Cloud) \[[02:14:05](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=8045)\].  
* **Nội dung chính:**  
  * **Rủi ro bảo mật:** Thông thường các AI Agent kết nối với các hệ thống bên thứ ba (MCP Server) qua Internet Public, dễ gặp rủi ro bị tấn công từ chối dịch vụ (DoS) hoặc tấn công đứng giữa (Man-in-the-middle) \[[02:20:26](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=8426)\].  
  * **Giải pháp Private Connection:** Ứng dụng tính năng AWS VPC Connection để đưa luồng kết nối của Amazon Q vào trong mạng nội bộ (Private Subnet). Sử dụng cơ chế phân giải DNS nội bộ của Route 53 Resolver, định tuyến qua Application Load Balancer (ALB) tích hợp chứng chỉ bảo mật ACM \[[02:21:33](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=8493)\]. Toàn bộ dữ liệu truy vấn từ AI Agent đến các API bên thứ ba (như Zalo, WhatsApp, Slack...) không hề đi qua Internet Public \[[02:24:00](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=8640)\].  
  * **Demo kỹ thuật:** Thực hiện kiểm tra câu lệnh truy vấn từ Amazon Q, cho thấy hệ thống chặn hoàn toàn các truy cập từ Public IP \[[02:24:04](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=8644)\] nhưng vẫn cho phép AI lấy thông tin Real-time về latency và các dịch vụ đang chạy trong mạng nội bộ một cách bảo mật \[[02:25:32](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=8732)\].  
  * **Chi phí vận hành hệ thống bảo mật (Cost Estimate):** Chi phí thiết lập mạng Private này dao động khoảng từ 250 \- 350 USD/tháng (bao gồm chi phí cố định cho Route 53 Resolver khoảng 180 USD, ALB 32 USD, tiền hạ tầng EC2 và chi phí Data Transfer In/Out thực tế) \[[02:28:18](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=8898)\].

Sự kiện kết thúc bằng hoạt động chụp hình lưu niệm giữa các speaker và người tham gia \[[02:31:08](https://www.youtube.com/watch?v=G8-WlI7f6dE&t=9068)\].

