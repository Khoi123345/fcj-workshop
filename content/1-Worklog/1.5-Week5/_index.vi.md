---
title: "Nhật ký công việc Tuần 5"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu Tuần 5:

* Xây dựng trọn bộ các UI Presenter trong Unity Client cho dự án AI Dungeon RPG.
* Phát triển các màn hình: MainMenu, Tạo nhân vật, Giao diện Cốt truyện, Giao diện Trận đấu và Túi đồ.
* Tích hợp các giao diện Unity với `ApiClient` để nhận và gửi dữ liệu lên Backend.
* Xử lý hiển thị dữ liệu động: Thanh Máu (HP), Năng lượng (MP), Thanh Kinh nghiệm (EXP) và danh sách nút lựa chọn.

### Nhiệm vụ thực hiện trong tuần:

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ 2 | - Thiết kế & lập trình `MainMenuPresenter` & `CharacterCreatePresenter` <br> - Kết nối UI tạo nhân vật với backend để lấy chỉ số khởi tạo | 20/07/2026 | 20/07/2026 | Unity UI Canvas Layout |
| Thứ 3 | - Thiết kế & lập trình `StoryViewPresenter` <br> - Xử lý hiển thị đoạn văn bản AI sinh ra và render động 3 nút lựa chọn hành động | 21/07/2026 | 21/07/2026 | Unity Dynamic UI Instantiation |
| Thứ 4 | - Thiết kế & lập trình `BattleViewPresenter` <br> - Tạo thanh HP/MP, bộ nút kỹ thuật (Tấn công, Dùng skill, Phòng thủ, Bỏ chạy) & hình ảnh Boss | 22/07/2026 | 22/07/2026 | Unity UI Animation & Health Bars |
| Thứ 5 | - Thiết kế & lập trình `InventoryViewPresenter` <br> - Dựng lưới hiển thị trang bị (Grid Layout), khung hiển thị thông số vật phẩm & nút sử dụng | 23/07/2026 | 23/07/2026 | Unity Grid Layout Group |
| Thứ 6 | - Ghép nối tất cả UI Presenter với `ApiClient` <br> - Kiểm tra luồng chuyển màn hình từ Main Menu -> Cốt truyện -> Lựa chọn -> Trận đấu -> Túi đồ | 24/07/2026 | 24/07/2026 | Unity Scene Management |

### Kết quả đạt được Tuần 5:

* Hoàn thiện toàn bộ các màn hình giao diện chính của game trong Unity.
* Hiển thị động thông số nhân vật mượt mà lên thanh HP/MP và ô lưới trang bị.
* Kết nối thành công toàn bộ giao diện Unity với các API endpoint của Backend.
