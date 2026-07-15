---
schema_version: 1
id: ss02_tutorial
type: tutorial
status: approved
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
created: '2026-07-15'
updated: '2026-07-15'
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

Bài thực hành này giúp các học viên tự tay khởi tạo, thiết lập cấu hình bảo mật cơ bản và cài đặt dịch vụ Web Server trên một máy chủ ảo (VPS) chạy hệ điều hành Ubuntu Server.

*   **Mục tiêu hoàn thành:**
    *   Tạo thành công Droplet (VPS) trên nền tảng DigitalOcean (hoặc nhà cung cấp tương đương).
    *   Cấu hình tài khoản quản trị thường (`non-root user`) có quyền `sudo`.
    *   Hardening SSH (vô hiệu hóa mật khẩu, chặn tài khoản `root` đăng nhập trực tiếp).
    *   Cấu hình tường lửa UFW để chỉ cho phép các cổng dịch vụ cần thiết.
    *   Cài đặt Nginx Web Server để phục vụ một trang web HTML tĩnh tự thiết lập.
*   **Thời lượng ước tính:** 45 phút.
*   **Ánh xạ lessons/sessions:** [ss02_lesson_01](file:///c:/Users/Nathan/backend_java_devops/k24-ptit-devops/workspace/sessions/ss2/session_02_lesson_01.md), [ss02_lesson_02](file:///c:/Users/Nathan/backend_java_devops/k24-ptit-devops/workspace/sessions/ss2/session_02_lesson_02.md), [ss02_lesson_03](file:///c:/Users/Nathan/backend_java_devops/k24-ptit-devops/workspace/sessions/ss2/session_02_lesson_03.md), [ss02_lesson_04](file:///c:/Users/Nathan/backend_java_devops/k24-ptit-devops/workspace/sessions/ss2/session_02_lesson_04.md).
*   **Môi trường / prerequisites:**
    *   Máy tính cá nhân chạy Windows/macOS/Linux có cài đặt phần mềm Terminal (Linux/macOS), PowerShell hoặc Git Bash (Windows).
    *   Một tài khoản DigitalOcean hoạt động bình thường (hoặc sử dụng mã ưu đãi của chương trình GitHub Student Developer Pack để nhận credit thực hành miễn phí).

<!-- section: prerequisites -->
## 1. Chuẩn bị

Trước khi bắt đầu thực hành, các học viên hãy chắc chắn rằng:
*   Môi trường CLI cục bộ đã sẵn sàng (gõ lệnh `ssh` trên Terminal máy cá nhân không báo lỗi lệnh không tìm thấy).
*   Tài khoản Cloud Provider đã đăng nhập và sẵn sàng khởi tạo tài nguyên.

<!-- section: step_01 -->
## Bước 1 — Tạo cặp khóa SSH Ed25519 trên máy cá nhân

**Mục tiêu step:** Tạo một cặp khóa mã hóa bất đối xứng an toàn trên máy tính cá nhân để chuẩn bị đăng nhập vào Cloud Server mà không cần sử dụng mật khẩu.

**Thao tác:**
1. Mở Terminal (macOS/Linux) hoặc Git Bash (Windows) trên máy tính cá nhân của các bạn.
2. Thực thi lệnh tạo khóa sau:
   ```bash
   ssh-keygen -t ed25519 -C "k24_ptit_devops_key"
   ```
3. Hệ thống sẽ hỏi đường dẫn lưu file khóa, các bạn hãy nhấn `Enter` để lưu ở thư mục mặc định (`~/.ssh/id_ed25519`).
4. Tại bước thiết lập mật mã bảo vệ khóa (`passphrase`), các bạn có thể nhập mật mã bảo vệ hoặc nhấn `Enter` hai lần để bỏ qua nếu muốn đăng nhập tự động hoàn toàn.
5. Kiểm tra sự tồn tại của file khóa vừa tạo:
   ```bash
   ls -l ~/.ssh/id_ed25519*
   ```
   Các bạn sẽ thấy 2 file: `id_ed25519` (khóa riêng tư - Private Key) và `id_ed25519.pub` (khóa công khai - Public Key).
6. Hiển thị và sao chép toàn bộ nội dung của khóa công khai (Public Key):
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   *Hãy copy lại toàn bộ dòng văn bản xuất hiện trên màn hình để sử dụng ở Bước 2.*

**Kết quả mong đợi / kiểm tra:**
Cặp khóa được tạo thành công trong thư mục `~/.ssh/`. Nội dung file `.pub` có dạng bắt đầu bằng `ssh-ed25519` và kết thúc bằng chuỗi nhãn `"k24_ptit_devops_key"`.

<!-- section: step_02 -->
## Bước 2 — Khởi tạo Droplet trên DigitalOcean

**Mục tiêu step:** Tạo một máy chủ ảo chạy hệ điều hành Ubuntu Server 24.04 LTS đặt tại trung tâm dữ liệu Singapore để tối ưu tốc độ kết nối.

**Thao tác:**
1. Đăng nhập vào trang quản trị DigitalOcean.
2. Nhấn nút **Create** ở góc trên cùng bên phải và chọn **Droplets**.
3. Chọn khu vực (Region) đặt máy chủ là **Singapore**.
4. Tại phần hệ điều hành (Datacenter Image), chọn **Ubuntu 24.04 LTS**.
5. Chọn loại cấu hình (Droplet Type) là **Basic**, tùy chọn CPU là **Regular** và gói giá **$6/month** (1 GB RAM, 1 vCPU, 25 GB SSD).
6. Tại phần phương thức xác thực (Authentication Method), chọn **SSH Keys**. Nhấn nút **New SSH Key**, dán toàn bộ nội dung khóa Public Key đã copy ở Bước 1 vào ô nhập liệu, đặt tên khóa là `ptit-key` rồi nhấn **Add SSH Key**.
7. Tại phần tùy chọn bổ sung, giữ nguyên các mặc định.
8. Đặt tên máy chủ (Hostname) dễ nhớ, ví dụ: `ptit-devops-server`.
9. Nhấn nút **Create Droplet** ở cuối trang và đợi khoảng 30–60 giây để hệ thống hoàn tất cài đặt máy chủ.
10. Ghi nhận lại địa chỉ IP Public của Droplet vừa tạo hiển thị trên bảng quản trị (ví dụ: `192.0.2.1`).

> **[IMAGE NEEDED]** Mô tả: Màn hình giao diện quản trị DigitalOcean hiển thị Droplet ptit-devops-server đã khởi tạo thành công và có địa chỉ IP Public.
> Gợi ý path: `assets/ss02/step_02_droplet_created.png`

**Kết quả mong đợi / kiểm tra:**
Droplet chuyển sang trạng thái hoạt động (Active / màu xanh lá) và hiển thị địa chỉ IPv4 Public của Droplet.

<!-- section: step_03 -->
## Bước 3 — Tạo tài khoản non-root `devops` và cấp quyền `sudo`

**Mục tiêu step:** Áp dụng nguyên tắc đặc quyền tối thiểu bằng cách tạo người dùng thông thường để quản trị hệ thống thay thế cho root.

**Thao tác:**
1. Đăng nhập vào máy chủ bằng tài khoản `root` và SSH Key vừa tạo từ Terminal máy cá nhân:
   ```bash
   ssh root@<IP_ADDRESS_CỦA_DROPLET>
   ```
2. Tạo một tài khoản người dùng mới có tên là `devops`:
   ```bash
   adduser devops
   ```
   *Nhập mật khẩu an toàn cho user mới khi hệ thống yêu cầu và nhấn Enter để bỏ qua các thông tin cá nhân bổ sung.*
3. Thêm người dùng `devops` vào nhóm cấu hình `sudo` để cấp quyền quản trị:
   ```bash
   usermod -aG sudo devops
   ```

**Kết quả mong đợi / kiểm tra:**
Tài khoản `devops` được tạo thành công trong hệ thống. Xác nhận tài khoản thuộc nhóm sudo bằng cách chạy lệnh:
```bash
groups devops
```
Đầu ra phải chứa cụm từ `sudo`.

<!-- section: step_04 -->
## Bước 4 — Thiết lập SSH Key và Hardening SSH daemon

**Mục tiêu step:** Phân bổ khóa bảo mật cho user `devops` và chặn các phương thức đăng nhập kém an toàn (nhập mật khẩu và login trực tiếp bằng root).

**Thao tác:**
1. Khi vẫn đang đăng nhập bằng quyền root trên máy chủ, hãy chuyển sang tài khoản `devops` vừa tạo:
   ```bash
   su - devops
   ```
2. Tạo thư mục cấu hình SSH trong thư mục home của user `devops`:
   ```bash
   mkdir ~/.ssh
   chmod 700 ~/.ssh
   ```
3. Tạo file `authorized_keys` và dán nội dung Public Key (đã tạo ở Bước 1) vào:
   ```bash
   nano ~/.ssh/authorized_keys
   ```
   *Dán nội dung khóa public key vào, lưu file và thoát khỏi editor nano.*
4. Phân quyền an toàn cho file chứa khóa:
   ```bash
   chmod 600 ~/.ssh/authorized_keys
   ```
5. Quay trở lại tài khoản `root` bằng lệnh:
   ```bash
   exit
   ```
6. Mở file cấu hình dịch vụ SSH daemon để tiến hành hardening bảo mật:
   ```bash
   nano /etc/ssh/sshd_config
   ```
7. Tìm và sửa đổi 2 dòng tham số sau thành cấu hình tương ứng (nếu dòng cấu hình có dấu `#` ở đầu thì xóa đi để kích hoạt):
   ```text
   PermitRootLogin no
   PasswordAuthentication no
   ```
8. Lưu file và thoát khỏi nano editor. Tiến hành kiểm tra lỗi cú pháp cấu hình SSH:
   ```bash
   sshd -t
   ```
9. Nếu không có lỗi gì phát sinh, hãy khởi động lại dịch vụ SSH daemon để áp dụng:
   ```bash
   systemctl restart ssh
   ```

> **[IMPORTANT]**
> **QUAN TRỌNG:** Tuyệt đối không tắt kết nối Terminal đang đăng nhập root hiện tại. Hãy mở một cửa sổ Terminal mới trên máy cá nhân để kiểm tra thử đăng nhập bằng user `devops` qua SSH:
> `ssh devops@<IP_ADDRESS_CỦA_DROPLET>`
> Nếu đăng nhập thành công bằng khóa SSH mà không yêu cầu nhập mật khẩu, các bạn có thể tắt phiên đăng nhập root cũ một cách an toàn.

**Kết quả mong đợi / kiểm tra:**
Đăng nhập thành công vào VPS bằng tài khoản `devops` sử dụng SSH Key. Đăng nhập trực tiếp bằng `root` sẽ báo lỗi `Permission denied (publickey)`.

<!-- section: step_05 -->
## Bước 5 — Cấu hình tường lửa UFW

**Mục tiêu step:** Thiết lập tường lửa UFW để ngăn chặn toàn bộ lưu lượng không hợp lệ đi vào máy chủ, chỉ mở duy nhất cổng dịch vụ SSH.

**Thao tác:**
1. Đăng nhập vào Droplet bằng user `devops` qua SSH.
2. Kiểm tra danh sách ứng dụng đã đăng ký với tường lửa UFW:
   ```bash
   sudo ufw app list
   ```
3. Cho phép cổng kết nối dịch vụ SSH đi vào qua tường lửa:
   ```bash
   sudo ufw allow OpenSSH
   ```
4. Kích hoạt hoạt động của tường lửa UFW:
   ```bash
   sudo ufw enable
   ```
   *Nhấn `y` và `Enter` khi hệ thống cảnh báo lệnh có thể làm gián đoạn kết nối SSH hiện tại.*
5. Kiểm tra trạng thái hoạt động thực tế của UFW:
   ```bash
   sudo ufw status verbose
   ```

**Kết quả mong đợi / kiểm tra:**
Tường lửa UFW hiển thị trạng thái `Status: active`. Luật mặc định là `deny (incoming)` và danh sách các cổng mở phải hiển thị cổng `22/tcp` (OpenSSH) ở trạng thái `ALLOW`.

<!-- section: step_06 -->
## Bước 6 — Cài đặt Nginx và cấu hình Server Block chạy website tĩnh

**Mục tiêu step:** Cài đặt phần mềm Web Server Nginx, mở cổng Web trên tường lửa UFW và thiết lập cấu hình phục vụ website tĩnh tùy chọn.

**Thao tác:**
1. Cập nhật danh sách gói phần mềm hệ thống và cài đặt Nginx:
   ```bash
   sudo apt update
   sudo apt install nginx -y
   ```
2. Cập nhật tường lửa UFW cho phép lưu lượng dịch vụ web đi vào (Nginx Full mở cả cổng 80 và 443):
   ```bash
   sudo ufw allow 'Nginx Full'
   ```
3. Tạo thư mục chứa mã nguồn tĩnh riêng cho website mới:
   ```bash
   sudo mkdir -p /var/www/ptit-app/html
   ```
4. Phân quyền sở hữu thư mục web cho tài khoản user `devops`:
   ```bash
   sudo chown -R $USER:$USER /var/www/ptit-app/html
   sudo chmod -R 755 /var/www/ptit-app
   ```
5. Tạo trang web tĩnh giao diện chào mừng `index.html`:
   ```bash
   nano /var/www/ptit-app/html/index.html
   ```
   Dán đoạn mã HTML sau vào file:
   ```html
   <!DOCTYPE html>
   <html lang="vi">
   <head>
       <meta charset="UTF-8">
       <title>PTIT DevOps Lab</title>
       <style>
           body { font-family: sans-serif; text-align: center; margin-top: 10% ; background-color: #eef2f3; }
           h1 { color: #2c3e50; }
       </style>
   </head>
   <body>
       <h1>Chào mừng các bạn sinh viên PTIT đến với Lab Web Server!</h1>
       <p>Nginx đã serve thành công trang web tĩnh của các bạn trên Cloud Server.</p>
   </body>
   </html>
   ```
   *Lưu file và thoát nano.*
6. Tạo một file cấu hình Server Block mới cho dự án:
   ```bash
   sudo nano /etc/nginx/sites-available/ptit-app
   ```
   Dán cấu hình sau (chú ý thay `IP_CỦA_DROPLET` bằng IP thực tế Droplet của các bạn):
   ```nginx
   server {
       listen 80;
       listen [::]:80;

       root /var/www/ptit-app/html;
       index index.html index.htm;

       server_name IP_CỦA_DROPLET;

       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```
   *Lưu file và thoát.*
7. Kích hoạt cấu hình mới bằng cách tạo liên kết tượng trưng (symlink):
   ```bash
   sudo ln -s /etc/nginx/sites-available/ptit-app /etc/nginx/sites-enabled/
   ```
8. Kiểm tra tính hợp lệ của cú pháp cấu hình Nginx:
   ```bash
   sudo nginx -t
   ```
9. Nếu cấu hình hợp lệ, tải lại dịch vụ Nginx để áp dụng thay đổi:
   ```bash
   sudo systemctl reload nginx
   ```

**Kết quả mong đợi / kiểm tra:**
Mở trình duyệt web trên máy cá nhân, truy cập địa chỉ `http://<IP_ADDRESS_CỦA_DROPLET>`. Màn hình trình duyệt hiển thị đúng trang giao diện HTML tùy biến của PTIT DevOps vừa tạo.

---

<!-- section: verify -->
## Kiểm tra tổng kết

Sau khi hoàn thành tất cả các bước, học viên hãy điền vào bảng kiểm tra sau để xác nhận cấu hình:

| Tiêu chí kiểm tra | Lệnh xác thực | Kết quả mong đợi | Xác nhận |
| :--- | :--- | :--- | :---: |
| **Đăng nhập Root** | `ssh root@<IP_ADDRESS>` | Trả về lỗi `Permission denied` | [ ] |
| **Đăng nhập DevOps** | `ssh devops@<IP_ADDRESS>` | Đăng nhập thành công bằng SSH Key | [ ] |
| **Trạng thái UFW** | `sudo ufw status` | `Status: active` và cho phép `OpenSSH`, `Nginx Full` | [ ] |
| **Cấu hình Nginx** | `sudo nginx -t` | `syntax is ok` và `test is successful` | [ ] |
| **Truy cập Website** | Truy cập IP trên trình duyệt | Hiển thị giao diện HTML chào mừng tự tạo | [ ] |

---

<!-- section: pitfalls -->
## Lỗi thường gặp

*   **Bị mất quyền truy cập (Lockout) hoàn toàn:** Xảy ra do bật UFW (`ufw enable`) khi chưa cho phép dịch vụ SSH. 
    *   *Khắc phục:* Đăng nhập Web Console trên dashboard DigitalOcean để tắt UFW (`sudo ufw disable`).
*   **Trang web báo lỗi 403 Forbidden:** Do Nginx không đọc được file `index.html` vì phân quyền thư mục không đúng.
    *   *Khắc phục:* Đảm bảo tất cả các thư mục cha và file mã nguồn đều được phân quyền tối thiểu `755` đối với thư mục và `644` đối với file.
*   **Không nạp được trang web mới cấu hình:** Do quên tạo liên kết symlink sang thư mục `sites-enabled` hoặc chưa thực thi lệnh reload dịch vụ Nginx.
    *   *Khắc phục:* Tạo symlink bằng lệnh `ln -s` và reload lại Nginx.

---

<!-- section: next -->
## Bước tiếp theo

Sau khi hoàn thành bài thực hành và hiểu rõ luồng triển khai, các học viên hãy chuyển sang phần **Homework** để thử thách bản thân với các bài tập phân quyền user nâng cao, tùy chỉnh cổng SSH, chạy song song nhiều cổng web và hardening cấu hình bảo mật nâng cao cho Nginx.
