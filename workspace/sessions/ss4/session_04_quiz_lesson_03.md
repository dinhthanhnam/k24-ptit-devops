---
schema_version: 1
id: ss04_quiz_lesson_03
type: quiz
status: approved
course_id: devops-basic
session: 4
unit: 3
title: "Quiz Lesson 03 - Làm việc Từ xa với GitHub và quy trình Teamwork"
session_kind: theory
quiz_kind: lesson
question_count: 5
maps_to:
  - ss04_lesson_03
depends_on:
  - ss04_lesson_03
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: "Session 04 / Lesson 03"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
---

# Quiz Lesson 03 — Làm việc Từ xa với GitHub và quy trình Teamwork

## Q1
Để cấu hình xác thực an toàn không dùng mật khẩu giữa máy tính cá nhân local và tài khoản GitHub, học viên cần sao chép nội dung của tệp tin nào để tải lên mục cấu hình SSH Key trên GitHub Console?

[A]
`~/.ssh/id_ed25519`
[EXP]
Đây là Khóa riêng tư (Private Key), cần giữ bí mật tuyệt đối ở local. Chia sẻ file này sẽ làm rò rỉ toàn bộ tài khoản bảo mật của bạn.
[B]
`~/.ssh/id_ed25519.pub`
[EXP]
Đúng. Tệp tin có đuôi `.pub` là Khóa công khai (Public Key), dùng để tải lên cấu hình trên GitHub để làm cơ sở đối chiếu xác thực chữ ký số.
[C]
`~/.ssh/config`
[EXP]
Tệp `config` là file cấu hình các host SSH ở máy local, không phải khóa công khai dùng để cấu hình xác thực trên GitHub Console.
[D]
`~/.ssh/known_hosts`
[EXP]
Tệp `known_hosts` lưu trữ dấu vân tay (fingerprint) của các server mà bạn từng kết nối để phòng tránh giả mạo, không phải khóa công khai của bạn.

@correct: B
@point: 20
@difficulty: 1
@concept: git-remote-github
@category: 1

## Q2
Sau khi cấu hình xong SSH Key trên GitHub Console, lệnh nào dưới đây được sử dụng để kiểm tra xem máy tính cá nhân local đã kết nối thành công và xác thực chính xác với máy chủ GitHub hay chưa?

[A]
`ssh git@github.com`
[EXP]
Lệnh này cố gắng mở một phiên đăng nhập shell trực tiếp vào GitHub, vốn không được GitHub hỗ trợ và sẽ không in ra thông báo chào mừng chuẩn xác.
[B]
`ssh -T git@github.com`
[EXP]
Đúng. Lệnh `ssh -T` gửi yêu cầu kết nối không mở shell để kiểm tra xác thực. Nếu thành công, GitHub sẽ trả về lời chào chứa username của bạn.
[C]
`git remote -v`
[EXP]
Lệnh `git remote -v` chỉ hiển thị danh sách các đường dẫn remote đã cấu hình ở local, không thực hiện kết nối mạng để kiểm tra xác thực SSH.
[D]
`ssh-keygen -t ed25519`
[EXP]
Lệnh này dùng để tạo mới một cặp khóa SSH trên máy local chứ không dùng để kiểm tra kết nối tới máy chủ GitHub.

@correct: B
@point: 20
@difficulty: 2
@concept: git-remote-github
@category: 1

## Q3
Học viên liên kết repository local với remote repository trên GitHub bằng lệnh `git remote add origin git@github.com:user/repo.git`. Trong lệnh này, tên gọi `origin` có ý nghĩa gì?

[A]
Là tên nhánh mặc định chứa toàn bộ commit gốc ban đầu của dự án local.
[EXP]
Nhánh mặc định của dự án local là `main` hoặc `master`, không phải `origin`.
[B]
Là giao thức mạng mã hóa được sử dụng để mã hóa dữ liệu truyền tải qua internet.
[EXP]
Giao thức mạng ở đây là SSH (thông qua tiền tố git@github.com) chứ không phải là `origin`.
[C]
Là thư mục ẩn lưu trữ toàn bộ lịch sử commit đã được đồng bộ lên đám mây GitHub.
[EXP]
Thư mục lưu trữ lịch sử ở remote là Git Directory nằm trên server GitHub, không phải tên gọi `origin`.
[D]
Là tên định danh (alias/nickname) do học viên tự đặt ở local để đại diện cho đường dẫn URL của remote repository.
[EXP]
Đúng. `origin` chỉ là một tên bí danh (alias) ở local trỏ đến đường dẫn URL của server chứa code. Bạn có thể đặt tên khác, nhưng origin là tiêu chuẩn mặc định.

@correct: D
@point: 20
@difficulty: 3
@concept: git-remote-github
@category: 1

## Q4
Lập trình viên muốn tải toàn bộ mã nguồn cùng lịch sử commit của một dự án công khai trên GitHub về máy tính local của mình lần đầu tiên. Lệnh Git nào dưới đây đáp ứng đúng yêu cầu này?

[A]
`git pull`
[EXP]
Lệnh `git pull` dùng để cập nhật code mới về một dự án local đã có sẵn liên kết remote, không dùng để tải dự án về lần đầu tiên khi chưa có thư mục.
[B]
`git fetch`
[EXP]
Lệnh `git fetch` chỉ tải thông tin thay đổi về local repository đã có sẵn, không tạo mới thư mục và clone toàn bộ dự án về lần đầu.
[C]
`git clone <URL>`
[EXP]
Đúng. Lệnh `git clone` tải toàn bộ mã nguồn, các nhánh và lịch sử commit của repository remote về máy local và tạo thư mục dự án tương ứng.
[D]
`git init <URL>`
[EXP]
Lệnh `git init` không nhận tham số URL và chỉ dùng để khởi tạo một repository trống tại thư mục hiện hành ở local.

@correct: C
@point: 20
@difficulty: 2
@concept: git-remote-github
@category: 1

## Q5
Học viên sửa code ở local, commit thành công và chuẩn bị push lên remote. Tuy nhiên, lệnh `git push` bị từ chối (rejected - non-fast-forward) do trước đó một thành viên khác đã push một commit mới lên nhánh `main` trên remote. Quy trình xử lý nào dưới đây là an toàn và chuẩn xác nhất?

[A]
Chạy lệnh `git push -f` để ép buộc remote ghi đè commit của mình lên và xóa bỏ commit của thành viên kia.
[EXP]
Đây là hành động nguy hiểm vì nó sẽ xóa vĩnh viễn commit của người khác trên remote, gây mất mát code và làm gián đoạn công việc của nhóm.
[B]
Xóa thư mục dự án ở local đi, tiến hành clone lại từ đầu rồi viết lại các phần code vừa chỉnh sửa.
[EXP]
Cách này gây lãng phí thời gian và công sức viết lại code của học viên, không đúng quy trình làm việc chuyên nghiệp của Git.
[C]
Chạy lệnh `git pull` để tải và gộp thay đổi mới từ remote về local, xử lý xung đột nếu có, sau đó chạy lại lệnh `git push`.
[EXP]
Đúng. Quy trình chuẩn là phải đồng bộ code mới nhất từ remote về local bằng `git pull`, giải quyết mọi xung đột ở máy local trước khi push lên remote.
[D]
Chạy lệnh `git remote remove origin` rồi thiết lập lại liên kết với một repository khác trên GitHub.
[EXP]
Lệnh này xóa liên kết với remote hiện tại và không giải quyết được vấn đề đồng bộ mã nguồn với nhóm làm việc.

@correct: C
@point: 20
@difficulty: 3
@concept: git-remote-github
@category: 1
