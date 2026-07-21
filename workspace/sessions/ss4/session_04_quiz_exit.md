---
schema_version: 1
id: ss04_quiz_exit
type: quiz
status: approved
course_id: devops-basic
session: 4
unit: 0
title: Quiz cuối giờ Session 04
session_kind: theory
tags: []
concepts: []
depends_on:
- ss04_lesson_01
- ss04_lesson_02
- ss04_lesson_03
- ss04_lesson_04
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: Session 04 / quiz_exit
language: vi
created: '2026-07-17'
updated: '2026-07-17'
quiz_kind: exit
question_count: 30
maps_to:
- ss04_lesson_01
- ss04_lesson_02
- ss04_lesson_03
- ss04_lesson_04
---

# Quiz cuối giờ Session 04

## Q1

Học viên muốn đưa tệp tin `index.html` trong Working Directory vào Staging Area để chuẩn bị tạo commit. Cú pháp lệnh nào sau đây chính xác?

[A]
`git status add index.html`
[EXP]
Lệnh `git status` dùng để kiểm tra trạng thái các file chứ không có tham số hay hành động `add` như trên.
[B]
`git add index.html`
[EXP]
Đúng. Lệnh `git add <tên_file>` được sử dụng để đưa tệp tin từ thư mục làm việc vào vùng chuẩn bị Staging Area.
[C]
`git commit index.html`
[EXP]
Lệnh `git commit` dùng để lưu trữ các thay đổi từ Staging Area vào lịch sử, không dùng để di chuyển file vào Staging.
[D]
`git push index.html`
[EXP]
Lệnh `git push` dùng để đẩy các commit từ local repository lên remote repository chứ không thao tác với file riêng lẻ.

@correct: B
@point: 20
@difficulty: 10
@concept: git-local-basics
@category: 1

## Q2

Học viên cần cấu hình tên hiển thị của tác giả để gán vào các commit sau này trên máy tính cá nhân. Lệnh nào sau đây thực hiện điều này?

[A]
`git config --global user.name "Nguyen Van A"`
[EXP]
Đúng. Cú pháp `git config --global user.name "tên"` dùng để cấu hình tên tác giả áp dụng trên toàn hệ thống.
[B]
`git create --global user.name "Nguyen Van A"`
[EXP]
Git không hỗ trợ lệnh bắt đầu bằng từ khóa `git create` để thực hiện cấu hình các thông số hệ thống.
[C]
`git setup --global user.name "Nguyen Van A"`
[EXP]
Git không hỗ trợ lệnh bắt đầu bằng từ khóa `git setup` để thiết lập thông tin định danh tác giả.
[D]
`git init --global user.name "Nguyen Van A"`
[EXP]
Lệnh `git init` dùng để khởi tạo một repository mới chứ không có tùy chọn để định cấu hình tên tác giả.

@correct: A
@point: 20
@difficulty: 10
@concept: git-local-basics
@category: 1

## Q3

Học viên muốn tạo đồng thời di chuyển sang một nhánh tính năng mới tên là `feature-payment` bằng một lệnh duy nhất. Cú pháp nào sau đây chính xác?

[A]
`git branch -c feature-payment`
[EXP]
Tùy chọn `-c` không đi kèm với lệnh `git branch` để hỗ trợ tạo và di chuyển trực tiếp sang nhánh mới đó.
[B]
`git switch -b feature-payment`
[EXP]
Lệnh `git switch` sử dụng tùy chọn `-c` (create) để tạo và chuyển nhánh, không sử dụng tùy chọn `-b` như checkout.
[C]
`git checkout -n feature-payment`
[EXP]
Lệnh `git checkout` không hỗ trợ tùy chọn `-n` để tạo và di chuyển trực tiếp sang một nhánh tính năng mới.
[D]
`git checkout -b feature-payment`
[EXP]
Đúng. Lệnh `git checkout -b <branch_name>` tạo một nhánh mới và tự động chuyển môi trường làm việc sang nhánh đó.

@correct: D
@point: 20
@difficulty: 10
@concept: git-branching-conflicts
@category: 1

## Q4

Học viên vừa tạo một repository trống trên GitHub và muốn tải toàn bộ mã nguồn cùng lịch sử của dự án đó về máy tính local. Lệnh nào sau đây phù hợp?

[A]
`git remote add origin <url_github>`
[EXP]
Lệnh `git remote add` chỉ thiết lập liên kết với remote repository chứ không tải mã nguồn dự án về máy.
[B]
`git pull origin main --force`
[EXP]
Lệnh `git pull` dùng để cập nhật các thay đổi mới từ remote về repository local hiện có, không dùng tải mới.
[C]
`git push origin main --force`
[EXP]
Lệnh `git push` dùng để đẩy các thay đổi từ máy local lên remote chứ không có chức năng tải dự án về máy.
[D]
`git clone <url_github_cua_repo>`
[EXP]
Đúng. Lệnh `git clone` tải bản sao toàn bộ mã nguồn cùng lịch sử commit của repository từ remote về máy local.

@correct: D
@point: 20
@difficulty: 10
@concept: git-remote-github
@category: 1

## Q5

