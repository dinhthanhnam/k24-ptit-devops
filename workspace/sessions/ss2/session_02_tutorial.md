---
schema_version: 1
id: ss02_tutorial
type: tutorial
status: draft
course_id: devops-basic
session: 2
unit: 0
title: Tutorial step-by-step — Virtual Private Server (VPS)
session_kind: theory
tags:
- tutorial
- step-by-step
concepts: []
depends_on:
- ss02_lesson_01
- ss02_lesson_02
- ss02_lesson_03
- ss02_lesson_04
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / tutorial
language: vi
created: '2026-07-16'
updated: '2026-07-16'
step_count: 6
maps_to:
- ss02_lesson_01
- ss02_lesson_02
- ss02_lesson_03
- ss02_lesson_04
image_policy: placeholder
---

# Tutorial step-by-step — Virtual Private Server (VPS)

<!-- section: overview -->
## 0. Tổng quan lab

Bài thực hành này hướng dẫn học viên thực hiện những bước cơ bản nhất để khởi tạo một máy chủ ảo (VPS) trên nền tảng đám mây DigitalOcean, cài đặt dịch vụ Web Server Nginx để phục vụ một trang web tĩnh mặc định và thiết lập tường lửa bảo vệ máy chủ cơ bản.

*   **Mục tiêu hoàn thành:**
    *   Tạo thành công Droplet (VPS) chạy Ubuntu Server trên DigitalOcean.
    *   Kết nối SSH thành công từ máy cá nhân bằng tài khoản `root`.
    *   Cài đặt dịch vụ Web Server Nginx cơ bản.
    *   Thay đổi nội dung tệp tin HTML mặc định để hiển thị thông điệp tùy biến.
    *   Thiết lập tường lửa UFW và Cloud Firewall cơ bản (chỉ mở cổng 22 và 80).
