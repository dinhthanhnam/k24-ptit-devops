---
schema_version: 1
id: ss04_quiz_lesson_04
type: quiz
status: approved
course_id: devops-basic
session: 4
unit: 4
title: "Quiz Lesson 04 - Kỹ thuật Git nâng cao và quản lý lịch sử"
session_kind: theory
quiz_kind: lesson
question_count: 5
maps_to:
  - ss04_lesson_04
depends_on:
  - ss04_lesson_04
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: "Session 04 / Lesson 04"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
---

# Quiz Lesson 04 — Kỹ thuật Git nâng cao và quản lý lịch sử

## Q1
Trong quá trình làm việc local, học viên lỡ gõ sai tin nhắn commit (commit message) vừa thực hiện. Lệnh nào dưới đây giúp chỉnh sửa tin nhắn này trực tiếp mà không cần tạo thêm commit mới?

[A]
`git commit --amend -m "tin_nhan_moi"`
[EXP]
Đúng. Tùy chọn `--amend` cho phép ghi đè và chỉnh sửa thông tin của commit gần đây nhất của nhánh hiện hành.
[B]
`git reset --soft HEAD~1`
[EXP]
Lệnh này dùng để hủy bỏ hoàn toàn commit gần nhất và chuyển code về vùng Staging Area, không phải lệnh sửa đổi trực tiếp tin nhắn.
[C]
`git revert HEAD --no-edit`
[EXP]
Lệnh này tạo ra một commit mới để đảo ngược thay đổi của commit gần nhất chứ không dùng để sửa tin nhắn của nó.
[D]
`git checkout --amend`
[EXP]
Lệnh `git checkout` không hỗ trợ tùy chọn `--amend` và sẽ báo lỗi cú pháp khi thực thi.

@correct: A
@point: 20
@difficulty: 1
@concept: git-advanced-history
@category: 1

## Q2
Học viên muốn sử dụng lệnh `git reset` để hủy bỏ các commit lỗi gần nhất và yêu cầu Git phải xóa sạch hoàn toàn mọi thay đổi ở cả vùng Staging Area và thư mục làm việc Working Directory. Chế độ (mode) nào dưới đây của `git reset` cần được chỉ định?

[A]
`--soft`
[EXP]
Chế độ `--soft` chỉ dời con trỏ nhánh, toàn bộ các file thay đổi vẫn được giữ nguyên vẹn ở vùng đệm Staging Area.
[B]
`--mixed`
[EXP]
Chế độ `--mixed` dời con trỏ nhánh và dọn dẹp Staging Area, nhưng giữ lại các file thay đổi ở thư mục làm việc Working Directory.
[C]
`--hard`
[EXP]
Đúng. Chế độ `--hard` là chế độ triệt tiêu, xóa bỏ sạch sẽ mọi thay đổi ở cả Staging Area và thư mục làm việc Working Directory.
[D]
`--revert`
[EXP]
Lệnh `git reset` không hỗ trợ tùy chọn `--revert`. Đây là một lệnh độc lập riêng biệt (`git revert`).

@correct: C
@point: 20
@difficulty: 2
@concept: git-advanced-history
@category: 1

## Q3
Khi bạn muốn hủy bỏ một thay đổi đã được đẩy (push) lên remote repository dùng chung của nhóm, tại sao sử dụng `git revert` lại an toàn hơn sử dụng `git reset`?

[A]
Vì `git revert` sẽ xóa bỏ hoàn toàn commit lỗi khỏi lịch sử của cả remote lẫn máy local của mọi thành viên.
[EXP]
Lệnh `git revert` không hề xóa bỏ commit lỗi mà chỉ tạo thêm commit đảo ngược, giúp lịch sử của mọi người không bị mất mát.
[B]
Vì `git revert` tạo ra một commit mới chứa các thay đổi đảo ngược mà không viết lại lịch sử cũ, giúp tránh xung đột lịch sử cho cả nhóm.
[EXP]
Đúng. Lệnh `git revert` không sửa đổi quá khứ mà chỉ đi tiếp bằng cách tạo một commit mới đảo ngược, giúp các thành viên pull/push bình thường.
[C]
Vì `git revert` tự động đưa mã nguồn về Staging Area của tất cả các máy tính thành viên khác để họ kiểm tra lại.
[EXP]
Git không thể tự can thiệp hay thay đổi vùng Staging Area trên máy local của các thành viên khác khi chưa có thao tác chủ động pull.
[D]
Vì `git revert` thực hiện khóa nhánh tạm thời để ngăn chặn các thành viên khác commit đè lên code của bạn.
[EXP]
Git không có cơ chế tự động khóa nhánh vật lý khi chạy lệnh revert. Việc an toàn là nhờ cơ chế lịch sử commit tuyến tính tiến lên.

