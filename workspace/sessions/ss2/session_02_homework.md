---
schema_version: 1
id: ss02_homework
type: homework
status: approved
course_id: devops-basic
session: 2
unit: 0
title: Homework Session 02
session_kind: theory
tags: []
concepts: []
depends_on: []
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02
language: vi
created: '2026-07-16'
updated: '2026-07-16'
exercise_count: 6
difficulty_mix:
  guided: 4
  hints: 1
  independent: 1
---

# Homework Session 02

### EX1 — Khởi tạo Droplet trên DigitalOcean
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_02]
- **owns_skills:** [digitalocean-droplet-creation]
- **assumes:** [cloud-server-provisioning]

#### Mục tiêu
*   Thực hành đăng ký tài khoản, lựa chọn cấu hình phần cứng phù hợp và khởi tạo thành công Droplet chạy hệ điều hành Ubuntu Server trên hạ tầng đám mây DigitalOcean.
*   Cấu hình xác thực an toàn bằng cặp khóa SSH (SSH Keypair) thay vì mật khẩu thô và thực hiện kết nối thành công từ máy cá nhân.

#### Yêu cầu
*   **Bối cảnh:** Nhóm DevOps của bạn cần tạo một máy chủ thử nghiệm trên hạ tầng đám mây DigitalOcean để chuẩn bị chạy các dự án Web.
*   **Ràng buộc:**
    *   Tạo Droplet chạy hệ điều hành **Ubuntu 22.04 LTS** (hoặc bản mới nhất).
    *   Lựa chọn cấu hình tối giản tiết kiệm chi phí: Basic plan, Regular SSD, CPU Shared (loại rẻ nhất, ví dụ: $4/tháng hoặc $6/tháng).
    *   Chọn datacenter region gần Việt Nam nhất (Singapore).
    *   Tại mục Authentication, bắt buộc chọn **SSH Keys**. Tạo mới một cặp khóa SSH từ máy cá nhân của bạn, thêm khóa công khai (Public Key) vào tài khoản DigitalOcean và gán vào Droplet khi khởi tạo.
    *   Kết nối thành công tới Droplet thông qua SSH từ máy tính cá nhân bằng tài khoản mặc định `root`.

#### Kiểm tra
*   **Lệnh kiểm tra:** Chạy lệnh SSH từ Terminal máy cá nhân:
    ```bash
    ssh -i /path/to/private_key root@<IP_ADDRESS_DROPLET>
    ```
*   **Kết quả mong đợi:** Truy cập thành công vào giao diện dòng lệnh của Droplet mà không cần nhập mật khẩu. Terminal hiển thị thông tin chào mừng của Ubuntu Server.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   Đường dẫn SSH hoạt động bằng SSH Key.
    *   Báo cáo Markdown mô tả các bước tạo Droplet và kết nối thành công.
*   **Yêu cầu không được có:**
    *   Cấm sử dụng tùy chọn mật khẩu thô (Password Authentication) khi khởi tạo Droplet để tránh rủi ro bảo mật brute-force.

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex1/`
*   **Cơ chế nộp:** Học viên viết một file `README.md` lưu trong thư mục bài tập mô tả chi tiết các bước tạo Droplet kèm ảnh chụp giao diện quản lý Droplet trên DigitalOcean Console hoặc đoạn log kết nối thành công từ Terminal.

#### Gợi ý/Bệ đỡ
*   Tạo khóa SSH trên máy cá nhân: `ssh-keygen -t ed25519 -C "your_email@example.com"`
*   Khóa công khai mặc định sẽ nằm ở tệp tin `.pub` (ví dụ: `~/.ssh/id_ed25519.pub`). Copy toàn bộ nội dung file này dán vào DigitalOcean khi được yêu cầu.

---

### EX2 — Khởi tạo User thường và thiết lập đặc quyền quản trị (Sudoers Configuration)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_03]
- **owns_skills:** [linux-user-management]
- **assumes:** [infrastructure-security]

#### Mục tiêu
*   Tạo một tài khoản người dùng thường (Non-root user) trên Ubuntu Server để hạn chế rủi ro khi thao tác trực tiếp bằng quyền root tối cao.
*   Cấp đặc quyền quản trị an toàn cho user thường thông qua nhóm `sudo` và sao chép cấu hình SSH Key để đăng nhập.

#### Yêu cầu
*   **Bối cảnh:** Vận hành hệ thống theo nguyên tắc đặc quyền tối thiểu (Least Privilege), bạn cần tạo tài khoản làm việc riêng có tên là `devops` để thực hiện cấu hình máy chủ hàng ngày thay vì dùng root.
*   **Ràng buộc:**
    *   Tạo tài khoản người dùng mới tên là `devops` trên Droplet.
    *   Thêm user `devops` vào nhóm quản trị `sudo`.
    *   Sao chép cấu hình SSH Key từ thư mục của root sang thư mục home của user `devops` để cho phép tài khoản này đăng nhập được qua SSH.
    *   Phân quyền chính xác cho thư mục `.ssh` và file `authorized_keys` của user `devops` để cơ chế bảo mật SSH hoạt động.

#### Kiểm tra
*   **Lệnh kiểm tra:**
    *   Thực hiện đăng nhập từ máy cá nhân: `ssh -i /path/to/private_key devops@<IP_ADDRESS_DROPLET>` (phải thành công).
    *   Sau khi đăng nhập, chạy lệnh: `sudo whoami` (phải yêu cầu nhập mật khẩu hoặc hiển thị kết quả là `root` thành công).
*   **Kết quả mong đợi:** Đăng nhập thành công và thực thi được lệnh sudo mà không gặp lỗi phân quyền.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   User `devops` tồn tại trên hệ thống và thuộc group `sudo`.
    *   Thư mục `~devops/.ssh` có quyền `700` và file `authorized_keys` có quyền `600`, thuộc sở hữu (owner/group) của user `devops`.
*   **Yêu cầu không được có:**
    *   Không được đổi quyền hoặc sở hữu của các tệp tin trong thư mục của root.
    *   Cấm chia sẻ khóa private key cho người khác.

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex2/`
*   **Cơ chế nộp:** Nộp file báo cáo `README.md` mô tả các lệnh Linux đã chạy để tạo user, copy SSH Key, phân quyền thư mục và log Terminal kiểm tra lệnh `sudo whoami`.

