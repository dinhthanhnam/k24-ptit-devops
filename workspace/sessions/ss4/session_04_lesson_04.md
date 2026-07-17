---
schema_version: 1
id: ss04_lesson_04
type: lesson
status: approved
course_id: devops-basic
session: 4
unit: 4
title: Kỹ thuật Git nâng cao và quản lý lịch sử
session_kind: theory
tags: []
concepts: &id001
- git-advanced-history
depends_on: []
builds_on: []
enables: []
owns: *id001
assumes:
- git-remote-github
does_not_cover: []
source: generated
pm_ref: Session 04 / Lesson 04
language: vi
created: '2026-07-17'
updated: '2026-07-17'
lesson_mode: practical
---

# Kỹ thuật Git nâng cao và quản lý lịch sử

<!-- section: problem -->
## 1. Đặt vấn đề
Trong quá trình làm việc lâu dài với dự án, lập trình viên không thể tránh khỏi những sai lầm khi làm việc với Git:
* **Commit sai sót:** Tin nhắn commit bị viết sai chính tả, hoặc commit xong mới phát hiện quên chưa lưu một file quan trọng.
* **Commit nhầm tệp tin rác:** Các tệp tin cấu hình tạm thời, log hệ thống, hoặc thư mục build phình to (`node_modules`, `target`, `.log`) bị đưa lên remote repository, gây nặng bộ nhớ và làm nhiễu lịch sử.
* **Nhu cầu khôi phục trạng thái cũ:** Khi phiên bản code mới chạy bị lỗi nghiêm trọng, lập trình viên cần quay trở lại trạng thái hoạt động tốt ở quá khứ nhưng băn khoăn giữa việc xóa hẳn lịch sử (Reset) hay giữ lại lịch sử để tránh làm ảnh hưởng đến cả nhóm (Revert).
* **Nhu cầu sao chép chọn lọc:** Nhánh phát triển có hàng chục commit thử nghiệm chưa hoàn chỉnh, bạn chỉ muốn lấy đúng một commit chứa tính năng sửa lỗi (Hotfix) đưa vào nhánh chính `main` mà không muốn gộp (merge) toàn bộ các thay đổi chưa hoàn thiện kia.

Để xử lý các tình huống thực tế này, bạn cần nắm vững các kỹ thuật Git nâng cao bao gồm sửa đổi commit (Amend), phục hồi code (Reset & Revert), **sao chép chọn lọc commit (Cherry-pick)** và tối ưu hóa hệ thống bằng `.gitignore`.

<!-- section: core -->
## 2. Kiến thức cốt lõi

### 2.1. Sửa đổi commit gần nhất (`git commit --amend`)
Tùy chọn `--amend` cho phép bạn ghi đè trực tiếp lên commit mới nhất của nhánh hiện tại. Lệnh này thường dùng để:
* Sửa đổi nội dung tin nhắn của commit vừa tạo.
* Bổ sung thêm các tệp tin bị quên vào commit vừa tạo mà không làm phát sinh thêm commit rác trong lịch sử.

*(Lưu ý: Chỉ nên sử dụng `--amend` đối với các commit local chưa được push lên remote).*

### 2.2. Phục hồi lịch sử: Git Reset vs Git Revert
Khi muốn hủy bỏ các thay đổi đã commit, Git cung cấp hai giải pháp với triết lý khác nhau:

1. **Git Reset (Xóa lịch sử):** Di chuyển con trỏ nhánh hiện tại lùi lại về một commit chỉ định trong quá khứ. Có 3 chế độ hoạt động chính:
   * `--soft`: Chỉ di chuyển con trỏ nhánh. Toàn bộ thay đổi của các commit bị hủy vẫn được giữ lại tại **Staging Area**.
   * `--mixed` (Mặc định): Di chuyển con trỏ nhánh và dọn dẹp Staging Area. Toàn bộ thay đổi của các commit bị hủy sẽ được giữ lại tại **Working Directory** dưới dạng tệp tin chưa được add.
   * `--hard` (Nguy hiểm): Di chuyển con trỏ nhánh, xóa sạch toàn bộ thay đổi ở cả Staging Area và Working Directory. Lịch sử và mã nguồn bị xóa bỏ triệt để.
