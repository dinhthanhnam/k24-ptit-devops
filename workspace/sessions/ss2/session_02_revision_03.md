---
schema_version: 1
id: ss02_revision_03
type: revision_questions
status: approved
course_id: devops-basic
session: 2
unit: 3
title: Ôn sau bài — Cơ chế bảo mật cho Infrastructure
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_03
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / revision L03
language: vi
created: '2026-07-14'
updated: '2026-07-14'
question_count: 2
maps_to:
- ss02_lesson_03
lesson_mode: theory
---

# Ôn sau bài — Cơ chế bảo mật cho Infrastructure

## RQ1
Nguyên tắc "đặc quyền tối thiểu" (Least Privilege) được áp dụng như thế nào trong việc cấu hình tài khoản quản trị hệ thống Linux Ubuntu Server? Hãy giải thích lợi ích bảo mật của phương pháp này.

*Hướng dẫn trả lời:*
*   **Cách áp dụng:** Không sử dụng trực tiếp tài khoản quản trị tối cao (`root`) cho các thao tác hàng ngày. Thay vào đó, học viên cần tạo một tài khoản người dùng thường (non-root user, ví dụ: `devops`) và thêm user này vào nhóm `sudo`. Khi cần thực hiện các tác vụ cấu hình hệ thống, học viên sử dụng lệnh `sudo` để nâng quyền tạm thời.
*   **Lợi ích bảo mật:**
    *   *Tránh sai sót tai hại:* Hạn chế tối đa các lệnh vô tình phá hủy hệ thống do chạy dưới quyền root (ví dụ: `rm -rf /`).
    *   *Kiểm soát và giám sát (Audit Log):* Khi dùng `sudo`, mọi lệnh thực hiện sẽ được ghi nhật ký (log) kèm theo tên của user thực hiện, giúp dễ dàng truy vết sự cố.
    *   *Giảm thiểu thiệt hại:* Nếu tài khoản user phụ bị tấn công, kẻ tấn công cũng không có ngay quyền root để kiểm soát toàn bộ máy chủ.

## RQ2
Phân tích hậu quả kỹ thuật và cơ chế khắc phục khi học viên bật tường lửa UFW (`ufw enable`) trên máy chủ từ xa mà quên cho phép lưu lượng đi vào qua cổng SSH (`ufw allow 22/tcp`).

*Hướng dẫn trả lời:*
*   **Hậu quả kỹ thuật:** 
    *   Khi lệnh `ufw enable` được thực thi, tường lửa UFW sẽ áp dụng chính sách mặc định là chặn toàn bộ lưu lượng đi vào (`default deny incoming`). 
    *   Nếu chưa cấu hình cho phép cổng SSH (cổng 22 mặc định), mọi gói tin yêu cầu kết nối SSH từ máy cá nhân của các bạn gửi tới server sẽ bị chặn đứng lập tức. 
    *   Kết quả là các bạn sẽ bị ngắt kết nối và khóa quyền truy cập (lockout) hoàn toàn khỏi máy chủ từ xa.
*   **Cơ chế khắc phục:** Do không thể kết nối qua SSH được nữa, cách duy nhất là học viên phải đăng nhập vào trang quản trị của nhà cung cấp Cloud (ví dụ: DigitalOcean), sử dụng tính năng **Web Console** (vốn là cổng kết nối trực tiếp không qua SSH mạng bên ngoài) để đăng nhập tài khoản và chạy lệnh tắt tường lửa (`sudo ufw disable`) hoặc cấu hình bổ sung cổng SSH.
