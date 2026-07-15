---
schema_version: 1
id: ss02_quiz_lesson_03
type: quiz
status: approved
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
updated: '2026-07-15'
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
Tường lửa cấp Hạ tầng Đám mây (Cloud Firewall, ví dụ: DigitalOcean Cloud Firewalls) có lợi thế vượt trội nào về mặt tối ưu tài nguyên hệ thống so với tường lửa cấp Hệ điều hành chạy trong VPS (UFW)?

[A]
Cloud Firewall giúp VPS không bị tốn CPU và băng thông mạng để xử lý và từ chối các gói tin rác/tấn công.
[EXP]
Đúng. Do Cloud Firewall lọc sạch lưu lượng xấu ở biên mạng của Datacenter trước khi gói tin đến được VPS, giúp VPS tiết kiệm tài nguyên xử lý.
[B]
Cloud Firewall tự động tăng gấp đôi băng thông card mạng vật lý của máy chủ ảo VPS.
[EXP]
Sai. Cloud Firewall không thay đổi phần cứng hay băng thông tối đa của card mạng.
[C]
Cloud Firewall chạy trực tiếp bên trong nhân Linux của VPS nên có tốc độ xử lý nhanh hơn.
[EXP]
Sai. Đây là mô tả của tường lửa cấp OS như iptables/UFW, không phải Cloud Firewall.
[D]
Cloud Firewall giúp loại bỏ hoàn toàn việc phải cấu hình địa chỉ IP Public cho VPS.
[EXP]
Sai. VPS vẫn cần IP Public để giao tiếp internet bình thường.

@correct: A
@point: 20
@difficulty: 2
@concept: infrastructure-security
@category: 1

## Q5
Trong thực tế triển khai hạ tầng Cloud (ví dụ trên DigitalOcean), tại sao các kỹ sư DevOps thường được khuyến nghị kết hợp cả UFW (tường lửa OS) và Cloud Firewall (tường lửa hạ tầng)?

[A]
Vì nếu UFW bị tắt do sơ suất của quản trị viên, lớp Cloud Firewall bên ngoài vẫn bảo vệ được máy chủ ảo và ngược lại.
[EXP]
Đúng. Đây là mô hình phòng thủ chiều sâu (Defense in Depth) nhằm tăng tính dự phòng bảo mật phòng hờ lỗi cấu hình hoặc tắt nhầm.
[B]
Vì bắt buộc phải bật cả hai thì dịch vụ SSH daemon trên cổng 22 mới cho phép kết nối.
[EXP]
Sai. SSH daemon hoạt động độc lập với tường lửa, chỉ cần ít nhất một tường lửa mở cổng là kết nối được.
[C]
Vì Cloud Firewall chỉ hoạt động khi có UFW gửi tín hiệu đồng bộ hóa cấu hình định kỳ.
[EXP]
Sai. Hai tường lửa này hoạt động độc lập và không đồng bộ hóa dữ liệu với nhau.
[D]
Vì kết hợp cả hai sẽ tự động mã hóa mọi dữ liệu tĩnh lưu trữ trên ổ đĩa của Droplet.
[EXP]
Sai. Tường lửa chỉ kiểm soát lưu lượng mạng, không có chức năng mã hóa ổ đĩa.

@correct: A
@point: 20
@difficulty: 3
@concept: infrastructure-security
@category: 1
