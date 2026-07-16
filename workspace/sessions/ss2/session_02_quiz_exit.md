---
schema_version: 1
id: ss02_quiz_exit
type: quiz
status: approved
course_id: devops-basic
session: 2
unit: 0
title: Quiz cuối giờ Session 02
session_kind: theory
tags: []
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
pm_ref: Session 02 / quiz_exit
language: vi
created: '2026-07-15'
updated: '2026-07-16'
quiz_kind: exit
question_count: 30
maps_to:
- ss02_lesson_01
- ss02_lesson_02
- ss02_lesson_03
- ss02_lesson_04
---

# Quiz cuối giờ Session 02

## Q1
Trong các cấu hình dưới đây của Nginx Server Block, cấu hình nào khai báo chính xác thư mục chứa mã nguồn tĩnh cho một website chạy ở cổng 8080?

[A]
```nginx
server {
    listen 8080;
    root /var/www/site-one/html;
    index index.html;
}
```
[EXP]
Đúng. Chỉ thị listen chỉ định cổng 8080 và root chỉ định thư mục chứa mã nguồn tĩnh.
[B]
```nginx
server {
    port 8080;
    directory /var/www/site-one/html;
    file index.html;
}
```
[EXP]
Sai. Nginx không sử dụng các chỉ thị port, directory, hay file để cấu hình đường dẫn và cổng.
[C]
```nginx
server {
    listen port 8080;
    document_root /var/www/site-one/html;
}
```
[EXP]
Sai. Chỉ thị listen không đi kèm từ khóa port và Nginx dùng root chứ không dùng document_root.
[D]
```nginx
server {
    connect 8080;
    path /var/www/site-one/html;
    index index.html;
}
```
[EXP]
Sai. Các chỉ thị connect và path không tồn tại trong cấu trúc cấu hình Server Block của Nginx.

@correct: A
@point: 20
@difficulty: 10
@concept: nginx-basic-setup
@category: 1

## Q2
Để phân quyền cho tệp tin authorized_keys chỉ có chủ sở hữu được đọc và ghi, học viên cần chạy lệnh phân quyền chmod nào sau đây?

[A]
`chmod 777 ~/.ssh/authorized_keys`
[EXP]
Sai. Lệnh này cấp toàn quyền đọc, ghi, thực thi cho mọi đối tượng, gây mất bảo mật nghiêm trọng.
[B]
`chmod 600 ~/.ssh/authorized_keys`
[EXP]
Đúng. Quyền 600 (rw-------) đảm bảo chỉ có chủ sở hữu (owner) có quyền đọc và ghi tệp tin khóa này.
[C]
`chmod 755 ~/.ssh/authorized_keys`
[EXP]
Sai. Quyền 755 cho phép nhóm và user khác có quyền đọc và thực thi, không an toàn cho SSH Key.
[D]
`chmod 444 ~/.ssh/authorized_keys`
[EXP]
Sai. Quyền 444 là chỉ đọc đối với tất cả mọi người, không cho phép cập nhật thêm key mới khi cần.

@correct: B
@point: 20
@difficulty: 10
@concept: cloud-server-provisioning
@category: 1

## Q3
Cú pháp chính xác của lệnh ufw để chỉ cho phép các kết nối đi vào cổng dịch vụ Web Nginx mặc định (HTTP) là gì?

[A]
`sudo ufw allow incoming http`
[EXP]
Sai. Cú pháp này không hợp lệ trong giao diện dòng lệnh của công cụ UFW.
[B]
`sudo ufw permit port 80`
[EXP]
Sai. UFW không sử dụng từ khóa permit hay port để thiết lập cho phép cổng.
[C]
`sudo ufw allow 80/tcp`
[EXP]
Đúng. Lệnh này cho phép các gói tin TCP đi vào cổng 80 (cổng HTTP mặc định của Nginx).
[D]
`sudo ufw open socket 80`
[EXP]
Sai. Từ khóa open và socket không phải là cú pháp của công cụ quản lý tường lửa UFW.

@correct: C
@point: 20
@difficulty: 10
@concept: infrastructure-security
@category: 1

## Q4
Khi cấu hình trang báo lỗi 404 tùy biến trong Nginx Server Block, cú pháp nào sau đây chỉ định chính xác đường dẫn chuyển hướng nội bộ?

[A]
`error_page 404 = /custom_404.html;`
[EXP]
Sai. Cú pháp chuyển hướng nội bộ không có dấu bằng `=` đứng trước tên file.
[B]
`redirect 404 to /custom_404.html;`
[EXP]
Sai. Nginx không sử dụng chỉ thị redirect để cấu hình trang báo lỗi.
[C]
`catch_error 404 /custom_404.html;`
[EXP]
Sai. Chỉ thị catch_error không tồn tại trong cú pháp Server Block của Nginx.
[D]
`error_page 404 /custom_404.html;`
[EXP]
Đúng. Chỉ thị error_page chỉ định mã lỗi 404 sẽ được xử lý bằng tài nguyên nội bộ /custom_404.html.

