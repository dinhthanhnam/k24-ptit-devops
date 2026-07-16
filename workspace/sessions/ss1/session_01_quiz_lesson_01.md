---
schema_version: 1
id: ss01_quiz_lesson_01
type: quiz
status: draft
course_id: devops-basic
session: 1
unit: 1
title: Quiz — Định hướng môn học DevOps in Action
session_kind: theory
tags:
- devops
- introduction
concepts:
- devops-introduction
depends_on:
- ss01_lesson_01
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: Session 01 / quiz_lesson_01
language: vi
created: '2026-07-16'
updated: '2026-07-16'
quiz_kind: lesson
question_count: 5
maps_to:
- ss01_lesson_01
---

# Quiz — Định hướng môn học DevOps in Action

## Q1
DevOps thực chất là gì? Chọn câu trả lời chính xác nhất để tránh bị các "DevOps lão làng" trêu chọc.

[A]
Là một loại công cụ thần kỳ chỉ cần mua về cài vào máy là toàn bộ hệ thống tự động vận hành 100% không cần con người.
[EXP]
Sai. DevOps không đơn thuần là một công cụ hay phần mềm mua sẵn; việc cài đặt công cụ mà không cải tiến quy trình và văn hóa làm việc sẽ không mang lại hiệu quả.
[B]
Là sự kết hợp giữa văn hóa, quy trình và công cụ giúp đội ngũ Phát triển (Dev) và Vận hành (Ops) hợp tác nhịp nhàng để phát hành sản phẩm nhanh và ổn định hơn.
[EXP]
Đúng. DevOps là văn hóa kết hợp con người, quy trình và các công cụ bổ trợ nhằm rút ngắn thời gian bàn giao và tăng độ ổn định của phần mềm.
[C]
Là tên một loại cà phê đặc biệt giúp các lập trình viên thức xuyên đêm làm việc mà không thấy mệt mỏi.
[EXP]
Sai. Đây là một câu trả lời tếu táo, không liên quan đến định nghĩa thực tế của DevOps trong phát triển phần mềm.
[D]
Là một chức danh công việc của một người chuyên đứng ra chịu trách nhiệm và đi đổ lỗi mỗi khi hệ thống server gặp sự cố.
[EXP]
Sai. DevOps đề cao tính chịu trách nhiệm chung và phối hợp tập thể, không phải nơi để tìm kiếm cá nhân đổ lỗi khi gặp sự cố.

@correct: B
@point: 20
@difficulty: 1
@concept: devops-introduction
@category: 1

## Q2
Trong mô hình phát triển phần mềm truyền thống trước khi có DevOps, mối quan hệ giữa Dev (Lập trình) và Ops (Vận hành) thường xuất hiện hiện tượng tiêu cực nào?

[A]
Dev viết code xong sẽ chuyển giao qua "bức tường hoang mang" (Wall of Confusion) cho Ops tự xử lý, dẫn đến sự thiếu đồng bộ và chậm trễ triển khai.
[EXP]
Đúng. Sự cô lập giữa Dev (muốn thay đổi nhanh) và Ops (muốn hệ thống ổn định) tạo ra "bức tường hoang mang" làm tăng thời gian đưa sản phẩm ra thị trường.
[B]
Dev và Ops luôn ngồi chung một bàn, cùng ăn trưa và thảo luận rất vui vẻ về cách thiết kế cơ sở dữ liệu mỗi ngày.
[EXP]
Sai. Đây là trạng thái lý tưởng của DevOps, không phải hiện tượng tiêu cực trong mô hình truyền thống (Silo).
[C]
Ops chủ động viết hộ các tính năng mới cho Dev để kịp tiến độ giao sản phẩm mà không cần kiểm thử.
[EXP]
Sai. Ops chịu trách nhiệm vận hành, không viết mã nguồn tính năng ứng dụng hộ cho bộ phận phát triển.
[D]
Dev và Ops dùng chung một tài khoản quản trị hệ thống và không bao giờ xảy ra xung đột khi gõ lệnh.
[EXP]
Sai. Trong mô hình cũ, hai bộ phận phân chia tài khoản cực kỳ nghiêm ngặt, việc dùng chung tài khoản không phản ánh bản chất phân tách truyền thống.

@correct: A
@point: 20
@difficulty: 1
@concept: devops-introduction
@category: 1

## Q3
Mô hình quy trình DevOps thường được biểu diễn trực quan nhất bằng hình vẽ nào dưới đây thể hiện sự lặp lại liên tục?