Học viên thực hiện chỉnh sửa file code nhưng chưa chạy lệnh add hay commit. Lệnh nào giúp học viên loại bỏ toàn bộ các thay đổi chưa lưu này để khôi phục trạng thái cũ của file?

[A]
Chạy lệnh `git reset --soft <file_name>`
[EXP]
Lệnh `git reset --soft` dùng để di chuyển con trỏ HEAD và giữ nguyên các thay đổi ở Staging Area, không áp dụng cho file lẻ.
[B]
Chạy lệnh `git revert HEAD --no-edit`
[EXP]
Lệnh `git revert` tạo một commit mới để đảo ngược thay đổi của một commit trước đó, không dùng hủy thay đổi chưa commit.
[C]
Chạy lệnh `git restore <file_name>`
[EXP]
Đúng. Lệnh `git restore <file_name>` (hoặc `git checkout -- <file>`) loại bỏ các thay đổi chưa commit ở Working Directory của file.
[D]
Chạy lệnh `git clean -fd --dry-run`
[EXP]
Lệnh `git clean` dùng để xóa các file chưa được theo dõi (Untracked files) khỏi thư mục làm việc, không khôi phục file sửa đổi.

@correct: C
@point: 20
@difficulty: 10
@concept: git-advanced-history
@category: 1

## Q6

Học viên muốn sao chép một commit cụ thể có mã hash là `a1b2c3d` từ nhánh `feature` sang nhánh hiện hành mà không muốn gộp toàn bộ nhánh. Cú pháp nào sau đây chính xác?

[A]
`git cherry-pick a1b2c3d`
[EXP]
Đúng. Lệnh `git cherry-pick` được dùng để áp dụng các thay đổi từ một commit cụ thể lên đầu nhánh hiện hành.
[B]
`git merge feature a1b2c3d`
[EXP]
Lệnh `git merge` dùng để gộp toàn bộ nhánh chứ không hỗ trợ truyền thêm mã hash commit riêng lẻ để gộp chọn lọc.
[C]
`git checkout feature a1b2c3d`
[EXP]
Cú pháp này sai, lệnh checkout với nhánh và hash không dùng để sao chép thay đổi commit sang nhánh khác.
[D]
`git reset --hard a1b2c3d`
[EXP]
Lệnh `git reset --hard` sẽ di chuyển con trỏ HEAD và xóa sạch thay đổi hiện tại, không sao chép commit chọn lọc.

@correct: A
@point: 20
@difficulty: 10
@concept: git-advanced-history
@category: 1

## Q7

Để gộp nhánh tính năng `feature` vào nhánh chính `main` bằng phương thức bắt buộc tạo một commit gộp (merge commit) mới ngay cả khi đủ điều kiện chạy Fast-forward. Học viên chạy lệnh nào?

[A]
`git merge feature --ff-only`
[EXP]
Tùy chọn `--ff-only` chỉ cho phép gộp nếu lịch sử là tuyến tính (Fast-forward), ngược lại sẽ báo lỗi và không merge.
[B]
`git merge feature --no-ff`
[EXP]
Đúng. Tùy chọn `--no-ff` (no fast-forward) ép buộc Git tạo một commit gộp mới để ghi lại lịch sử phân nhánh rõ ràng.
[C]
`git merge feature --squash`
[EXP]
Tùy chọn `--squash` gộp tất cả commit của nhánh phụ thành một thay đổi chưa commit ở local, không tạo ngay merge commit.
[D]
`git merge feature --rebase`
[EXP]
Không tồn tại tùy chọn `--rebase` đi kèm trực tiếp trong cú pháp của lệnh thực hiện hành động git merge.

@correct: B
@point: 20
@difficulty: 10
@concept: git-branching-conflicts
@category: 1

## Q8

Sau khi tạo cặp khóa SSH bằng lệnh `ssh-keygen`, học viên cần tìm tệp tin nào lưu trữ khóa công khai (Public Key) để đưa lên cấu hình tài khoản GitHub?

[A]
Tệp tin private key `~/.ssh/id_ed25519`
[EXP]
Đây là tệp tin lưu trữ khóa riêng tư (Private Key), cần được bảo mật tuyệt đối tại local và không được chia sẻ.
[B]
Tệp lưu danh sách `~/.ssh/known_hosts`
[EXP]
Tệp này lưu fingerprint nhận diện các máy chủ từ xa mà người dùng từng kết nối, không chứa khóa công khai của bạn.
[C]
Tệp public key `~/.ssh/id_ed25519.pub`
[EXP]
Đúng. Tệp tin có phần mở rộng `.pub` chứa khóa công khai dùng để đăng ký xác thực với các máy chủ từ xa như GitHub.
[D]
Tệp cấu hình client `~/.ssh/config`
[EXP]
Tệp tin này dùng để định cấu hình các host và bí danh kết nối SSH ở client, không chứa khóa mã hóa xác thực.

@correct: C
@point: 20
@difficulty: 10
@concept: git-remote-github
@category: 1

## Q9

Học viên vừa thực hiện lệnh commit ở máy local nhưng phát hiện ra mình gõ nhầm thông điệp (commit message). Lệnh nào sau đây giúp sửa nhanh thông điệp này?

