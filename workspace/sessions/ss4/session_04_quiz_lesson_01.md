---
schema_version: 1
id: ss04_quiz_lesson_01
type: quiz
status: approved
course_id: devops-basic
session: 4
unit: 1
title: "Quiz Lesson 01 - Khởi tạo và thao tác cơ bản với Git (Local)"
session_kind: theory
quiz_kind: lesson
question_count: 5
maps_to:
  - ss04_lesson_01
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
---

# Quiz Lesson 01 — Khởi tạo và thao tác cơ bản với Git (Local)

## Q1
Trong kiến trúc lưu trữ của Git, hệ thống quản lý phiên bản phân tán (DVCS) này khác biệt như thế nào so với hệ thống quản lý phiên bản tập trung (CVCS) truyền thống?

[A]
Mỗi lập trình viên chỉ cần tải phiên bản code mới nhất về máy và thực hiện mọi commit trực tiếp lên một server chung duy nhất.
[EXP]
Đây là đặc điểm hoạt động của hệ thống quản lý phiên bản tập trung (CVCS), không phải hệ thống phân tán (DVCS).
[B]
Mỗi lập trình viên đều sở hữu một bản sao đầy đủ của toàn bộ lịch sử commit dự án trên máy cá nhân thay vì chỉ chứa file hiện tại.
[EXP]
Đây là điểm cốt lõi của DVCS. Git lưu trữ toàn bộ lịch sử commit tại máy local, cho phép làm việc độc lập và offline trước khi push.
[C]
Mọi lịch sử commit của dự án được lưu trữ độc quyền trên Cloud và máy cá nhân của lập trình viên hoàn toàn không lưu trữ tệp tin `.git`.
[EXP]
Lịch sử commit được lưu trữ ngay trong thư mục ẩn `.git` tại máy local của lập trình viên, không bắt buộc phải đẩy lên Cloud.
[D]
Git không hỗ trợ khả năng xem lịch sử commit hoặc so sánh các phiên bản khác nhau khi máy tính cá nhân không kết nối internet.
[EXP]
Lập trình viên hoàn toàn có thể xem log, chạy git diff và so sánh các phiên bản ngoại tuyến vì cơ sở dữ liệu đã có sẵn ở local.

@correct: B
@point: 20
@difficulty: 1
@concept: git-local-basics
@category: 1

## Q2
Học viên khởi tạo một tệp tin mới có tên là `app.js` trong thư mục dự án vừa chạy lệnh `git init`. Khi chạy lệnh `git status`, trạng thái mặc định của tệp tin `app.js` này được Git ghi nhận là gì?

[A]
Modified (Tệp tin đã có trong commit trước đó nhưng vừa phát sinh chỉnh sửa mới tại thư mục làm việc local).
[EXP]
Modified chỉ xảy ra khi file đã từng được Git theo dõi trước đó. File mới tạo hoàn toàn chưa được theo dõi nên không thể là Modified.
[B]
Staged (Tệp tin đã được chuyển vào vùng đệm và sẵn sàng ghi nhận snapshot vào lịch sử trong lần commit tiếp theo).
[EXP]
File mới tạo chỉ chuyển sang trạng thái Staged sau khi học viên chạy lệnh `git add`. Hiện tại file chưa được thêm vào vùng đệm.
[C]
Untracked (Tệp tin mới tạo chưa được đưa vào vùng đệm Staging Area và Git chưa thực hiện theo dõi thay đổi).
[EXP]
Đúng. Bất kỳ file mới tạo nào trong thư mục làm việc đều mặc định ở trạng thái Untracked cho đến khi chạy lệnh `git add`.
[D]
Committed (Tệp tin đã được lưu trữ an toàn trong cơ sở dữ liệu lịch sử và thư mục làm việc của dự án hoàn toàn sạch).
[EXP]
File chỉ ở trạng thái Committed sau khi chạy lệnh `git commit`. File mới tạo chưa thể được ghi nhận tự động vào lịch sử.

@correct: C
@point: 20
@difficulty: 2
@concept: git-local-basics
@category: 1

## Q3
Khi học viên cài đặt Git trên máy tính cá nhân mới và thực hiện lệnh `git commit` lần đầu tiên, hành động này sẽ gặp lỗi và bị Git ngăn chặn nếu thiếu cấu hình thông tin nào dưới đây?