*   **Thời lượng ước tính:** 30 phút.
*   **Ánh xạ lessons/sessions:** [ss02_lesson_01](file:///c:/Users/Nathan/backend_java_devops/k24-ptit-devops/workspace/sessions/ss2/session_02_lesson_01.md), [ss02_lesson_02](file:///c:/Users/Nathan/backend_java_devops/k24-ptit-devops/workspace/sessions/ss2/session_02_lesson_02.md), [ss02_lesson_03](file:///c:/Users/Nathan/backend_java_devops/k24-ptit-devops/workspace/sessions/ss2/session_02_lesson_03.md), [ss02_lesson_04](file:///c:/Users/Nathan/backend_java_devops/k24-ptit-devops/workspace/sessions/ss2/session_02_lesson_04.md).
*   **Môi trường / prerequisites:**
    *   Máy tính cá nhân có Terminal (macOS/Linux) hoặc Git Bash / PowerShell (Windows).
    *   Tài khoản DigitalOcean đã sẵn sàng sử dụng.

<!-- section: prerequisites -->
## 1. Chuẩn bị

Trước khi bắt đầu thực hành, các học viên hãy chắc chắn rằng:
*   Môi trường dòng lệnh (CLI) trên máy cá nhân có thể chạy được lệnh `ssh`.
*   Tài khoản DigitalOcean đã đăng nhập hoạt động tốt.

<!-- section: step_01 -->
## Bước 1 — Tạo cặp khóa SSH Ed25519 trên máy cá nhân

**Mục tiêu step:** Tạo một cặp khóa mã hóa an toàn trên máy tính cá nhân để chuẩn bị đăng nhập vào Droplet mà không cần nhập mật khẩu.

**Thao tác:**
1. Mở Terminal (macOS/Linux) hoặc Git Bash (Windows) trên máy tính cá nhân.
2. Chạy lệnh sau để sinh cặp khóa SSH:
   ```bash
   ssh-keygen -t ed25519 -C "ptit_vps_key"
   ```
3. Nhấn `Enter` để đồng ý lưu khóa tại đường dẫn mặc định (`~/.ssh/id_ed25519`).
4. Nhấn `Enter` hai lần tại bước yêu cầu nhập mật mã bảo vệ (`passphrase`) để cho phép kết nối tự động.
5. Sao chép nội dung khóa công khai (Public Key) vừa tạo để chuẩn bị dán lên DigitalOcean Droplet:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   *Hãy sao chép toàn bộ dòng kết quả hiển thị (bắt đầu bằng ssh-ed25519).*

**Kết quả mong đợi / kiểm tra:**
Cặp khóa được tạo thành công trong thư mục `~/.ssh/`. Nội dung khóa công khai có cấu trúc chuẩn của thuật toán Ed25519.

<!-- section: step_02 -->
## Bước 2 — Khởi tạo Droplet trên DigitalOcean

**Mục tiêu step:** Khởi tạo một Droplet (VPS) chạy hệ điều hành Ubuntu Server 24.04 LTS tại khu vực Singapore.

**Thao tác:**
1. Đăng nhập vào DigitalOcean Console.
2. Nhấn nút **Create** ở góc trên bên phải và chọn **Droplets**.
3. Chọn khu vực đặt máy chủ (Region) gần Việt Nam nhất: **Singapore**.
4. Chọn hệ điều hành (Image): **Ubuntu 24.04 LTS**.
5. Chọn loại cấu hình (Size): Chọn gói **Basic**, loại CPU **Regular** và cấu hình thấp nhất (ví dụ: gói $4/tháng hoặc $6/tháng).
6. Tại phần phương thức xác thực (Authentication), chọn **SSH Keys**. Nhấn nút **New SSH Key**, dán toàn bộ nội dung khóa Public Key đã copy ở Bước 1 vào, đặt tên khóa là `ptit-key` rồi nhấn **Add SSH Key**.
7. Đặt tên máy chủ (Hostname), ví dụ: `ptit-vps-demo`.
8. Nhấn nút **Create Droplet** và chờ khoảng 30–60 giây để hệ thống khởi tạo xong.
9. Ghi lại địa chỉ IP công cộng (Public IP) của Droplet hiển thị trên danh sách thiết bị.

> **[IMAGE NEEDED]** Giao diện quản lý Droplet hiển thị địa chỉ IP Public sau khi Droplet được tạo thành công.
> Gợi ý path: `assets/ss02/step_02_droplet_created.png`

**Kết quả mong đợi / kiểm tra:**
Droplet chuyển sang trạng thái Active (màu xanh lá) và hiển thị địa chỉ IPv4 Public (ví dụ: `192.0.2.1`).

<!-- section: step_03 -->
## Bước 3 — Kết nối SSH vào Droplet bằng quyền root

**Mục tiêu step:** Sử dụng SSH Keypair để đăng nhập thành công vào giao diện dòng lệnh của máy chủ ảo.

**Thao tác:**
1. Mở Terminal hoặc Git Bash trên máy cá nhân.
2. Chạy lệnh kết nối SSH tới máy chủ ảo:
   ```bash
   ssh root@<IP_ADDRESS_DROPLET>
   ```
   *Thay thế `<IP_ADDRESS_DROPLET>` bằng địa chỉ IP thực tế của Droplet ghi nhận được ở Bước 2.*
3. Nhập `yes` và nhấn `Enter` nếu hệ thống hiển thị thông báo xác thực dấu vân tay của máy chủ lần đầu tiên kết nối.

**Kết quả mong đợi / kiểm tra:**
Đăng nhập thành công mà không cần nhập mật khẩu. Terminal hiển thị thông tin chào mừng của Ubuntu Server với dấu nhắc lệnh dạng:
`root@ptit-vps-demo:~#`

<!-- section: step_04 -->
## Bước 4 — Cài đặt Web Server Nginx

**Mục tiêu step:** Cài đặt gói dịch vụ Nginx trên hệ điều hành Ubuntu Server để máy chủ sẵn sàng phục vụ website.

**Thao tác:**
1. Sau khi đã đăng nhập SSH vào Droplet, cập nhật danh sách gói phần mềm:
   ```bash
   apt update
   ```
2. Thực thi cài đặt Nginx:
   ```bash
   apt install nginx -y
   ```
3. Kiểm tra trạng thái hoạt động của dịch vụ Nginx:
   ```bash
   systemctl status nginx
   ```

**Kết quả mong đợi / kiểm tra:**
Dịch vụ Nginx cài đặt thành công và hiển thị trạng thái `active (running)` trong Terminal.

<!-- section: step_05 -->
## Bước 5 — Cập nhật trang HTML mặc định của Nginx

**Mục tiêu step:** Thay thế giao diện trang mặc định của Nginx bằng một trang HTML tùy biến đơn giản.

**Thao tác:**
1. Mở file HTML mặc định của Nginx bằng công cụ soạn thảo văn bản nano:
   ```bash
   nano /var/www/html/index.html
   ```
2. Xóa toàn bộ nội dung cũ trong file (nếu có) và thay thế bằng đoạn mã HTML đơn giản sau:
   ```html
   <!DOCTYPE html>
   <html lang="vi">
   <head>
       <meta charset="UTF-8">
       <title>PTIT DevOps Lab</title>
       <style>
           body { font-family: sans-serif; text-align: center; margin-top: 15% ; background-color: #fafafa; }
           h1 { color: #d32f2f; }
       </style>
   </head>
   <body>
       <h1>Chào mừng đến với PTIT DevOps Course - Session 02!</h1>
       <p>Hệ thống Web Server Nginx cơ bản đã hoạt động thành công trên máy chủ ảo của bạn.</p>
   </body>
   </html>
   ```
3. Nhấn `Ctrl + O` để lưu file, nhấn `Enter` xác nhận, và nhấn `Ctrl + X` để thoát khỏi editor nano.

**Kết quả mong đợi / kiểm tra:**
Tệp tin `index.html` được ghi nhận nội dung mới. Không cần khởi động lại Nginx vì đây là tài nguyên tĩnh.

<!-- section: step_06 -->
## Bước 6 — Cấu hình tường lửa cơ bản (UFW & Cloud Firewall)

**Mục tiêu step:** Bảo vệ máy chủ ảo bằng cách chặn toàn bộ lưu lượng mạng ngoài các cổng dịch vụ 22 (SSH) và 80 (HTTP).

**Thao tác:**
1. **Lớp 1 (UFW trong OS):**
   * Cho phép dịch vụ SSH đi qua tường lửa:
     ```bash
     ufw allow 22/tcp
     ```
   * Cho phép cổng Web Nginx đi qua tường lửa:
     ```bash
     ufw allow 80/tcp
     ```
   * Kích hoạt tường lửa UFW:
     ```bash
     ufw enable
     ```
     *(Nhấn `y` và `Enter` để xác nhận cảnh báo).*
   * Kiểm tra trạng thái tường lửa:
     ```bash
     ufw status
     ```

2. **Lớp 2 (DO Cloud Firewall ở tầng hạ tầng):**
   * Truy cập DigitalOcean Console, tìm đến mục **Firewalls** trong menu bên trái.
   * Tạo một Cloud Firewall mới. Cấu hình phần **Inbound Rules** chỉ cho phép:
     * SSH (Port 22) từ mọi nguồn (All IPv4 & All IPv6).
     * HTTP (Port 80) từ mọi nguồn.
   * Tại mục **Apply to Droplets**, nhập tên Droplet `ptit-vps-demo` của bạn để áp dụng luật bảo vệ.
   * Nhấn **Create Firewall** để hoàn tất.

**Kết quả mong đợi / kiểm tra:**
* Lệnh `ufw status` trong OS hiển thị `Status: active` và mở đúng cổng 22, 80.
* Từ trình duyệt trên máy tính cá nhân, truy cập địa chỉ IP Droplet: `http://<IP_ADDRESS_DROPLET>`. Giao diện hiển thị đúng trang HTML tùy biến đã cập nhật ở Bước 5.

---

<!-- section: verify -->
## Kiểm tra tổng kết

Sau khi hoàn tất, học viên tự kiểm tra hệ thống theo bảng xác thực sau:

| Tiêu chí | Lệnh/Cách kiểm tra | Kết quả mong đợi |
| :--- | :--- | :--- |
| **Đăng nhập SSH** | `ssh root@<IP>` từ máy cá nhân | Đăng nhập thành công bằng SSH Key |
| **Trạng thái dịch vụ** | `systemctl status nginx` | Hiển thị `active (running)` |
| **Tường lửa OS** | `ufw status` | Hiển thị active và cho phép cổng 22, 80 |
| **Website hiển thị** | Truy cập `http://<IP>` trên trình duyệt | Hiển thị trang HTML tùy biến của PTIT |

---

<!-- section: pitfalls -->
## Lỗi thường gặp

*   **Bị mất kết nối (Lockout):** Xảy ra khi kích hoạt tường lửa UFW mà quên chưa chạy lệnh `ufw allow 22/tcp`.
    *   *Khắc phục:* Đăng nhập thông qua tính năng Console trên trang DigitalOcean để tắt UFW (`ufw disable`) rồi cấu hình lại.
*   **Trang web báo lỗi 403 Forbidden:** Do phân quyền tệp tin `/var/www/html/index.html` bị sai.
    *   *Khắc phục:* Đảm bảo file index.html có quyền đọc cho tất cả mọi người (`chmod 644 /var/www/html/index.html`).

---

<!-- section: next -->
## Bước tiếp theo

Sau khi nắm vững các bước cơ bản trong bài thực hành này, hãy chuyển sang làm phần **Homework** để thử thách bản thân với các kỹ năng nâng cao hơn: quản lý người dùng thường, phân quyền sudo chi tiết, phân quyền sở hữu thư mục web và cấu hình Server Block tùy biến đầy đủ.
