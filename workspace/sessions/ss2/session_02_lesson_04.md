---
schema_version: 1
id: ss02_lesson_04
type: lesson
status: approved
course_id: devops-basic
session: 2
unit: 4
title: Cài đặt và cấu hình Web Server Nginx
session_kind: theory
tags: []
concepts:
- nginx-basic-setup
depends_on: []
builds_on: []
enables: []
owns:
- nginx-basic-setup
assumes:
- infrastructure-security
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / Lesson 04
language: vi
created: '2026-07-14'
updated: '2026-07-15'
lesson_mode: practical
---

# Cài đặt và cấu hình Web Server Nginx

<!-- section: problem -->
## 1. Đặt vấn đề
Sau khi máy chủ ảo (VPS) đã được cài đặt và bảo mật an toàn, nhu cầu tiếp theo là làm sao để hiển thị trang web hoặc ứng dụng lên mạng internet cho người dùng truy cập. 

Nếu các bạn chạy trực tiếp ứng dụng thô (ví dụ: máy chủ Node.js chạy ở cổng 3000, Python Flask chạy ở cổng 5000) ra internet, hệ thống sẽ gặp các hạn chế lớn:
*   **Hiệu năng kém:** Các máy chủ ứng dụng (Application Server) không được tối ưu để phục vụ các file tĩnh (HTML, CSS, hình ảnh) với số lượng kết nối lớn cùng lúc.
*   **Thiếu an toàn:** Việc phơi bày trực tiếp cổng ứng dụng nội bộ ra internet làm tăng nguy cơ bị tấn công khai thác lỗ hổng bảo mật dịch vụ.
*   **Khó quản trị:** Không thể chạy nhiều ứng dụng khác nhau ở cùng một cổng tiêu chuẩn (HTTP cổng 80, HTTPS cổng 443).

Để giải quyết vấn đề này, các kỹ sư DevOps thường sử dụng một **Web Server** làm trung gian xử lý yêu cầu. Nginx là giải pháp hàng đầu nhờ kiến trúc hướng sự kiện (event-driven) cực kỳ nhẹ, chịu tải tốt và dễ cấu hình.

<!-- section: core -->
## 2. Kiến thức cốt lõi
*   **Nginx (Engine X):** Là một phần mềm Web Server mã nguồn mở, hoạt động như một Reverse Proxy (Proxy ngược), Load Balancer (Bộ cân bằng tải) và HTTP Cache.
*   **Cổng kết nối tiêu chuẩn (Web Ports):**
    *   **Cổng 80 (HTTP - Hypertext Transfer Protocol):** Giao thức truyền tải siêu văn bản không mã hóa thông tin.
    *   **Cổng 443 (HTTPS - HTTP Secure):** Giao thức truyền tải siêu văn bản được mã hóa bảo mật thông qua chứng chỉ SSL/TLS.
*   **Cấu trúc thư mục Nginx trên Ubuntu:**
    *   `/etc/nginx/nginx.conf`: File cấu hình chính của toàn bộ dịch vụ Nginx.
    *   `/etc/nginx/sites-available/`: Thư mục chứa cấu hình của từng website (Server Blocks).
    *   `/etc/nginx/sites-enabled/`: Thư mục chứa liên kết tượng trưng (symlink) trỏ đến file cấu hình trong `sites-available`. Chỉ những file nằm trong thư mục này mới thực sự được Nginx tải và áp dụng.
    *   `/var/www/html/`: Thư mục mặc định chứa mã nguồn tĩnh (HTML/CSS) của website.
*   **Server Block (Virtual Host):** Cấu hình của Nginx cho phép chạy nhiều website khác nhau (ví dụ: `siteA.com` và `siteB.com`) trên cùng một địa chỉ IP máy chủ vật lý bằng cách phân biệt theo tên miền (`server_name`) hoặc cổng truy cập.
*   **Xác thực cơ bản (HTTP Basic Authentication):** Là cơ chế bảo mật tích hợp sẵn trong giao thức HTTP, yêu cầu người dùng nhập đúng tài khoản và mật khẩu thông qua một hộp thoại (popup) trên trình duyệt trước khi được phép truy cập vào tài nguyên. Nginx hỗ trợ cấu hình cơ chế này thông qua hai chỉ thị: `auth_basic` (để đặt thông báo yêu cầu đăng nhập) và `auth_basic_user_file` (để trỏ tới tệp tin chứa thông tin mật khẩu đã được mã hóa/băm, thường được tạo thông qua lệnh `htpasswd` của gói công cụ `apache2-utils`).

<!-- section: steps -->
## 3. Các bước thực hành

### Bước 1 — Cài đặt Nginx trên Ubuntu Server
Đăng nhập vào Cloud Server bằng user `devops` qua SSH. Trước tiên, cập nhật danh sách gói phần mềm của hệ thống:
```bash
sudo apt update
```
Tiến hành cài đặt Nginx:
```bash
sudo apt install nginx -y
```

### Bước 2 — Quản lý dịch vụ Nginx bằng systemctl
Sau khi cài đặt xong, Nginx sẽ tự động chạy. Các bạn có thể kiểm tra trạng thái hoạt động bằng lệnh:
```bash
sudo systemctl status nginx
```

Các lệnh quản lý dịch vụ Nginx quan trọng khác cần ghi nhớ:
```bash
# Khởi động dịch vụ Nginx
sudo systemctl start nginx

# Dừng dịch vụ Nginx
sudo systemctl stop nginx

# Khởi động lại dịch vụ Nginx (ngắt kết nối cũ và nạp lại cấu hình)
sudo systemctl restart nginx

# Reload lại cấu hình Nginx (áp dụng cấu hình mới mà không làm gián đoạn kết nối hiện tại)
sudo systemctl reload nginx

# Cho phép Nginx tự động khởi động cùng hệ điều hành
sudo systemctl enable nginx
```

