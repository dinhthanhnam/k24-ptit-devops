---
schema_version: 1
id: ss02_quiz_lesson_01
type: quiz
status: approved
course_id: devops-basic
session: 2
unit: 1
title: Quiz — Khái niệm ảo hóa (Virtualization)
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_01
builds_on: []
enables: []
owns: []
assumes:
- virtualization-basics
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / quiz_lesson / L01
language: vi
created: '2026-07-14'
updated: '2026-07-14'
quiz_kind: lesson
question_count: 5
maps_to:
- ss02_lesson_01
---

# Quiz — Khái niệm ảo hóa (Virtualization)

## Q1
Mục đích chính của công nghệ ảo hóa (Virtualization) trong việc tối ưu hóa hạ tầng công nghệ thông tin là gì?

[A]
Tăng tốc độ truy cập internet vật lý cho các máy chủ trong trung tâm dữ liệu.
[EXP]
Sai. Ảo hóa không tác động trực tiếp vào đường truyền vật lý hay băng thông internet của máy chủ.
[B]
Chia nhỏ tài nguyên phần cứng vật lý thành nhiều môi trường ảo hóa độc lập.
[EXP]
Đúng. Ảo hóa giúp phân chia các tài nguyên vật lý (CPU, RAM, Disk) để tạo ra các máy ảo hoạt động độc lập và tối ưu hiệu suất sử dụng.
[C]
Dịch tự động các tập lệnh của hệ điều hành này sang hệ điều hành khác chạy song song.
[EXP]
Sai. Đây là chức năng giả lập (Emulation) hoặc dịch tập lệnh, không phải mục tiêu cốt lõi của ảo hóa.
[D]
Thay thế hoàn toàn phần cứng vật lý bằng các linh kiện điện tử hoạt động trên đám mây.
[EXP]
Sai. Ảo hóa vẫn phải chạy trên hạ tầng phần cứng vật lý thực tế của trung tâm dữ liệu.

@correct: B
@point: 20
@difficulty: 1
@concept: virtualization-basics
@category: 1

## Q2
Trong hệ thống ảo hóa, thành phần phần mềm nào chịu trách nhiệm trực tiếp trong việc quản lý và phân phối tài nguyên phần cứng vật lý cho các máy ảo?

[A]
Hypervisor (hoặc VMM - Virtual Machine Monitor).
[EXP]
Đúng. Hypervisor là lớp phần mềm quản lý việc trừu tượng hóa và phân phối tài nguyên vật lý cho các máy ảo một cách an toàn và cô lập.
[B]
Hệ điều hành khách (Guest Operating System).
[EXP]
Sai. Guest OS chạy bên trong máy ảo, nó chỉ sử dụng tài nguyên được cấp phát chứ không có quyền quản lý hay phân phối phần cứng vật lý bên dưới.
[C]
Ứng dụng Containerization (như dịch vụ Docker).
[EXP]
Sai. Containerization là công nghệ ảo hóa ở cấp độ hệ điều hành, hoạt động phía trên hệ điều hành và không quản lý trực tiếp phần cứng vật lý của máy chủ.
[D]
Giao diện dòng lệnh (Command Line Interface).
[EXP]
Sai. CLI chỉ là công cụ giao tiếp bằng văn bản giữa người dùng và hệ điều hành, không quản lý tài nguyên.

@correct: A
@point: 20
@difficulty: 2
@concept: virtualization-basics
@category: 1

## Q3
Khi thiết kế hệ thống ảo hóa cho một trung tâm dữ liệu (Data Center) yêu cầu hiệu năng cao nhất và độ trễ thấp nhất, lựa chọn nào sau đây là phù hợp nhất?