[A]
Thiếu cấu hình địa chỉ IP tĩnh của máy chủ Git chứa repository trung tâm để đồng bộ mã nguồn.
[EXP]
Git hoạt động local nên không cần IP tĩnh của máy chủ chứa repository trung tâm khi thực hiện commit ở local.
[B]
Thiếu cấu hình thông tin định danh tác giả bao gồm tên người dùng (user.name) và email (user.email).
[EXP]
Đúng. Git bắt buộc phải biết ai là tác giả tạo ra commit để ghi vào siêu dữ liệu (metadata) lịch sử. Nếu thiếu, Git sẽ báo lỗi.
[C]
Thiếu cấu hình đường dẫn tuyệt đối đến tệp tin thực thi của trình soạn thảo mã nguồn mặc định trên OS.
[EXP]
Nếu không cấu hình editor, Git sẽ tự động sử dụng trình soạn thảo mặc định của hệ điều hành (như Vim hoặc Nano) chứ không báo lỗi dừng commit.
[D]
Thiếu cấu hình khóa công khai SSH Key kết nối trực tiếp đến tài khoản cá nhân trên nền tảng GitHub.
[EXP]
Việc commit ở local hoàn toàn độc lập với việc kết nối SSH Key lên GitHub. Khóa SSH chỉ cần khi đẩy code lên remote server.

@correct: B
@point: 20
@difficulty: 3
@concept: git-local-basics
@category: 1

## Q4
Trong quá trình làm việc với dự án, học viên muốn xem lại danh sách lịch sử các commit đã thực hiện kèm theo thông tin tác giả và thời gian ghi nhận. Lệnh Git nào dưới đây đáp ứng yêu cầu này?

[A]
`git status`
[EXP]
Lệnh `git status` dùng để xem trạng thái hiện tại của các file (Untracked, Modified, Staged) chứ không hiển thị lịch sử commit.
[B]
`git diff`
[EXP]
Lệnh `git diff` dùng để so sánh sự khác biệt nội dung giữa Working Directory và Staging Area chứ không hiển thị danh sách commit.
[C]
`git init`
[EXP]
Lệnh `git init` dùng để khởi tạo một Git repository mới trong thư mục hiện hành chứ không dùng để truy xuất lịch sử.
[D]
`git log`
[EXP]
Đúng. Lệnh `git log` hiển thị toàn bộ danh sách lịch sử các commit đã thực hiện theo thứ tự thời gian từ mới nhất đến cũ nhất.

@correct: D
@point: 20
@difficulty: 2
@concept: git-local-basics
@category: 1

## Q5
Học viên chỉnh sửa file `index.html`, chạy lệnh `git add index.html`. Sau đó học viên tiếp tục chỉnh sửa file `index.html` lần thứ hai rồi chạy lệnh `git commit -m "Update homepage"`. Trạng thái của phần chỉnh sửa lần thứ hai sau khi commit là gì?

[A]
Được ghi nhận đầy đủ vào commit mới cùng với lần chỉnh sửa thứ nhất do cùng thuộc một tệp tin.
[EXP]
Git không commit theo tệp tin mà commit theo snapshot tại Staging Area. Những thay đổi sau lệnh `git add` sẽ không được đưa vào commit.
[B]
Bị Git tự động xóa bỏ hoàn toàn khỏi thư mục làm việc để đảm bảo tính đồng bộ với Staging Area.
[EXP]
Git không bao giờ tự động xóa code của người dùng trong thư mục làm việc Working Directory khi commit.
[C]
Nằm lại thư mục làm việc Working Directory ở trạng thái Modified và chưa được đưa vào commit mới.
[EXP]
Đúng. Lần sửa thứ hai xảy ra sau lệnh `git add` nên nó chưa được cập nhật vào Staging Area. Do đó khi commit, nó sẽ ở lại Working Directory dưới dạng Modified.
[D]
Bị lỗi xung đột tệp tin (Conflict) và hệ thống yêu cầu học viên phải merge thủ công trước khi commit.
[EXP]
Xung đột (Conflict) chỉ xảy ra khi merge các nhánh có thay đổi chồng chéo, không xảy ra trong quy trình commit thông thường ở local.

@correct: C
@point: 20
@difficulty: 3
@concept: git-local-basics
@category: 1