@correct: D
@point: 20
@difficulty: 10
@concept: nginx-basic-setup
@category: 1

## Q5
Lệnh nào sau đây được sử dụng để tạo một tài khoản người dùng hệ thống mới trên hệ điều hành Ubuntu Server?

[A]
`sudo adduser devops`
[EXP]
Đúng. Lệnh adduser tạo tài khoản mới kèm theo các bước thiết lập thư mục home và mật khẩu tương tác.
[B]
`sudo usercreate devops`
[EXP]
Sai. Lệnh usercreate không tồn tại trên hệ điều hành Linux Ubuntu Server.
[C]
`sudo makeuser devops`
[EXP]
Sai. Không có lệnh makeuser trong hệ thống quản lý tài khoản của Linux.
[D]
`sudo newuser devops`
[EXP]
Sai. newuser không phải là lệnh chuẩn để thêm người dùng mới trên Ubuntu.

@correct: A
@point: 20
@difficulty: 10
@concept: infrastructure-security
@category: 1

## Q6
Để cấu hình ghi log truy cập của một ứng dụng ra một file riêng trong Nginx Server Block, học viên sử dụng chỉ thị nào sau đây?

[A]
`log_output /var/log/nginx/my-app.log;`
[EXP]
Sai. Chỉ thị log_output không tồn tại trong cấu trúc cấu hình của Nginx.
[B]
`access_log /var/log/nginx/my-app.access.log;`
[EXP]
Đúng. Chỉ thị access_log chỉ định đường dẫn tuyệt đối của tệp nhật ký truy cập dành riêng cho website đó.
[C]
`write_log /var/log/nginx/my-app.access.log;`
[EXP]
Sai. Nginx không sử dụng chỉ thị write_log để ghi nhật ký truy cập.
[D]
`access_record /var/log/nginx/my-app.log;`
[EXP]
Sai. access_record không phải là chỉ thị hợp lệ của máy chủ Web Nginx.

@correct: B
@point: 20
@difficulty: 10
@concept: nginx-basic-setup
@category: 1

## Q7
Cú pháp lệnh để kích hoạt (enable) tường lửa UFW hoạt động ngay lập tức trên hệ thống Ubuntu Server là gì?

[A]
`sudo ufw start`
[EXP]
Sai. systemd quản lý ufw dịch vụ chứ lệnh ufw trực tiếp không có tham số start.
[B]
`sudo ufw turn-on`
[EXP]
Sai. Tham số turn-on không phải là lệnh hợp lệ của công cụ UFW.
[C]
`sudo ufw enable`
[EXP]
Đúng. Lệnh này kích hoạt tường lửa UFW và áp dụng các luật cấu hình ngay lập tức.
[D]
`sudo ufw activate`
[EXP]
Sai. Tham số activate không tồn tại trong bộ lệnh của tường lửa UFW.

@correct: C
@point: 20
@difficulty: 10
@concept: infrastructure-security
@category: 1

## Q8
Học viên muốn tạo liên kết tượng trưng (symlink) từ file cấu hình sites-available sang sites-enabled của Nginx, lệnh nào sau đây là đúng?

[A]
`sudo link -s /etc/nginx/sites-available/app.conf /etc/nginx/sites-enabled/app.conf`
[EXP]
Sai. Lệnh để tạo liên kết tượng trưng là ln chứ không phải link.
[B]
`sudo cp /etc/nginx/sites-available/app.conf /etc/nginx/sites-enabled/app.conf`
[EXP]
Sai. Lệnh cp sao chép tệp tin vật lý chứ không tạo liên kết tượng trưng động.
[C]
`sudo make-symlink /etc/nginx/sites-available/app.conf /etc/nginx/sites-enabled/app.conf`
[EXP]
Sai. make-symlink không phải là lệnh của hệ điều hành Linux Ubuntu.
[D]
`sudo ln -s /etc/nginx/sites-available/app.conf /etc/nginx/sites-enabled/app.conf`
[EXP]
Đúng. Cú pháp `ln -s` tạo liên kết tượng trưng mềm để kích hoạt cấu hình Server Block.

@correct: D
@point: 20
@difficulty: 10
@concept: nginx-basic-setup
@category: 1

## Q9
Để kiểm tra lỗi cú pháp của các tệp tin cấu hình Nginx trước khi nạp lại dịch vụ, học viên chạy lệnh nào dưới đây?

[A]
`sudo nginx -t`
[EXP]
Đúng. Tham số `-t` (test) yêu cầu Nginx kiểm tra toàn bộ cú pháp file cấu hình và thông báo lỗi cụ thể.
[B]
`sudo nginx --check`
[EXP]
Sai. Nginx không hỗ trợ tham số --check để kiểm tra cú pháp tệp tin cấu hình.
[C]
`sudo nginx status`
[EXP]
Sai. systemctl mới dùng status để kiểm tra dịch vụ, nginx status không kiểm tra cú pháp.
[D]
`sudo nginx -v`
[EXP]
Sai. Tham số `-v` hiển thị thông tin phiên bản Nginx đang cài đặt, không kiểm tra cấu hình.