[A]
`git commit -m "thong_diep_moi"`
[EXP]
Lệnh này sẽ tạo thêm một commit hoàn toàn mới kế tiếp trong lịch sử, không phải sửa đổi commit cũ.
[B]
`git commit --amend -m "thong_diep_moi"`
[EXP]
Đúng. Tùy chọn `--amend` cho phép thay thế commit gần nhất bằng một commit mới có thông điệp hoặc nội dung cập nhật.
[C]
`git revert HEAD -m "thong_diep_moi"`
[EXP]
Lệnh revert tạo commit mới đảo ngược thay đổi của commit cũ, không dùng để sửa thông điệp của commit hiện tại.
[D]
`git reset --soft HEAD~1`
[EXP]
Lệnh này di chuyển HEAD về commit cũ và giữ nguyên các thay đổi trong Staging Area chứ không thay thế trực tiếp thông điệp commit.

@correct: B
@point: 20
@difficulty: 10
@concept: git-advanced-history
@category: 1

## Q10

Trong quá trình làm việc với Git, lệnh nào được sử dụng để kiểm tra danh sách các nhánh (branches) hiện có ở máy local và hiển thị nhánh hiện hành?

[A]
`git branch`
[EXP]
Đúng. Lệnh `git branch` không kèm tham số hiển thị danh sách các nhánh local và đánh dấu sao `*` trước nhánh hiện hành.
[B]
`git checkout`
[EXP]
Lệnh `git checkout` không kèm tham số dùng để kiểm tra trạng thái tệp tin hoặc di chuyển con trỏ HEAD chứ không liệt kê nhánh.
[C]
`git switch`
[EXP]
Lệnh `git switch` không đi kèm tham số sẽ báo lỗi cú pháp chứ không hiển thị danh sách các nhánh hiện có của dự án.
[D]
`git status`
[EXP]
Lệnh `git status` hiển thị trạng thái các tệp tin thay đổi ở Working Directory và Staging Area, không liệt kê danh sách nhánh.

@correct: A
@point: 20
@difficulty: 10
@concept: git-branching-conflicts
@category: 1

## Q11

Học viên muốn đẩy toàn bộ các commit của nhánh `main` ở local lên remote repository có tên định danh là `origin` và thiết lập theo dõi (tracking). Lệnh nào sau đây chính xác?

[A]
`git push origin main`
[EXP]
Lệnh này đẩy commit lên remote nhưng không thiết lập mối quan hệ theo dõi mặc định cho các lần push/pull sau này.
[B]
`git push --all origin main`
[EXP]
Tùy chọn `--all` dùng để đẩy tất cả các nhánh local lên remote, không dùng để thiết lập theo dõi cho riêng một nhánh.
[C]
`git push -t origin main`
[EXP]
Tùy chọn `-t` (hoặc `--tags`) dùng để đẩy các tag (nhãn phiên bản) lên remote chứ không thiết lập theo dõi nhánh.
[D]
`git push -u origin main`
[EXP]
Đúng. Tùy chọn `-u` (hoặc `--set-upstream`) dùng để đẩy nhánh lên remote đồng thời thiết lập mối quan hệ theo dõi lâu dài.

@correct: D
@point: 20
@difficulty: 10
@concept: git-remote-github
@category: 1

## Q12

Học viên muốn kiểm tra trạng thái của thư mục làm việc (Working Directory) để xem những tệp tin nào đã thay đổi, chưa được add hay đã được đưa vào Staging Area. Lệnh nào sau đây phù hợp?

[A]
`git diff`
[EXP]
Lệnh `git diff` dùng để xem chi tiết sự khác biệt nội dung bên trong file, không hiển thị tổng quan danh sách file theo trạng thái.
[B]
`git log`
[EXP]
Lệnh `git log` dùng để xem lịch sử các commit đã thực hiện trong dự án chứ không hiển thị trạng thái hiện tại của file.
[C]
`git status`
[EXP]
Đúng. Lệnh `git status` hiển thị tóm tắt trạng thái của các file (Untracked, Modified, Staged) trong Working Directory.
[D]
`git show`
[EXP]
Lệnh `git show` hiển thị chi tiết nội dung thay đổi của một commit cụ thể, không dùng kiểm tra thư mục làm việc hiện hành.

@correct: C
@point: 20
@difficulty: 10
@concept: git-local-basics
@category: 1

## Q13

Học viên đang ở nhánh `main` và chạy lệnh `git merge feature-a`. Trong quá trình gộp nhánh xảy ra xung đột (Merge Conflict). Học viên muốn xem danh sách các file đang bị xung đột để tiến hành xử lý, lệnh nào sau đây cung cấp thông tin trực quan nhất?

[A]
`git status`
[EXP]
Đúng. Lệnh `git status` liệt kê rõ ràng các file bị xung đột dưới mục "Unmerged paths" bằng màu đỏ để lập trình viên dễ nhận biết.
[B]
`git diff`
[EXP]
Lệnh `git diff` hiển thị chi tiết các thay đổi dòng code cụ thể bị xung đột trong các file, không hiển thị danh sách file rút gọn.
[C]
`git branch`
[EXP]
Lệnh `git branch` chỉ liệt kê danh sách các nhánh hiện có trong repository và nhánh hiện hành chứ không kiểm tra trạng thái file.
[D]
`git log`
[EXP]
Lệnh `git log` dùng để xem lịch sử các commit đã thực hiện trong quá trình phát triển dự án, không hiển thị các file đang bị xung đột.

