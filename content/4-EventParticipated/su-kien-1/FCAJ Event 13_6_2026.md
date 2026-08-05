FCAJ Event 13/6/2026

# A. Kiên và Thọ

## **1\. Thông tin chung & Diễn giả**

* **Chủ đề:** A scalable URL shortening service on AWS (Dịch vụ rút gọn liên kết có thể mở rộng trên AWS).  
* **Diễn giả:**  
  * **Đinh Trung Kiên:** Lead developer tại một công ty startup.  
  * **Nguyễn Minh Thọ:** Sinh viên.  
* **Sự kiện:** Thuộc chuỗi AWS Journey / FCAJ Meetup.

## **2\. Đặt vấn đề & Luồng xử lý cơ bản (Simple Flow)**

* **Bản chất của URL Shortener:** Chuyển đổi một đường dẫn dài phức tạp thành một liên kết ngắn gọn (Ví dụ từ liên kết mua sách Amazon dài thành mã ngắn dạng a.co/d/...).  
* **Mô hình cơ bản ban đầu:** Người dùng → Frontend → Backend → Database (Ghi nhận mã ngắn và URL dài vào cơ sở dữ liệu).  
* **Đánh giá mô hình cơ bản:**  
  * *Ưu điểm:* Dễ triển khai, chi phí rẻ.  
  * *Nhược điểm:* Dễ bị tổn thương (bảo mật), độ trễ khi đọc cao (Read Latency), có điểm lỗi đơn lẻ (Single Point of Failure), và rất khó để mở rộng quy mô (Hard to scale) khi lượng truy cập lớn.

## **3\. Kiến trúc tổng quan trên AWS (Overview Architecture)**

Để giải quyết các nhược điểm trên, hai diễn giả đề xuất một kiến trúc hệ thống phân tán mạnh mẽ sử dụng hàng loạt dịch vụ của AWS:

* **Lớp bảo mật & Điều hướng (Edge/Security):** Sử dụng **Amazon Route 53** (quản lý DNS), **Amazon CloudFront** (mạng phân phối nội dung CDN), kết hợp với **AWS WAF** (Tường lửa ứng dụng web) để chặn mã độc, **AWS Secrets Manager**, **KMS**, **IAM** và **Certificate Manager** để quản lý chứng chỉ, mã hóa và phân quyền.  
* **Lớp Frontend:** Được triển khai và quản lý thông qua **Amazon Amplify**.  
* **Lớp Backend (Tính toán):** Chạy trên **AWS Fargate** (Amazon ECS) với cơ chế cân bằng tải **Application Load Balancer (ALB)**, chia làm các Service chạy trên các Availability Zone (AZ) khác nhau để đảm bảo tính sẵn sàng cao.  
* **Lớp Lưu trữ & Caching:** Sử dụng **Amazon DynamoDB** làm cơ sở dữ liệu chính và cụm **Amazon ElastiCache for Redis** (nằm trong vùng Database Subnet riêng biệt) để làm bộ nhớ đệm tăng tốc độ đọc/ghi.

## **4\. Đi sâu vào kiến trúc xử lý (Inside the architecture)**

Hệ thống được tối ưu hóa bằng cách tách biệt luồng Tạo mã (Create Flow) và luồng Chuyển hướng (Forward Flow):

* **Dịch vụ tạo khóa trước \- Key Generation Service (KGS):**  
  * Thay vì tạo mã ngẫu nhiên khi người dùng gửi yêu cầu (dễ bị trùng lặp và tốn thời gian), một service chạy trên **Amazon ECS Container** sẽ tạo trước các chuỗi mã ngắn (ví dụ: GpFHUcn, aB3xZ9q).  
  * Các mã này được đẩy vào một hàng đợi trong **Amazon ElastiCache (Redis)** bằng lệnh LPUSH key\_queue.  