2. **Git Revert (Đảo ngược lịch sử):** Không xóa bỏ commit cũ, mà tạo ra một **commit mới** có nội dung hoàn toàn đối lập/đảo ngược với commit được chỉ định. Lịch sử cũ được giữ nguyên, đảm bảo an toàn tuyệt đối khi làm việc nhóm trên các nhánh chung đã push lên remote.

### 2.3. Trạng thái Detached HEAD
Bình thường, con trỏ HEAD sẽ trỏ vào con trỏ của một nhánh (như `main`). Tuy nhiên, khi bạn checkout trực tiếp đến một commit hash cụ thể (`git checkout <commit_hash>`), HEAD sẽ trỏ trực tiếp đến commit đó thay vì con trỏ nhánh. Trạng thái này gọi là **Detached HEAD** (HEAD bị tách rời). 
Ở trạng thái này, bạn có thể chạy thử nghiệm hoặc sửa đổi code tạm thời, nhưng nếu bạn tạo commit mới tại đây, các commit đó sẽ không thuộc về nhánh nào và dễ bị Git tự động dọn dẹp khi bạn checkout sang nhánh khác.

### 2.4. Khái niệm `git cherry-pick` (Trích xuất chọn lọc)
Lệnh `git cherry-pick <commit_hash>` cho phép bạn sao chép và áp dụng duy nhất thay đổi của một commit cụ thể từ một nhánh khác vào nhánh hiện tại mà bạn đang đứng làm việc. Thay vì gộp toàn bộ nhánh (Merge), cherry-pick giúp bạn cô lập và tái sử dụng mã nguồn cực kỳ linh hoạt (ví dụ: port một bản sửa lỗi hotfix từ nhánh thử nghiệm về thẳng nhánh chính).

### 2.5. Cơ chế hoạt động của `.gitignore`
Tệp tin cấu hình đặc biệt `.gitignore` nằm ở thư mục gốc của dự án chứa danh sách các mẫu đường dẫn (glob patterns) mà Git sẽ tự động bỏ qua, không theo dõi và không hiển thị dưới mục Untracked.
* Các tệp tin cần đưa vào `.gitignore` thường là: `.log` (log hệ thống), `/target` hoặc `/build` (thư mục biên dịch), `node_modules` (thư viện tải về), `.env` (chứa secret keys cá nhân).
* **Lưu ý:** `.gitignore` chỉ có tác dụng với các file chưa từng được Git theo dõi. Nếu file đã được commit từ trước, bạn phải xóa cache của nó ra khỏi Git bằng lệnh `git rm --cached <file>` thì `.gitignore` mới bắt đầu có hiệu lực với file đó.

<!-- section: steps -->
## 3. Các step thực hành

### Step 1 — Thiết lập tệp tin `.gitignore`
Tạo và viết quy tắc bỏ qua tệp tin rác trong dự án.

1. Tạo file `.gitignore` tại thư mục gốc của repository:
   ```bash
   touch .gitignore
   ```
2. Thêm các quy tắc bỏ qua file log và thư mục build bằng cách mở file và viết:
   ```text
   # Bỏ qua toàn bộ các file có đuôi .log
   *.log
   # Bỏ qua toàn bộ nội dung trong thư mục build/
   build/
   ```
3. Tạo thử file rác để kiểm tra:
   ```bash
   touch app.log
   mkdir build && touch build/output.txt
   ```
4. Kiểm tra trạng thái dự án:
   ```bash
   git status
   ```
   *Kết quả:* Git hiển thị tệp `.gitignore` trong danh mục Untracked, nhưng hoàn toàn không nhìn thấy tệp `app.log` và thư mục `build/`.

### Step 2 — Thực hành sửa đổi commit gần nhất (Git Amend)
Sửa đổi tin nhắn commit vừa thực hiện mà không tạo thêm commit mới.

1. Đưa tệp `.gitignore` vào staging và commit:
   ```bash
   git add .gitignore
   git commit -m "Them file gitignore"
   ```