@correct: A
@point: 20
@difficulty: 11
@concept: git-branching-conflicts
@category: 1

## Q14

Khi xảy ra xung đột gộp nhánh (Merge Conflict), trong file code xuất hiện ký tự `<<<<<<< HEAD` và `=======`. Đoạn code nằm giữa hai dòng ký tự đánh dấu này biểu thị cho nội dung nào?

[A]
Các thay đổi mới được thực hiện trên nhánh phụ mà học viên đang muốn gộp vào nhánh chính.
[EXP]
Các thay đổi ở nhánh phụ cần gộp vào được đặt ở giữa dòng phân cách `=======` và dòng kết thúc `>>>>>>>`.
[B]
Các thay đổi mới được thực hiện trên nhánh hiện tại (HEAD) nơi học viên đang đứng chạy lệnh merge.
[EXP]
Đúng. Phần nội dung nằm giữa `<<<<<<< HEAD` và `=======` thể hiện các thay đổi cục bộ của nhánh hiện tại đang đứng để gộp.
[C]
Các thay đổi của tổ tiên chung gần nhất (Common Ancestor) trước khi hai nhánh bắt đầu phân tách ra.
[EXP]
Git không hiển thị nội dung của commit tổ tiên chung giữa các ký tự đánh dấu xung đột này ở chế độ mặc định.
[D]
Các thay đổi đã được hệ thống tự động gộp thành công và chuẩn bị được đưa vào commit gộp mới.
[EXP]
Các phần code tự động gộp thành công sẽ không bị đánh dấu xung đột mà được Git tự động xử lý trực tiếp vào file.

@correct: B
@point: 20
@difficulty: 11
@concept: git-branching-conflicts
@category: 1

## Q15

Học viên commit một tệp chứa mật khẩu nhạy cảm lên Git. Sau đó, học viên thêm tên file này vào `.gitignore` rồi tạo thêm commit mới. Tệp nhạy cảm này có được bảo mật không?

[A]
Có, bất kỳ file nào được định nghĩa trong `.gitignore` đều sẽ được Git tự động gỡ bỏ khỏi lịch sử commit trước đó.
[EXP]
`.gitignore` không có tác dụng hồi tố, nó không thể tự xóa các file nhạy cảm đã tồn tại trong lịch sử commit cũ của Git.
[B]
Không, Git vẫn tiếp tục theo dõi tệp tin nhạy cảm này vì nó đã được đưa vào hệ thống quản lý lịch sử từ trước.
[EXP]
Đúng. Đối với các file đã được Git theo dõi, quy tắc trong `.gitignore` sẽ không có tác dụng cho đến khi file bị gỡ khỏi cache.
[C]
Có, Git sẽ tự động chuyển tệp tin này sang trạng thái Untracked ngay sau khi file `.gitignore` được commit.
[EXP]
Git không tự động chuyển trạng thái của một file đã được theo dõi sang Untracked khi ta khai báo nó trong `.gitignore`.
[D]
Không, vì quy tắc trong `.gitignore` chỉ áp dụng đối với các tệp tin lưu trữ tại Staging Area chứ không phải Working Directory.
[EXP]
Quy tắc của `.gitignore` áp dụng cho Working Directory nhưng chỉ đối với các file Untracked, không liên quan đến Staging Area.

@correct: B
@point: 20
@difficulty: 11
@concept: git-advanced-history
@category: 1

## Q16

Học viên chạy lệnh `git reset --mixed HEAD~1` để sửa đổi lịch sử. Sau khi lệnh thực thi thành công, trạng thái của các thay đổi ở commit gần nhất sẽ như thế nào?

[A]
Được giữ nguyên trong Staging Area và sẵn sàng để học viên tạo commit mới tiếp theo.
[EXP]
Trạng thái được giữ nguyên trong Staging Area là đặc tính của tùy chọn `--soft` chứ không phải tùy chọn `--mixed`.
[B]
Bị xóa bỏ hoàn toàn khỏi cả Working Directory và Staging Area mà không thể khôi phục lại.
[EXP]
Việc xóa sạch thay đổi ở cả thư mục làm việc và vùng chuẩn bị là cơ chế hoạt động của tùy chọn reset `--hard`.
[C]
Được tự động đẩy lên remote repository để cập nhật lịch sử đồng bộ cho các thành viên.
[EXP]
Lệnh `git reset` chỉ thực hiện các thao tác thay đổi ở môi trường local của học viên, không tự động tương tác với remote.
[D]
Được giữ lại trong Working Directory dưới dạng Modified và bị loại bỏ khỏi Staging Area.
[EXP]
Đúng. Tùy chọn mặc định `--mixed` di chuyển con trỏ nhánh về commit trước, đưa thay đổi về dạng chưa add ở Working Directory.

@correct: D
@point: 20
@difficulty: 11
@concept: git-advanced-history
@category: 1

## Q17

Học viên muốn loại bỏ một commit lỗi trên nhánh `main` chung của nhóm mà không làm ảnh hưởng đến lịch sử commit của các thành viên khác. Lệnh nào sau đây là an toàn nhất?