* **Luồng Tạo liên kết (Create Flow):**  
  * Khi có yêu cầu tạo URL ngắn, Backend (chạy SpringBoot trên ECS) chỉ cần lấy một mã có sẵn từ Redis ra bằng lệnh RPOP.  
  * Sau đó, nó ghi cặp dữ liệu {Mã ngắn \- URL dài} vào **DynamoDB**. Quá trình này diễn ra ngay lập tức và không sợ bị trùng mã (collision-free).  
* **Luồng Chuyển hướng liên kết (Forward Flow):**  
  * Khi người dùng click vào URL ngắn, hệ thống sẽ kiểm tra trong bộ nhớ đệm **Redis** trước (Lookup).  
  * Nếu tìm thấy (Cache hit), hệ thống trả về ngay URL dài để chuyển hướng.  
  * Nếu không thấy (Cache miss), hệ thống mới truy vấn vào **DynamoDB** để lấy dữ liệu.

## **5\. Tổng kết các nguyên lý thiết kế (Summary)**

Bài thuyết trình đúc kết 4 nguyên lý cốt lõi giúp hệ thống đạt hiệu năng cao:

1. **Separation of Concerns (Phân tách mối quan tâm):** Luồng Đọc (Read) và luồng Ghi (Write) được xử lý độc lập, tối ưu theo từng đặc thù lưu lượng thay vì dùng chung một điểm nghẽn.  
2. **Defense at the Edge (Phòng thủ tại vùng biên):** Bảo mật và bộ nhớ đệm (caching) được đẩy về gần người dùng nhất có thể (CloudFront/WAF), giúp giảm tải hoàn toàn cho hệ thống lõi phía sau.  
3. **Pre-computation over On-demand (Tính toán trước thay vì tính toán khi có yêu cầu):** Các mã ngắn được sinh ra trước và xếp hàng đợi, giúp việc xử lý yêu cầu tạo link diễn ra tức thì.  
4. **Cache-aside Pattern (Mô hình bộ nhớ đệm bên cạnh):** Ưu tiên đọc từ bộ nhớ đệm in-memory trước. Chỉ khi không có mới truy cập Database, giữ cho độ trễ ở mức thấp nhất và giảm tải cho DB

# B. Mr. Đạt Phạm và Mr. Cường Nguyễn

Đây là nội dung chi tiết bài chia sẻ có tên **"Câu chuyện thực tế đến văn hóa tại tập đoàn đa quốc gia"** được trình bày bởi hai diễn giả **Mr. Đạt Phạm** (Data Analytics Engineer) và **Mr. Cường Nguyễn** (Process Engineer) trong chuỗi sự kiện *AWS First Cloud Journey AI*.

Nội dung slide đi từ thực tế công việc dữ liệu đến các góc nhìn triết lý phát triển bản thân và sứ mệnh của kỹ sư công nghệ Việt Nam, cụ thể như sau:

## **Phần 1: Thực tế làm gì? (Section 1\)**

Phần này giải quyết câu hỏi: *"Sinh viên năm 3 \- 4 cần trang bị tư duy gì trước những biến động về yêu cầu tuyển dụng?"*

### **1\. Thực tế công việc của Data Analytics Engineer trong doanh nghiệp**

Công việc sẽ khác nhau tùy thuộc vào domain (ngành nghề), mô hình kinh doanh và phòng ban hỗ trợ. Slide lấy ví dụ thực tế từ hai môi trường:

* **Tại Kamereo (Nền tảng B2B cung ứng thực phẩm):**  
  * Xây dựng báo cáo theo ngày, tuần, tháng, quý để theo dõi hiệu suất vận hành.  
  * Thiết kế Dashboard quản lý xu hướng dữ liệu, phát hiện bất thường và hỗ trợ ra quyết định.  
  * Phân tích chỉ số kinh doanh/vận hành, tìm nguyên nhân gốc rễ và đề xuất giải pháp.  
  * Phối hợp đa phòng ban giải quyết các bài toán thực tế phát sinh.  
