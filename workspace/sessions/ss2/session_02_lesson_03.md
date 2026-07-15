---
schema_version: 1
id: ss02_lesson_03
type: lesson
status: approved
course_id: devops-basic
session: 2
unit: 3
title: Cơ chế bảo mật cho Infrastructure
session_kind: theory
tags: []
concepts:
- infrastructure-security
depends_on: []
builds_on: []
enables: []
owns:
- infrastructure-security
assumes:
- cloud-server-provisioning
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / Lesson 03
language: vi
created: '2026-07-14'
updated: '2026-07-14'
lesson_mode: theory
---

# Cơ chế bảo mật cho Infrastructure

<!-- section: objectives -->
## 1. Mục tiêu
*   Hiểu rõ tầm quan trọng của việc thiết lập bảo mật máy chủ ngay sau khi khởi tạo.
*   Nắm vững cơ chế hoạt động và tầm quan trọng của tường lửa (Firewall) trong bảo mật hạ tầng.
*   Biết cách vô hiệu hóa xác thực mật khẩu và hạn chế tài khoản `root` để bảo vệ dịch vụ SSH.
*   Cấu hình thành công tường lửa UFW (Uncomplicated Firewall) trên Ubuntu Server.

<!-- section: problem -->
## 2. Đặt vấn đề
Ngay sau khi một máy chủ ảo (Cloud VPS) được khởi tạo thành công và có địa chỉ IP công cộng (Public IP) trên mạng internet, nó lập tức lọt vào tầm ngắm của hàng triệu công cụ dò quét tự động (botnet, port scanner). 

Nếu các bạn giữ nguyên cấu hình mặc định:
1.  **Đăng nhập bằng tài khoản quản trị tối cao (`root`):** Kẻ tấn công chỉ cần tìm đúng mật khẩu là có toàn quyền kiểm soát hệ thống.
2.  **Cho phép đăng nhập bằng mật khẩu (Password Authentication):** Botnet sẽ liên tục gửi hàng ngàn yêu cầu đăng nhập mỗi phút (tấn công Brute-force/Dictionary attack) cho đến khi đoán ra mật khẩu đăng nhập.
3.  **Mở tất cả các cổng mạng:** Bất kỳ phần mềm nào chạy ẩn trên server nếu có lỗ hổng bảo mật đều có thể bị khai thác từ xa qua các cổng không được bảo vệ.

Một máy chủ không được bảo mật (unhardened) có thể bị chiếm quyền điều khiển hoặc bị lợi dụng để đào tiền ảo, phát tán thư rác chỉ trong vòng vài giờ sau khi online. Do đó, thiết lập bảo mật hạ tầng là bước đi bắt buộc đầu tiên của mọi kỹ sư DevOps.

<!-- section: core -->
## 3. Kiến thức cốt lõi

### 3.1. Nguyên tắc đặc quyền tối thiểu (Least Privilege)
Trong bảo mật hệ thống, nguyên tắc **đặc quyền tối thiểu** yêu cầu bất kỳ thực thể nào (người dùng, ứng dụng, tiến trình) chỉ được cấp các quyền hạn tối thiểu cần thiết để hoàn thành công việc của mình.
*   *Áp dụng:* Không bao giờ sử dụng tài khoản `root` cho công việc quản trị hàng ngày. Thay vào đó, hãy tạo một tài khoản người dùng thông thường (non-root user), chỉ nâng quyền lên quản trị bằng lệnh `sudo` khi thực sự cần cấu hình hệ thống.