[A]
`git reset --hard <hash_commit_loi> && git push -f`
[EXP]
Sử dụng reset và push force sẽ ghi đè lịch sử trên remote, gây lỗi nghiêm trọng và xung đột lịch sử cho các thành viên khác.
[B]
`git reset --soft HEAD~1`
[EXP]
Lệnh này chỉ dời con trỏ nhánh ở máy local, nếu đẩy lên remote mà không dùng force sẽ bị từ chối và không xóa được commit lỗi.
[C]
`git revert <hash_commit_loi>`
[EXP]
Đúng. `git revert` tạo ra một commit mới để đảo ngược các thay đổi lỗi, đây là cách an toàn nhất khi làm việc nhóm.
[D]
`git checkout <hash_commit_loi> --force`
[EXP]
Lệnh này chỉ chuyển trạng thái thư mục làm việc về commit cũ tạm thời chứ không tạo ra thay đổi hay commit hủy lỗi nào.

@correct: C
@point: 20
@difficulty: 11
@concept: git-advanced-history
@category: 1

## Q18

Trong khi đang thực hiện giải quyết xung đột gộp nhánh (Merge Conflict) nhưng học viên phát hiện mình thao tác nhầm và muốn hủy bỏ toàn bộ quá trình merge này để quay lại trạng thái trước khi merge. Lệnh nào sau đây chính xác?

[A]
`git merge --abort`
[EXP]
Đúng. Lệnh `git merge --abort` khôi phục lại trạng thái của repository về trước thời điểm bắt đầu chạy lệnh gộp nhánh.
[B]
`git reset --hard HEAD`
[EXP]
Lệnh này xóa sạch các thay đổi chưa commit nhưng không kết thúc trạng thái đang merge của Git một cách an toàn.
[C]
`git merge --clean`
[EXP]
Không tồn tại tùy chọn `--clean` đi kèm trong lệnh merge để hỗ trợ việc hủy bỏ quá trình gộp nhánh hiện tại.
[D]
`git checkout --abort`
[EXP]
Lệnh checkout không quản lý tiến trình gộp nhánh nên tùy chọn `--abort` không có tác dụng trong trường hợp này.

@correct: A
@point: 20
@difficulty: 11
@concept: git-branching-conflicts
@category: 1

## Q19

Học viên chạy lệnh `git push` nhưng bị hệ thống từ chối với thông báo "non-fast-forward". Nguyên nhân phổ biến nhất của lỗi này là gì?

[A]
Hệ thống mạng internet local của học viên gặp sự cố gián đoạn kết nối tới máy chủ GitHub.
[EXP]
Nếu mất mạng, Git sẽ báo lỗi kết nối (connection timeout/refused) chứ không hiển thị thông báo "non-fast-forward".
[B]
Remote repository đã có những commit mới do thành viên khác đẩy lên mà local của học viên chưa cập nhật.
[EXP]
Đúng. Thông báo chỉ ra rằng nhánh trên remote có các commit mới hơn mà máy local chưa có, cần pull về trước khi push.
[C]
Cặp khóa SSH được cấu hình trên máy tính cá nhân của học viên chưa được xác thực thành công với GitHub.
[EXP]
Nếu lỗi xác thực SSH, Git sẽ báo lỗi từ chối quyền truy cập (Permission denied) chứ không báo lỗi non-fast-forward.
[D]
Học viên chưa chạy lệnh khởi tạo Git (`git init`) trong thư mục dự án hiện hành ở máy tính local.
[EXP]
Nếu chưa khởi tạo Git, học viên không thể tạo commit hay chạy lệnh push nên lỗi này sẽ không xuất hiện tại đây.

@correct: B
@point: 20
@difficulty: 11
@concept: git-remote-github
@category: 1

## Q20

Khi chạy lệnh `git merge feature` trên nhánh `main` và nhận được thông báo "Fast-forward". Lịch sử commit của hai nhánh lúc này có đặc điểm gì?

[A]
Nhánh `main` và nhánh `feature` có lịch sử rẽ nhánh song song và cả hai đều có những commit mới độc lập.
[EXP]
Nếu cả hai đều có commit mới độc lập, Git sẽ phải sử dụng cơ chế 3-Way Merge chứ không thể chạy Fast-forward.
[B]
Nhánh `feature` đã được tạo ra từ rất lâu và chứa quá nhiều commit phức tạp so với nhánh chính `main`.
[EXP]
Số lượng commit và thời gian tạo nhánh không quyết định việc Git áp dụng cơ chế gộp Fast-forward hay 3-Way.
[C]
Học viên đã cấu hình bắt buộc tạo merge commit bằng cách thêm tùy chọn `--no-ff` khi chạy lệnh gộp nhánh.
[EXP]
Tùy chọn `--no-ff` sẽ ngăn chặn cơ chế Fast-forward hoạt động và bắt buộc tạo một commit gộp mới trong mọi trường hợp.
[D]
Nhánh `main` không phát sinh thêm bất kỳ commit mới nào kể từ thời điểm nhánh `feature` được tách ra từ nó.
[EXP]
Đúng. Lịch sử lúc này là tuyến tính, Git chỉ cần di chuyển con trỏ nhánh `main` tiến thẳng lên vị trí commit của `feature`.

