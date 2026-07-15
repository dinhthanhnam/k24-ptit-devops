---
schema_version: 1
id: ss02_revision_02
type: revision_questions
status: approved
course_id: devops-basic
session: 2
unit: 2
title: Ôn sau bài — Khởi tạo Cloud Server thực tế
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_02
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / revision L02
language: vi
created: '2026-07-14'
updated: '2026-07-14'
question_count: 2
maps_to:
- ss02_lesson_02
lesson_mode: practical
---

# Ôn sau bài — Khởi tạo Cloud Server thực tế

## RQ1
Tại sao phương pháp xác thực bằng cặp khóa SSH (SSH Key Pair) lại bảo mật hơn nhiều so với việc sử dụng mật khẩu (Password) thông thường khi đăng nhập vào máy chủ Linux?

*Hướng dẫn trả lời:*
*   **Về độ phức tạp:** Mật khẩu thông thường thường ngắn và dễ bị tấn công Brute-force/Dictionary. Ngược lại, cặp khóa SSH (ví dụ thuật toán Ed25519) sử dụng mã hóa khóa công khai với độ dài và độ phức tạp toán học cực lớn, khiến việc dò quét khóa gần như là bất khả thi trong thực tế.
*   **Chống tấn công trung gian:** Mật khẩu dạng plain text có thể bị nghe lén hoặc đánh cắp khi truyền qua môi trường mạng không an toàn. Khóa SSH sử dụng cơ chế ký số (digital signature) và xác thực bất đối xứng, khóa riêng tư (Private Key) không bao giờ được gửi qua mạng giúp triệt tiêu hoàn toàn rủi ro này.
*   **Tự động hóa an toàn:** Sử dụng SSH Key giúp việc đăng nhập và tự động hóa tác vụ diễn ra an toàn mà không cần lưu trữ mật khẩu tĩnh ở dạng văn bản thuần trong các script.

## RQ2
Hãy mô tả ngắn gọn quy trình xác thực bất đối xứng hoạt động như thế nào khi các bạn thực hiện lệnh kết nối `ssh root@<IP_ADDRESS>` sử dụng cặp khóa SSH Key từ máy cá nhân lên server.

*Hướng dẫn trả lời:*
*   **Bước 1 - Yêu cầu kết nối:** Máy cá nhân của các bạn gửi yêu cầu kết nối tới cổng SSH của máy chủ (Server).
*   **Bước 2 - Tạo thử thách (Challenge):** Server tìm kiếm Public Key tương ứng trong file `authorized_keys` của tài khoản yêu cầu kết nối. Nếu tìm thấy, Server tạo ra một thông điệp ngẫu nhiên, mã hóa nó bằng Public Key này và gửi lại cho máy cá nhân.
*   **Bước 3 - Giải mã thử thách:** Máy cá nhân nhận thông điệp đã mã hóa, sử dụng Private Key tương ứng đang lưu trữ tại máy để giải mã thông điệp gốc.
*   **Bước 4 - Xác thực thành công:** Máy cá nhân tạo ra một chữ ký số từ thông điệp đã giải mã và gửi lại cho Server. Server kiểm tra chữ ký, nếu khớp sẽ cho phép thiết lập kết nối mà không cần nhập mật khẩu.