* **Tại Colgate-Palmolive (Tập đoàn FMCG đa quốc gia):**  
  * Tham gia dự án dữ liệu máy móc, vận hành và thiết bị IoT trong nhà máy.  
  * Tìm kiếm cơ hội tối ưu chi phí sản xuất và nâng cao hiệu suất vận hành.  
  * Hỗ trợ các sáng kiến chuyển đổi số doanh nghiệp.  
  * Xây dựng giải pháp dữ liệu giúp nhà máy vận hành hiệu quả dài hạn.

### **2\. Bốn kỹ năng cốt lõi cần thiết**

* **Tư duy phản biện:** Khả năng phân tích thông tin một cách khách quan để đưa ra những nhận định sáng suốt.  
* **Kỹ năng giao tiếp:** Truyền đạt ý tưởng và kết quả phân tích một cách rõ ràng, dễ hiểu đến mọi đối tượng.  
* **Kể chuyện với dữ liệu (Data Storytelling):** Biến những con số khô khan thành những câu chuyện có ý nghĩa và thúc đẩy hành động.  
* **Giải quyết vấn đề:** Xác định các thách thức và tìm kiếm những giải pháp tối ưu dựa trên nền tảng dữ liệu.  
* *Trích dẫn thực tế của diễn giả:* *"Khi làm báo cáo mình không chỉ đưa ra số liệu cho sếp mà còn tìm hiểu nguyên nhân biến động GMV của công ty, xác định những điểm chưa tốt để cải thiện."*

### **3\. Minh họa Phân tích dữ liệu thực tế (Case study từ Kamereo)**

Diễn giả minh họa bằng một Dashboard vận hành thực tế tại Hà Nội bao gồm các phần:

* **Phân tích dữ liệu lịch sử và xu hướng:** Theo dõi doanh thu Sales \- B2B, tỷ lệ đóng góp doanh số (% Sales Contribution), và giá vốn hàng bán (COGS) qua các tháng từ cuối năm 2024 đến giữa năm 2025 theo từng danh mục (Rau, Trái cây, Thịt, Trứng, Sữa...).  
* **Nghiên cứu thị trường (Market Report):** Đánh giá thị trường Việt Nam về Rau củ, Ức gà và Thịt bò nhập khẩu (Tốc độ tăng trưởng, Hành vi tiêu dùng, Phân tích từ khóa tìm kiếm nhằm tối ưu content/SEO và chiến lược cung ứng đồ ăn sẵn RTC/RTE).  
* **Hanoi Overview & Operations Dashboard (Dữ liệu trước thuế tính đến 28/06/2025):**  
  * *Metrics last week:* GMV đạt 499M (+0.5%), Giá trị đơn hàng trung bình (AOV) đạt 913K (-4.5%), Số đơn hàng/ngày là 78 đơn (+5.2%).  
  * *Operation Performance:* Theo dõi Chi phí xử lý đơn hàng (Fulfillment Cost \- FFM%) đang ở mức 11.7% \- 13.2% và Chi phí giao hàng chặng cuối (Last Mile Cost \- LMC%) ở mức 7.8%.  
  * *Backup Performance:* Quản lý chi phí nhà cung cấp dự phòng rủi ro để đảm bảo an toàn vận hành, hiện tại đang ở mức 11.1% (vượt mục tiêu target 7%).  
  * *Fill rate Performance:* Tỷ lệ đơn hàng đủ hàng cung ứng cho khách đạt 99.1% (vượt mục tiêu target 99%).

### **4\. Mô hình 5 giai đoạn Tư duy phát triển nghề nghiệp**

Mô hình tập trung nâng cao năng lực thực tế thay vì chạy theo chức danh:

1. **Follower (Người thực thi):** Giai đoạn thực tập sinh/Junior mới. Làm việc theo hướng dẫn chi tiết, làm quen môi trường và tích lũy kỹ năng nền tảng.  
2. **Learner (Người học chủ động):** Bắt đầu hiểu cách giải quyết bài toán nhưng vẫn cần mentor định hướng. Hỏi những câu hỏi có chiều sâu để tích lũy thực chiến.  
3. **Problem Solver (Người giải quyết vấn đề):** Cột mốc quan trọng. Không làm theo checklist, chủ động phân tích sâu, đề xuất giải pháp tối ưu và cam kết chất lượng đầu ra.  
4. **System Thinker (Người tư duy hệ thống):** Nhìn bài toán ở bức tranh toàn cảnh, hiểu mối liên kết chéo giữa các bộ phận, dự đoán rủi ro vận hành, đánh giá tác động tài chính và tối ưu hệ thống lâu dài.  
5. **Super Star (Người dẫn dắt):** Đỉnh cao. Đóng vai trò xây dựng tầm nhìn, định hướng chiến lược dữ liệu toàn diện và phát triển thế hệ kế cận.