@correct: A
@point: 20
@difficulty: 10
@concept: nginx-basic-setup
@category: 1

## Q10
Chỉ thị nào dùng để kích hoạt tính năng bảo mật thư mục bằng mật khẩu (Basic Authentication) trong cấu hình location của Nginx?

[A]
`password_protect "Admin Area";`
[EXP]
Sai. password_protect không phải là chỉ thị cấu hình hợp lệ của Nginx.
[B]
`auth_basic "Khu vuc quan tri";`
[EXP]
Đúng. Chỉ thị auth_basic dùng để bật cơ chế xác thực cơ bản và hiển thị thông báo.
[C]
`basic_authentication on;`
[EXP]
Sai. Nginx không sử dụng chỉ thị basic_authentication để kiểm soát xác thực.
[D]
`http_auth_require true;`
[EXP]
Sai. http_auth_require không phải là cú pháp của Web Server Nginx.

@correct: B
@point: 20
@difficulty: 10
@concept: nginx-basic-setup
@category: 1

## Q11
Để thêm một người dùng thường có tên là `devops` vào nhóm `sudo` để cấp quyền quản trị, lệnh nào sau đây là đúng?

[A]
`sudo useradd -group sudo devops`
[EXP]
Sai. Cú pháp này không đúng để sửa đổi nhóm của một người dùng đã tồn tại.
[B]
`sudo add-user devops to sudo`
[EXP]
Sai. add-user to không phải là lệnh hợp lệ của hệ điều hành Linux Ubuntu.
[C]
`sudo usermod -aG sudo devops`
[EXP]
Đúng. Tham số `-aG` (append Group) thêm người dùng vào nhóm sudo mà không xóa khỏi các nhóm cũ.
[D]
`sudo groupadd sudo devops`
[EXP]
Sai. Lệnh groupadd dùng để tạo một nhóm mới chứ không dùng để gán người dùng vào nhóm.

@correct: C
@point: 20
@difficulty: 10
@concept: infrastructure-security
@category: 1

## Q12
Cú pháp lệnh để cho phép một cổng dịch vụ tùy chỉnh (ví dụ cổng 2222) đi qua tường lửa UFW là gì?

[A]
`sudo ufw open port 2222`
[EXP]
Sai. UFW không sử dụng từ khóa open hay port trong cấu trúc lệnh.
[B]
`sudo ufw accept 2222/tcp`
[EXP]
Sai. UFW sử dụng từ khóa allow chứ không dùng accept cho các luật cho phép.
[C]
`sudo ufw allow port 2222`
[EXP]
Sai. Chỉ định cổng trong UFW không đi kèm từ khóa port.
[D]
`sudo ufw allow 2222/tcp`
[EXP]
Đúng. Cú pháp `allow <port>/<protocol>` mở chính xác cổng mạng trên tường lửa UFW.

@correct: D
@point: 20
@difficulty: 10
@concept: infrastructure-security
@category: 1

## Q13
Một học viên phát hiện ra rằng sau khi chạy lệnh `sudo ufw enable`, kết nối SSH hiện tại vẫn hoạt động nhưng không thể mở thêm kết nối mới qua cổng 22. Nguyên nhân logic nào sau đây giải thích hiện tượng này?

[A]
UFW đã áp dụng luật mặc định chặn incoming và học viên chưa chạy lệnh `ufw allow 22/tcp`.
[EXP]
Đúng. Phiên kết nối cũ được giữ do Linux duy trì socket đã kết nối, nhưng kết nối mới bị UFW chặn vì chưa có luật cho phép.
[B]
Hệ thống bị cạn kiệt bộ nhớ RAM vật lý ngay lập tức khi kích hoạt tường lửa UFW.
[EXP]
Sai. Tường lửa UFW tiêu thụ rất ít RAM, không thể gây cạn kiệt RAM ngay lập tức.
[C]
Nhà cung cấp đám mây tự động khóa tài khoản của học viên khi phát hiện lệnh kích hoạt UFW.
[EXP]
Sai. Nhà cung cấp đám mây khuyến khích bảo mật hệ thống, không tự động khóa tài khoản vì lệnh này.
[D]
Tường lửa UFW tự động thay đổi cổng kết nối SSH của hệ điều hành sang cổng 80.
[EXP]
Sai. Tường lửa chỉ lọc gói tin, không tự ý cấu hình lại cổng của dịch vụ SSH daemon.

@correct: A
@point: 20
@difficulty: 11
@concept: infrastructure-security
@category: 1

## Q14
Học viên cấu hình `auth_basic_user_file /etc/nginx/.htpasswd;` nhưng quên tạo file `.htpasswd` bằng công cụ htpasswd. Điều gì sẽ xảy ra khi truy cập vào thư mục được bảo vệ?

