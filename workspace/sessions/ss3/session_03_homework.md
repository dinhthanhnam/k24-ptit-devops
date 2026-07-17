---
schema_version: 1
id: ss03_homework
type: homework
status: draft
course_id: devops-basic
session: 3
unit: 0
title: "Bài tập thực hành Virtual Private Server (VPS) nâng cao"
session_kind: practice
practice_of: [2]
maps_to_sessions: [2]
exercise_count: 6
difficulty_mix:
  guided: 4
  hints: 1
  independent: 1
depends_on:
  - ss02_homework
  - ss02_lesson_01
  - ss02_lesson_02
  - ss02_lesson_03
  - ss02_lesson_04
builds_on: []
enables: []
owns: []
assumes:
  - virtualization-basics
  - cloud-server-provisioning
  - infrastructure-security
  - nginx-basic-setup
does_not_cover:
  - vps-deploy
source: generated
pm_ref: "Session 03"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
---

# Bài tập thực hành Virtual Private Server (VPS) nâng cao

Buổi thực hành ôn tập này giúp các học viên củng cố kiến thức về quản lý hạ tầng ảo hóa, gia tăng mức độ bảo mật cho hệ thống máy chủ (Hardening), cấu hình nâng cao dịch vụ Web Server Nginx và làm quen với các kỹ năng quản trị hệ thống thực tế.

---

### EX1 — Thay đổi cổng kết nối SSH (SSH Port Hardening)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_03]
- **owns_skills:** [ssh-port-hardening]
- **assumes:** [infrastructure-security]

#### Mục tiêu
* Thay đổi cổng dịch vụ SSH mặc định từ `22` sang `2222` trên máy chủ ảo nhằm hạn chế tối đa các cuộc quét cổng tự động của botnet trên mạng internet.
* Thực hiện cấu hình tường lửa UFW trước khi khởi động lại dịch vụ để tránh nguy cơ bị khóa quyền truy cập (Lockout).

#### Yêu cầu
* **Bối cảnh:** Ngay khi máy chủ ảo được khởi tạo, cổng 22 liên tục bị brute-force. Học viên quyết định thay đổi cổng truy cập SSH sang cổng `2222` để gia tăng bảo mật.
* **Ràng buộc:**
  * Thực hiện thay đổi chỉ thị cổng kết nối sang `Port 2222` trong tệp cấu hình hệ thống `/etc/ssh/sshd_config` (hoặc tệp tin cấu hình drop-in tương ứng).
  * Sử dụng tường lửa UFW trong OS để mở cổng `2222/tcp` **trước khi** khởi động lại dịch vụ SSH daemon.
  * Chỉ thực hiện thao tác bằng tài khoản người dùng thường `devops` có quyền `sudo`, không sử dụng tài khoản `root` trực tiếp.

#### Kiểm tra
* **Lệnh kiểm tra:**
  * Từ máy tính cá nhân, chạy lệnh kiểm tra kết nối qua cổng mới:
    ```bash
    ssh -p 2222 devops@<IP_ADDRESS_DROPLET>
    ```
  * Chạy lệnh kiểm tra kết nối qua cổng mặc định cũ:
    ```bash
    ssh -p 22 devops@<IP_ADDRESS_DROPLET>
    ```
* **Kết quả mong đợi:**
  * Kết nối thành công qua cổng `2222` bằng SSH Key.
  * Kết nối qua cổng `22` bị chặn hoàn toàn (báo lỗi Connection refused hoặc Timeout).

#### Tiêu chí chấm
* **Yêu cầu phải có:**
  * Minh chứng tệp tin cấu hình `/etc/ssh/sshd_config` đã được chỉnh sửa đúng chỉ thị.
  * Lệnh `sudo ufw status` hiển thị cổng `2222/tcp` ở trạng thái `ALLOW`.
  * Log Terminal hoặc ảnh chụp kết nối thành công qua cổng `2222` và bị từ chối ở cổng `22`.
* **Yêu cầu không được có:**
  * Tuyệt đối không được tắt phiên làm việc SSH hiện tại khi chưa kiểm tra thành công kết nối mới trên Terminal khác để tránh lockout thiết bị.
  * Cấm mở cổng 22 khi đã chuyển đổi sang cổng 2222.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_03/ex1/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` mô tả các bước thực hiện cấu hình kèm theo đoạn trích xuất log terminal chứng minh.

#### Gợi ý/Bệ đỡ
1. Sử dụng lệnh `sudo nano /etc/ssh/sshd_config` để chỉnh sửa file. Tìm dòng `#Port 22` hoặc `Port 22`, sửa lại thành `Port 2222`.
2. Cho phép UFW mở cổng mới: `sudo ufw allow 2222/tcp`.
3. Khởi động lại dịch vụ SSH để áp dụng: `sudo systemctl restart ssh` (hoặc `sudo systemctl restart sshd`).
4. **Không tắt cửa sổ Terminal hiện tại.** Mở một Terminal mới trên máy cá nhân và chạy lệnh `ssh -p 2222 devops@<IP>` để test thử.