@correct: D
@point: 20
@difficulty: 11
@concept: git-branching-conflicts
@category: 1

## Q21

Học viên chạy lệnh `git pull` để cập nhật code mới từ GitHub về máy local và gặp thông báo xảy ra xung đột (Merge Conflict). Cơ chế nào đã được thực thi bên dưới lệnh `git pull`?

[A]
Chạy lệnh `git clone` để tải lại dự án và chạy `git push` để đẩy các thay đổi lên.
[EXP]
Lệnh `git pull` không thực hiện tải lại toàn bộ dự án hay đẩy bất kỳ thay đổi nào từ local lên remote.
[B]
Chạy lệnh `git init` để cấu hình lại dự án và chạy `git add` để lưu các tệp tin mới.
[EXP]
Lệnh `git pull` chỉ hoạt động trên repository đã tồn tại và không liên quan đến việc khởi tạo hay chuẩn bị file.
[C]
Chạy lệnh `git fetch` để tải các thay đổi từ remote và chạy `git merge` để gộp vào local.
[EXP]
Đúng. Lệnh `git pull` thực chất là chạy `git fetch` để lấy thông tin mới từ remote, sau đó chạy `git merge` để gộp vào local.
[D]
Chạy lệnh `git checkout` để chuyển sang nhánh remote và chạy `git reset` để cập nhật.
[EXP]
Lệnh `git pull` không tự động chuyển nhánh hay xóa bỏ các commit local của học viên thông qua reset.

@correct: C
@point: 20
@difficulty: 11
@concept: git-remote-github
@category: 1

## Q22

Trạng thái "Untracked" của một tệp tin trong Git biểu thị điều gì về mối quan hệ giữa tệp tin đó với hệ thống quản lý lịch sử Git?

[A]
Tệp tin đã được đưa vào Staging Area nhưng chưa được tạo commit chính thức để lưu lại lịch sử.
[EXP]
Tệp tin nằm trong Staging Area nhưng chưa commit được gọi là đang ở trạng thái Staged (đã chuẩn bị), không phải Untracked.
[B]
Tệp tin mới được tạo ra trong thư mục dự án và chưa từng được Git ghi nhận hay theo dõi thay đổi.
[EXP]
Đúng. Trạng thái Untracked nghĩa là Git hoàn toàn chưa theo dõi tệp tin này trong lịch sử phiên bản của nó.
[C]
Tệp tin đã được commit thành công và không có bất kỳ chỉnh sửa mới nào trong thư mục làm việc.
[EXP]
Tệp tin đã commit và chưa sửa đổi ở thư mục làm việc nằm ở trạng thái Unmodified (chưa sửa đổi), không phải Untracked.
[D]
Tệp tin đã bị xóa hoàn toàn khỏi đĩa cứng vật lý nhưng Git vẫn lưu thông tin ở cache Staging Area.
[EXP]
File bị xóa vật lý nhưng vẫn nằm trong cache theo dõi của Git sẽ ở trạng thái Deleted (đã xóa), không phải Untracked.

@correct: B
@point: 20
@difficulty: 11
@concept: git-local-basics
@category: 1

## Q23

Khi làm việc nhóm trên nhánh chính `main` đã được đẩy lên remote, học viên phát hiện một commit cũ bị lỗi. Giải pháp nào sau đây tuân thủ đúng best practice để sửa lỗi?

[A]
Chạy lệnh `git revert` cho commit lỗi để tạo một commit đảo ngược mới và push lên remote.
[EXP]
Đúng. Đây là giải pháp an toàn nhất vì nó không sửa đổi lịch sử đã chia sẻ, tránh gây xung đột cho các thành viên khác.
[B]
Sử dụng `git reset --hard` để quay về commit trước lỗi và push force (`git push -f`) lên remote.
[EXP]
Việc viết lại lịch sử của một nhánh chung bằng push force sẽ làm hỏng lịch sử của các lập trình viên khác trong nhóm.
[C]
Sửa code trực tiếp trên máy tính local của mình rồi lưu lại và không tạo commit mới để tránh rác lịch sử.
[EXP]
Nếu không tạo commit mới và push lên remote thì các thành viên khác sẽ không thể nhận được bản sửa lỗi này.
[D]
Xóa bỏ repository hiện tại trên máy local rồi thực hiện clone lại toàn bộ dự án từ trên GitHub về.
[EXP]
Việc clone lại dự án không hề giải quyết được lỗi nằm trong commit cũ đã tồn tại trên remote repository.

@correct: A
@point: 20
@difficulty: 6
@concept: git-advanced-history
@category: 1

## Q24

Học viên đang phát triển một tính năng lớn trên nhánh `feature-checkout`. Học viên nên tổ chức thực hiện các commit như thế nào để đảm bảo lịch sử dự án rõ ràng nhất?