[A]
Học viên được truy cập tự do vào thư mục mà không cần mật khẩu.
[EXP]
Sai. Nginx sẽ từ chối truy cập và báo lỗi vì không tìm thấy file cơ sở dữ liệu xác thực.
[B]
Nginx trả về lỗi Internal Server Error (HTTP 500) hoặc chặn truy cập kèm theo log lỗi.
[EXP]
Đúng. Việc cấu hình trỏ vào file không tồn tại khiến Nginx báo lỗi 500 hoặc 403 và ghi nhận log lỗi đường dẫn.
[C]
Nginx tự động tạo một mật khẩu mặc định ngẫu nhiên và hiển thị trên màn hình.
[EXP]
Sai. Nginx không có tính năng tự sinh và hiển thị mật khẩu đăng nhập ngẫu nhiên.
[D]
Hệ điều hành Ubuntu tự động khởi động lại VPS để khôi phục tệp tin bị thiếu.
[EXP]
Sai. Hệ điều hành không tự động khởi động lại VPS chỉ vì một file cấu hình ứng dụng bị thiếu.

@correct: B
@point: 20
@difficulty: 11
@concept: nginx-basic-setup
@category: 1

## Q15
Học viên cấu hình Server Block cho hai website chạy song song ở cổng 80. Website A có `server_name siteA.com`, Website B có `server_name siteB.com`. Khi người dùng truy cập bằng IP trực tiếp `http://<IP_ADDRESS>`, Nginx sẽ phản hồi như thế nào?

[A]
Hiển thị trang lỗi 404 vì truy cập bằng IP không khớp với bất kỳ tên miền nào.
[EXP]
Sai. Nginx vẫn phản hồi một trang web mặc định chứ không báo lỗi 404 ngay.
[B]
Nginx ngẫu nhiên chọn một trong hai website để hiển thị cho người dùng.
[EXP]
Sai. Quy trình xử lý của Nginx tuân theo luật rõ ràng, không chọn ngẫu nhiên.
[C]
Nginx hiển thị website mặc định (mặc định là website đầu tiên được nạp trong danh sách cấu hình).
[EXP]
Đúng. Khi không khớp server_name, Nginx sẽ chuyển tiếp yêu cầu đến server block mặc định (default_server), mặc định là cấu hình đầu tiên được nạp.
[D]
Máy chủ ảo VPS sẽ bị sập dịch vụ Nginx ngay lập tức vì xung đột tên miền.
[EXP]
Sai. Xung đột tên miền không làm sập dịch vụ Nginx khi dịch vụ đang chạy.

@correct: C
@point: 20
@difficulty: 11
@concept: nginx-basic-setup
@category: 1

## Q16
Học viên tạo một file cấu hình Server Block mới trong `/etc/nginx/sites-available/` nhưng quên tạo liên kết tượng trưng (symlink) sang `/etc/nginx/sites-enabled/`. Sau khi chạy `sudo systemctl reload nginx`, website mới có hoạt động không?

[A]
Có, vì Nginx tự động quét và nạp toàn bộ tệp tin trong sites-available.
[EXP]
Sai. File chính nginx.conf chỉ cấu hình nạp các file từ sites-enabled.
[B]
Không, vì Nginx chỉ nạp các tệp cấu hình được liên kết hoặc lưu trong sites-enabled.
[EXP]
Đúng. sites-available chỉ là nơi lưu trữ bản nháp cấu hình, Nginx chỉ thực thi các file nằm trong sites-enabled.
[C]
Có, nhưng website sẽ chạy ở cổng 80 mặc định thay vì cổng cấu hình.
[EXP]
Sai. Cấu hình chưa được nạp nên website mới hoàn toàn không hoạt động.
[D]
Không, và Nginx sẽ báo lỗi cú pháp cấu hình khi chạy lệnh kiểm tra.
[EXP]
Sai. Nginx không báo lỗi cú pháp vì file nháp trong sites-available không được nạp vào để kiểm tra.

@correct: B
@point: 20
@difficulty: 11
@concept: nginx-basic-setup
@category: 1

## Q17
Học viên cấu hình chặn cổng 80 trên UFW nhưng Nginx vẫn đang cấu hình lắng nghe ở cổng 80. Khi người dùng truy cập từ internet vào website, hiện tượng gì sẽ xảy ra?

[A]
Trình duyệt hiển thị thông báo lỗi hết hạn thời gian kết nối (Connection Timeout).
[EXP]
Đúng. Tường lửa UFW chặn gói tin đi vào cổng 80 ở tầng OS, khiến yêu cầu từ trình duyệt bị treo và timeout trước khi chạm được tới Nginx.
[B]
Nginx trả về lỗi 403 Forbidden vì tường lửa đã từ chối quyền truy cập.
[EXP]
Sai. Lỗi 403 do Nginx trả về khi yêu cầu đã chạm đến Nginx nhưng bị từ chối quyền thư mục, ở đây gói tin bị chặn từ tường lửa.
[C]
Website vẫn truy cập bình thường vì Nginx có đặc quyền bỏ qua tường lửa UFW.
[EXP]
Sai. Nginx là ứng dụng chạy trên OS, vẫn phải tuân thủ các luật lọc gói tin của tường lửa OS.
[D]
Trình duyệt hiển thị trang báo lỗi 502 Bad Gateway của máy chủ Web Nginx.
[EXP]
Sai. Lỗi 502 xảy ra khi Nginx làm proxy nhưng không kết nối được ứng dụng backend, ở đây kết nối bị chặn trước Nginx.

