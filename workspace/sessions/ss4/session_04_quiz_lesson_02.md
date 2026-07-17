---
schema_version: 1
id: ss04_quiz_lesson_02
type: quiz
status: approved
course_id: devops-basic
session: 4
unit: 2
title: "Quiz Lesson 02 - Quản lý Nhánh (Branching) và xử lý Xung đột"
session_kind: theory
quiz_kind: lesson
question_count: 5
maps_to:
  - ss04_lesson_02
depends_on:
  - ss04_lesson_02
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: "Session 04 / Lesson 02"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
---

# Quiz Lesson 02 — Quản lý Nhánh (Branching) và xử lý Xung đột

## Q1
Trong hệ thống quản lý phiên bản Git, bản chất thực sự của một "Nhánh" (Branch) là gì?

[A]
Là một bản sao thư mục độc lập trên ổ đĩa cứng được sao chép hoàn toàn từ dự án gốc.
[EXP]
Git không sao chép vật lý các thư mục khi tạo nhánh mới, giúp thao tác tạo và chuyển nhánh diễn ra tức thời.
[B]
Là một con trỏ di động trỏ trực tiếp đến một commit cụ thể trong lịch sử của dự án.
[EXP]
Đúng. Nhánh trong Git chỉ đơn giản là một con trỏ (movable pointer) trỏ đến một commit cụ thể. Khi có commit mới, con trỏ tự động di chuyển tiến lên.
[C]
Là một file nén zip lưu trữ toàn bộ các snapshot dữ liệu lịch sử được đồng bộ lên máy chủ.
[EXP]
Tệp nén zip không phải là định nghĩa của nhánh. Nhánh chỉ là con trỏ nhẹ tham chiếu đến commit.
[D]
Là một nhãn đánh dấu cố định gắn liền với tác giả tạo ra commit đó và không thể di dời.
[EXP]
Nhãn cố định không thể di dời là đặc điểm của thẻ (Tag), không phải của nhánh (Branch) vốn liên tục di động khi có commit mới.

@correct: B
@point: 20
@difficulty: 1
@concept: git-branching-conflicts
@category: 1

## Q2
Lập trình viên muốn tạo một nhánh mới tên là `feature-payment` để phát triển tính năng thanh toán, đồng thời tự động chuyển ngay sang nhánh này. Lệnh Git nào dưới đây thực hiện đúng và nhanh nhất yêu cầu trên?

[A]
`git branch feature-payment`
[EXP]
Lệnh này chỉ tạo ra nhánh mới mà không tự động chuyển sang nhánh đó. Lập trình viên vẫn đứng ở nhánh cũ.
[B]
`git checkout -b feature-payment`
[EXP]
Đúng. Lệnh `git checkout -b` (hoặc `git switch -c`) thực hiện song song cả hai việc: tạo mới nhánh và chuyển nhánh làm việc sang nhánh đó.
[C]
`git merge feature-payment`
[EXP]
Lệnh này dùng để gộp nhánh `feature-payment` vào nhánh hiện hành, không có tác dụng tạo mới hay chuyển nhánh.
[D]
`git log feature-payment`
[EXP]
Lệnh này dùng để xem lịch sử commit của nhánh `feature-payment` chứ không dùng để khởi tạo hay di chuyển nhánh làm việc.

@correct: B
@point: 20
@difficulty: 2
@concept: git-branching-conflicts
@category: 1

## Q3
Trong trường hợp nào dưới đây Git sẽ thực hiện cơ chế gộp nhánh kiểu **3-Way Merge** (Recursive Merge) thay vì **Fast-forward Merge**?

