---
schema_version: 1
id: ss02_homework
type: homework
status: draft
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
created: '2026-07-15'
updated: '2026-07-15'
exercise_count: 6
difficulty_mix:
  guided: 4
  hints: 1
  independent: 1
---

# Homework Session 02

### EX1 — Phân quyền quản trị chi tiết (User & Sudo Management)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_03]
- **owns_skills:** [linux-user-privileges]
- **assumes:** [infrastructure-security]

#### Mục tiêu
*   Tạo người dùng mới và phân quyền hạn sử dụng lệnh quản trị thông qua cấu hình `sudoers`.
*   Phân biệt được quyền thực thi của tài khoản có cấu hình sudo đầy đủ và tài khoản bị giới hạn quyền.

#### Yêu cầu
*   **Bối cảnh:** Nhằm đảm bảo an toàn vận hành, nhóm DevOps cần phân quyền cho một thực tập sinh mới tên là `sys-viewer` chỉ được phép xem các file log của dịch vụ web Nginx mà không được can thiệp vào các hoạt động hệ thống khác.
*   **Ràng buộc:** 
    *   Tạo user `sys-admin` có toàn quyền sudo.
    *   Tạo user `sys-viewer` chỉ được chạy duy nhất lệnh `cat` đối với các tệp tin lưu trong thư mục `/var/log/nginx/` bằng quyền root. Các lệnh sudo khác đều phải bị chặn hoàn toàn.
    *   Không sửa trực tiếp file cấu hình gốc `/etc/sudoers`. Hãy tạo file cấu hình riêng trong `/etc/sudoers.d/`.

#### Kiểm tra
*   **Lệnh kiểm tra:** Đăng nhập vào user `sys-viewer` và thực hiện:
    *   `sudo cat /var/log/nginx/access.log` (phải đọc được nội dung).
    *   `sudo apt update` hoặc `sudo cat /etc/shadow` (phải bị hệ thống báo lỗi cấm chạy).
*   **Kết quả mong đợi:** Lệnh xem log hoạt động bình thường, các lệnh khác hiển thị thông báo *sys-viewer is not allowed to execute...*.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   File cấu hình phân quyền sudoers được đặt tên là `sys-viewer` nằm trong thư mục `/etc/sudoers.d/`.
    *   Nội dung file phải chỉ định đường dẫn tuyệt đối của lệnh `cat` và đường dẫn wildcard giới hạn đối với thư mục log Nginx.