[A]
Hình tròn hoàn hảo để tượng trưng cho sự trọn vẹn và không bao giờ xảy ra lỗi trong quá trình chạy.
[EXP]
Sai. Quy trình phát triển thực tế luôn có lỗi xảy ra và cần cải tiến liên tục, hình tròn đơn giản không lột tả được các giai đoạn đan xen.
[B]
Hình tam giác đều tượng trưng cho sự vững chắc của hạ tầng và đội ngũ nhân sự.
[EXP]
Sai. Hình tam giác không được dùng làm biểu tượng chuẩn để mô tả quy trình DevOps.
[C]
Hình vô cực (infinity loop) bao gồm các giai đoạn đan xen liên tục từ Plan, Code, Build, Test đến Release, Deploy, Operate và Monitor.
[EXP]
Đúng. Vòng lặp vô cực thể hiện tính liên tục, không ngừng nghỉ của chu kỳ phản hồi và cải tiến phần mềm trong DevOps.
[D]
Hình zigzag gồ ghề thể hiện đường đi gian nan của các lỗi phát sinh trong hệ thống.
[EXP]
Sai. Mặc dù quy trình có khó khăn nhưng hình zigzag không phải là biểu tượng chuẩn được công nhận của DevOps.

@correct: C
@point: 20
@difficulty: 1
@concept: devops-introduction
@category: 1

## Q4
Hiểu lầm tai hại và phổ biến nhất của người mới khi bắt đầu tiếp cận DevOps là gì?

[A]
Cho rằng làm DevOps bắt buộc phải biết sử dụng hệ điều hành Linux cơ bản.
[EXP]
Sai. Đây là yêu cầu thực tế và kỹ năng cần thiết để làm việc với máy chủ, không phải hiểu lầm tai hại.
[B]
Nghĩ rằng chỉ cần cài đặt thành thạo các công cụ như Docker, Jenkins hay Kubernetes là đã giải quyết xong bài toán DevOps.
[EXP]
Đúng. Công cụ chỉ là phương tiện; nếu không thay đổi tư duy phối hợp con người và tối ưu quy trình làm việc thì hệ thống vẫn không đạt hiệu quả DevOps.
[C]
Hiểu rằng DevOps yêu cầu sự thay đổi lớn về mặt văn hóa phối hợp giữa các phòng ban.
[EXP]
Sai. Đây là nhận thức đúng đắn và cốt lõi của DevOps, không phải hiểu lầm.
[D]
Nghĩ rằng làm DevOps đòi hỏi phải thực hành gõ lệnh thực tế nhiều hơn là học thuộc lý thuyết suông.
[EXP]
Sai. Thực hành gõ lệnh là phương pháp học tập đúng đắn được khuyến nghị đối với kỹ năng thực chiến DevOps.

@correct: B
@point: 20
@difficulty: 1
@concept: devops-introduction
@category: 1

## Q5
Để đạt kết quả tốt nhất khi theo học môn "DevOps Basics" tại PTIT, học viên cần chuẩn bị tâm thế học tập như thế nào?

[A]
Chỉ cần học thuộc lòng toàn bộ slide bài giảng lý thuyết trước ngày thi để lấy điểm số cao mà không cần thực hành.
[EXP]
Sai. Học thuộc lòng không giúp học viên làm chủ được kỹ năng thực chiến của máy chủ hay CI/CD.
[B]
Chủ động tự tay thực hành gõ lệnh trên server ảo, không ngại đối mặt với lỗi (bug) và tích cực rèn luyện kỹ năng gỡ lỗi (debug).
[EXP]
Đúng. DevOps là kỹ năng thực hành; chỉ có việc tự gõ lệnh và gỡ lỗi thực tế mới giúp học viên làm chủ được hệ thống.
[C]
Nhờ các bạn khác trong lớp làm bài tập hộ, đến buổi thi chỉ cần copy cấu hình chạy thử là đủ.
[EXP]
Sai. Việc học đối phó này không giúp học viên có được kỹ năng thực tế khi đi làm sau này.
[D]
Đợi đến khi tốt nghiệp ra trường và đi làm thực tế ở doanh nghiệp rồi mới bắt đầu tìm hiểu về lệnh Linux hay Docker.
[EXP]
Sai. Học sớm giúp các bạn học viên PTIT có lợi thế cạnh tranh rất lớn trước khi ra trường làm việc thực tế.

@correct: B
@point: 20
@difficulty: 1
@concept: devops-introduction
@category: 1