[A]
Cài đặt Hypervisor Type 2 chạy trên nền tảng của hệ điều hành Windows Server.
[EXP]
Sai. Hypervisor Type 2 phải đi qua một lớp hệ điều hành Host trung gian nên hiệu năng sẽ bị hạn chế và độ trễ cao hơn.
[B]
Triển khai toàn bộ hệ thống bằng phần mềm giả lập kiến trúc tập lệnh (Emulation).
[EXP]
Sai. Giả lập tiêu tốn cực kỳ nhiều tài nguyên do phải dịch tập lệnh bằng phần mềm, hiệu năng rất thấp.
[C]
Sử dụng Hypervisor Type 1 cài đặt trực tiếp lên phần cứng của máy chủ vật lý.
[EXP]
Đúng. Hypervisor Type 1 hoạt động trực tiếp trên phần cứng vật lý mà không cần OS trung gian nên mang lại hiệu năng cao nhất và độ trễ thấp nhất.
[D]
Cài đặt Hypervisor Type 2 chạy trên nền tảng của hệ điều hành Linux Ubuntu.
[EXP]
Sai. Mặc dù Linux nhẹ nhưng Hypervisor Type 2 vẫn phải chạy qua lớp Host OS, không thể đạt hiệu năng tối ưu như Type 1.

@correct: C
@point: 20
@difficulty: 2
@concept: virtualization-basics
@category: 1

## Q4
Đặc điểm nào dưới đây mô tả chính xác nhất về trạng thái hoạt động của một Máy ảo (Virtual Machine - VM)?

[A]
Không thể cài đặt hệ điều hành riêng biệt mà phải dùng chung với máy chủ vật lý.
[EXP]
Sai. Mỗi máy ảo có thể cài đặt một Hệ điều hành khách (Guest OS) hoàn toàn độc lập với máy chủ vật lý và các máy ảo khác.
[B]
Khi một máy ảo bị nhiễm virus thì toàn bộ các máy ảo khác sẽ bị lây nhiễm ngay lập tức.
[EXP]
Sai. Hypervisor đảm bảo tính cô lập hoàn toàn giữa các máy ảo, lỗi hoặc mã độc từ một máy ảo không thể tự lây lan sang máy khác.
[C]
Dữ liệu của máy ảo được lưu trữ trực tiếp lên RAM vật lý dưới dạng các biến tạm thời.
[EXP]
Sai. Máy ảo lưu trữ dữ liệu bền vững dưới dạng các tệp tin cấu hình và ổ đĩa ảo trên bộ nhớ lưu trữ vật lý của server.
[D]
Hoạt động độc lập như một máy tính vật lý thật với đầy đủ cấu hình phần cứng ảo hóa.
[EXP]
Đúng. Máy ảo hoạt động hoàn toàn độc lập, có vCPU, RAM ảo, ổ cứng ảo và card mạng ảo do Hypervisor cấp phát.

@correct: D
@point: 20
@difficulty: 2
@concept: virtualization-basics
@category: 1

## Q5
Sự khác biệt cơ bản nhất về cơ chế hoạt động giữa Ảo hóa (Virtualization) và Giả lập (Emulation) là gì?

[A]
Ảo hóa yêu cầu bản quyền phần mềm đắt tiền còn giả lập hoàn toàn miễn phí.
[EXP]
Sai. Cả hai công nghệ đều có các giải pháp mã nguồn mở miễn phí hoặc phiên bản thương mại có phí.
[B]
Ảo hóa chia sẻ kiến trúc phần cứng của Host, giả lập phải dịch tập lệnh bằng code.
[EXP]
Đúng. Ảo hóa chia sẻ trực tiếp kiến trúc tập lệnh của máy vật lý nên hiệu năng cao, còn giả lập phải dịch chuyển tập lệnh giữa các kiến trúc khác nhau nên rất chậm.
[C]
Giả lập chỉ chạy được ứng dụng di động còn ảo hóa chỉ chạy được hệ điều hành Windows.
[EXP]
Sai. Giả lập và ảo hóa đều có thể chạy nhiều loại hệ điều hành và ứng dụng khác nhau tùy cấu hình.
[D]
Ảo hóa hoạt động trên đám mây còn giả lập chỉ hoạt động được trên máy tính cá nhân.
[EXP]
Sai. Cả hai công nghệ đều có thể chạy trên máy tính cá nhân hoặc trên hạ tầng máy chủ đám mây.

@correct: B
@point: 20
@difficulty: 3
@concept: virtualization-basics
@category: 1