## **Phần 2: Văn hóa tại MNC (Section 2\)**

Phần này chia sẻ sâu về môi trường và quy trình tại các tập đoàn đa quốc gia.

### **1\. Quy trình tuyển dụng chuẩn tại MNCs**

Bao gồm 4 vòng khắt khe:

1. **Sàng lọc & Sơ vấn:** Hệ thống ATS quét hồ sơ. Trao đổi nhanh 15-30 phút bằng Tiếng Anh với Recruiter.  
2. **Test Năng lực:** Làm bài test tư duy logic, giải thuật (Tech) hoặc Situation Test (đối với mảng Supply Chain).  
3. **Phỏng vấn Chuyên môn:** Làm việc trực tiếp với Tech Lead/Manager. Đào sâu bài toán thực tế bằng mô hình **STAR** (Situation, Task, Action, Result).  
4. **Sự hòa hợp văn hóa (Culture Fit):** Phỏng vấn với Leadership/Sếp lớn để đánh giá mức độ tương thích về giá trị cốt lõi.

### **2\. Giải mã văn hóa doanh nghiệp**

Mượn định nghĩa của Tiến sĩ Giản Tư Trung (Tác giả sách "Đúng Việc"): *"Văn hóa doanh nghiệp chính là cách nghĩ, cách sống và cách làm của doanh nghiệp. Hay cụ thể hơn, là cách nghĩ, cách sống và cách làm việc của từng con người trong doanh nghiệp đó."*

* **Văn hóa No-Blame Post-Mortem (Khối MNC Công nghệ):** Khi xảy ra lỗi hệ thống nghiêm trọng, các kỹ sư tập trung tìm nguyên nhân cốt rễ để sửa đổi hệ thống thay vì đổ lỗi cho cá nhân.  
* **Văn hóa Caring & Inclusive (Khối MNC Tiêu dùng nhanh \- FMCG):** Đặt con người làm trung tâm của mọi sự phát triển, xây dựng môi trường tôn trọng sự đa dạng và không ngừng cải tiến.

## **Phần 3: Trăn trở của quốc gia & Tiêu chuẩn toàn cầu**

### **1\. Bối cảnh lịch sử "Huyết mạch số Việt Nam" (1975 \- 1997\)**

Sự phát triển kinh tế và chuỗi cung ứng Việt Nam trải qua 3 cột mốc lớn:

* **1975 \- 1986 (Cô lập):** Bao vây cấm vận toàn diện, kinh tế tem phiếu, lạm phát phi mã. Logistics chỉ là phân phát hàng hóa nội bộ thủ công.  
* **1986 \- 1995 (Đổi mới & Phá băng):** Đổi mới kinh tế mở đường, đàm phán ngoại giao thành công gỡ nút thắt cấm vận. Ngoại giao chính là hoạt động "Logistics" mở đường đầu tiên.  
* **1997 (Internet gõ cửa):** Ngày 19/11/1997, Việt Nam chính thức kết nối Internet toàn cầu, khai thông dòng chảy tri thức số cho toàn dân tộc (Slide lồng hình ảnh đề thi tốt nghiệp THPT môn Ngữ Văn năm 2026 nói về sự ra đời của máy in Gutenberg và cuộc cách mạng tri thức).

### **2\. Kỷ nguyên FDI, Chuỗi cung ứng & Công xưởng số**

Sự chuyển dịch kép thông qua hai chuỗi hiệu ứng Domino:

* **Chuỗi Domino vật lý (Production & Logistics):** WTO/FTA → Thu hút FDI → Thúc đẩy Sản xuất (Production) → Phát triển Logistics.  
* **Chuỗi Domino kỹ thuật số (Digital Factory):** Mạng 4G/Broadband → Bùng nổ Smartphone → Làn sóng Startups → Ứng dụng Điện toán đám mây (Cloud).

### **3\. Nâng cấp cuộc chơi: Từ "Làm được" sang "Làm đúng chuẩn"**

Để hội nhập thế giới, kỹ sư Việt Nam cần tuân thủ các tiêu chuẩn khắt khe cao nhất:

* **Chuỗi cung ứng vật lý (Logistics):** Phải tuân thủ **GMP** (Thực hành sản xuất tốt), **GSP** (Thực hành bảo quản tốt), **GDP** (Thực hành phân phối tốt) để *bảo vệ uy tín và an toàn hàng hóa vật lý*.  
* **Chuỗi cung ứng số (Tech/Cloud):** Phải tuân thủ **ISO 27001** (Hệ thống an toàn thông tin), **SOC 2** (Kiểm soát hệ thống dịch vụ đám mây), **GDPR** (Bảo vệ dữ liệu quyền riêng tư) để *bảo vệ tài sản số & chủ quyền dữ liệu quốc gia*.  
* *Bài học từ Á Đông:* Học hỏi mô hình **Toyota Production System (TPS)** của Nhật Bản (triết lý *Wakon Yosai \- Hòa hồn Dương tài*) và chiến lược xây dựng các Chaebol hướng ra xuất khẩu theo tiêu chuẩn quốc tế khắt khe dưới thời Park Chung-hee của Hàn Quốc.

## **Kết luận: Triết lý "Đúng việc" của thế hệ mới**

Slide khép lại bằng mô hình 3 trụ cột (lấy cảm hứng từ triết gia Jürgen Habermas) định vị sứ mệnh của người trẻ công nghệ:

1. **LÀM NGƯỜI (Human \- Vùng Xã hội):** Hướng tới sự thấu hiểu, đồng cảm, chân thành. Trở thành con người tử tế, tự quản trị nội tâm vững vàng để đạt trạng thái viên mãn trọn vẹn.  
2. **LÀM NGHỀ (Professional \- Vùng Kinh tế):** Vận hành bằng tiền tệ, lợi ích, năng suất. Giải các bài toán thực tế mang tinh thần phụng sự, tìm thấy mục đích và ý nghĩa sâu sắc.  
3. **LÀM DÂN (Citizen \- Vùng Chính trị):** Vận hành bằng quyền lực, thể chế, pháp luật. Ý thức trách nhiệm với quốc gia, tạo ra di sản công nghệ tử tế cho thế hệ mai sau.

**Thông điệp cuối cùng:** *"Sứ mệnh của thế hệ mới: Gánh vác huyết mạch số quốc gia."*

# C. Hoàng Trọng

Đây là nội dung chi tiết bài thuyết trình của diễn giả **Trong H. Truong** (DevOps Engineer @ Endava Vietnam) với chủ đề xoay quanh công việc thực tế của một Kỹ sư DevOps.

## **1\. Xu hướng thị trường và Thu nhập (Thực trạng ngành IT Việt Nam)**

Mở đầu bài chia sẻ, diễn giả đưa ra các số liệu tổng quan về thị trường để lý giải sức hút của các ngành nghề công nghệ:

* **Nhu cầu tuyển dụng (2016-2025):** Các biểu đồ cho thấy nhu cầu tuyển dụng các vị trí liên quan đến hạ tầng và dữ liệu (AI/ML Engineer, Data Engineer, Cloud Engineer, Security Engineer, DevOps Engineer) đang có tốc độ tăng trưởng cao hơn hẳn so với các vị trí truyền thống (Frontend, Backend, Mobile, Full-stack).  
* **Mức lương theo vị trí và kinh nghiệm (2025-2026):**  
  * *DevOps Engineer & Cloud Engineer* có dải lương khá tương đồng: Junior (16-28 triệu), Mid (28-45 triệu), Senior (45-65 triệu) và Lead/Expert (65-100 triệu).  
  * Mức lương này nhỉnh hơn một chút so với nhóm phát triển phần mềm truyền thống, nhưng thấp hơn so với nhóm Data Engineer (67-105 triệu cho level Expert) và AI/ML Engineer (cao nhất lên đến 78-120 triệu cho level Expert).