#### Gợi ý/Bệ đỡ
*   Sử dụng lệnh `sudo rsync --archive --chown=devops:devops ~/.ssh /home/devops/` để sao chép thư mục SSH từ root sang user mới một cách an toàn và tự động cập nhật owner.

---

### EX3 — Cài đặt Nginx và cấu hình Website tĩnh cơ bản (Basic Nginx Web Server)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_04]
- **owns_skills:** [nginx-basic-installation]
- **assumes:** [nginx-basic-setup]

#### Mục tiêu
*   Cài đặt dịch vụ Web Server Nginx trên hệ điều hành Ubuntu Server thông qua trình quản lý gói `apt`.
*   Thiết lập một Server Block tùy chỉnh lắng nghe trên cổng mặc định HTTP (`80`) để phục vụ một trang HTML tĩnh của dự án.

#### Yêu cầu
*   **Bối cảnh:** Bạn cần dựng một website giới thiệu đơn giản chạy trên máy chủ Droplet vừa tạo để người dùng ngoài internet truy cập qua IP của máy chủ.
*   **Ràng buộc:**
    *   Cài đặt phiên bản Nginx mới nhất từ repository mặc định của Ubuntu.
    *   Tạo thư mục chứa mã nguồn tĩnh tại đường dẫn `/var/www/web-app/html/` và tạo một file `index.html` đơn giản hiển thị dòng chữ: "Welcome to DevOps Course - Session 02".
    *   Tạo file cấu hình Server Block riêng biệt cho trang web tại `/etc/nginx/sites-available/web-app.conf` cấu hình lắng nghe cổng `80`, trỏ root về thư mục mã nguồn vừa tạo.
    *   Kích hoạt Server Block bằng cách tạo liên kết tượng trưng (symlink) sang thư mục `/etc/nginx/sites-enabled/`.
    *   Xóa hoặc hủy kích hoạt cấu hình trang mặc định `default` của Nginx để tránh xung đột cổng 80.

#### Kiểm tra
*   **Lệnh kiểm tra:**
    *   Chạy kiểm tra cú pháp cấu hình Nginx: `sudo nginx -t` (phải hiển thị `syntax is ok`).
    *   Reload lại Nginx: `sudo systemctl reload nginx`.
    *   Từ máy cá nhân, truy cập trình duyệt bằng địa chỉ IP: `http://<IP_ADDRESS_DROPLET>`.
*   **Kết quả mong đợi:** Trình duyệt hiển thị đúng trang HTML tùy biến đã viết với dòng chữ chào mừng.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   File cấu hình `web-app.conf` chứa đúng chỉ thị `listen 80;` and `root /var/www/web-app/html;`.
    *   Symlink tồn tại chính xác trong thư mục `sites-enabled`.
