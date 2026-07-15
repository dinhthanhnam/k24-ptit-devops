---
schema_version: 1
id: ss02_revision_04
type: revision_questions
status: approved
course_id: devops-basic
session: 2
unit: 4
title: Ôn sau bài — Cài đặt và cấu hình Web Server Nginx
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_04
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / revision L04
language: vi
created: '2026-07-15'
updated: '2026-07-15'
question_count: 2
maps_to:
- ss02_lesson_04
lesson_mode: practical
---

# Ôn sau bài — Cài đặt và cấu hình Web Server Nginx

## RQ1
Hãy trình bày vai trò của hai thư mục `/etc/nginx/sites-available/` và `/etc/nginx/sites-enabled/` trên hệ điều hành Ubuntu Server. Tại sao các bạn không cấu hình trực tiếp toàn bộ trang web vào file cấu hình gốc `/etc/nginx/nginx.conf`?

*Hướng dẫn trả lời:*
*   **Vai trò của hai thư mục:**
    *   `/etc/nginx/sites-available/`: Thư mục lưu trữ tất cả các file cấu hình chi tiết của từng website (Server Blocks) được tạo ra. Các file ở đây ở chế độ "chờ" và chưa có hiệu lực.
    *   `/etc/nginx/sites-enabled/`: Thư mục chứa các liên kết tượng trưng (symbolic link/symlink) trỏ sang file cấu hình thực tế bên `sites-available`. Chỉ những file cấu hình được tạo liên kết ở đây mới được Nginx nạp vào hệ thống để hoạt động.
*   **Tại sao không sửa trực tiếp file `nginx.conf`:**
    *   *Tính module hóa và quản trị:* Tách biệt cấu hình giúp các bạn dễ dàng quản lý, bật/tắt (enable/disable) từng trang web riêng lẻ chỉ bằng việc tạo hoặc xóa liên kết tượng trưng mà không ảnh hưởng tới cấu hình gốc hay các website khác.
    *   *Tránh lỗi hệ thống:* Sửa trực tiếp file cấu hình gốc `nginx.conf` rất dễ làm hỏng cú pháp toàn bộ dịch vụ, khiến Nginx bị sập hoàn toàn và ảnh hưởng tới toàn bộ website đang chạy chung trên server.

## RQ2
Lỗi **403 Forbidden** là gì trong Nginx? Hãy nêu 2 nguyên nhân phổ biến dẫn đến lỗi này khi học viên thực hành cấu hình Server Block mới và cách khắc phục tương ứng.

*Hướng dẫn trả lời:*
*   **Định nghĩa lỗi:** Lỗi 403 Forbidden xảy ra khi Web Server Nginx hiểu được yêu cầu truy cập từ trình duyệt của người dùng nhưng từ chối xử lý hoặc không cho phép truy cập vào tài nguyên đó.
*   **2 nguyên nhân phổ biến và cách khắc phục:**
    1.  *Lỗi phân quyền thư mục web:* Thư mục chứa mã nguồn tĩnh (ví dụ: `/var/www/ptit-app/html`) không cho phép user chạy Nginx (mặc định là `www-data`) có quyền đọc (read) hoặc thực thi (execute).
        *   *Cách khắc phục:* Cấp lại quyền cho thư mục web bằng lệnh `sudo chmod -R 755 /var/www/ptit-app` và `sudo chown -R www-data:www-data /var/www/ptit-app`.
    2.  *Không tìm thấy file trang chủ mặc định:* Trong file cấu hình Server Block, các bạn chỉ định các file trang chủ tại chỉ thị `index` (ví dụ: `index index.html index.htm;`), nhưng trong thư mục root thực tế lại không có bất kỳ file nào trùng tên.
        *   *Cách khắc phục:* Tạo đúng file `index.html` trong thư mục gốc được khai báo của dự án.
