---
title: "Nhật ký công việc Tuần 3"
date: 2026-07-06
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3:

* Tìm hiểu mô hình kiến trúc Unity UI Presenter (Tách biệt UI View và Logic xử lý trong Unity).
* Học cách giao tiếp API bất đồng bộ sử dụng `UnityWebRequest` và cơ chế async/await trong C#.
* Viết lớp helper `ApiClient` để phục vụ gọi các API RESTful từ client Unity.
* Xây dựng các UI hỗ trợ như hiệu ứng Loading (Spinner) và bảng thông báo lỗi (Error Modal).

### Nhiệm vụ thực hiện trong tuần:

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ 2 | - Tìm hiểu giao diện Canvas trong Unity, Anchors, Auto Layout Groups & UI Events <br> - Đọc hiểu mô hình MVP (Model-View-Presenter) ứng dụng trong thiết kế UI Game | 06/07/2026 | 06/07/2026 | Unity UI Documentation |
| Thứ 3 | - Tìm hiểu lớp `UnityWebRequest` gửi request HTTP GET/POST <br> - Thực hành lập trình bất đồng bộ async/await trong Unity C# | 07/07/2026 | 07/07/2026 | UnityWebRequest Manual |
| Thứ 4 | - Viết lớp `ApiClient.cs` tái sử dụng cho toàn dự án Unity <br> - Tích hợp parse dữ liệu JSON sử dụng các lớp DTO từ `GameShared.dll` | 08/07/2026 | 08/07/2026 | Async C# in Unity |
| Thứ 5 | - Thiết kế component UI Loading Spinner hiển thị khi chờ API response <br> - Xây dựng popup thông báo lỗi mạng (Network Error / Timeout popup) | 09/07/2026 | 09/07/2026 | Unity UX Design |
| Thứ 6 | - Gọi thử nghiệm mock API từ `ApiClient` để kiểm tra luồng gửi và nhận dữ liệu <br> - Re-factor code Presenter đảm bảo không trộn lẫn logic giao diện và gọi mạng | 10/07/2026 | 10/07/2026 | Refactoring UI Code |

### Kết quả đạt được Tuần 3:

* Làm chủ cách sắp xếp UI chuyên nghiệp trong Unity và áp dụng chuẩn mô hình UI Presenter.
* Viết thành công lớp `ApiClient` thực hiện gọi API bất đồng bộ mượt mà không làm đơ game.
* Tích hợp thành công giao diện chờ (Loading Overlay) và thông báo lỗi giúp trải nghiệm người dùng tốt hơn.