[A]
Nhánh chính `main` không hề có thêm commit nào mới kể từ khi nhánh phụ được tách ra.
[EXP]
Trong trường hợp này, Git sẽ thực hiện Fast-forward Merge bằng cách dời thẳng con trỏ nhánh `main` lên mà không cần tạo commit gộp.
[B]
Nhánh phụ được tạo ra và chưa có bất kỳ commit nào mới so với commit gốc của nhánh chính.
[EXP]
Nếu nhánh phụ không có commit mới, việc merge sẽ không làm thay đổi mã nguồn và không cần tạo commit gộp mới hay 3-way merge.
[C]
Lập trình viên chạy lệnh gộp nhánh kèm theo tùy chọn `--abort` trên terminal của máy cá nhân.
[EXP]
Tùy chọn `--abort` dùng để hủy bỏ quá trình gộp nhánh khi xảy ra xung đột chứ không phải cơ chế thực hiện gộp nhánh.
[D]
Nhánh chính `main` đã phát sinh thêm các commit mới song song kể từ khi nhánh phụ được tách ra.
[EXP]
Đúng. Khi cả hai nhánh đều có những commit mới độc lập kể từ điểm rẽ nhánh, Git phải sử dụng thuật toán 3-Way Merge để tạo ra một commit gộp mới.

@correct: D
@point: 20
@difficulty: 2
@concept: git-branching-conflicts
@category: 1


## Q4
Khi xảy ra hiện tượng xung đột gộp (Merge Conflict), tệp tin bị xung đột sẽ nằm ở trạng thái nào dưới đây khi chạy lệnh kiểm tra `git status`?

[A]
Untracked (Tệp tin bị xung đột chưa được đưa vào hệ thống theo dõi lịch sử của Git).
[EXP]
Tệp tin xung đột phải là tệp tin đã được theo dõi (tracked) bởi Git từ trước nên không thể là Untracked.
[B]
Staged (Tệp tin đã được giải quyết xung đột thành công và sẵn sàng để ghi nhận commit).
[EXP]
Khi vừa xảy ra conflict, tệp tin ở trạng thái chưa được giải quyết và chưa sẵn sàng commit. Chỉ sau khi chạy `git add`, nó mới là Staged.
[C]
Both modified (Tệp tin được chỉnh sửa ở cả hai nhánh và Git đang chờ người dùng giải quyết thủ công).
[EXP]
Đúng. Khi gặp conflict, lệnh `git status` sẽ liệt kê tệp tin đó dưới trạng thái `Both modified` (cả hai nhánh cùng sửa đổi).
[D]
Clean (Thư mục làm việc hoàn toàn sạch sẽ và không có thay đổi nào cần xử lý).
[EXP]
Thư mục làm việc đang có xung đột chưa giải quyết nên không thể ở trạng thái sạch (clean).

@correct: C
@point: 20
@difficulty: 3
@concept: git-branching-conflicts
@category: 1

## Q5
Trong quá trình gộp nhánh `feature-ui` vào `main`, terminal báo lỗi Merge Conflict. Lập trình viên phát hiện mình bị nhầm lẫn và muốn hủy bỏ hoàn toàn lệnh merge này để đưa toàn bộ code quay về trạng thái an toàn trước khi chạy lệnh merge. Lệnh nào dưới đây đáp ứng yêu cầu đó?

[A]
`git merge --abort`
[EXP]
Đúng. Lệnh `git merge --abort` sẽ dừng quá trình merge đang bị xung đột và khôi phục lại trạng thái của repository về trước khi chạy lệnh merge.
[B]
`git add .`
[EXP]
Lệnh `git add .` dùng để đưa các file đã giải quyết xong xung đột vào Staging Area để chuẩn bị commit, không có tác dụng hủy merge.
[C]
`git commit -m "abort"`
[EXP]
Bạn không thể commit khi dự án đang bị xung đột chưa giải quyết. Lệnh này sẽ bị Git từ chối và báo lỗi.
[D]
`git branch -d feature-ui`
[EXP]
Bạn không thể xóa nhánh `feature-ui` khi đang trong quá trình merge nhánh đó. Hơn nữa lệnh này không có tác dụng khôi phục lại code.

@correct: A
@point: 20
@difficulty: 3
@concept: git-branching-conflicts
@category: 1