@correct: A
@point: 20
@difficulty: 11
@concept: nginx-basic-setup
@category: 1

## Q18
Sau khi sửa đổi tệp cấu hình `/etc/ssh/sshd_config` để đổi cổng SSH sang 2222, học viên chạy lệnh `sudo systemctl restart ssh` và bị ngắt kết nối ngay lập tức. Nguyên nhân logic nhất là gì?

[A]
Học viên đã cấu hình sai cú pháp khiến dịch vụ SSH daemon bị sập và không thể khởi động lại.
[EXP]
Sai. If sai cú pháp, tiến trình cũ bị dừng nhưng tiến trình mới không lên được, tuy nhiên lỗi lockout thường do quên cấu hình tường lửa.
[B]
Học viên chưa cho phép cổng 2222/tcp đi qua tường lửa UFW trước khi khởi động lại dịch vụ.
[EXP]
Đúng. Khi SSH chuyển sang cổng 2222, các kết nối mới và kết nối đang thử lại qua cổng này đều bị UFW chặn do chưa có luật cho phép.
[C]
Hệ điều hành Ubuntu tự động tắt dịch vụ SSH khi phát hiện cổng kết nối bị thay đổi.
[EXP]
Sai. Ubuntu không tự động tắt dịch vụ SSH chỉ vì thay đổi cổng.
[D]
Nhà cung cấp đám mây tự động xóa máy chủ vì phát hiện thay đổi cấu hình cổng mặc định.
[EXP]
Sai. Nhà cung cấp không can thiệp xóa VPS của khách hàng vì thao tác cấu hình hệ điều hành này.

@correct: B
@point: 20
@difficulty: 11
@concept: cloud-server-provisioning
@category: 1

## Q19
Trong Nginx Server Block, nếu học viên cấu hình chỉ thị `internal;` bên trong block `location = /custom_404.html` nhưng không định nghĩa chỉ thị `error_page 404 /custom_404.html;`. Điều gì xảy ra khi người dùng truy cập trực tiếp URL `http://<IP>/custom_404.html`?

[A]
Hiển thị nội dung trang custom_404.html bình thường.
[EXP]
Sai. Chỉ thị internal chặn truy cập trực tiếp từ người dùng mạng ngoài.
[B]
Nginx hiển thị mã lỗi 404 Not Found hoặc 403 Forbidden.
[EXP]
Đúng. Do có chỉ thị internal bảo vệ truy cập trực tiếp, người dùng ngoài gọi URL này sẽ bị Nginx từ chối và trả về lỗi.
[C]
Trình duyệt bị treo kết nối và báo lỗi Connection Timeout.
[EXP]
Sai. Kết nối vẫn đến được Nginx và Nginx trả về mã lỗi HTTP lập tức chứ không bị timeout mạng.
[D]
Nginx tự động chuyển hướng người dùng sang trang chủ của website.
[EXP]
Sai. Nginx không tự động chuyển hướng về trang chủ trừ khi có cấu hình rewrite hay return.

@correct: B
@point: 20
@difficulty: 11
@concept: nginx-basic-setup
@category: 1

## Q20
Khi cấu hình DigitalOcean Cloud Firewall chỉ cho phép cổng SSH và gán Droplets vào đó, nhưng quên mở cổng HTTP (80). Người dùng bên ngoài internet truy cập website sẽ nhận được kết quả nào?

[A]
Trình duyệt hiển thị thông báo lỗi từ chối kết nối hoặc hết hạn thời gian kết nối.
[EXP]
Đúng. Cloud Firewall chặn gói tin cổng 80 từ biên mạng trước khi đến được VPS, gây ra hiện tượng timeout kết nối.
[B]
Nginx hiển thị trang lỗi 403 Forbidden của website.
[EXP]
Sai. Gói tin bị chặn từ tường lửa đám mây bên ngoài nên không thể chạm tới Nginx để nhận phản hồi lỗi 403.
[C]
Website vẫn truy cập bình thường vì Nginx tự động mở cổng trên Cloud Firewall.
[EXP]
Sai. Nginx chạy bên trong hệ điều hành của máy ảo, không thể tự tương tác và thay đổi cấu hình tường lửa đám mây bên ngoài.
[D]
Hệ điều hành Ubuntu của Droplet sẽ bị sập hoàn toàn do xung đột tường lửa.
[EXP]
Sai. Chặn cổng mạng không gây sập hệ điều hành của Droplet.

@correct: A
@point: 20
@difficulty: 11
@concept: infrastructure-security
@category: 1

