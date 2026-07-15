---
schema_version: 1
id: ss02_quiz_lesson_04
type: quiz
status: approved
course_id: devops-basic
session: 2
unit: 4
title: Quiz — Cài đặt và cấu hình Web Server Nginx
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_04
builds_on: []
enables: []
owns: []
assumes:
- nginx-basic-setup
- infrastructure-security
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / quiz_lesson / L04
language: vi
created: '2026-07-15'
updated: '2026-07-15'
quiz_kind: lesson
question_count: 5
maps_to:
- ss02_lesson_04
---

# Quiz — Cài đặt và cấu hình Web Server Nginx

## Q1
Hạn chế lớn nhất khi chạy trực tiếp các máy chủ ứng dụng thô (Node.js, Python, Java) ra internet mà không sử dụng Web Server (như Nginx) làm trung gian là gì?

[A]
Học viên không thể thay đổi mã nguồn của ứng dụng sau khi đã public ra ngoài.
[EXP]
Sai. Các bạn vẫn có thể thay đổi mã nguồn bình thường, việc chạy trực tiếp không ảnh hưởng đến khả năng chỉnh sửa mã nguồn.
[B]
Hiệu năng phục vụ file tĩnh kém và tăng nguy cơ bảo mật cho ứng dụng nội bộ.
[EXP]
Đúng. Các máy chủ ứng dụng thô không được tối ưu để serve file tĩnh (HTML/CSS/Ảnh) và việc phơi trực tiếp cổng nội bộ làm tăng rủi ro bảo mật.
[C]
Hệ điều hành Linux Ubuntu sẽ tự động khóa các tiến trình chạy ứng dụng thô.
[EXP]
Sai. Ubuntu không tự động khóa các tiến trình này trừ khi chúng vi phạm chính sách bảo mật hoặc cạn kiệt tài nguyên hệ thống.
[D]
Trình duyệt web của người dùng không thể kết nối tới các cổng ứng dụng thô.
[EXP]
Sai. Trình duyệt vẫn kết nối được bình thường bằng cách chỉ định cổng (ví dụ: http://ip:3000), nhưng giao diện này không chuyên nghiệp và kém an toàn.

@correct: B
@point: 20
@difficulty: 1
@concept: nginx-basic-setup
@category: 1

## Q2
Trong các cổng mạng (ports) tiêu chuẩn dành cho lưu lượng dịch vụ web, cổng nào được sử dụng mặc định lần lượt cho giao thức HTTP và HTTPS?

[A]
Cổng 80 cho HTTP và cổng 443 cho HTTPS.
[EXP]
Đúng. Đây là hai cổng tiêu chuẩn quốc tế được quy định mặc định: cổng 80 cho HTTP (chưa mã hóa) và cổng 443 cho HTTPS (có mã hóa bảo mật).
[B]
Cổng 22 cho HTTP và cổng 80 cho HTTPS.
[EXP]
Sai. Cổng 22 mặc định được sử dụng cho giao thức kết nối từ xa SSH, không liên quan trực tiếp đến HTTP.
[C]
Cổng 443 cho HTTP và cổng 80 cho HTTPS.
[EXP]
Sai. Đây là sự nhầm lẫn ngược vị trí cổng của hai giao thức với nhau.
[D]
Cổng 8080 cho HTTP và cổng 8443 cho HTTPS.
[EXP]
Sai. Đây là các cổng thay thế thường dùng trong môi trường phát triển (development), không phải cổng tiêu chuẩn mặc định trên môi trường production.

@correct: A
@point: 20
@difficulty: 1
@concept: nginx-basic-setup
@category: 1

## Q3
Thư mục nào sau đây trong cấu trúc của Nginx trên Ubuntu chứa các liên kết tượng trưng (symlinks) để chỉ thị cho Nginx biết những website nào đang hoạt động?

[A]
`/var/www/html/`
[EXP]
Sai. Thư mục này chỉ chứa các tệp tin tĩnh (HTML/CSS) mặc định của website, không chứa file cấu hình hay liên kết tượng trưng.
[B]
`/etc/nginx/sites-available/`
[EXP]
Sai. Thư mục này chứa toàn bộ các file cấu hình chi tiết được tạo ra nhưng ở trạng thái chờ kích hoạt, không chứa liên kết tượng trưng.
[C]
`/etc/nginx/sites-enabled/`
[EXP]
Đúng. Thư mục này chứa các liên kết tượng trưng trỏ sang `sites-available`, chỉ những cấu hình có liên kết tại đây mới thực sự được Nginx nạp và chạy.
[D]
`/etc/nginx/conf.d/`
[EXP]
Sai. Thư mục này chứa các cấu hình chung của hệ thống Nginx, không chứa liên kết tượng trưng kích hoạt từng website riêng.

@correct: C
@point: 20
@difficulty: 2
@concept: nginx-basic-setup
@category: 1

## Q4
Khi tiến hành thay đổi cấu hình Server Block trong Nginx, các bạn nên chạy lệnh nào sau đây để kiểm tra tính chính xác của cú pháp trước khi áp dụng?

[A]
`sudo systemctl restart nginx`
[EXP]
Sai. Lệnh này khởi động lại dịch vụ ngay lập tức, nếu cấu hình lỗi sẽ làm sập Nginx và gián đoạn truy cập của người dùng.
[B]
`sudo systemctl status nginx`
[EXP]
Sai. Lệnh này chỉ hiển thị trạng thái hoạt động hiện tại của tiến trình Nginx, không có chức năng kiểm tra cú pháp file cấu hình.
[C]
`sudo ufw status verbose`
[EXP]
Sai. Lệnh này dùng để kiểm tra trạng thái hoạt động của tường lửa UFW, không liên quan đến cấu hình của Nginx.
[D]
`sudo nginx -t`
[EXP]
Đúng. Lệnh `nginx -t` (test) giúp kiểm tra toàn bộ cấu hình xem có lỗi cú pháp hay không trước khi tiến hành reload dịch vụ một cách an toàn.

@correct: D
@point: 20
@difficulty: 2
@concept: nginx-basic-setup
@category: 1

## Q5
Khi người dùng truy cập vào trang web và nhận được thông báo lỗi **403 Forbidden** từ Nginx, nguyên nhân phổ biến nào dưới đây liên quan đến phân quyền thư mục?

[A]
Nginx không có quyền đọc (read) hoặc thực thi (execute) trên thư mục chứa mã nguồn tĩnh.
[EXP]
Đúng. Nếu thư mục root chứa website tĩnh không được phân quyền cho phép user chạy Nginx (`www-data`) đọc dữ liệu, Nginx sẽ từ chối truy cập và trả về lỗi 403.
[B]
Học viên quên chưa tạo liên kết tượng trưng (symlink) sang thư mục sites-enabled.
[EXP]
Sai. Nếu quên tạo symlink, Nginx sẽ không nhận biết được Server Block đó và trả về trang mặc định hoặc lỗi không tìm thấy tên miền chứ không trả về 403.
[C]
Tường lửa UFW chưa được cấu hình mở cổng 80 hoặc 443 cho lưu lượng mạng đi vào.
[EXP]
Sai. Nếu chưa mở cổng tường lửa, trình duyệt của người dùng sẽ báo lỗi Timeout (không thể kết nối), không nhận được mã lỗi HTTP từ Nginx.
[D]
File cấu hình Server Block của các bạn bị thiếu dấu chấm phẩy ở cuối dòng chỉ thị.
[EXP]
Sai. Thiếu dấu chấm phẩy là lỗi cú pháp cấu hình, khiến Nginx báo lỗi khi kiểm tra hoặc reload chứ không trả về mã lỗi 403 cho người dùng.

@correct: A
@point: 20
@difficulty: 3
@concept: nginx-basic-setup
@category: 1
