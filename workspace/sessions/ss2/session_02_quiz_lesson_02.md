---
schema_version: 1
id: ss02_quiz_lesson_02
type: quiz
status: approved
course_id: devops-basic
session: 2
unit: 2
title: Quiz — Khởi tạo Cloud Server thực tế
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_02
builds_on: []
enables: []
owns: []
assumes:
- cloud-server-provisioning
- virtualization-basics
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / quiz_lesson / L02
language: vi
created: '2026-07-14'
updated: '2026-07-14'
quiz_kind: lesson
question_count: 5
maps_to:
- ss02_lesson_02
---

# Quiz — Khởi tạo Cloud Server thực tế

## Q1
Khái niệm Virtual Private Server (VPS) được mô tả chính xác nhất bởi đặc điểm nào sau đây?

[A]
Là máy chủ ảo có hệ điều hành, tài nguyên cấu hình và IP tĩnh riêng biệt.
[EXP]
Đúng. Mỗi VPS hoạt động như một máy chủ độc lập, có hệ điều hành, IP riêng và tài nguyên (CPU, RAM, Disk) được phân chia rõ ràng.
[B]
Là một chương trình phần mềm chỉ chạy được các ứng dụng web tĩnh cơ bản.
[EXP]
Sai. VPS chạy một hệ điều hành đầy đủ, có thể cài đặt bất kỳ dịch vụ hay ứng dụng nào phù hợp (database, backend, web server).
[C]
Là phần cứng vật lý chuyên dụng được thuê riêng toàn bộ thiết bị cho một khách hàng.
[EXP]
Sai. Đây là khái niệm Dedicated Server (máy chủ vật lý riêng), không phải máy chủ ảo VPS được phân chia qua ảo hóa.
[D]
Là máy chủ không có địa chỉ IP công cộng và chỉ kết nối được qua mạng nội bộ.
[EXP]
Sai. VPS thông thường được cấp phát địa chỉ IP công cộng (IP Public) để người dùng ngoài internet có thể truy cập vào.

@correct: A
@point: 20
@difficulty: 1
@concept: cloud-server-provisioning
@category: 1

## Q2
Khi khởi tạo Cloud Server cho các học viên tại Việt Nam, lý do quan trọng nhất để ưu tiên chọn Region Singapore thay vì các Region tại Mỹ hay Châu Âu là gì?

[A]
Chi phí thuê máy chủ tại khu vực Singapore luôn rẻ hơn các khu vực khác.
[EXP]
Sai. Chi phí thuê VPS phụ thuộc vào nhà cung cấp và cấu hình phần cứng, không phải lúc nào Region Singapore cũng rẻ nhất.
[B]
Chỉ có Region Singapore mới hỗ trợ hệ điều hành Linux Ubuntu Server.
[EXP]
Sai. Tất cả các Region của các nhà cung cấp đám mây lớn đều hỗ trợ đầy đủ các hệ điều hành phổ biến bao gồm cả Ubuntu.
[C]
Vị trí địa lý gần Việt Nam giúp giảm thiểu tối đa độ trễ truyền tải mạng.
[EXP]
Đúng. Region gần Việt Nam nhất (như Singapore) giúp rút ngắn quãng đường truyền tín hiệu vật lý, từ đó giảm độ trễ (latency) và tăng tốc kết nối.
[D]
Quy định pháp lý bắt buộc mọi máy chủ của học viên phải đặt tại Đông Nam Á.
[EXP]
Sai. Không có quy định pháp lý nào bắt buộc học viên phải đặt máy chủ thực hành tại đây, việc chọn hoàn toàn vì tối ưu mặt kỹ thuật.

@correct: C
@point: 20
@difficulty: 2
@concept: cloud-server-provisioning
@category: 1

## Q3
Hiện tượng gì sẽ xảy ra trên máy chủ Linux khi dung lượng bộ nhớ RAM bị cạn kiệt hoàn toàn do ứng dụng chạy quá tải?