## Q21
Học viên cấu hình UFW trên Ubuntu cho phép cổng 8080 (`sudo ufw allow 8080/tcp`) nhưng cấu hình DigitalOcean Cloud Firewall của Droplet đó chỉ mở cổng 22 (SSH). Kết quả truy cập website ở cổng 8080 từ internet là gì?

[A]
Website vẫn truy cập bình thường vì tường lửa trong OS đã cho phép.
[EXP]
Sai. Gói tin bị chặn từ Cloud Firewall bên ngoài trước khi chạm tới card mạng của OS.
[B]
Trình duyệt báo lỗi Connection Timeout hoặc kết nối bị từ chối.
[EXP]
Đúng. Lưu lượng đi vào cổng 8080 bị Cloud Firewall chặn đứng tại biên mạng của hạ tầng đám mây, không thể gửi tới hệ điều hành.
[C]
Nginx trả về lỗi 502 Bad Gateway do xung đột giữa hai tường lửa.
[EXP]
Sai. Không xảy ra lỗi 502 Bad Gateway vì gói tin không chạm tới được Nginx.
[D]
Droplet tự động khởi động lại để cập nhật đồng bộ cấu hình tường lửa.
[EXP]
Sai. Hạ tầng đám mây và hệ điều hành không tự động khởi động lại để đồng bộ hóa.

@correct: B
@point: 20
@difficulty: 11
@concept: infrastructure-security
@category: 1

## Q22
Học viên vô hiệu hóa PermitRootLogin (`PermitRootLogin no`) nhưng quên tạo cặp khóa SSH Key cho user thường `devops`. Đồng thời, PasswordAuthentication vẫn giữ là `no`. Học viên sẽ gặp tình trạng nào?

[A]
Học viên vẫn đăng nhập được bằng root bằng mật khẩu thông thường.
[EXP]
Sai. PermitRootLogin đã chặn root và PasswordAuthentication đã tắt đăng nhập mật khẩu.
[B]
Hệ thống tự động bật lại cơ chế đăng nhập mật khẩu để cứu hộ học viên.
[EXP]
Sai. Hệ điều hành không tự ý thay đổi cấu hình tệp tin cấu hình bảo mật để tự cứu hộ.
[C]
Học viên bị mất quyền truy cập SSH hoàn toàn vào máy chủ ảo VPS.
[EXP]
Đúng. Root bị cấm đăng nhập, mật khẩu bị tắt, user thường không có SSH Key để xác thực dẫn đến mất hoàn toàn quyền truy cập từ xa qua SSH.
[D]
Học viên có thể kết nối bằng cách sử dụng cổng mạng 80 của Nginx để đăng nhập.
[EXP]
Sai. Cổng 80 chỉ dành cho HTTP, không hỗ trợ giao thức đăng nhập SSH.

@correct: C
@point: 20
@difficulty: 11
@concept: cloud-server-provisioning
@category: 1

## Q23
Tại sao việc cấu hình tường lửa UFW mặc định chặn toàn bộ lưu lượng đi vào (`default deny incoming`) và chỉ cho phép các cổng dịch vụ cần thiết lại là một best practice trong bảo mật hệ thống?

[A]
Giúp giảm tối đa bề mặt tấn công của máy chủ bằng cách đóng toàn bộ các cổng không sử dụng.
[EXP]
Đúng. Mọi dịch vụ chạy ẩn hoặc có lỗi bảo mật trên các cổng chưa khai báo đều được bảo vệ an toàn khỏi các cuộc dò quét từ bên ngoài.
[B]
Ngăn chặn hoàn toàn việc các tiến trình bên trong máy chủ kết nối ra ngoài internet.
[EXP]
Sai. Chỉ chặn chiều đi vào (incoming), chiều đi ra (outgoing) mặc định vẫn được phép để tải gói phần mềm.
[C]
Giúp tăng tốc độ xử lý tính toán của vi xử lý CPU máy chủ ảo lên gấp 2 lần.
[EXP]
Sai. Tường lửa chỉ lọc lưu lượng mạng, không có tính năng tăng tốc năng lực tính toán của CPU.
[D]
Giúp tự động mã hóa toàn bộ dữ liệu lưu trên đĩa cứng của máy chủ ảo.
[EXP]
Sai. Việc mã hóa dữ liệu trên đĩa do phần mềm mã hóa ổ đĩa đảm nhận, không phải tường lửa.

@correct: A
@point: 20
@difficulty: 6
@concept: infrastructure-security
@category: 1

## Q24
Để giảm thiểu tối đa nguy cơ máy chủ ảo VPS bị dò quét và tấn công brute-force tự động vào dịch vụ SSH, giải pháp nào sau đây là tối ưu nhất?