## **2\. Góc nhìn thực tế về DevOps**

* **Hình ảnh "ảo tưởng" (What people think DevOps is):** Người viết CI/CD pipelines, "chuyên gia" Docker/Kubernetes, kỹ sư nền tảng đám mây, hoặc đơn giản là người chịu trách nhiệm deploy code và chuyên thức đêm sửa lỗi production.  
* **Thực tế đau thương (What the...):** DevOps không chỉ là vài thao tác đơn giản. Nó bao hàm một khối lượng kiến thức khổng lồ: CI/CD, IaC (Terraform, Ansible), Container/K8s, Cloud (AWS, Azure), Microservices, Bảo mật (SAST/DAST, OPA), Giám sát (Prometheus, ELK), Serverless.... Diễn giả ví von công việc này giống như Người Nhện: *"Với sức mạnh to lớn đi kèm trách nhiệm khổng lồ... và cả những cơn đau đầu"*.

## **3\. DevOps thực sự làm gì? (Scope of Work)**

Công việc của một DevOps không cố định mà **phụ thuộc rất lớn vào ngữ cảnh**, bao gồm: Quy mô công ty, quy mô dự án, cấu trúc nhóm, độ phức tạp của sản phẩm, mức độ trưởng thành của hạ tầng đám mây...

Thực tế công việc hàng ngày của DevOps là giải quyết yêu cầu từ mọi phía:

* *Developer (Dev):* "Code chạy ở local nhưng tèo trên staging" → DevOps phải hỗ trợ debug và troubleshoot.  
* *Tester/QA:* "Môi trường test sập rồi" → DevOps phải khôi phục môi trường và cấp quyền.  
* *Client/User:* "Sao hệ thống chậm thế?" → DevOps phải trực chiến (On-call rotation), xử lý sự cố (Incident handling).  
* *Project Manager:* "Hôm nay release được không?" → DevOps phải quản lý quy trình, làm rõ quyền sở hữu (Ownership).  
* *Security Team:* "Package này dính lỗ hổng" → DevOps phải rà soát, vá lỗi bảo mật.  
* *Finance:* "Sao hóa đơn Cloud tháng này cao thế?" → DevOps phải đi điều tra và tối ưu chi phí tài nguyên.

## **4\. Hành trang cho người mới (What should you learn first?)**

Với hệ sinh thái công cụ (DevOps Tool Landscape) khổng lồ trải dài từ Planning, Source Control, CI/Build, Testing, Deploy, Monitor... người mới rất dễ bị ngợp. Diễn giả khuyên nên tập trung vào các **Nền tảng cốt lõi (Fundamentals)** trước:

* **Nền tảng:** Hệ điều hành Linux, Kiến thức mạng cơ bản (Networking), Ngôn ngữ lập trình (Python, Golang).  
* **Công cụ cốt lõi:** Git & CI/CD, Containers (Docker).  
* **Kiến thức vận hành:** Hiểu cách các ứng dụng chạy (Build, test, deploy, logs, cấu hình, biến môi trường).  
* **Thực hành:** Xây dựng các project nhỏ → Deploy một ứng dụng đơn giản → Tự động hóa nó → Giám sát nó → Tự làm hỏng nó rồi tự sửa (Break it, fix it).

## **5\. Những bài học đắt giá (Things I learned the hard way)**

Diễn giả đúc kết lại những kinh nghiệm "xương máu" sau quá trình làm nghề:

* Copy câu lệnh không có nghĩa là bạn hiểu nó.  
* Học cách xác định chính xác ai là người chịu trách nhiệm cho vấn đề (Real owner of the problem).  
* Luôn tự hỏi **"Tại sao" (Why)** trước khi hỏi **"Làm như thế nào" (How)**.  
* Giao tiếp là một phần quan trọng của công việc.  
* DevOps không phải là việc cố gắng trở thành một "anh hùng" gánh team.

## **6\. Thế nào là một Kỹ sư DevOps giỏi?**

* Công cụ (Tools) sẽ liên tục thay đổi, nhưng **Nền tảng (Fundamentals)** thì luôn ở lại. Hãy giữ sự tò mò và học hỏi không ngừng.  
* Tư duy hệ thống (Think in systems) thay vì chỉ nhìn vào từng task lẻ tẻ.  
* Tự động hóa những công việc nhàm chán, lặp đi lặp lại.  
* Làm cho mọi thứ trở nên rõ ràng và dễ sử dụng cho cả team.  
* Biết cách sử dụng AI (như ChatGPT) để nâng cao kỹ năng, nhưng **không được tắt não** và phụ thuộc hoàn toàn vào nó (như meme chú bò ngồi nhìn máy tính).

# D. Hiếu Nghị

Đây là nội dung chi tiết bài chia sẻ của diễn giả **Danh Hoàng Hiếu Nghị** (AI Engineer – AWS Community Builder – AWS Student Builder Group Leader) được trình bày vào ngày 12/06/2026.

Chủ đề của bài thuyết trình là **"From First Cloud AI Journey to AWS Partner"** (Hành trình từ chương trình đám mây đầu tiên đến đối tác chiến lược của AWS). Nội dung đúc kết lại lộ trình 8 bước phát triển cá nhân từ một sinh viên tò mò cho đến khi trở thành chuyên gia và lãnh đạo cộng đồng công nghệ:

## **Lộ trình 8 bước phát triển (Hành trình cốt lõi)**

Diễn giả Nghị chia sẻ một framework gồm 8 giai đoạn tịnh tiến để định hình sự nghiệp:

1. **Student Curiosity (Bắt đầu với sự tò mò):** Nuôi dưỡng niềm đam mê và đặt những câu hỏi đầu tiên về công nghệ đám mây/AI.  
2. **First Cloud Journey (Tìm môi trường phù hợp):** Tham gia vào các chương trình đào tạo và định hướng nền tảng.  
3. **Workshop & Community (Học hỏi từ người khác):** Chủ động tham gia các buổi workshop, giao lưu để mở rộng góc nhìn từ cộng đồng.  
4. **Hands-on Labs (Học bằng thực hành):** Trực tiếp cấu hình, xây dựng hệ thống qua các bài lab thực chiến thay vì chỉ học lý thuyết xuông.  
5. **School Projects (Ứng dụng vào bài toán thực tế):** Mang kiến thức đám mây và AI áp dụng trực tiếp vào các đồ án, bài tập trên trường lớp.  
6. **Portfolio (Thể hiện năng lực):** Đóng gói sản phẩm, xây dựng hồ sơ năng lực (portfolio) cá nhân một cách chuyên nghiệp.  
7. **AWS Partner (Giải quyết bài toán của thế giới thực):** Làm việc tại các tổ chức đối tác của AWS, trực tiếp xử lý các dự án thương mại quy mô lớn.  
8. **Share Back (Giúp đỡ thế hệ xây dựng tiếp theo):** Quay trở lại dẫn dắt, chia sẻ kiến thức và tạo bệ phóng cho các đàn em khóa dưới.

## **Chi tiết các chương trình và cột mốc đồng hành**

### **Giai đoạn 1: First Cloud AI Journey Program (Tiền thân là First Cloud Journey)**