[A]
Tích lũy toàn bộ thay đổi trong nhiều ngày rồi thực hiện một commit lớn duy nhất khi tính năng hoàn thành.
[EXP]
Commit quá lớn sẽ rất khó để review code, tìm lỗi hoặc quay lại phiên bản trước đó khi có sự cố phát sinh.
[B]
Thực hiện commit liên tục sau mỗi dòng code gõ xong để đảm bảo không bị mất bất kỳ thay đổi nhỏ nào.
[EXP]
Commit quá vụn vặt và không có ý nghĩa chức năng rõ ràng sẽ làm rác lịch sử commit và gây khó khăn khi đọc log.
[C]
Đẩy thẳng các file chưa hoàn thiện lên nhánh chính `main` của nhóm để nhờ đồng nghiệp sửa lỗi giúp.
[EXP]
Việc đẩy code chưa hoàn thiện hoặc bị lỗi lên nhánh chính sẽ làm ảnh hưởng đến tiến độ chạy dự án của toàn nhóm.
[D]
Chia nhỏ tính năng thành các phần độc lập và tạo commit riêng kèm thông điệp mô tả rõ ràng cho mỗi phần.
[EXP]
Đúng. Đây là best practice (Atomic Commit) giúp lịch sử rõ ràng, dễ theo dõi, kiểm thử và cô lập lỗi khi cần thiết.

@correct: D
@point: 20
@difficulty: 6
@concept: git-branching-conflicts
@category: 1

## Q25

Học viên đang viết dở code cho một tính năng nhưng cần kiểm tra gấp một lỗi trên nhánh khác. Giải pháp nào sau đây giúp chuyển nhánh mà không làm mất hoặc commit đè code dở?

[A]
Chạy lệnh `git reset --hard` để dọn sạch Working Directory trước khi chuyển sang nhánh khác làm việc.
[EXP]
Lệnh `git reset --hard` sẽ xóa sạch hoàn toàn các thay đổi chưa lưu của bạn ở thư mục làm việc, gây mất code.
[B]
Tạo một commit tạm thời với thông điệp tùy ý để lưu lại code dở rồi thực hiện chuyển nhánh ngay.
[EXP]
Tạo commit tạm sẽ làm rác lịch sử commit của dự án với các thông điệp vô nghĩa và mã nguồn chưa hoàn chỉnh.
[C]
Sử dụng lệnh `git stash` để lưu tạm các thay đổi vào bộ nhớ đệm của Git trước khi chuyển sang nhánh khác.
[EXP]
Đúng. `git stash` lưu tạm thời các thay đổi chưa commit vào một vùng nhớ tạm để khôi phục lại sau khi chuyển về.
[D]
Sao chép thủ công toàn bộ các file thay đổi ra một thư mục tạm ngoài dự án trước khi chuyển nhánh.
[EXP]
Đây là thao tác thủ công, tốn thời gian và dễ xảy ra sai sót so với việc sử dụng các tính năng tích hợp của Git.

@correct: C
@point: 20
@difficulty: 6
@concept: git-local-basics
@category: 1

## Q26

Khi làm việc nhóm trên GitHub, quy trình (workflow) nào dưới đây giúp giảm thiểu tối đa xung đột gộp nhánh (Merge Conflict) khi các thành viên cùng phát triển?

[A]
Thường xuyên chạy `git pull` để đồng bộ code mới nhất từ remote về local trước khi bắt đầu viết code mới.
[EXP]
Đúng. Thường xuyên đồng bộ giúp học viên luôn làm việc trên nền code mới nhất, giảm thiểu thay đổi chồng chéo.
[B]
Chỉ thực hiện đồng bộ code với remote một lần duy nhất vào cuối tuần sau khi tất cả đã hoàn thành công việc.
[EXP]
Việc để quá lâu không đồng bộ sẽ tích tụ lượng thay đổi cực lớn, dẫn đến xung đột vô cùng phức tạp khi gộp.
[C]
Mỗi thành viên tự tạo một repository GitHub riêng biệt và độc lập hoàn toàn để tự quản lý dự án cá nhân.
[EXP]
Đây không phải là làm việc nhóm phối hợp trên cùng dự án mà là chia cắt dự án, không áp dụng cho teamwork thực tế.
[D]
Yêu cầu các thành viên chỉ được phép sử dụng duy nhất một tài khoản GitHub chung để push code trực tiếp.
[EXP]
Dùng chung tài khoản không giải quyết được xung đột mã nguồn và vi phạm nguyên tắc bảo mật, định danh tác giả.

@correct: A
@point: 20
@difficulty: 6
@concept: git-remote-github
@category: 1

## Q27

Học viên muốn cấu hình xác thực SSH với GitHub. Để đảm bảo tính bảo mật cao nhất theo các khuyến nghị bảo mật hiện đại, học viên nên lựa chọn thuật toán nào để sinh khóa?

[A]
Sử dụng thuật toán `RSA` truyền thống với độ dài khóa mặc định là 2048 bit.
[EXP]
RSA 2048 bit hiện nay không còn được khuyến nghị ưu tiên hàng đầu bằng các thuật toán hiện đại hơn do hiệu năng thấp.
[B]
Sử dụng thuật toán `Ed25519` hiện đại có độ bảo mật cao và hiệu năng nhanh.
[EXP]
Đúng. Thuật toán Ed25519 là tiêu chuẩn hiện đại, bảo mật tốt hơn và nhanh hơn đáng kể so với các thuật toán cũ.
[C]
Sử dụng thuật toán `DSA` thế hệ cũ vì đây là tiêu chuẩn ban đầu của hệ thống.
[EXP]
DSA hiện nay đã lỗi thời, không còn an toàn và không được GitHub chấp nhận cho các khóa xác thực SSH mới tạo.
[D]
Sử dụng thuật toán `MD5` để sinh chuỗi mã hóa kết nối trực tiếp với máy chủ.
[EXP]
MD5 là một thuật toán băm (hashing), không phải thuật toán sinh cặp khóa mã hóa bất đối xứng để xác thực SSH.