[A]
Cài đặt nhiều phần mềm diệt virus chạy quét liên tục 24/7 trên máy chủ ảo.
[EXP]
Sai. Phần mềm diệt virus không ngăn chặn được các cuộc tấn công brute-force vào dịch vụ SSH từ bên ngoài.
[B]
Tăng cấu hình phần cứng CPU của Droplet lên mức tối đa để chống sập khi bị brute-force.
[EXP]
Sai. Tăng cấu hình chỉ giúp máy chủ chịu tải tốt hơn chứ không giải quyết tận gốc rủi ro bị chiếm quyền điều khiển.
[C]
Thay thế hoàn toàn xác thực mật khẩu bằng khóa SSH Key và đổi cổng kết nối mặc định.
[EXP]
Đúng. Kết hợp đổi cổng tùy chỉnh để tránh botnet quét cổng mặc định 22 và dùng SSH Key cực kỳ phức tạp để chống dò mật khẩu.
[D]
Tắt dịch vụ SSH daemon hoàn toàn và chỉ thao tác trực tiếp qua phần cứng vật lý.
[EXP]
Sai. Tắt SSH daemon sẽ khiến học viên không thể quản trị máy chủ từ xa, đi ngược lại nhu cầu vận hành Cloud.

@correct: C
@point: 20
@difficulty: 6
@concept: infrastructure-security
@category: 1

## Q25
Khi thiết kế kiến trúc bảo mật cho một hệ thống chạy trên Cloud, tại sao khuyến nghị áp dụng cơ chế phòng thủ chiều sâu (Defense in Depth) bằng cách kết hợp cả UFW trong OS và Cloud Firewall bên ngoài?

[A]
Để tự động chia tải (load balancing) lưu lượng mạng đi vào máy chủ ảo VPS.
[EXP]
Sai. Tường lửa chỉ thực hiện chức năng lọc gói tin, không làm nhiệm vụ cân bằng tải lưu lượng mạng.
[B]
Vì bắt buộc phải sử dụng cả hai lớp thì hệ điều hành Ubuntu mới kích hoạt được Nginx.
[EXP]
Sai. Nginx hoạt động độc lập và không yêu cầu có cả hai tường lửa mới chạy được.
[C]
Để tăng dung lượng lưu trữ của ổ đĩa cứng ảo Droplet lên gấp hai lần.
[EXP]
Sai. Dung lượng lưu trữ đĩa cứng hoàn toàn độc lập với các lớp tường lửa mạng được cấu hình.
[D]
Để tạo tính dự phòng bảo mật, tránh trường hợp một lớp tường lửa bị lỗi hoặc cấu hình sai do sơ suất con người.
[EXP]
Đúng. Phòng thủ chiều sâu đảm bảo nếu một lớp bảo vệ bị tắt do nhầm lẫn hoặc lỗi cấu hình, lớp bảo vệ còn lại vẫn giữ an toàn cho máy chủ.

@correct: D
@point: 20
@difficulty: 6
@concept: infrastructure-security
@category: 1

## Q26
Một doanh nghiệp muốn cấu hình Nginx Server Block để phục vụ ứng dụng nội bộ của nhân viên. Biện pháp bảo mật cơ bản nào phù hợp nhất để ngăn người dùng bên ngoài internet truy cập tự do vào website này khi chưa có hệ thống VPN?

[A]
Cài đặt chứng chỉ SSL/TLS tự cấp phát (Self-signed Certificate) trên Nginx.
[EXP]
Sai. Chứng chỉ SSL chỉ mã hóa đường truyền chứ không chặn truy cập từ người dùng không được phép.
[B]
Thiết lập HTTP Basic Authentication để yêu cầu tài khoản và mật khẩu đăng nhập.
[EXP]
Đúng. Basic Authentication là giải pháp đơn giản và hiệu quả giúp bảo vệ nhanh các đường dẫn nhạy cảm hoặc website nội bộ khỏi truy cập công cộng.
[C]
Cấu hình chỉ thị internal cho toàn bộ thư mục root của website.
[EXP]
Sai. Chỉ thị internal chặn mọi truy cập trực tiếp từ bên ngoài, khiến trang web không thể sử dụng thông thường.
[D]
Thay đổi cổng lắng nghe của Server Block sang cổng 80 mặc định.
[EXP]
Sai. Sử dụng cổng 80 mặc định càng giúp người ngoài dễ dàng truy cập website hơn.

@correct: B
@point: 20
@difficulty: 6
@concept: nginx-basic-setup
@category: 1

## Q27
Khi cấu hình DigitalOcean Cloud Firewall, việc đặt phạm vi nguồn (Source) của luật SSH là địa chỉ IP tĩnh của văn phòng thay vì `All IPv4` mang lại lợi ích gì?

[A]
Giúp tăng tốc độ xử lý lệnh dòng lệnh khi kết nối SSH lên gấp 3 lần.
[EXP]
Sai. Giới hạn IP chỉ tăng tính bảo mật, không ảnh hưởng đến tốc độ thực thi lệnh trong phiên SSH.
[B]
Cho phép học viên đăng nhập bằng root mà không cần cấu hình khóa SSH Key.
[EXP]
Sai. Cơ chế xác thực SSH vẫn yêu cầu SSH Key hoặc mật khẩu bình thường tùy cấu hình của SSH daemon.
[C]
Chỉ cho phép các máy tính kết nối từ văn phòng thực hiện kết nối SSH tới máy chủ, chặn hoàn toàn mọi IP khác.
[EXP]
Đúng. Giới hạn IP nguồn giúp khóa chặt cổng SSH, ngăn chặn bất kỳ kẻ tấn công nào ngoài văn phòng kết nối thử vào cổng SSH của server.
[D]
Tự động cấu hình tường lửa UFW bên trong hệ điều hành Ubuntu đồng bộ theo.
[EXP]
Sai. Hai tường lửa này độc lập, Cloud Firewall không tự động cấu hình đồng bộ hóa UFW bên trong VPS.

