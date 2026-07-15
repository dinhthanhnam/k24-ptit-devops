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
created: '2026-07-15'
updated: '2026-07-15'
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
Trong cơ chế phân quyền lệnh của CPU (CPU Rings), lớp Hypervisor và hệ điều hành máy ảo (Guest OS) thông thường được phân bổ chạy ở các phân cấp nào để bảo đảm tính an toàn bảo mật hệ thống?

[A]
Hypervisor chạy ở Ring 3, Guest OS chạy ở Ring 0.
[EXP]
Sai. Ring 3 có đặc quyền thấp nhất dành cho ứng dụng, không thể chạy Hypervisor tại đây.
[B]
Cả Hypervisor và Guest OS đều chạy trực tiếp chung ở Ring 0.
[EXP]
Sai. Nếu chạy chung Ring 0 vật lý, tính cô lập giữa các máy ảo sẽ bị phá vỡ hoàn toàn do Guest OS có thể can thiệp phần cứng.
[C]
Hypervisor kiểm soát Ring 0, Guest OS bị giới hạn ở Ring thấp hơn hoặc Ring ảo.
[EXP]
Đúng. Hypervisor cần giữ quyền tối cao ở Ring 0 vật lý để quản trị hệ thống, đẩy Guest OS xuống các Ring thấp hơn (hoặc Ring ảo) để kiểm soát các lệnh nhạy cảm.
[D]
Hypervisor chạy ở Ring 1, Guest OS chạy ở Ring 3.
[EXP]
Sai. Cấu hình này khiến Hypervisor không có đủ đặc quyền quản lý phần cứng (Ring 1 không có đủ thẩm quyền như Ring 0).

@correct: C
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
Dốc mốc lịch sử nào sau đây đánh dấu sự ra đời của giải pháp ảo hóa thương mại đầu tiên cho phép nhiều máy ảo chia sẻ tài nguyên phần cứng?

[A]
VMware ra mắt công nghệ dịch nhị phân x86 vào năm 1990.
[EXP]
Sai. VMware thành lập và nộp bằng sáng chế vào năm 1998, không phải năm 1990.
[B]
Dự án phát triển hệ điều hành CP-40 của IBM cho phần cứng System/360 vào năm 1967.
[EXP]
Đúng. CP-40 phát triển năm 1967 là hệ thống máy ảo thương mại đầu tiên chạy trên nền tảng máy Mainframe để chia sẻ tài nguyên đắt đỏ.
[C]
Intel công bố công nghệ hỗ trợ phần cứng Intel VT-x Vanderpool vào năm 1998.
[EXP]
Sai. Intel VT-x được giới thiệu vào năm 2005, không phải 1998.
[D]
AMD giới thiệu AMD-V Pacifica trên dòng chip Athlon 64 vào năm 1960.
[EXP]
Sai. AMD-V được giới thiệu vào năm 2006, không phải 1960.

@correct: B
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
