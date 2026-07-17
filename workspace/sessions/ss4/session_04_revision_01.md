---
schema_version: 1
id: ss04_revision_01
type: revision_questions
status: approved
course_id: devops-basic
session: 4
unit: 1
title: "Ôn tập - Khởi tạo và thao tác cơ bản với Git (Local)"
session_kind: theory
tags:
  - git
  - revision
concepts: []
depends_on:
  - ss04_lesson_01
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: "Session 04 / Lesson 01"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
maps_to:
  - ss04_lesson_01
lesson_mode: practical
question_count: 3
---

# Ôn tập sau bài: Khởi tạo và thao tác cơ bản với Git (Local)

## RQ1
Tại sao Git lại thiết kế vùng đệm (Staging Area/Index) nằm giữa thư mục làm việc (Working Directory) và thư mục lưu trữ chính thức (Git Directory/Repository)? Việc này mang lại lợi ích gì cho lập trình viên so với việc commit trực tiếp các thay đổi?

*Hướng dẫn trả lời:*
* **Tạo sự linh hoạt và kiểm soát tốt hơn:** Staging Area cho phép lập trình viên chọn lọc chính xác những thay đổi nào (từng tệp tin, thậm chí từng dòng code) sẽ đi vào commit tiếp theo, thay vì phải lưu toàn bộ thư mục làm việc vốn có thể chứa nhiều tệp tin nháp chưa hoàn chỉnh.
* **Tạo các commit gọn gàng, đúng nghĩa (Atomicity):** Lập trình viên có thể chia nhỏ một loạt thay đổi lớn ở local thành các commit nhỏ hơn, có ý nghĩa hơn, giúp lịch sử dự án trở nên rõ ràng và dễ theo dõi hơn.
* **Cho phép xem lại và điều chỉnh trước khi lưu trữ chính thức:** Học viên có thể chạy `git diff` để review kỹ lưỡng các thay đổi đã staged trước khi thực hiện snapshot chính thức.

## RQ2
Giả sử bạn có một file `app.js` đã được commit vào Git trước đó (đã được Git theo dõi). Bạn thực hiện chỉnh sửa nội dung file `app.js` ở máy local, sau đó chạy lệnh `git commit -m "update code"` mà hoàn toàn không chạy lệnh `git add app.js` trước đó. Thay đổi mới này của bạn có được lưu trữ vào commit mới trong Git Directory hay không? Hãy giải thích cơ chế hoạt động của Git trong trường hợp này.

*Hướng dẫn trả lời:*
* **Không được lưu trữ:** Thay đổi mới này sẽ không được đưa vào commit mới.
* **Giải thích cơ chế:** Git hoạt động theo mô hình snapshot dựa trên những gì có trong **Staging Area (Index)** chứ không dựa trên tệp tin trong Working Directory. Khi file `app.js` bị sửa đổi, trạng thái của nó ở Working Directory chuyển thành `Modified`. Do chưa chạy lệnh `git add app.js`, sự thay đổi này chưa được cập nhật vào Staging Area. Khi chạy lệnh `git commit`, Git chỉ tạo snapshot từ các thay đổi đang có trạng thái `Staged` ở vùng đệm. Vì vậy, thay đổi mới của file `app.js` vẫn sẽ nằm lại ở máy local dưới trạng thái `Modified`.

## RQ3
Khi bạn chạy lệnh `git init` để khởi tạo một dự án mới, Git sẽ tạo ra một thư mục ẩn có tên là `.git`. Hãy giải thích vai trò của thư mục `.git` này và cảnh báo điều gì sẽ xảy ra nếu lập trình viên vô tình xóa thư mục ẩn này khỏi dự án của họ.

*Hướng dẫn trả lời:*
* **Vai trò của thư mục `.git`:** Đây là thư mục lưu trữ Git (Git Directory / Repository). Nó chứa toàn bộ cơ sở dữ liệu lịch sử dự án, các file cấu hình local, các con trỏ nhánh (HEAD, refs), các index tệp tin, và toàn bộ các snapshot dữ liệu của các lần commit trước đó.
* **Cảnh báo khi bị xóa:** Nếu vô tình xóa thư mục `.git`, dự án của bạn sẽ ngay lập tức trở thành một thư mục văn bản thông thường và không còn liên kết với hệ thống quản lý phiên bản nào. Toàn bộ lịch sử commit, các nhánh đã tạo, thông tin cấu hình local, và khả năng khôi phục về các phiên bản cũ ở máy local sẽ bị **mất vĩnh viễn** (trừ khi đã được push và đồng bộ lên một remote repository từ xa như GitHub).
