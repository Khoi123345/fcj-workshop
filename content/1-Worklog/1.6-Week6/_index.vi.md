---
title: "Nhật ký công việc Tuần 6"
date: 2026-07-27
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu Tuần 6:

* Lập trình logic game trên Backend .NET 8 AWS Lambda để chống gian lận (Anti-Cheat).
* Phát triển bộ tính toán trận đấu theo lượt (Tính sát thương, Chí mạng, Giảm giáp, Né tránh).
* Xây dựng hệ thống Tăng cấp (Level Up), công thức tăng chỉ số và cơ chế Xử lý khi Nhân vật tử trận (Death System).
* Xây dựng logic Backend cho Túi đồ (Thay trang bị, Sử dụng bình máu, tính toán lại chỉ số cộng thêm).

### Nhiệm vụ thực hiện trong tuần:

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ 2 | - Lập trình `BattleService.cs` trên Backend .NET 8 <br> - Viết thuật toán tính toán sát thương theo lượt (Sát thương vật lý, Phép thuật, Tỷ lệ chí mạng) | 27/07/2026 | 27/07/2026 | Game Combat Math |
| Thứ 3 | - Phát triển logic lượt đánh cho Boss và sử dụng kỹ năng tự động <br> - Trả về `BattleResult` DTO chứa đầy đủ diễn biến sau mỗi lượt đánh | 28/07/2026 | 28/07/2026 | Boss Turn State Machine |
| Thứ 4 | - Viết `LevelUpService.cs` (Tính toán kinh nghiệm nhận được & Tăng chỉ số nhân vật) <br> - Viết `DeathSystem.cs` (Cơ chế hồi sinh & hình phạt khi nhân vật hết máu) | 29/07/2026 | 29/07/2026 | RPG Progression Systems |
| Thứ 5 | - Viết `InventoryService.cs` (Logic mặc/tháo trang bị, tính toán lại tổng chỉ số) <br> - Xử lý logic sử dụng bình HP/MP hồi máu tức thì trên server | 30/07/2026 | 30/07/2026 | Inventory Management Patterns |
| Thứ 6 | - Tạo các Lambda Handler cho `/battle/action`, `/character/levelup`, `/inventory/equip` <br> - Viết unit test cho các trường hợp đặc biệt (đánh quá máu, nhân vật tử trận) | 31/07/2026 | 02/08/2026 | xUnit for .NET 8 |

### Kết quả đạt được Tuần 6:

* Xây dựng hoàn chỉnh bộ logic game Serverless trên .NET 8 AWS Lambda.
* Đảm bảo tính minh bạch và chống hack tuyệt đối nhờ tính toán toàn bộ logic trận đấu ở Server.
* Hoàn thành trọn bộ API xử lý Trận đấu, Thăng cấp, Hồi sinh và Quản lý túi đồ.
