---
title: "Nhật ký công việc Tuần 2"
date: 2026-06-29
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu Tuần 2:

* Tìm hiểu thiết kế Class Library nâng cao trong C# và phân tách dự án trong Monorepo.
* Thiết kế và xây dựng các lớp DTO (Data Transfer Object) và Domain Model trong `GameShared`.
* Định nghĩa cấu trúc dữ liệu cho Nhân vật, Trận đấu (Battle), Túi đồ (Inventory) và Cốt truyện AI.
* Kiểm tra khả năng biên dịch và dùng chung thư viện giữa môi trường .NET 8 Backend và Unity Engine.

### Nhiệm vụ thực hiện trong tuần:

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ 2 | - Nghiên cứu chuẩn .NET Standard 2.1 để đảm bảo tương thích với Unity C# <br> - Cấu hình file `GameShared.csproj` cho dự án thư viện dùng chung | 29/06/2026 | 29/06/2026 | Microsoft .NET Standard Docs |
| Thứ 3 | - Thiết kế DTOs cho Nhân vật & Chỉ số: `PlayerStats`, `CharacterProfile`, `LevelProgress` <br> - Thêm các attribute hỗ trợ serialize/deserialize JSON | 30/06/2026 | 30/06/2026 | System.Text.Json Docs |
| Thứ 4 | - Thiết kế DTOs cho Trận đấu (Battle System): `BattleRequest`, `BattleResult`, `TurnAction`, `BossStats` <br> - Khởi tạo các Enum về loại sát thương và hành động chiến đấu | 01/07/2026 | 01/07/2026 | Game Architecture Patterns |
| Thứ 5 | - Thiết kế DTOs cho Túi đồ (Inventory): `ItemModel`, `EquipRequest`, `InventoryState` <br> - Thiết kế DTOs cho AI Cốt truyện: `StoryPromptRequest`, `StoryNodeResponse`, `ChoiceOption` | 02/07/2026 | 02/07/2026 | Clean Code C# |
| Thứ 6 | - Build xuất file `GameShared.dll` và import thử nghiệm vào dự án Unity <br> - Kiểm tra đọc/ghi dữ liệu JSON thử nghiệm để đảm bảo không bị lỗi dữ liệu | 03/07/2026 | 03/07/2026 | Unity C# Scripting |

### Kết quả đạt me Tuần 2:

* Xây dựng xong thư viện `GameShared` đảm bảo tính đồng bộ dữ liệu giữa Frontend và Backend.
* Tránh việc viết lặp lại code (DRY - Don't Repeat Yourself) cho các lớp dữ liệu.
* Đảm bảo `GameShared.dll` hoạt động trơn tru cả trong Unity C# và dự án .NET 8 Lambda.