---

### EX2 — Cấu hình trang lỗi tùy chỉnh (Custom Error Page 404)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_04]
- **owns_skills:** [nginx-custom-error-pages]
- **assumes:** [nginx-basic-setup]

#### Mục tiêu
* Cấu hình dịch vụ Web Server Nginx để phục vụ một trang lỗi 404 (Not Found) tự thiết kế thay cho trang báo lỗi mặc định đơn điệu của hệ thống.
* Bảo mật tệp tin HTML báo lỗi bằng chỉ thị `internal` của Nginx để ngăn người dùng truy cập trực tiếp vào tệp nguồn này.

#### Yêu cầu
* **Bối cảnh:** Trang web chính thức của học viên cần hiển thị một giao diện lỗi thân thiện khi người dùng gõ sai đường dẫn tĩnh trên trình duyệt.
* **Ràng buộc:**
  * Tạo tệp tin `404.html` chứa mã HTML tùy biến (hiển thị thông điệp báo lỗi tùy biến) lưu trong thư mục web root `/var/www/my-web/html/`.
  * Cấu hình Server Block của Nginx sử dụng chỉ thị `error_page 404 /404.html;`.
  * Thiết lập block `location = /404.html { internal; }` trỏ root chính xác và ngăn chặn người dùng từ internet truy cập trực tiếp bằng URL `http://<IP>/404.html`.

#### Kiểm tra
* **Lệnh kiểm tra:**
  * Sử dụng trình duyệt hoặc curl truy cập một đường dẫn không tồn tại:
    ```bash
    curl -I http://<IP_ADDRESS_DROPLET>/invalid-path-demo
    ```
  * Sử dụng curl truy cập trực tiếp tệp tin lỗi:
    ```bash
    curl -I http://<IP_ADDRESS_DROPLET>/404.html
    ```
* **Kết quả mong đợi:**
  * Truy cập đường dẫn lỗi trả về mã trạng thái `404 Not Found` kèm nội dung trang HTML tùy biến.
  * Truy cập trực tiếp đường dẫn `/404.html` trả về mã trạng thái `404 Not Found` (do cơ chế `internal` của Nginx chặn truy cập trực tiếp).

#### Tiêu chí chấm
* **Yêu cầu phải có:**
  * Tệp cấu hình Server Block Nginx chứa đúng cú pháp chỉ thị `error_page` và cấu hình location tương ứng.
  * Tệp tin `404.html` hoạt động tốt.