* **Vận hành:** Cung cấp một hệ thống học tập trực tuyến (LMS) bài bản. Người học được làm chủ (master) các dịch vụ AWS cốt lõi đóng vai trò là xương sống của hạ tầng đám mây hiện đại.  
* **Nội dung đào tạo thiết lập nền tảng bao gồm:**  
  * Thiết lập tài khoản và chiến lược quản lý tối ưu chi phí (AWS Budgets, AWS Support).  
  * Quản lý danh tính và phân quyền truy cập an toàn (AWS IAM).  
  * Thiết kế kiến trúc mạng và hạ tầng cô lập (Amazon VPC).  
  * Triển khai và tối ưu hóa các dịch vụ tính toán (Amazon EC2).  
  * Ứng dụng các giải pháp lưu trữ và cơ sở dữ liệu (Storage & Databases).  
  * Xây dựng hệ thống giám sát và tracking vận hành (Monitoring & Observability).  
* *Hình ảnh minh họa:* Slide ghi lại hình ảnh bảng xếp hạng Kahoot và bức ảnh lưu niệm của các thế hệ thành viên xuất sắc đời đầu trong cộng đồng.

### **Giai đoạn 2: AWS Student Builder Group Program (Tiền thân là AWS Cloud Clubs)**

* **Hoạt động:** Chuyển dịch lên vai trò thủ lĩnh, dẫn dắt các câu lạc bộ học thuật công nghệ dành cho sinh viên.  
* *Hình ảnh minh họa:* Bức ảnh diễn giả Nghị cùng ban cán sự nhận bằng khen/kỷ niệm chương tại Chương trình liên hoan các câu lạc bộ học thuật & Sinh viên 5 tốt \- Khoa CNTT Trường Đại học Sư phạm Kỹ thuật TP.HCM. Đồng thời là các buổi training online quy mô lớn qua Google Meet thu hút hàng trăm sinh viên tham gia (ví dụ: Workshop ngày 30/05/2026 với chủ đề *"Build Voice Agents at Scale with Amazon Bedrock AI"* do Kiet Tran và Nghi Danh trình bày).  
* **Hệ thống phần thưởng & Swag của chương trình:** Thành viên tham gia tích cực có cơ hội nhận các phần quà thương hiệu (Cotton Twill Cap, Khăn trải bàn, Áo thun, Pop Socket, Fidget Cube) cùng lộ trình tích lũy Badge khắt khe gồm: *Leader Badge (QA Learning License), Core Team Badge, các gói AWS Credits tài trợ từ $25, $200 cho đến $500, và voucher thi chứng chỉ AWS quốc tế miễn phí*.

### **Giai đoạn 3: AWS Community Builder Program**

* Cột mốc khẳng định vị thế chuyên gia khi được công nhận là **AWS Community Builder**.  
* *Hình ảnh minh họa:* Poster sự kiện lớn **AWS Community Day Vietnam 2025** tổ chức tại Tòa nhà Bitexco (TP.HCM), nơi quy tụ các gương mặt đầu ngành như Shafraz Rahim (AWS), Donnie Prakoso (Principal Developer Advocate), Ho Viet Anh (AWS Community Hero),... và sự đóng góp của các Community Builder trẻ tuổi. Slide cũng khoe các bộ quà tặng độc quyền "Swag" được AWS gửi tặng qua các năm (Năm 1: mũ, bình nước, sổ; Năm 2: Balo, cốc; Năm 3: Hộp bút cao cấp).

### **Giai đoạn 4: AWS Partners (Đích đến chuyên nghiệp)**

* Bước chân vào thế giới thực với tư cách đối tác chiến lược của AWS.  
* *Hình ảnh minh họa:* Đội ngũ nhân sự tại **RENOVA CLOUD** ăn mừng chiến thắng rực rỡ với danh hiệu danh giá **"AWS Partner of the Year \- Vietnam 2026"** (Đối tác AWS xuất sắc nhất năm 2026 tại Việt Nam) cùng thông điệp đầy tự hào: *"Three Wins. One Team."*

**Thông điệp kết luận:** Diễn giả nhấn mạnh câu nói: *"Getting the job is just a beginning..."* (Nhận được một công việc mới chỉ là sự khởi đầu). Để đi xa trong ngành công nghệ, việc liên tục kết nối (Linkedin Connection) và không ngừng sẻ chia (Share Back) cho cộng đồng chính là chìa khóa mở ra những cánh cửa lớn hơn.