*   **Yêu cầu không được có:**
    *   Cấm sửa trực tiếp cấu hình trong file `/etc/nginx/nginx.conf`.
    *   Tránh cấu hình sai đường dẫn root dẫn đến lỗi `404 Not Found` hoặc lỗi `403 Forbidden`.

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex3/`
*   **Cơ chế nộp:** Học viên nộp tệp tin cấu hình Nginx `web-app.conf` và file `index.html` lên thư mục bài tập của mình trên GitHub.

#### Gợi ý/Bệ đỡ
*   Sau khi tạo cấu hình, luôn chạy `sudo nginx -t` để kiểm tra lỗi cú pháp trước khi nạp lại cấu hình dịch vụ.

---

### EX4 — Cấu hình tường lửa bảo vệ máy chủ (UFW & Cloud Firewall Integration)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_03]
- **owns_skills:** [firewall-setup]
- **assumes:** [infrastructure-security]

#### Mục tiêu
*   Thiết lập tường lửa UFW (Uncomplicated Firewall) ngay trong hệ điều hành Ubuntu để lọc các gói tin mạng đi vào.
*   Kết hợp cấu hình DigitalOcean Cloud Firewall ở tầng hạ tầng để bảo vệ máy chủ từ biên mạng trước khi gói tin chạm đến Droplet.

#### Yêu cầu
*   **Bối cảnh:** Nhằm tránh máy chủ bị khai thác qua các cổng dịch vụ không sử dụng, bạn cần cấu hình tường lửa 2 lớp để chỉ cho phép lưu lượng SSH và HTTP đi vào Droplet.
*   **Ràng buộc:**
    *   **Lớp 1 (UFW trong OS):** Kích hoạt tường lửa UFW, thiết lập chặn mặc định lưu lượng đi vào (`default deny incoming`), cho phép lưu lượng đi ra ngoài (`default allow outgoing`). Mở cổng `22/tcp` (SSH) và `80/tcp` (HTTP).
    *   **Lớp 2 (DO Cloud Firewall):** Truy cập DigitalOcean Console, tạo một Cloud Firewall mới. Cấu hình Inbound Rules chỉ cho phép: SSH (cổng 22) từ mọi nguồn (hoặc IP của bạn) và HTTP (cổng 80) từ mọi nguồn. Gán Droplet của bạn vào Cloud Firewall này.

#### Kiểm tra
*   **Lệnh kiểm tra:**
    *   Trên Droplet, chạy lệnh: `sudo ufw status verbose` (phải hiển thị trạng thái active và danh sách cổng cho phép).
    *   Từ máy cá nhân, thử kết nối SSH và truy cập HTTP cổng 80 (phải thành công). Thử ping hoặc quét thử một cổng khác không mở (phải bị chặn/timeout).
*   **Kết quả mong đợi:** UFW hiển thị Active, kết nối dịch vụ an toàn, các cổng khác bị chặn hoàn toàn.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   UFW được kích hoạt trong OS.
    *   Ảnh chụp cấu hình Cloud Firewall trên DigitalOcean cho thấy Droplet đã được gán vào.
*   **Yêu cầu không được có:**
    *   Tuyệt đối không được kích hoạt UFW mà quên mở cổng SSH `22/tcp` trước (gây lockout thiết bị).

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex4/`
*   **Cơ chế nộp:** Học viên nộp báo cáo `README.md` kèm ảnh chụp màn hình thiết lập Cloud Firewall trên DigitalOcean Console và đầu ra text của lệnh `sudo ufw status`.

#### Gợi ý/Bệ đỡ
*   Cú pháp nhanh UFW:
    ```bash
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    sudo ufw allow 22/tcp
    sudo ufw allow 80/tcp
    sudo ufw enable
    ```

---

### EX5 — Quản lý quyền sở hữu thư mục Web (Directory Permission Management)
- **tier:** hints
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_03, ss02_lesson_04]
- **owns_skills:** [web-directory-permissions]
- **assumes:** [infrastructure-security]

#### Mục tiêu
*   Hiểu rõ cơ chế phân quyền tệp tin và thư mục (Chown & Chmod) trên Linux.
*   Thiết lập phân quyền tối ưu cho thư mục web tĩnh để user `devops` có thể chỉnh sửa mã nguồn mà không cần dùng quyền `root`/`sudo`, đồng thời dịch vụ Nginx (chạy dưới user `www-data`) vẫn có quyền đọc và hiển thị website.

#### Yêu cầu
*   **Bối cảnh:** Bạn muốn deploy phiên bản mới của website tĩnh, nhưng hiện tại thư mục `/var/www/web-app/` đang thuộc sở hữu của `root`, khiến tài khoản `devops` không thể sửa đổi file trực tiếp.
*   **Ràng buộc:**
    *   Thay đổi chủ sở hữu (owner) của thư mục `/var/www/web-app/` và toàn bộ nội dung bên trong sang user `devops`.
    *   Thay đổi nhóm sở hữu (group) sang nhóm `www-data` (nhóm chạy của Nginx).
    *   Thiết lập quyền truy cập (chmod) sao cho: Chủ sở hữu (`devops`) có quyền đọc và ghi (Read/Write), Nhóm sở hữu (`www-data`) có quyền đọc (Read) để phục vụ web tĩnh, người dùng khác không có quyền truy cập hoặc chỉ được đọc.
    *   Đảm bảo sau khi phân quyền, Nginx không bị lỗi `403 Forbidden` khi truy cập trang web.