* **Yêu cầu không được có:**
  * Cấm sửa đổi trực tiếp tệp tin cấu hình gốc `/etc/nginx/nginx.conf`.
  * Không để lộ nội dung file `404.html` khi truy cập trực tiếp qua URL.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_03/ex2/`
* **Cơ chế nộp:** Học viên nộp tệp tin `404.html` và file cấu hình Server Block Nginx đã được chỉnh sửa lên GitHub.

#### Gợi ý/Bệ đỡ
* Khai báo trong Server Block:
  ```nginx
  error_page 404 /404.html;

  location = /404.html {
      root /var/www/my-web/html;
      internal;
  }
  ```
* Nhớ kiểm tra cú pháp bằng `sudo nginx -t` trước khi chạy `sudo systemctl reload nginx`.

---

### EX3 — Bảo mật tài nguyên bằng HTTP Basic Authentication
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_03, ss02_lesson_04]
- **owns_skills:** [http-basic-auth]
- **assumes:** [infrastructure-security, nginx-basic-setup]

#### Mục tiêu
* Cài đặt và sử dụng công cụ băm mật khẩu để bảo vệ một đường dẫn hoặc thư mục nhạy cảm trên Web Server.
* Cấu hình Nginx yêu cầu xác thực tài khoản/mật khẩu trực tiếp trên trình duyệt bằng cơ chế HTTP Basic Authentication.

#### Yêu cầu
* **Bối cảnh:** Trang web có một thư mục quản trị nội bộ `/admin` chứa thông tin nhạy cảm. Bạn cần thiết lập lớp mật khẩu bảo vệ để ngăn chặn người ngoài truy cập trái phép.
* **Ràng buộc:**
  * Cài đặt gói công cụ `apache2-utils` để lấy tiện ích sinh mật khẩu băm.
  * Tạo tệp mật khẩu ẩn `.htpasswd` lưu trữ tại thư mục `/etc/nginx/` (không được đặt trong thư mục chứa mã nguồn tĩnh `/var/www/` để tránh nguy cơ rò rỉ file mật khẩu).
  * Tạo tài khoản quản trị tên là `admin_user` và băm mật khẩu lưu vào file `.htpasswd`.
  * Cấu hình block `location /admin` trong file Server Block Nginx yêu cầu xác thực Basic Auth trỏ tới file `.htpasswd` vừa tạo.

#### Kiểm tra
* **Lệnh kiểm tra:**
  * Sử dụng curl gửi request tới thư mục quản trị:
    ```bash
    curl -I http://<IP_ADDRESS_DROPLET>/admin
    ```
  * Sử dụng curl kèm thông tin tài khoản hợp lệ:
    ```bash
    curl -u admin_user:<PASSWORD> http://<IP_ADDRESS_DROPLET>/admin
    ```
* **Kết quả mong đợi:**
  * Request thông thường trả về mã trạng thái HTTP `401 Unauthorized` và tiêu đề `WWW-Authenticate`.
  * Request kèm thông tin đăng nhập đúng trả về mã trạng thái HTTP `200 OK` (hoặc `404 Not Found` nếu chưa có file index bên trong, nhưng không được trả về 401).

#### Tiêu chí chấm
* **Yêu cầu phải có:**
  * Tệp cấu hình Server Block Nginx có định nghĩa `location /admin` với các chỉ thị `auth_basic`.
  * File `.htpasswd` được tạo thành công tại `/etc/nginx/.htpasswd` (nộp file mẫu thay thế hash thật bằng dummy hash lên git).
* **Yêu cầu không được có:**
  * Không lưu trữ tệp tin `.htpasswd` trong thư mục công khai của Web Server (như `/var/www/...`).

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_03/ex3/`
* **Cơ chế nộp:** Nộp file cấu hình Nginx Server Block và file `.htpasswd` mẫu lên thư mục bài tập.

#### Gợi ý/Bệ đỡ
1. Cài đặt công cụ băm: `sudo apt install apache2-utils -y`
2. Tạo file mật khẩu: `sudo htpasswd -c /etc/nginx/.htpasswd admin_user` (Hệ thống sẽ hỏi mật khẩu, hãy nhập mật khẩu bảo mật của bạn).
3. Cấu hình Nginx:
   ```nginx
   location /admin {
       auth_basic "Restricted Admin Area";
       auth_basic_user_file /etc/nginx/.htpasswd;
       try_files $uri $uri/ =404;
   }
   ```

---

### EX4 — Chạy song song nhiều cổng dịch vụ (Nginx Virtual Hosts)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_04]
- **owns_skills:** [nginx-multi-port-virtual-hosts]
- **assumes:** [nginx-basic-setup]

#### Mục tiêu
* Cấu hình Nginx chạy song song hai trang web tĩnh độc lập trên cùng một địa chỉ IP máy chủ ảo thông qua việc phân chia cổng dịch vụ (`8080` và `8090`).
* Thiết lập tường lửa UFW và Cloud Firewall mở cổng tương ứng để người dùng ngoài internet truy cập được.

#### Yêu cầu
* **Bối cảnh:** Học viên cần triển khai hai môi trường thử nghiệm độc lập: trang kiểm thử ứng dụng (Beta App) và trang thông tin nội bộ (Internal App) chạy song song trên cùng một Droplet.
* **Ràng buộc:**
  * Tạo hai thư mục lưu trữ mã nguồn riêng biệt: `/var/www/beta-app/html/` và `/var/www/internal-app/html/`. Mỗi thư mục chứa một file `index.html` có tiêu đề tương ứng.
  * Cấu hình Server Block của Nginx lắng nghe trên cổng `8080` trỏ root về thư mục beta-app.
  * Cấu hình Server Block thứ hai lắng nghe trên cổng `8090` trỏ root về thư mục internal-app.
  * Mở các cổng `8080` và `8090` trên tường lửa UFW và trên DigitalOcean Cloud Firewall.

#### Kiểm tra
* **Lệnh kiểm tra:**
  * Sử dụng trình duyệt hoặc curl truy cập các cổng:
    ```bash
    curl http://<IP_ADDRESS_DROPLET>:8080
    curl http://<IP_ADDRESS_DROPLET>:8090
    ```