[A]
Hệ điều hành tự động tăng dung lượng vCPU vật lý để bù đắp tài nguyên RAM.
[EXP]
Sai. vCPU và RAM là hai thành phần phần cứng độc lập, hệ thống không thể tự tăng cấu hình CPU vật lý khi thiếu RAM.
[B]
Cơ chế Out-Of-Memory (OOM) killer được kích hoạt để tắt bớt tiến trình.
[EXP]
Đúng. Khi cạn kiệt RAM, nhân Linux (kernel) sẽ kích hoạt cơ chế OOM killer để chấm dứt một hoặc nhiều tiến trình ngốn RAM nhằm tránh sập toàn bộ hệ điều hành.
[C]
Máy chủ sẽ tự động chuyển toàn bộ dữ liệu đang chạy trên RAM sang lưu ở card mạng.
[EXP]
Sai. Card mạng (Network Card) chỉ phục vụ truyền nhận dữ liệu, không có chức năng lưu trữ hay chạy chương trình thay thế cho bộ nhớ RAM.
[D]
Mọi dữ liệu trên ổ đĩa SSD của máy chủ ảo sẽ bị xóa sạch để giải phóng bộ nhớ.
[EXP]
Sai. Thiếu RAM chỉ ảnh hưởng đến các tiến trình đang hoạt động trong bộ nhớ tạm thời, dữ liệu ghi trên ổ đĩa cứng không bị xóa.

@correct: B
@point: 20
@difficulty: 2
@concept: cloud-server-provisioning
@category: 1

## Q4
Lệnh nào sau đây được sử dụng để tạo một cặp khóa SSH mới sử dụng thuật toán Ed25519 trên máy tính cá nhân của các bạn?

[A]
`ssh-keygen -t rsa -b 4096 -C "email"`
[EXP]
Sai. Lệnh này tạo khóa SSH sử dụng thuật toán RSA cũ hơn với độ dài khóa 4096 bit, không phải thuật toán Ed25519.
[B]
`cat ~/.ssh/id_ed25519.pub`
[EXP]
Sai. Lệnh `cat` chỉ dùng để hiển thị nội dung của tệp tin public key đã có sẵn, không có chức năng tạo mới cặp khóa.
[C]
`ssh root@<IP_ADDRESS_CỦA_DROPLET>`
[EXP]
Sai. Đây là lệnh dùng để thực hiện kết nối SSH tới máy chủ từ xa thông qua tài khoản root, không dùng để tạo khóa.
[D]
`ssh-keygen -t ed25519 -C "email"`
[EXP]
Đúng. Chỉ thị `-t ed25519` yêu cầu lệnh tạo khóa sử dụng thuật toán mã hóa hiện đại và an toàn Ed25519.

@correct: D
@point: 20
@difficulty: 2
@concept: cloud-server-provisioning
@category: 1

## Q5
Một học viên tắt máy ảo (Power Off) trong trang dashboard quản trị của Cloud Provider nhưng không chọn xóa (Destroy). Hành động này ảnh hưởng như thế nào đến tài khoản của học viên?

[A]
Tài khoản vẫn tiếp tục bị tính phí vì ổ đĩa và IP Public vẫn được giữ riêng.
[EXP]
Đúng. Khi chỉ tắt máy (Power Off), nhà cung cấp vẫn phải giữ riêng tài nguyên ổ đĩa cứng lưu trữ và địa chỉ IP Public cho tài khoản đó, do đó hệ thống vẫn tiếp tục tính phí.
[B]
Hệ thống sẽ dừng tính phí ngay lập tức vì máy chủ ảo không còn tiêu thụ điện.
[EXP]
Sai. Việc tiêu thụ điện chỉ là một phần nhỏ, chi phí giữ chỗ cho ổ cứng và tài nguyên mạng vẫn phát sinh nên học viên vẫn bị tính phí bình thường.
[C]
Toàn bộ mã nguồn ứng dụng lưu trên máy chủ ảo sẽ bị xóa sạch ngay sau khi tắt.
[EXP]
Sai. Dữ liệu trên ổ đĩa của máy chủ ảo chỉ bị xóa hoàn toàn khi học viên thực hiện lệnh xóa máy (Destroy/Delete), tắt máy không làm mất dữ liệu.
[D]
Tài khoản sẽ bị khóa vĩnh viễn do vi phạm điều khoản sử dụng tài nguyên tĩnh.
[EXP]
Sai. Đây là hành vi sử dụng dịch vụ thông thường, nhà cung cấp khuyến khích nhưng học viên cần lưu ý về chi phí phát sinh để tránh mất tiền oan.

@correct: A
@point: 20
@difficulty: 3
@concept: cloud-server-provisioning
@category: 1