### 3.2. Giảm bề mặt tấn công của dịch vụ SSH (SSH Hardening)
Dịch vụ SSH (mặc định chạy ở cổng 22) là lối vào chính của quản trị viên, đồng thời cũng là mục tiêu tấn công hàng đầu. Để bảo mật SSH, chúng ta cần thay đổi cấu hình trong file `/etc/ssh/sshd_config` với các cơ chế:
*   **Vô hiệu hóa xác thực mật khẩu (`PasswordAuthentication no`):** Bắt buộc chỉ cho phép kết nối bằng khóa SSH (SSH Key). Vì khóa Ed25519 cực kỳ dài và phức tạp, kẻ tấn công hoàn toàn không có khả năng giải mã hay brute-force thành công.
*   **Vô hiệu hóa đăng nhập trực tiếp tài khoản root (`PermitRootLogin no`):** Buộc quản trị viên phải đăng nhập bằng tài khoản non-root trước, sau đó mới dùng lệnh nâng quyền `sudo` để thao tác tiếp. Điều này tạo thêm một lớp bảo vệ vững chắc và giúp ghi lại nhật ký (log) ai đã truy cập hệ thống.

### 3.3. Cơ chế hoạt động của tường lửa (Firewall)
**Tường lửa (Firewall)** là một hệ thống bảo mật mạng có nhiệm vụ giám sát và kiểm soát lưu lượng mạng ra/vào hệ thống dựa trên các quy tắc bảo mật được thiết lập trước.
Tường lửa hoạt động như một người bảo vệ tại cửa khẩu:
*   **Mặc định chặn toàn bộ lưu lượng đi vào (Default Deny Incoming):** Mọi gói tin từ internet gửi tới server sẽ bị chặn đứng, ngoại trừ những cổng dịch vụ được khai báo cho phép rõ ràng.
*   **Mặc định cho phép toàn bộ lưu lượng đi ra (Default Allow Outgoing):** Server có thể tự do kết nối ra ngoài internet để tải bản cập nhật phần mềm hoặc liên kết dịch vụ.
*   **UFW (Uncomplicated Firewall):** Là một công cụ quản lý tường lửa giao diện dòng lệnh đơn giản trên Ubuntu, được xây dựng như một lớp bọc bên ngoài công cụ tường lửa hệ thống `iptables` giúp người dùng dễ cấu hình hơn.

<!-- section: practice -->
## 4. Thực hành và minh hoạ

### Bước 1 — Tạo tài khoản non-root có quyền sudo
Kết nối vào server bằng tài khoản root, sau đó chạy lệnh sau để tạo một user mới tên là `devops`:
```bash
adduser devops
```
*(Hệ thống sẽ yêu cầu thiết lập mật khẩu cho user mới và một số thông tin cá nhân. Hãy đặt mật khẩu đủ mạnh).*

Cấp quyền quản trị (`sudo`) cho user `devops`:
```bash
usermod -aG sudo devops
```

### Bước 2 — Thiết lập SSH Key cho user mới
Để đăng nhập được bằng user `devops` qua SSH Key, học viên phải sao chép Public Key từ tài khoản `root` sang thư mục cá nhân của `devops`.
```bash
# Tạo thư mục lưu khóa SSH cho user devops
mkdir -p /home/devops/.ssh

# Sao chép file chứa các public key đã cấu hình của root sang cho devops
cp /root/.ssh/authorized_keys /home/devops/.ssh/

# Thay đổi quyền sở hữu thư mục và file về cho user devops
chown -R devops:devops /home/devops/.ssh
chmod 700 /home/devops/.ssh
chmod 600 /home/devops/.ssh/authorized_keys
```

Bây giờ, hãy mở một cửa sổ Terminal mới trên máy cá nhân và kiểm tra thử xem có đăng nhập được bằng user `devops` mà không cần mật khẩu hay không:
```bash
ssh devops@<IP_ADDRESS_CỦA_SERVER>
```
Nếu đăng nhập thành công, các học viên đã sẵn sàng chuyển sang bước hardening tiếp theo.