* **Kết quả mong đợi:**
  * Cổng `8080` trả về đúng giao diện trang Beta App.
  * Cổng `8090` trả về đúng giao diện trang Internal App.

#### Tiêu chí chấm
* **Yêu cầu phải có:**
  * File cấu hình Nginx Server Blocks định nghĩa các cổng lắng nghe `8080` và `8090`.
  * Các trang HTML tĩnh hiển thị đúng nội dung yêu cầu.
  * Trạng thái UFW hiển thị mở thành công các cổng `8080/tcp` và `8090/tcp`.
* **Yêu cầu không được có:**
  * Cấm sử dụng chung một thư mục root cho cả hai cổng dịch vụ.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_03/ex4/`
* **Cơ chế nộp:** Nộp các tệp cấu hình Nginx và các file `index.html` tương ứng lên GitHub.

#### Gợi ý/Bệ đỡ
* Các bạn có thể tạo một file cấu hình duy nhất `/etc/nginx/sites-available/multi-port.conf` chứa cả hai block `server { ... }` riêng biệt để dễ quản lý.
* Đừng quên bật luật cho UFW: `sudo ufw allow 8080/tcp` và `sudo ufw allow 8090/tcp`.

---

### EX5 — Thiết lập thư mục Web an toàn tại phân vùng hệ thống (`/opt/`)
- **tier:** hints
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_03, ss02_lesson_04]
- **owns_skills:** [opt-directory-web-hosting]
- **assumes:** [infrastructure-security, nginx-basic-setup]

#### Mục tiêu
* Chuyển vị trí lưu trữ website tĩnh và logs ra khỏi các đường dẫn mặc định của hệ thống sang phân vùng `/opt/` (thư mục tùy chọn cho các phần mềm add-on) để cô lập mã nguồn.
* Thực hiện phân quyền tệp tin và thư mục nâng cao đảm bảo bảo mật và phân tách vai trò rõ ràng giữa tài khoản quản trị thường (`devops`) và tiến trình chạy của Nginx (`www-data`).

#### Yêu cầu
* **Bối cảnh:** Để chuẩn bị chạy môi trường Production thực tế, doanh nghiệp yêu cầu cô lập hoàn toàn mã nguồn web và cấu hình logs của dự án ra khỏi phân vùng mặc định của hệ điều hành.
* **Ràng buộc:**
  * Di chuyển hoặc tạo mới thư mục chứa mã nguồn tại đường dẫn `/opt/my-app/html/`.
  * Tạo thư mục lưu trữ logs riêng tại `/opt/my-app/logs/`.
  * Phân quyền sở hữu đệ quy cho toàn bộ thư mục `/opt/my-app/` thuộc về user `devops` và group `www-data`.
  * Cấu hình phân quyền truy cập: User `devops` có toàn quyền đọc/ghi (`750` hoặc `755` đối với thư mục, `640` || `644` đối với tệp tin). Group `www-data` có quyền đọc và thực thi trên thư mục web tĩnh, đồng thời có quyền ghi vào thư mục `/opt/my-app/logs/` để ghi nhận logs.
  * Cấu hình Server Block của Nginx ghi log truy cập (`access_log`) và log lỗi (`error_log`) trực tiếp vào đường dẫn log mới này.

#### Kiểm tra
* **Lệnh kiểm tra:**
  * Trên máy chủ, chạy lệnh kiểm tra phân quyền:
    ```bash
    ls -la /opt/my-app/
    ```
  * Ghi thử file bằng user `devops` không dùng `sudo`:
    ```bash
    echo "Update Test" >> /opt/my-app/html/index.html
    ```
  * Kiểm tra nội dung logs phát sinh sau khi truy cập:
    ```bash
    tail -f /opt/my-app/logs/access.log
    ```
* **Kết quả mong đợi:**
  * Thư mục thuộc sở hữu chính xác của `devops:www-data`.
  * Ghi file thành công bằng user thường mà không cần nâng quyền root.
  * Nginx hoạt động bình thường (không lỗi 403) và tự động ghi log vào tệp tin chỉ định.

#### Tiêu chí chấm
* **Yêu cầu phải có:**
  * File cấu hình Nginx Server Block cấu hình đúng root và đường dẫn logs mới.
  * Quyền hạn thư mục logs cho phép Nginx ghi nhận dữ liệu thành công.
* **Yêu cầu không được có:**
  * Cấm phân quyền dạng `777` (cho phép bất kỳ ai ghi đè dữ liệu) trên thư mục web và logs.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_03/ex5/`