@correct: B
@point: 20
@difficulty: 6
@concept: git-remote-github
@category: 1

## Q28

Học viên muốn loại bỏ các file tạm, file log tự động sinh ra trong dự án khỏi sự theo dõi của Git một cách triệt để mà không cần phải add thủ công. Giải pháp tối ưu nhất là gì?

[A]
Chạy lệnh `git clean -fd` định kỳ mỗi khi chuẩn bị tạo một commit mới.
[EXP]
Đây chỉ là giải pháp tạm thời xóa file vật lý hiện tại chứ không ngăn chặn các file đó sinh ra và bị theo dõi lại sau này.
[B]
Tạo một nhánh phụ riêng biệt chỉ chứa các file log này để tránh làm rác nhánh chính.
[EXP]
Việc này làm phức tạp hóa cấu trúc nhánh không cần thiết và không ngăn được Git theo dõi các file rác đó.
[C]
Định nghĩa các pattern tên file cần bỏ qua trong tệp tin đặc biệt `.gitignore`.
[EXP]
Đúng. Tệp `.gitignore` khai báo các mẫu tên file/thư mục cần Git bỏ qua vĩnh viễn không đưa vào hệ thống theo dõi.
[D]
Xóa thủ công từng file log trong thư mục dự án trước khi chạy lệnh git commit.
[EXP]
Cách này rất thủ công, dễ bỏ sót và tốn thời gian hơn nhiều so với việc định cấu hình tự động bằng `.gitignore`.

@correct: C
@point: 20
@difficulty: 6
@concept: git-advanced-history
@category: 1

## Q29

Khi một nhánh tính năng `feature` đã được gộp hoàn tất vào nhánh chính `main` và đẩy lên remote thành công. Học viên nên làm gì tiếp theo với nhánh `feature` đó?

[A]
Tiếp tục giữ nguyên nhánh đó ở cả local và remote để dự phòng lịch sử.
[EXP]
Việc giữ lại các nhánh đã merge xong chỉ làm rác danh sách nhánh, gây khó khăn cho việc quản lý dự án lâu dài.
[B]
Đổi tên nhánh đó thành một nhánh phụ khác để chuẩn bị làm tính năng mới.
[EXP]
Tái sử dụng nhánh cũ dễ dẫn đến xung đột lịch sử commit cũ, khuyên dùng tạo nhánh mới sạch sẽ từ main.
[C]
Push đè một commit rỗng lên nhánh đó trên remote để xóa toàn bộ các code cũ.
[EXP]
Cách này không giúp dọn dẹp nhánh mà còn tạo ra lịch sử commit rác không cần thiết trên remote repository.
[D]
Xóa nhánh đó ở cả local và remote để giữ cho repository gọn gàng, sạch sẽ.
[EXP]
Đúng. Xóa nhánh đã merge hoàn tất là best practice giúp quản lý danh sách nhánh hiệu quả và tránh nhầm lẫn.

@correct: D
@point: 20
@difficulty: 6
@concept: git-branching-conflicts
@category: 1

## Q30

Trong quá trình học viên chạy lệnh `git cherry-pick <hash>` để sao chép một commit vá lỗi từ nhánh khác sang nhánh hiện hành, hệ thống báo xảy ra xung đột (conflict). Sau khi học viên đã mở file và sửa xong xung đột thủ công, học viên cần chạy chuỗi lệnh nào để hoàn tất quá trình cherry-pick?

[A]
Chạy `git add <file>` để đánh dấu đã sửa, sau đó chạy `git cherry-pick --continue` để hoàn thành.
[EXP]
Đúng. Sau khi sửa xung đột thủ công, học viên phải add file để lưu trạng thái và dùng flag `--continue` để hoàn thành.
[B]
Chạy `git commit` trực tiếp mà không cần add để hệ thống tự động hoàn tất quá trình cherry-pick.
[EXP]
Git yêu cầu bạn phải đánh dấu file đã giải quyết xung đột bằng lệnh add trước khi cho phép tiếp tục hành động.
[C]
Chạy `git cherry-pick --abort` để lưu lại toàn bộ các sửa đổi xung đột mà bạn vừa thực hiện.
[EXP]
Tùy chọn `--abort` sẽ hủy bỏ hoàn toàn tiến trình cherry-pick hiện tại và đưa dự án về trạng thái trước đó.
[D]
Chạy `git push` trực tiếp lên remote để hệ thống GitHub tự động giải quyết các xung đột đó.
[EXP]
Bạn không thể push code khi đang ở trạng thái xung đột dở dang chưa hoàn tất commit cục bộ tại máy local.

@correct: A
@point: 20
@difficulty: 6
@concept: git-advanced-history
@category: 1

