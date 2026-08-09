---
title: "Nhật ký công việc Tuần 7"
date: 2026-08-03
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu Tuần 7:

* Tích hợp dịch vụ sinh cốt truyện AI từ Amazon Bedrock lên giao diện Unity Story UI.
* Ghép nối hoàn chỉnh luồng chơi End-to-End: Cốt truyện AI -> Chọn hành động -> Trận đấu -> Thăng cấp -> Nhận đồ -> Tiếp tục cốt truyện.
* Kiểm thử toàn bộ hệ thống, xử lý độ trễ mạng, timeout khi gọi AI và các lỗi giao diện phát sinh.
* Tối ưu hóa UI/UX với hiệu ứng chuyển cảnh, hiển thị số sát thương nhảy (Damage Numbers) và âm thanh game.

### Nhiệm vụ thực hiện trong tuần:

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| Thứ 2 | - Đẩy API `/story/next` tích hợp Amazon Bedrock (Claude LLM) lên Backend <br> - Truyền lịch sử lựa chọn và trạng thái nhân vật vào Prompt gọi Bedrock | 03/08/2026 | 03/08/2026 | Bedrock Context Management |
| Thứ 3 | - Kiểm thử tính năng chọn rẽ nhánh trên Unity UI (chọn Lựa chọn 1 / Lựa chọn 2 / Lựa chọn 3) <br> - Kích hoạt chuyển cảnh vào trận đấu (Battle Mode) dựa trên quyết định từ câu chuyện AI | 04/08/2026 | 04/08/2026 | Unity Event Flow |
| Thứ 4 | - Chạy thử nghiệm luồng chơi End-to-End toàn diện (Đọc câu chuyện -> Chọn rẽ nhánh -> Vào trận đấu -> Thắng/Thua -> Nhận phần thưởng -> Mở kịch bản tiếp theo) | 05/08/2026 | 05/08/2026 | End-to-End Game Testing |
| Thu | - Xử lý trường hợp timeout nếu AI phản hồi quá 5 giây (Thêm fallback story node) <br> - Thêm hiệu ứng số sát thương nảy (Floating Damage Text) và hiệu ứng tụt thanh máu | 06/08/2026 | 06/08/2026 | Unity UI Polish & DOTween |
| Fri | - Thêm âm thanh khi bấm nút (UI Click), nhạc nền phiêu lưu & giao diện khi tử trận <br> - Fix các lỗi vỡ khung chữ (Text wrapping) và căn chỉnh nút trên nhiều độ phân giải màn hình | 07/08/2026 | 09/08/2026 | Game Polish Checklist |

### Kết quả đạt được Tuần 7:

* Tích hợp thành công AI Amazon Bedrock (Claude LLM) sinh câu chuyện thông minh theo đúng ngữ cảnh.
* Hoàn thiện luồng chơi game khép kín từ quyết định nội dung đến chiến đấu và tăng cấp.
* Giao diện Unity Client đạt độ hoàn thiện cao, có hiệu ứng sinh động, âm thanh mượt mà và xử lý lỗi mạng tốt.