### Bước 3 — Hardening cấu hình SSH Daemon
Mở file cấu hình dịch vụ SSH bằng editor `nano` (cần quyền `sudo`):
```bash
sudo nano /etc/ssh/sshd_config
```
Tìm các dòng cấu hình sau, bỏ dấu thăng `#` ở đầu dòng (nếu có) và sửa giá trị thành `no`:
```text
PermitRootLogin no
PasswordAuthentication no
```
*(Nếu không tìm thấy dòng cấu hình tương ứng, các bạn có thể tự thêm chúng vào cuối file).*

Nhấn **Ctrl + O** và **Enter** để lưu file, nhấn **Ctrl + X** để thoát khỏi editor.

Khởi động lại dịch vụ SSH để áp dụng cấu hình mới:
```bash
sudo systemctl restart ssh
```
> [!IMPORTANT]
> **Tuyệt đối không tắt cửa sổ kết nối SSH hiện tại.** 
> Hãy mở một cửa sổ Terminal mới trên máy cá nhân và thử đăng nhập lại để đảm bảo cấu hình SSH mới hoạt động bình thường. Nếu có lỗi xảy ra, các bạn vẫn còn cửa sổ kết nối cũ để sửa lại cấu hình.

### Bước 4 — Thiết lập tường lửa UFW
Mặc định UFW trên Ubuntu ở trạng thái tắt. Hãy thiết lập các luật (rules) trước khi bật tường lửa lên:

1.  **Thiết lập các luật mặc định:**
    ```bash
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    ```
2.  **Cho phép dịch vụ SSH (cổng 22):**
    ```bash
    sudo ufw allow 22/tcp
    ```
3.  **Kích hoạt tường lửa UFW:**
    ```bash
    sudo ufw enable
    ```
    *(Hệ thống sẽ hiển thị cảnh báo lệnh này có thể làm gián đoạn kết nối SSH hiện tại, hãy gõ `y` và nhấn **Enter**).*
4.  **Kiểm tra trạng thái tường lửa:**
    ```bash
    sudo ufw status verbose
    ```

> **[IMAGE NEEDED]** Mô tả: Kết quả màn hình Terminal sau khi chạy lệnh sudo ufw status hiển thị cổng 22/tcp được ALLOW Incoming.
> Gợi ý path: `assets/ss02/step_04_ufw_status.png`

<!-- section: pitfalls -->
## 5. Lỗi sai thường gặp
*   **Bật UFW khi chưa ALLOW cổng SSH:** Đây là lỗi kinh điển của người mới bắt đầu. Nếu các bạn chạy lệnh `ufw enable` mà quên chạy `ufw allow 22/tcp` (hoặc cổng SSH tùy chỉnh của các bạn), các bạn sẽ ngay lập tức bị đẩy ra khỏi máy chủ và không bao giờ kết nối lại được nữa, buộc phải xóa VPS đi tạo lại hoặc khôi phục qua Web Console của nhà cung cấp.
*   **Hardening SSH mà chưa copy key sang user non-root:** Khi các bạn sửa `PasswordAuthentication no` và `PermitRootLogin no`, học viên chỉ có thể đăng nhập bằng SSH Key thông qua user thường. Nếu các bạn chưa sao chép Public Key vào thư mục `.ssh` của user thường, học viên sẽ hoàn toàn mất quyền truy cập vào máy chủ.
*   **Không chạy thử nghiệm kết nối mới trước khi ngắt kết nối cũ:** Hãy luôn giữ một phiên kết nối SSH hoạt động để làm "phao cứu sinh" đề phòng trường hợp cấu hình mới bị lỗi.

<!-- section: references -->
## 6. Tài liệu tham khảo
*   [Ubuntu Community Help Wiki - UFW](https://help.ubuntu.com/community/UFW)
*   [Mozilla Infosec - OpenSSH Security Guidelines](https://infosec.mozilla.org/guidelines/openssh.html)
*   [Debian Wiki - SSH Hardening](https://wiki.debian.org/SSH)

<!-- companions: sau khi lesson approved → revision `ss02_revision_03` + quiz `ss02_quiz_lesson_03` (get_quiz_plan) -->