@correct: B
@point: 20
@difficulty: 3
@concept: git-advanced-history
@category: 1

## Q4
Học viên muốn sao chép và áp dụng duy nhất một commit sửa lỗi hotfix từ nhánh `bugfix-auth` vào nhánh chính `main` hiện hành mà không muốn gộp (merge) toàn bộ các thay đổi khác chưa hoàn thiện trên nhánh phụ này. Lệnh Git nào đáp ứng yêu cầu?

[A]
`git merge bugfix-auth`
[EXP]
Lệnh `git merge` sẽ gộp toàn bộ các commit của nhánh `bugfix-auth` vào `main`, bao gồm cả các commit chứa tính năng chưa hoàn thiện.
[B]
`git cherry-pick <commit_hash_hotfix>`
[EXP]
Đúng. Lệnh `git cherry-pick` cho phép chọn lọc một commit cụ thể dựa trên mã hash của nó để áp dụng trực tiếp lên nhánh hiện tại.
[C]
`git checkout bugfix-auth`
[EXP]
Lệnh này chỉ chuyển nhánh làm việc sang nhánh `bugfix-auth` chứ không thực hiện việc sao chép commit nào vào `main`.
[D]
`git commit --amend`
[EXP]
Lệnh này dùng để chỉnh sửa commit gần nhất ở nhánh hiện tại, không dùng để sao chép commit từ nhánh khác sang.

@correct: B
@point: 20
@difficulty: 2
@concept: git-advanced-history
@category: 1

## Q5
Học viên vô tình commit một tệp cấu hình chứa mật khẩu nhạy cảm lên Git. Sau đó, học viên viết thêm tên file này vào tệp `.gitignore` rồi commit tiếp. File mật khẩu này có được Git tự động bỏ qua từ thời điểm này trở đi không?

[A]
Có, bất kỳ file nào được định nghĩa trong `.gitignore` đều sẽ được Git tự động gỡ bỏ hoàn toàn khỏi toàn bộ lịch sử commit trước đó.
[EXP]
`.gitignore` không có tác dụng hồi tố. Nó không thể tự xóa các file nhạy cảm đã tồn tại trong lịch sử commit cũ của Git.
[B]
Có, Git sẽ ngay lập tức bỏ qua và không theo dõi tệp tin đó nữa ngay khi file `.gitignore` được commit thành công.
[EXP]
Git chỉ bỏ qua các file chưa từng được theo dõi (Untracked). File đã được commit thì Git vẫn sẽ tiếp tục theo dõi thay đổi của nó.
[C]
Không, vì quy tắc trong `.gitignore` chỉ áp dụng đối với các tệp tin lưu trữ tại Staging Area chứ không áp dụng cho Working Directory.
[EXP]
Quy tắc của `.gitignore` áp dụng cho Working Directory nhưng chỉ đối với các file Untracked, không liên quan đến việc phân biệt vùng như trên.
[D]
Không, học viên phải chạy lệnh `git rm --cached <file_name>` để gỡ bỏ file ra khỏi cache theo dõi của Git thì `.gitignore` mới bắt đầu có hiệu lực.
[EXP]
Đúng. Đối với các file đã được Git theo dõi từ trước, học viên bắt buộc phải xóa file khỏi cache theo dõi của Git bằng lệnh `git rm --cached` thì quy tắc bỏ qua trong `.gitignore` mới có tác dụng.

@correct: D
@point: 20
@difficulty: 3
@concept: git-advanced-history
@category: 1