* **Cơ chế nộp:** Nộp tệp tin cấu hình Nginx và file báo cáo README.md hiển thị log kiểm tra và trạng thái phân quyền.

#### Gợi ý/Bệ đỡ
* *Gợi ý:* Để Nginx ghi được logs vào thư mục `/opt/my-app/logs/`, group `www-data` cần được cấp quyền ghi (`write`) đối với thư mục `logs/` đó (ví dụ: `chmod 775 /opt/my-app/logs/` hoặc phân quyền sở hữu thư mục logs cho `www-data:www-data`).

---

### EX6 — Tích hợp hệ thống phân quyền, bảo mật và đa cổng dịch vụ
- **tier:** independent
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_02, ss02_lesson_03, ss02_lesson_04]
- **owns_skills:** [production-ready-vps-integration]
- **assumes:** [cloud-server-provisioning, infrastructure-security, nginx-basic-setup]

#### Mục tiêu
* Tích hợp toàn bộ các kỹ năng đã thực hành: tự động hóa thiết lập máy chủ ảo, hardening bảo mật, thay đổi cổng SSH mặc định, thiết lập tường lửa 2 lớp, cài đặt Nginx chạy đa cổng và bảo vệ tài nguyên tĩnh bằng HTTP Basic Auth.

#### Yêu cầu
* **Bối cảnh:** Bạn được giao thiết kế và triển khai từ đầu một hạ tầng VPS chạy thử nghiệm sản phẩm an toàn cho dự án cá nhân. Hãy tự thực hiện và cấu hình hệ thống theo các tiêu chuẩn kỹ thuật khắt khe.
* **Ràng buộc:**
  1. Khởi tạo một Droplet mới trên DigitalOcean bằng SSH Key.
  2. Tạo user quản trị thường tên là `admin-user` thuộc nhóm `sudo`, cấp quyền SSH Key để đăng nhập.
  3. Cấu hình đổi cổng kết nối SSH daemon sang cổng tùy chọn `2222`.
  4. Cấu hình tường lửa UFW và Cloud Firewall chỉ cho phép kết nối đi vào đối với các cổng: `2222/tcp` (SSH), `80/tcp` (HTTP) và `8080/tcp` (Quản trị). Chặn toàn bộ các cổng khác.
  5. Cấu hình Nginx chạy song song 2 Server Blocks:
     * Cổng `80` trỏ root về `/opt/app/main/html/` (Website chính của doanh nghiệp).
     * Cổng `8080` trỏ root về `/opt/app/admin/html/` (Trang quản lý nội bộ).
  6. Trang quản lý nội bộ chạy cổng `8080` bắt buộc phải được bảo mật bằng HTTP Basic Authentication.
  7. Cả hai website đều phải cấu hình trang báo lỗi `404.html` tùy biến riêng biệt và cấu hình ghi logs riêng biệt vào `/opt/app/main/logs/` và `/opt/app/admin/logs/`.
  8. Mọi thao tác deploy file, reload dịch vụ Nginx phải do user `admin-user` thực hiện, không sử dụng tài khoản root.

#### Kiểm tra
* **Lệnh kiểm tra:** Học viên tự xây dựng kịch bản kiểm tra toàn diện hệ thống từ máy cá nhân và cung cấp đầy đủ các minh chứng cụ thể.
* **Kết quả mong đợi:** Hệ thống chạy trơn tru, an toàn, phân tách cổng và quyền hạn chính xác.

#### Tiêu chí chấm
* **Yêu cầu phải có:**
  * Bộ tệp tin cấu hình Nginx Server Blocks.
  * File báo cáo `README.md` mô tả kiến trúc hệ thống, chi tiết các lệnh cấu hình đã chạy và hình ảnh/logs chứng minh toàn bộ các yêu cầu của bài toán đã hoạt động tốt.
* **Yêu cầu không được có:**
  * Không để lộ cổng 22 mở, không dùng Password Authentication.
  * Cấm phân quyền thư mục web tĩnh dạng 777.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_03/ex6/`
* **Cơ chế nộp:** Học viên nộp bộ file cấu hình và file báo cáo README.md lên thư mục bài tập của mình trên GitHub.

#### Gợi ý/Bệ đỡ
* **Không có gợi ý cấu hình chi tiết.** Học viên tự chủ động hệ thống hóa kiến thức để thực hành độc lập hoàn toàn bài tập này.
