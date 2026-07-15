---
schema_version: 1
id: ss02_quiz_lesson_03
type: quiz
status: draft
course_id: devops-basic
session: 2
unit: 3
title: Quiz — Cơ chế bảo mật cho Infrastructure
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_03
builds_on: []
enables: []
owns: []
assumes:
- infrastructure-security
- cloud-server-provisioning
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / quiz_lesson / L03
language: vi
created: '2026-07-14'
updated: '2026-07-14'
quiz_kind: lesson
question_count: 5
maps_to:
- ss02_lesson_03
---

# Quiz — Cơ chế bảo mật cho Infrastructure

## Q1
Trong bảo mật hạ tầng, hành vi nào sau đây tuân thủ đúng nguyên tắc đặc quyền tối thiểu (Least Privilege)?

[A]
Sử dụng tài khoản thường có quyền sudo để quản trị và chỉ nâng quyền khi cần.
[EXP]
Đúng. Thay vì đăng nhập trực tiếp root, việc sử dụng user thường và nâng quyền tạm thời bằng sudo giúp giảm thiểu tối đa rủi ro thao tác sai và kiểm soát log tốt hơn.
[B]
Cấp quyền root vĩnh viễn cho tất cả các ứng dụng chạy trên máy chủ để tránh lỗi.
[EXP]
Sai. Cấp quyền root cho mọi ứng dụng vi phạm nghiêm trọng nguyên tắc Least Privilege, nếu ứng dụng có lỗ hổng bảo mật, kẻ tấn công sẽ chiếm ngay quyền kiểm soát server.
[C]
Chia sẻ mật khẩu tài khoản quản trị root cho toàn bộ thành viên trong nhóm DevOps.
[EXP]
Sai. Chia sẻ tài khoản dùng chung làm mất khả năng quy trách nhiệm cá nhân (non-repudiation) và tăng nguy cơ rò rỉ thông tin đăng nhập.
[D]
Cấu hình cho phép mọi địa chỉ IP từ internet kết nối trực tiếp vào tài khoản root.
[EXP]
Sai. Cho phép kết nối root tự do từ internet làm tăng bề mặt tấn công của hệ thống, vi phạm nguyên tắc bảo mật.

@correct: A
@point: 20
@difficulty: 1
@concept: infrastructure-security
@category: 1

## Q2
Sau khi cấu hình tham số `PasswordAuthentication no` trong file `/etc/ssh/sshd_config`, dịch vụ SSH của máy chủ sẽ thay đổi như thế nào?

[A]
Mọi kết nối SSH từ máy cá nhân đến máy chủ sẽ bị chặn hoàn toàn.
[EXP]
Sai. Lệnh này chỉ tắt phương thức xác thực bằng mật khẩu, người dùng vẫn có thể đăng nhập bình thường nếu cấu hình khóa SSH Key.
[B]
Người dùng bắt buộc phải đổi mật khẩu mới có độ phức tạp cao hơn khi đăng nhập.
[EXP]
Sai. Hệ thống không yêu cầu đổi mật khẩu mà bỏ qua hoàn toàn phương thức nhập mật khẩu, chuyển sang bắt buộc dùng SSH Key.
[C]
Vô hiệu hóa đăng nhập bằng mật khẩu, bắt buộc đăng nhập bằng khóa SSH Key.
[EXP]
Đúng. Chỉ thị này tắt cơ chế xác thực mật khẩu thông thường, chỉ chấp nhận đăng nhập thông qua các khóa SSH hợp lệ đã cấu hình.
[D]
Hệ thống tự động chuyển cổng kết nối dịch vụ SSH từ cổng 22 sang cổng khác.
[EXP]
Sai. Lệnh này không thay đổi cổng dịch vụ SSH, cổng mặc định vẫn giữ nguyên (trừ khi cấu hình rõ chỉ thị Port).

@correct: C
@point: 20
@difficulty: 2
@concept: infrastructure-security
@category: 1

## Q3
Mục đích chính của việc thiết lập tham số `PermitRootLogin no` trong file cấu hình dịch vụ SSH là gì?