#### Kiểm tra
*   **Lệnh kiểm tra:**
    *   Chạy lệnh: `ls -la /var/www/web-app/` để kiểm tra phân quyền.
    *   Đăng nhập bằng user `devops` và thử chạy lệnh chỉnh sửa file: `echo "Update" >> /var/www/web-app/html/index.html` mà không dùng `sudo` (phải ghi thành công).
*   **Kết quả mong đợi:** Ghi file thành công bằng user thường, web hiển thị nội dung mới bình thường mà không bị lỗi Nginx.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   Thư mục và file thuộc sở hữu của `devops:www-data`.
    *   Quyền truy cập thư mục là `755` hoặc `750` và file là `644` hoặc `640`.
*   **Yêu cầu không được có:**
    *   Cấm sử dụng quyền `777` trên bất kỳ file hoặc thư mục nào (đây là lỗ hổng bảo mật nghiêm trọng).

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex5/`
*   **Cơ chế nộp:** Nộp báo cáo `README.md` hiển thị kết quả đầu ra của lệnh `ls -la /var/www/web-app/` và các bước kiểm tra ghi file từ user `devops`.

#### Gợi ý/Bệ đỡ
*   *Gợi ý:* Sử dụng các lệnh `chown -R` và `chmod -R` kết hợp để phân quyền đệ quy cho toàn bộ thư mục web.

---

### EX6 — Thiết lập hạ tầng ứng dụng tĩnh hoàn chỉnh (Production-ready Simple Setup)
- **tier:** independent
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_02, ss02_lesson_03, ss02_lesson_04]
- **owns_skills:** [production-vps-provisioning]
- **assumes:** [cloud-server-provisioning, infrastructure-security, nginx-basic-setup]

#### Mục tiêu
*   Tích hợp toàn bộ kiến thức và kỹ năng đã học trong Session 2 để dựng một máy chủ ảo, phân quyền bảo mật, cài đặt Nginx và thiết lập các lớp tường lửa hoàn chỉnh theo chuẩn thực tế.

#### Yêu cầu
*   **Bối cảnh:** Bạn được giao nhiệm vụ thiết lập một máy chủ Droplet mới trên DigitalOcean để vận hành trang Landing Page chính thức của một dự án cá nhân. Hãy tự thực hiện từ đầu đến cuối các thiết lập hạ tầng.
*   **Ràng buộc:**
    1.  Tạo Droplet mới trên DigitalOcean bằng SSH Key.
    2.  Tạo user quản trị thường tên là `admin-user` thuộc nhóm `sudo`, copy SSH Key để tài khoản này kết nối được.
    3.  Cài đặt Web Server Nginx.
    4.  Tạo thư mục ứng dụng tại `/var/www/landing-page/html/`. Gán sở hữu cho `admin-user:www-data`.
    5.  Tạo file cấu hình Server Block riêng chạy ở cổng `80` mặc định, trỏ root về thư mục trên.
    6.  Kích hoạt Server Block và tắt trang mặc định của Nginx.
    7.  Cấu hình tường lửa UFW và DigitalOcean Cloud Firewall chỉ cho phép kết nối cổng `22` và `80`.

#### Kiểm tra
*   **Lệnh kiểm tra:** Học viên tự thiết kế kịch bản kiểm tra (ví dụ: dùng curl, truy cập trình duyệt, check log, check status dịch vụ) và ghi nhận kết quả.
*   **Kết quả mong đợi:** Tất cả các thành phần hoạt động trơn tru, bảo mật và truy cập thành công website từ internet thông qua IP Droplet.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   File cấu hình Nginx Server Block và file mã nguồn trang Landing Page mẫu.
    *   Tài liệu hướng dẫn (README.md) mô tả toàn bộ vòng đời thiết lập từ Droplet ban đầu cho tới website hoạt động trực tuyến.
*   **Yêu cầu không được có:**
    *   Không để lại các lỗ hổng như cổng SSH mặc định mở kèm Password Authentication, hay thư mục web bị phân quyền `777`.
    *   Không thực hiện các thao tác quản trị trực tiếp từ root sau khi đã tạo `admin-user`.

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex6/`
*   **Cơ chế nộp:** Học viên nộp tệp tin cấu hình Nginx và file báo cáo chi tiết `README.md` lên thư mục bài tập của mình trên GitHub.

#### Gợi ý/Bệ đỡ
*   *Không có gợi ý cấu hình bước thực hiện.* Học viên tự chủ động hệ thống hóa kiến thức để thực hành độc lập bài tập này.
