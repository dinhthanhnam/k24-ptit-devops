---
schema_version: 1
id: ss04_revision_02
type: revision_questions
status: approved
course_id: devops-basic
session: 4
unit: 2
title: "Ôn tập - Quản lý Nhánh (Branching) và xử lý Xung đột"
session_kind: theory
tags:
  - git
  - revision
concepts: []
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
maps_to:
  - ss04_lesson_02
lesson_mode: practical
question_count: 3
---

# Ôn tập sau bài: Quản lý Nhánh (Branching) và xử lý Xung đột

## RQ1
Hãy phân biệt rõ sự khác biệt giữa hai cơ chế gộp nhánh **Fast-forward Merge** và **3-Way Merge** (Recursive Merge) trong Git. Điều kiện cần thiết để Git thực hiện được một cú gộp Fast-forward là gì?

*Hướng dẫn trả lời:*
* **Sự khác biệt cốt lõi:**
  * *Fast-forward Merge:* Git không tạo ra một commit gộp (merge commit) mới mà chỉ đơn giản là dịch chuyển con trỏ nhánh hiện tại tiến lên phía trước để trùng khớp với con trỏ của nhánh được gộp vào. Lịch sử commit sẽ là một đường thẳng liên tục.
  * *3-Way Merge:* Git tạo ra một commit gộp mới (merge commit) để lưu trữ snapshot kết hợp của cả hai nhánh. Lịch sử commit sẽ hiển thị luồng phân nhánh rõ ràng (tách ra và gộp lại).
* **Điều kiện thực hiện Fast-forward:** Nhánh được gộp vào (ví dụ nhánh chính `main`) phải không có thêm bất kỳ commit mới nào được tạo ra kể từ thời điểm nhánh phụ (nhánh được merge) được tách ra.

## RQ2
Khi chạy lệnh gộp nhánh và gặp Merge Conflict, Git sẽ đánh dấu xung đột trực tiếp vào nội dung tệp tin. Hãy giải thích ý nghĩa của các dòng ký hiệu và các khối mã nguồn dưới đây:
```html
<<<<<<< HEAD
<h3>Giao dien dang nhap bang Google</h3>
=======
<h3>Giao dien dang nhap bang Facebook</h3>
>>>>>>> feature-facebook
```

*Hướng dẫn trả lời:*
* **`<<<<<<< HEAD`**: Đánh dấu bắt đầu của khối xung đột. Phần nội dung nằm ngay dưới dòng này cho tới dòng phân cách `=======` là những thay đổi thuộc về nhánh hiện hành mà bạn đang đứng làm việc (nhánh nhận gộp, được đại diện bởi con trỏ HEAD).
* **`=======`**: Dòng phân cách giữa hai khối thay đổi xung đột của hai nhánh.
* **`>>>>>>> feature-facebook`**: Đánh dấu kết thúc khối xung đột. Phần nội dung nằm giữa dòng phân cách `=======` và dòng này là những thay đổi của nhánh phụ đang được gộp vào (ở đây là nhánh `feature-facebook`).

## RQ3
Giả sử bạn đang giải quyết một ca xung đột phức tạp trong file cấu hình và phát hiện ra mình đã xóa nhầm một số logic quan trọng, đồng thời muốn hủy bỏ toàn bộ lệnh merge hiện tại để quay về trạng thái sạch sẽ trước khi chạy lệnh merge, bạn cần dùng lệnh nào? Sau khi đã sửa xong xung đột trong file, bạn cần chạy những lệnh nào tiếp theo để chính thức đóng commit gộp?

*Hướng dẫn trả lời:*
* **Lệnh hủy bỏ merge đang bị xung đột:** Chạy lệnh `git merge --abort`. Lệnh này sẽ đưa toàn bộ dự án và tệp tin trở lại trạng thái ngay trước khi chạy lệnh gộp nhánh `git merge`.
* **Các bước hoàn tất merge sau khi đã sửa xong file:**
  1. Chạy lệnh `git add <tên_file_bị_xung_đột>` (ví dụ: `git add login.html`) để thông báo cho Git biết file đó đã được giải quyết xung đột xong và đưa file vào Staging Area.
  2. Chạy lệnh `git commit -m "Merge branch and resolve conflict"` để tạo commit gộp chính thức lưu lại lịch sử.