[A]
Chặn hoàn toàn các kết nối mạng internet đi vào cổng SSH của máy chủ.
[EXP]
Sai. Chỉ thị này không chặn kết nối mạng mà chỉ chặn quyền đăng nhập của duy nhất tài khoản root qua giao thức SSH.
[B]
Ngăn chặn đăng nhập trực tiếp bằng root, bắt buộc đăng nhập qua user thường.
[EXP]
Đúng. Việc cấm root đăng nhập trực tiếp buộc kẻ tấn công phải dò tìm được cả username phụ và mật khẩu/khóa SSH của user đó, tạo thêm một lớp bảo mật.
[C]
Cho phép tài khoản root kết nối SSH mà không cần sử dụng public key.
[EXP]
Sai. Chỉ thị này cấm đăng nhập root, không phải cho phép kết nối bỏ qua khóa public key.
[D]
Tự động giới hạn quyền hạn của tài khoản root về mức của một user thông thường.
[EXP]
Sai. Quyền hạn của tài khoản root bên trong hệ thống không bị thay đổi, chỉ có quyền đăng nhập từ xa qua SSH là bị chặn.

@correct: B
@point: 20
@difficulty: 2
@concept: infrastructure-security
@category: 1

## Q4
Khi các bạn cấu hình luật mặc định cho tường lửa UFW là `sudo ufw default deny incoming`, điều gì sẽ xảy ra với lưu lượng mạng?

[A]
Tất cả lưu lượng đi ra từ server kết nối đến internet sẽ bị chặn hoàn toàn.
[EXP]
Sai. Luật này chỉ áp dụng cho lưu lượng đi vào (incoming), lưu lượng đi ra (outgoing) không bị ảnh hưởng bởi chỉ thị này.
[B]
Tường lửa sẽ tự động mở cổng cho toàn bộ dịch vụ phổ biến (HTTP, HTTPS, SSH).
[EXP]
Sai. Luật này chặn mọi kết nối đi vào theo mặc định, không tự động mở bất kỳ cổng nào trừ khi có cấu hình cụ thể bằng lệnh ufw allow.
[C]
Tất cả các gói tin đi vào và đi ra khỏi máy chủ đều bị tường lửa chặn lại.
[EXP]
Sai. Chỉ có lưu lượng đi vào (incoming) là bị chặn, lưu lượng đi ra vẫn hoạt động bình thường.
[D]
Mọi yêu cầu kết nối đi vào từ bên ngoài đến máy chủ đều bị chặn theo mặc định.
[EXP]
Đúng. Đây là quy tắc bảo mật an toàn, mặc định chặn tất cả lưu lượng đi vào, học viên phải khai báo cho phép từng dịch vụ cụ thể.

@correct: D
@point: 20
@difficulty: 2
@concept: infrastructure-security
@category: 1

## Q5
Để đảm bảo không bị khóa quyền kết nối (lockout) ngoài ý muốn khi tiến hành hardening SSH và bật tường lửa UFW, các bạn nên thực hiện biện pháp phòng ngừa nào sau đây?

[A]
Tắt hoàn toàn tường lửa UFW trước khi khởi động lại dịch vụ SSH daemon.
[EXP]
Sai. Việc tắt UFW tạm thời không giúp bảo vệ hệ thống khi bật lại và không phải là cách kiểm thử an toàn cấu hình SSH.
[B]
Giữ nguyên phiên kết nối SSH hiện tại và mở Terminal mới để kiểm tra kết nối.
[EXP]
Đúng. Giữ nguyên kết nối cũ giúp các bạn có "phao cứu sinh" để khôi phục/sửa đổi cấu hình nếu kết nối mới bị lỗi do cấu hình sai.
[C]
Chia sẻ private key lên các diễn đàn DevOps để nhờ cộng đồng kiểm tra lỗi cấu hình.
[EXP]
Sai. Tuyệt đối không chia sẻ private key vì điều này làm mất hoàn toàn tính bảo mật của tài khoản, bất cứ ai có key đều có thể kiểm soát server.
[D]
Khởi động lại máy chủ vật lý ngay lập tức sau khi sửa đổi bất kỳ cấu hình nào.
[EXP]
Sai. Khởi động lại server mà cấu hình bị lỗi sẽ khiến hệ thống không thể khởi động dịch vụ SSH, khiến lỗi trầm trọng hơn và khó sửa.

@correct: B
@point: 20
@difficulty: 3
@concept: infrastructure-security
@category: 1