2. Phát hiện tin nhắn viết sai hoặc muốn đổi sang tiếng Việt chuyên nghiệp hơn. Chạy lệnh:
   ```bash
   git commit --amend -m "Cau hinh file .gitignore de bo qua file rac va logs"
   ```
3. Xem lại lịch sử:
   ```bash
   git log -n 1
   ```
   *Kết quả:* Bạn chỉ thấy duy nhất 1 commit mới được cập nhật lại tin nhắn mới, không có commit rác trung gian.

### Step 3 — Trải nghiệm trạng thái Detached HEAD
Thao tác "du hành thời gian" về xem lại trạng thái của các commit cũ.

1. Xem lịch sử commit rút gọn để lấy mã hash:
   ```bash
   git log --oneline
   ```
2. Checkout trực tiếp về mã hash của commit khởi tạo ban đầu (ví dụ: `a1b2c3d`):
   ```bash
   git checkout <commit_hash>
   ```
3. Quan sát thông báo của Git: Hệ thống hiển thị cảnh báo `You are in 'detached HEAD' state...`.
4. Xem lại mã nguồn: file `.gitignore` biến mất vì lúc này con trỏ HEAD đang đứng tại thời điểm quá khứ chưa tạo file đó.
5. Để quay trở lại trạng thái bình thường của nhánh chính:
   ```bash
   git checkout main
   ```

### Step 4 — Thực hành Git Reset (--soft và --mixed)
Hủy bỏ commit nhưng vẫn giữ lại các phần mã nguồn đã viết để chỉnh sửa tiếp.

1. Tạo một commit thử nghiệm mới:
   ```bash
   echo "function connect() {}" > db.js
   git add db.js
   git commit -m "Them ham ket noi database"
   ```
2. Thực hiện reset lùi lại 1 commit bằng chế độ `--soft`:
   ```bash
   git reset --soft HEAD~1
   ```
   *(HEAD~1 có nghĩa là lùi về trước HEAD 1 commit).*
3. Chạy `git status`: File `db.js` vẫn tồn tại và đang ở trạng thái **Staged** (màu xanh).
4. Tiếp tục thực hiện reset sang chế độ `--mixed`:
   ```bash
   git reset --mixed HEAD
   ```
5. Chạy `git status`: File `db.js` vẫn tồn tại nhưng đã chuyển sang trạng thái **Modified/Untracked** (màu đỏ) ở Working Directory.

### Step 5 — Thực hành Git Reset --hard (Xóa triệt để)
Hủy bỏ commit và xóa sạch toàn bộ mã nguồn liên quan.

1. Đưa file `db.js` vào staging và commit lại:
   ```bash
   git add db.js
   git commit -m "Them ham ket noi db de reset hard"
   ```
2. Tiến hành reset chế độ triệt tiêu:
   ```bash
   git reset --hard HEAD~1
   ```
3. Kiểm tra thư mục: File `db.js` đã bị xóa sạch hoàn toàn khỏi ổ cứng máy tính. Lịch sử commit cũng bị lùi lại.

### Step 6 — Thực hành đảo ngược an toàn với Git Revert
Tạo commit đảo ngược thay đổi để chia sẻ an toàn với nhóm.

1. Tạo một commit mới:
   ```bash
   echo "Chuoi ki tu loi" > config.txt
   git add config.txt
   git commit -m "Them file cau hinh loi"
   ```
2. Lấy mã hash commit vừa tạo qua `git log --oneline`.
3. Thực hiện revert commit đó:
   ```bash
   git revert <commit_hash> --no-edit
   ```
   *(Tùy chọn `--no-edit` để tự động dùng tin nhắn đảo ngược mặc định của Git).*
4. Kiểm tra lại thư mục: File `config.txt` đã bị xóa bỏ (hoặc đảo ngược nội dung). Chạy `git log --oneline` hiển thị commit lỗi ban đầu vẫn còn, và có thêm một commit mới tên là `Revert "Them file cau hinh loi"`.