@correct: C
@point: 20
@difficulty: 6
@concept: infrastructure-security
@category: 1

## Q28
Học viên cấu hình tệp tin mật khẩu basic authentication tại `/etc/nginx/.htpasswd`. Cấu hình phân quyền tệp tin (chmod) nào sau đây là tối ưu nhất để đảm bảo an toàn?

[A]
`chmod 777 /etc/nginx/.htpasswd` và cấp quyền cho tất cả mọi người chỉnh sửa.
[EXP]
Sai. Cấp quyền 777 cho file mật khẩu là lỗ hổng bảo mật nghiêm trọng trên hệ điều hành.
[B]
`chmod 000 /etc/nginx/.htpasswd` để không ai có quyền đọc tệp tin này kể cả Nginx.
[EXP]
Sai. Quyền 000 khiến Nginx không thể đọc file để xác thực mật khẩu, gây lỗi 500.
[C]
`chmod 755 /etc/nginx/.htpasswd` và đặt file trong thư mục /var/www/html/ để dễ nạp.
[EXP]
Sai. Đặt trong thư mục gốc sẽ khiến người dùng tải được file mật khẩu về, vi phạm bảo mật.
[D]
`chmod 600 /etc/nginx/.htpasswd` và thuộc quyền sở hữu của user `www-data` (hoặc root).
[EXP]
Đúng. Quyền 600 giúp chỉ chủ sở hữu được đọc ghi, ngăn chặn các user khác trên OS (như devops) đọc trộm file mật khẩu đã mã hóa.

@correct: D
@point: 20
@difficulty: 6
@concept: nginx-basic-setup
@category: 1

## Q29
Tại sao học viên không nên sử dụng trực tiếp tài khoản quản trị tối cao root để thực hiện các thao tác DevOps hàng ngày trên server?

[A]
Vì tài khoản root bị giới hạn băng thông internet tối đa chỉ bằng một nửa tài khoản thường.
[EXP]
Sai. Quyền hạn mạng không bị giới hạn dựa trên tài khoản người dùng đăng nhập hệ thống.
[B]
Để tránh các lỗi gõ nhầm lệnh nghiêm trọng có thể phá hủy toàn bộ hệ thống ngay lập tức.
[EXP]
Đúng. Tài khoản root có toàn quyền thực thi mọi lệnh phá hủy mà không có cảnh báo hay chặn quyền từ hệ thống.
[C]
Vì hệ điều hành Ubuntu sẽ tự động khóa tài khoản root sau 2 giờ sử dụng liên tục.
[EXP]
Sai. Ubuntu không tự động khóa tài khoản root vì thời gian sử dụng liên tục.
[D]
Để tiết kiệm chi phí thuê tài nguyên CPU vật lý của máy chủ ảo VPS.
[EXP]
Sai. Tài khoản đăng nhập không ảnh hưởng đến chi phí thuê hay tài nguyên sử dụng của VPS.

@correct: B
@point: 20
@difficulty: 6
@concept: infrastructure-security
@category: 1

## Q30
Khi tiến hành hardening dịch vụ SSH và cấu hình tường lửa, tại sao học viên luôn được yêu cầu kiểm tra kỹ càng bằng cách mở Terminal mới trước khi đóng phiên kết nối hiện tại?

[A]
Để đảm bảo cấu hình mới chạy ổn định và giữ phiên kết nối cũ làm phao cứu sinh nếu bị lỗi.
[EXP]
Đúng. Giữ phiên kết nối cũ giúp sửa lại cấu hình nếu phát hiện lỗi lockout ở phiên kết nối mới thử nghiệm.
[B]
Để hệ điều hành tự động đồng bộ hóa cấu hình tường lửa UFW lên đám mây.
[EXP]
Sai. Việc mở phiên kết nối mới không kích hoạt đồng bộ hóa tường lửa lên đám mây.
[C]
Để Nginx tự động dọn dẹp các tệp tin cấu hình dư thừa trong sites-available.
[EXP]
Sai. Nginx không tự động dọn dẹp cấu hình dư thừa khi có kết nối SSH mới.
[D]
Để giải phóng bộ nhớ RAM vật lý đang bị chiếm dụng bởi các tiến trình SSH daemon cũ.
[EXP]
Sai. Mở thêm phiên kết nối chỉ tiêu tốn thêm một ít RAM chứ không giải phóng RAM.

@correct: A
@point: 20
@difficulty: 6
@concept: cloud-server-provisioning
@category: 1