### Bước 3 — Cấu hình tường lửa UFW cho phép lưu lượng HTTP/HTTPS
Để người dùng ngoài internet có thể truy cập vào dịch vụ web, các bạn phải mở cổng 80 và 443 trên tường lửa UFW.
Nginx cung cấp sẵn các profile cấu hình trong UFW. Kiểm tra danh sách profile:
```bash
sudo ufw app list
```
Đầu ra sẽ hiển thị các profile: `Nginx HTTP`, `Nginx HTTPS`, `Nginx Full`.

Hãy chọn cho phép **Nginx Full** (mở cả cổng 80 và cổng 443):
```bash
sudo ufw allow 'Nginx Full'
```
Kiểm tra lại trạng thái UFW:
```bash
sudo ufw status
```

Bây giờ, các học viên có thể mở trình duyệt web trên máy cá nhân và truy cập vào địa chỉ IP của server: `http://<IP_ADDRESS_CỦA_SERVER>`. Các bạn sẽ nhìn thấy trang chào mừng mặc định của Nginx.

> **[IMAGE NEEDED]** Mô tả: Trang mặc định Welcome to nginx hiển thị thành công trên trình duyệt web.
> Gợi ý path: `assets/ss02/step_03_nginx_welcome.png`

### Bước 4 — Chuẩn bị thư mục và mã nguồn tĩnh cho website mới
Thay vì dùng trang mặc định, chúng ta sẽ tạo một website riêng.
Tạo thư mục lưu trữ mã nguồn cho ứng dụng:
```bash
sudo mkdir -p /var/www/ptit-app/html
```
Cấp quyền sở hữu thư mục cho user đang đăng nhập:
```bash
sudo chown -R $USER:$USER /var/www/ptit-app/html
sudo chmod -R 755 /var/www/ptit-app
```

Tạo một file giao diện `index.html` đơn giản bằng editor `nano`:
```bash
nano /var/www/ptit-app/html/index.html
```
Dán đoạn mã HTML sau vào file:
```html
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <title>Chào mừng tới K24 PTIT DevOps</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 100px; background-color: #f4f4f9; }
        h1 { color: #d32f2f; }
    </style>
</head>
<body>
    <h1>Chào mừng các bạn đến với học phần DevOps Basics!</h1>
    <p>Hệ thống Web Server Nginx đã được cài đặt và cấu hình thành công.</p>
</body>
</html>
```
Lưu file và thoát khỏi editor.

### Bước 5 — Cấu hình Server Block mới
Tạo một file cấu hình Server Block mới trong thư mục `sites-available`:
```bash
sudo nano /etc/nginx/sites-available/ptit-app
```
Dán cấu hình sau vào file (chú ý thay thế `IP_ADDRESS_CỦA_SERVER` bằng IP thực tế của Droplet):
```nginx
server {
    listen 80;
    listen [::]:80;

    root /var/www/ptit-app/html;
    index index.html index.htm;

    server_name IP_ADDRESS_CỦA_SERVER;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Lưu file và thoát.

Kích hoạt Server Block bằng cách tạo liên kết tượng trưng (symlink) sang thư mục `sites-enabled`:
```bash
sudo ln -s /etc/nginx/sites-available/ptit-app /etc/nginx/sites-enabled/
```

### Bước 6 — Kiểm tra cấu hình và áp dụng
Để tránh lỗi cú pháp làm sập toàn bộ dịch vụ Nginx đang chạy, hãy luôn kiểm tra file cấu hình trước khi reload:
```bash
sudo nginx -t
```
Nếu đầu ra hiển thị thông báo `syntax is ok` và `test is successful`, các bạn có thể reload lại Nginx một cách an toàn:
```bash
sudo systemctl reload nginx
```

Bây giờ, truy cập lại trang `http://<IP_ADDRESS_CỦA_SERVER>` trên trình duyệt, các bạn sẽ thấy trang web chào mừng của PTIT DevOps vừa tạo thay vì trang mặc định của Nginx.

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
*   **Quên dấu chấm phẩy (`;`) trong file cấu hình Nginx:** Cú pháp của Nginx bắt buộc kết thúc mỗi dòng chỉ thị cấu hình bằng dấu chấm phẩy. Thiếu dấu này sẽ khiến lệnh `nginx -t` báo lỗi và không thể khởi động/tải lại cấu hình.
*   **Chỉnh sửa trực tiếp file `nginx.conf`:** Đây là thói quen xấu. Việc sửa trực tiếp cấu hình gốc dễ gây ra lỗi toàn hệ thống và khó khôi phục. Hãy luôn tạo cấu hình riêng trong `sites-available` và liên kết sang `sites-enabled`.
*   **Quên liên kết tượng trưng (symlink):** Tạo file cấu hình trong `sites-available` nhưng quên liên kết sang `sites-enabled` khiến cấu hình của các bạn hoàn toàn vô hiệu.
*   **Lỗi phân quyền thư mục web:** Nếu thư mục chứa mã nguồn tĩnh không cho phép user `www-data` (user chạy Nginx) đọc thông tin, trình duyệt sẽ trả về lỗi **403 Forbidden**. Hãy chắc chắn thư mục gốc có phân quyền đọc thích hợp (755).

<!-- section: references -->
## 5. Tài liệu tham khảo
*   [Nginx Official Documentation](https://nginx.org/en/docs/)
*   [DigitalOcean - How to Install Nginx on Ubuntu 24.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-24-04)

<!-- companions: sau khi lesson approved → revision `ss02_revision_04` + quiz `ss02_quiz_lesson_04` (get_quiz_plan) -->