*   **Yêu cầu không được có:**
    *   Cấm cấp quyền cho user `sys-viewer` chạy lệnh `cat` trên toàn bộ hệ thống (ví dụ: cấm dùng `/usr/bin/cat *` hoặc `/usr/bin/cat /etc/*`).
    *   Cấm sửa đổi trực tiếp file gốc `/etc/sudoers`.

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex1/`
*   **Cơ chế nộp:** Học viên nộp tệp tin `sudoers_sys_viewer` (chứa nội dung cấu hình sudoers đã thiết lập) và một file báo cáo Markdown `README.md` mô tả các bước thực hiện kèm đoạn text log kiểm tra thành công/bị từ chối trên Terminal. Hạn chế nộp bằng hình ảnh.

#### Gợi ý/Bệ đỡ
*   Sử dụng lệnh `sudo visudo -f /etc/sudoers.d/sys-viewer` để tạo file cấu hình.
*   Cú pháp phân quyền: `sys-viewer ALL=(root) NOPASSWD: /usr/bin/cat /var/log/nginx/*` (dùng `which cat` để xác định đường dẫn lệnh).

---

### EX2 — Thay đổi cổng kết nối SSH mặc định (Custom SSH Port)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_02, ss02_lesson_03]
- **owns_skills:** [ssh-port-hardening]
- **assumes:** [cloud-server-provisioning, infrastructure-security]

#### Mục tiêu
*   Thay đổi cấu hình cổng lắng nghe mặc định của dịch vụ SSH daemon để giảm thiểu các cuộc tấn công quét cổng tự động từ bên ngoài.
*   Cập nhật cấu hình tường lửa UFW tương ứng để đảm bảo an toàn kết nối.

#### Yêu cầu
*   **Bối cảnh:** Cổng SSH mặc định (22) liên tục bị dò quét bởi mã độc trên internet. Các bạn cần đổi cổng SSH sang một cổng tùy chỉnh an toàn để tăng mức độ bảo mật cho server.
*   **Ràng buộc:** 
    *   Thay đổi cổng lắng nghe của SSH daemon thành cổng `2222`.
    *   Cấu hình tường lửa UFW mở cổng `2222/tcp` và đóng cổng `22/tcp` cũ.
    *   Đảm bảo không bị lockout (mất kết nối hoàn toàn khỏi VPS).

#### Kiểm tra
*   **Lệnh kiểm tra:**
    *   Từ máy cá nhân, thực hiện kết nối: `ssh -p 2222 devops@<IP_ADDRESS>` (phải kết nối thành công).
    *   Thực hiện: `ssh devops@<IP_ADDRESS>` (phải báo lỗi Connection refused).
*   **Kết quả mong đợi:** Đăng nhập thành công qua cổng 2222 bằng khóa SSH Key, không kết nối được qua cổng 22 mặc định.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   File cấu hình `sshd_config` được cập nhật chỉ thị `Port 2222`.
    *   Báo cáo trạng thái tường lửa UFW cho thấy cổng 2222 đã ở trạng thái ALLOW và cổng 22 cũ đã bị xóa.
*   **Yêu cầu không được có:**
    *   Không bật cấu hình Password Authentication (phải giữ nguyên `PasswordAuthentication no`).
    *   Không được tắt tường lửa UFW hoàn toàn để đối phó kết nối.

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex2/`
*   **Cơ chế nộp:** Học viên nộp tệp tin báo cáo `report.md` chứa nội dung dòng cấu hình đã thay đổi trong `/etc/ssh/sshd_config` và đầu ra dạng văn bản của lệnh `sudo ufw status`. Không chấp nhận nộp bằng ảnh chụp màn hình.

#### Gợi ý/Bệ đỡ
*   Luôn mở cổng `2222/tcp` trên UFW (`sudo ufw allow 2222/tcp`) trước khi khởi động lại dịch vụ SSH (`sudo systemctl restart ssh`).
*   Không được tắt cửa sổ Terminal đang cấu hình cho đến khi đăng nhập thử thành công trên một cửa sổ Terminal mới.

---

### EX3 — Cấu hình chạy song song nhiều Web Port trên Nginx
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_04]
- **owns_skills:** [nginx-multi-port]
- **assumes:** [nginx-basic-setup]

#### Mục tiêu
*   Cấu hình chạy đồng thời nhiều website tĩnh khác nhau trên cùng một dịch vụ Nginx bằng cách phân biệt theo cổng kết nối (Port-based Virtual Hosts).
*   Cấu hình tường lửa UFW tương ứng để mở các cổng tùy chỉnh đó.

#### Yêu cầu
*   **Bối cảnh:** Phòng máy của PTIT cần chạy thử nghiệm 2 phiên bản giao diện web tĩnh khác nhau trên cùng một máy chủ ảo mà chưa có tên miền riêng.
*   **Ràng buộc:** 
    *   Trang web thứ nhất (`site-one`) đặt tại `/var/www/site-one/html`, lắng nghe ở cổng `8080`.
    *   Trang web thứ hai (`site-two`) đặt tại `/var/www/site-two/html`, lắng nghe ở cổng `8090`.
    *   Tường lửa UFW phải mở cổng `8080/tcp` và `8090/tcp`.

#### Kiểm tra
*   **Lệnh kiểm tra:** Sử dụng công cụ `curl` cục bộ hoặc truy cập trình duyệt:
    *   `curl http://localhost:8080` (trả về nội dung trang 1).
    *   `curl http://localhost:8090` (trả về nội dung trang 2).
*   **Kết quả mong đợi:** Cả hai website đều hiển thị nội dung html tương ứng của chúng.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   2 file cấu hình Server Block riêng biệt trong thư mục `/etc/nginx/sites-available/` và được kích hoạt bằng symlink sang `/etc/nginx/sites-enabled/`.
    *   Chỉ thị `listen` chỉ định chính xác cổng `8080` và `8090`.
*   **Yêu cầu không được có:**
    *   Cấm viết gộp chung 2 block `server` vào một file cấu hình duy nhất để đảm bảo tính module hóa.
    *   Cấm sửa đổi trực tiếp vào file cấu hình gốc `/etc/nginx/nginx.conf`.

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex3/`
*   **Cơ chế nộp:** Học viên nộp 2 file cấu hình Server Block (đặt tên là `site-one.conf` và `site-two.conf`) lên thư mục nộp bài trên GitHub.

#### Gợi ý/Bệ đỡ
*   Nhớ cấp quyền sở hữu thư mục chứa mã nguồn tĩnh bằng lệnh `chown` để tránh lỗi 403.
*   Sau khi tạo file cấu hình, chạy `sudo ln -s` để tạo liên kết tượng trưng kích hoạt cấu hình.

---

### EX4 — Cấu hình tùy biến trang báo lỗi (Custom Error Page 404)
- **tier:** guided
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_04]
- **owns_skills:** [nginx-custom-error-pages]
- **assumes:** [nginx-basic-setup]

#### Mục tiêu
*   Tối ưu trải nghiệm người dùng bằng cách cấu hình Nginx tự động chuyển hướng các yêu cầu truy cập file không tồn tại (Lỗi 404 Not Found) về một trang giao diện HTML tùy biến thân thiện.

#### Yêu cầu
*   **Bối cảnh:** Thay vì hiển thị trang báo lỗi trắng mặc định khô khan của Nginx khi người dùng nhập sai đường dẫn, các bạn cần thiết lập một trang báo lỗi mang thương hiệu riêng.
*   **Ràng buộc:** 
    *   Tạo file giao diện lỗi `custom_404.html` đặt trong thư mục gốc của website.
    *   Cấu hình Server Block để tự động chuyển hướng các mã lỗi 404 về file này.
    *   Chỉ cho phép file `custom_404.html` được nạp nội bộ bởi Nginx (`internal;`), không cho phép người dùng truy cập trực tiếp file này bằng URL `http://<IP>/custom_404.html`.

#### Kiểm tra
*   **Lệnh kiểm tra:** Sử dụng lệnh `curl -I http://localhost/duong-dan-khong-ton-tai` hoặc truy cập trình duyệt.
*   **Kết quả mong đợi:** Đầu ra hiển thị mã HTTP 404 nhưng nội dung HTML hiển thị trang tùy biến `custom_404.html`.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   Đoạn cấu hình `error_page 404 /custom_404.html;` và block `location = /custom_404.html` có chứa chỉ thị `internal;`.
    *   File `custom_404.html` thực tế tồn tại trong thư mục gốc.
*   **Yêu cầu không được có:**
    *   Tránh cấu hình chuyển hướng làm thay đổi mã trạng thái HTTP từ 404 về 200 (vì điều này sẽ gây sai lệch dữ liệu SEO của website).

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex4/`
*   **Cơ chế nộp:** Nộp file cấu hình Server Block đã cập nhật và nội dung file mã nguồn `custom_404.html` lên thư mục bài tập của các bạn trên GitHub.

#### Gợi ý/Bệ đỡ
*   Cấu hình mẫu:
   ```nginx
   error_page 404 /custom_404.html;
   location = /custom_404.html {
       root /var/www/ptit-app/html;
       internal;
   }
   ```

---

### EX5 — Đặt mật khẩu bảo vệ thư mục nhạy cảm (Nginx Basic Authentication)
- **tier:** hints
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_04]
- **owns_skills:** [nginx-basic-auth]
- **assumes:** [nginx-basic-setup]

#### Mục tiêu
*   Thiết lập cơ chế bảo mật xác thực cơ bản (HTTP Basic Authentication) bằng mật khẩu để bảo vệ một đường dẫn thư mục nhạy cảm trên website chống truy cập tự do từ internet.

#### Yêu cầu
*   **Bối cảnh:** Trang web của các bạn có một thư mục quản trị nội bộ tên là `/admin/` chứa các thông tin nhạy cảm. Các bạn cần cấu hình Nginx yêu cầu nhập đúng tài khoản và mật khẩu mới cho phép truy cập.
*   **Ràng buộc:** 
    *   Cài đặt công cụ mã hóa mật khẩu và tạo file lưu thông tin tài khoản `/etc/nginx/.htpasswd`.
    *   Khởi tạo tài khoản quản trị có tên đăng nhập là `admin`.
    *   Cấu hình Nginx yêu cầu xác thực đối với duy nhất thư mục `/admin/` trên website, các trang khác vẫn cho phép truy cập công cộng tự do.

#### Kiểm tra
*   **Lệnh kiểm tra:** Sử dụng lệnh `curl -I http://localhost/admin/`.
*   **Kết quả mong đợi:** Đầu ra trả về mã trạng thái HTTP `401 Unauthorized` yêu cầu xác thực. Khi kết nối qua trình duyệt, xuất hiện hộp thoại đăng nhập.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   File chứa thông tin mật khẩu được bảo mật ẩn tại `/etc/nginx/.htpasswd` (nội dung mật khẩu phải được băm/mã hóa, không để dạng plain-text).
    *   Block `location /admin` hoặc `location /admin/` chứa các chỉ thị `auth_basic` và `auth_basic_user_file`.
*   **Yêu cầu không được có:**
    *   Cấm đặt file `.htpasswd` bên trong thư mục root của website (để tránh người dùng tải trực tiếp file mật khẩu này về).

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex5/`
*   **Cơ chế nộp:** Nộp file cấu hình Server Block và tệp tin `.htpasswd` (đã được thay đổi/xóa mật khẩu thực tế bằng mật khẩu demo như `admin:admin` để đảm bảo an toàn thông tin) lên thư mục bài tập trên GitHub.

#### Gợi ý/Bệ đỡ
*   Cài đặt gói hỗ trợ tạo mật khẩu bằng lệnh: `sudo apt install apache2-utils -y`.
*   Sử dụng lệnh `sudo htpasswd -c /etc/nginx/.htpasswd admin` để tạo tài khoản mới.

---

### EX6 — Thiết lập môi trường triển khai tối giản (Production-ready Site Setup)
- **tier:** independent
- **maps_to_sessions:** [2]
- **maps_to_lessons:** [ss02_lesson_02, ss02_lesson_03, ss02_lesson_04]
- **owns_skills:** [nginx-production-setup]
- **assumes:** [cloud-server-provisioning, infrastructure-security, nginx-basic-setup]

#### Mục tiêu
*   Tích hợp toàn bộ các kỹ năng đã học để thiết lập một môi trường triển khai ứng dụng thực tế đáp ứng các ràng buộc khắt khe về cấu trúc thư mục, cổng kết nối, ghi log và bảo mật tường lửa.

#### Yêu cầu
*   **Bối cảnh:** Các bạn được bàn giao một server mới và yêu cầu thiết lập hoàn chỉnh hạ tầng chạy trang web theo cấu hình đóng gói tối ưu để bàn giao cho đội vận hành.
*   **Ràng buộc:** 
    1.  Mã nguồn ứng dụng nằm tại thư mục `/opt/my-app/html/`. Cấp quyền sở hữu cho user `devops`.
    2.  Nginx lắng nghe và phục vụ ứng dụng tại cổng **`9000`**.
    3.  Tường lửa UFW chặn hoàn toàn cổng `80` và `443` thông thường, chỉ mở cổng SSH tùy chỉnh ở EX2 (hoặc 22 mặc định) và cổng dịch vụ web `9000`.
    4.  Cấu hình ghi nhật ký truy cập (access log) của website này ra một file riêng đặt tại đường dẫn `/var/log/nginx/my-app.access.log`.

#### Kiểm tra
*   **Lệnh kiểm tra:**
    *   Thực hiện truy cập `curl http://localhost:9000` (phải trả về HTML).
    *   Refresh trình duyệt kết nối cổng 9000 và chạy lệnh `tail -f /var/log/nginx/my-app.access.log` xem log ghi nhận real-time.
*   **Kết quả mong đợi:** Website hoạt động bình thường ở cổng 9000, các kết nối vào cổng 80 bị UFW chặn (Connection Timeout), log truy cập được ghi nhận đúng file cấu hình riêng.

#### Tiêu chí chấm
*   **Yêu cầu phải có:**
    *   File cấu hình Server Block hoàn chỉnh chứa chỉ thị `access_log /var/log/nginx/my-app.access.log;`.
    *   Thư mục `/opt/my-app/html/` có phân quyền cho phép user `www-data` hoặc nhóm sở hữu tương ứng đọc file.
    *   Bảng trạng thái UFW chứng minh chỉ mở cổng SSH và cổng 9000.
*   **Yêu cầu không được có:**
    *   Cấm ghi log truy cập chung vào file hệ thống mặc định `/var/log/nginx/access.log`.

#### Hướng dẫn nộp bài
*   **Đường dẫn trên GitHub:** `homework/session_02/ex6/`
*   **Cơ chế nộp:** Học viên nộp file cấu hình Server Block hoàn chỉnh (`my-app.conf`) và một file báo cáo Markdown `README.md` trình bày chi tiết cấu trúc, các lệnh UFW đã chạy, cấu hình log và kết quả xác thực bằng text.

#### Gợi ý/Bệ đỡ
*   *Không có gợi ý cấu hình bước thực hiện.* Học viên tự nghiên cứu tài liệu chính thức của Nginx và UFW để hoàn thành.