### Step 7 — Thực hành trích xuất chọn lọc với Git Cherry-pick
Sao chép duy nhất một commit hotfix từ nhánh khác về nhánh `main`.

1. Tạo và chuyển sang nhánh phụ `hotfix-branch`:
   ```bash
   git checkout -b hotfix-branch
   ```
2. Thực hiện hai commit khác nhau:
   * Commit 1 (Tính năng chưa hoàn thiện):
     ```bash
     echo "Code tinh nang A dang viet do" > feature_a.js
     git add feature_a.js
     git commit -m "Dang viet tinh nang A"
     ```
   * Commit 2 (Bản vá lỗi khẩn cấp):
     ```bash
     echo "Code sua loi hotfix" > fix_bug.js
     git add fix_bug.js
     git commit -m "Sua loi hotfix he thong"
     ```
3. Lấy mã commit hash của commit **Sua loi hotfix he thong** (ví dụ: `e5f6g7h`):
   ```bash
   git log --oneline
   ```
4. Quay trở về nhánh chính `main`:
   ```bash
   git checkout main
   ```
5. Thực hiện cherry-pick để chỉ lấy đúng bản vá lỗi đưa vào `main`:
   ```bash
   git cherry-pick <commit_hash_hotfix>
   ```
6. Kiểm tra thư mục: Chỉ có file `fix_bug.js` xuất hiện trên `main`, file `feature_a.js` hoàn toàn không có mặt. Lịch sử commit trên nhánh `main` được cập nhật thêm một commit vá lỗi mới.

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
* **Chạy `git reset --hard` gây mất code chưa commit:** Lệnh `git reset --hard` sẽ ghi đè và xóa bỏ hoàn toàn tất cả các thay đổi chưa được commit tại Working Directory. Một khi đã chạy lệnh này, bạn sẽ không thể khôi phục lại những dòng code chưa lưu đó.
* **Dùng `git reset` trên nhánh chung đã push lên remote:** Nếu bạn reset lùi lịch sử ở local trên nhánh `main`, sau đó push lên remote, Git sẽ báo lỗi từ chối do lịch sử local bị đi sau remote. Nếu cố tình dùng `git push -f` để ghi đè, bạn sẽ xóa lịch sử của các lập trình viên khác trong nhóm và gây xung đột nghiêm trọng cho dự án. Hãy luôn dùng `git revert` khi làm việc trên nhánh chung đã push.
* **Quên xử lý conflict khi chạy `git cherry-pick`:** Tương tự như merge, cherry-pick vẫn có thể gây ra xung đột nếu dòng code trong commit được chọn trùng lặp sửa đổi với dòng code hiện hành trên nhánh đích. Khi đó, bạn phải sửa conflict thủ công, chạy `git add` và chạy `git cherry-pick --continue` để hoàn tất.
* **Đưa file vào `.gitignore` sau khi đã commit:** `.gitignore` không có tác dụng ngược. Nếu bạn lỡ commit tệp cấu hình chứa mật khẩu, việc thêm nó vào `.gitignore` sau đó không làm tệp tin đó biến mất khỏi lịch sử theo dõi. Bạn phải chạy lệnh `git rm --cached <file_name>` trước khi commit file `.gitignore` để gỡ bỏ tệp đó khỏi cache theo dõi của Git.

<!-- section: references -->
## 5. Tài liệu tham khảo
* [Sách Pro Git - Chương 7.7: Kỹ thuật Reset trong Git (Demystifying Reset)](https://git-scm.com/book/vi/v2/Git-Tools-Reset-Demystified)
* [Atlassian Git Tutorials: Git Reset, Git Revert and Git Cherry-pick](https://www.atlassian.com/git/tutorials/undoing-changes)
* [Sách Pro Git - Chương 2.2: Bỏ qua các tệp tin (.gitignore)](https://git-scm.com/book/vi/v2/Git-C%C4%83n-B%E1%BA%A3n-Ghi-L%E1%BA%A1i-Thay-%C4%90%E1%BB%95i-v%C3%A0o-Kho-Ch%E1%BB%A9a#_ignoring_files)

