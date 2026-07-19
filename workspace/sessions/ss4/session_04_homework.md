---
schema_version: 1
id: ss04_homework
type: homework
status: approved
course_id: devops-basic
session: 4
unit: 0
title: Homework Session 04
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
pm_ref: Session 04
language: vi
created: '2026-07-17'
updated: '2026-07-17'
exercise_count: 6
difficulty_mix:
  guided: 4
  hints: 1
  independent: 1
---

# Bài tập Session 04

### EX1 — Khởi tạo Local Repository và Cấu hình danh tính
- **tier:** guided
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_01]
- **owns_skills:** []
- **assumes:** []

#### Mục tiêu
- Khởi tạo thành công một Git repository trống tại thư mục làm việc cục bộ.
- Thiết lập thông tin danh tính tác giả (tên và email) ở cấp độ cục bộ (local).
- Tạo tệp tin mới, đưa vào vùng chuẩn bị (Staging Area) và tiến hành commit đầu tiên.
- Đọc và phân tích trạng thái thư mục làm việc và lịch sử commit thông qua lệnh log.

#### Yêu cầu
- **Bối cảnh:** Học viên bắt đầu một dự án phần mềm mới và muốn quản lý mã nguồn bằng Git ở local.
- **Ràng buộc:** Cấu hình email và tên tác giả bắt buộc phải sử dụng tùy chọn `--local` (không sử dụng `--global` để tránh ảnh hưởng đến các cấu hình toàn cục khác của máy tính).

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Kiểm tra cấu hình email cục bộ:
    ```bash
    git config --local user.email
    ```
  * Kiểm tra cấu hình tên cục bộ:
    ```bash
    git config --local user.name
    ```
  * Xem lịch sử commit:
    ```bash
    git log --oneline
    ```
- **Kết quả mong đợi:**
  * Lệnh cấu hình in ra đúng email và tên học viên đã cấu hình riêng cho dự án này.
  * `git log` hiển thị tối thiểu 1 commit đầu tiên với thông điệp rõ nghĩa.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Thư mục ẩn `.git` bên trong thư mục dự án cục bộ.
  * Tệp tin `README.md` đã được đưa vào Staging Area và commit thành công.
  * Tệp `.git/config` chứa cấu hình `user.name` và `user.email` tương ứng.
- **Yêu cầu không được có:**
  * Không cấu hình đè lên cấu hình toàn cục (`--global`) của máy tính.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_04/ex1/`
* **Cơ chế nộp:** Học viên tạo thư mục bài tập trên kho lưu trữ, nộp tệp báo cáo `README.md` liệt kê các lệnh cấu hình đã thực hiện (khởi tạo, cấu hình danh tính cục bộ, add, commit) kèm theo ảnh chụp màn hình hoặc kết quả chạy lệnh `git log --oneline` và `git config --local --list` để chứng minh đã cấu hình thành công.

#### Gợi ý/Bệ đỡ
1. Tạo một thư mục mới có tên là `git-basics` và di chuyển vào bên trong thư mục đó.
2. Khởi tạo Git repository bằng lệnh `git init`.
3. Cấu hình danh tính cục bộ cho dự án này:
   ```bash
   git config --local user.name "Ten Cua Ban"
   git config --local user.email "email_cua_ban@example.com"
   ```
4. Tạo tệp tin `README.md` và viết dòng chữ: `Day la du an dau tien su dung Git`.
5. Kiểm tra trạng thái bằng lệnh `git status`.
6. Đưa tệp tin vào Staging Area: `git add README.md`.
7. Tạo commit đầu tiên: `git commit -m "Khoi tao commit dau tien voi README.md"`.
8. Kiểm tra lịch sử commit bằng lệnh `git log`.

---

### EX2 — Quản lý nhánh và Giải quyết xung đột (Merge Conflict)
- **tier:** guided
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_02]
- **owns_skills:** []
- **assumes:** [git-local-basics]

#### Mục tiêu
- Tạo mới và di chuyển linh hoạt giữa các nhánh (branch) cục bộ.
- Cố ý tạo ra xung đột gộp nhánh (Merge Conflict) và xử lý xung đột thủ công.
- Hoàn thành commit gộp nhánh và hiểu cơ chế gộp 3 vùng (3-Way Merge).

#### Yêu cầu
- **Bối cảnh:** Học viên phát triển một tính năng mới trên nhánh phụ nhưng đồng thời nhánh chính `main` cũng được cập nhật, dẫn đến xung đột trên cùng một dòng code ở file `README.md`.
- **Ràng buộc:** Tránh tự động gộp, học viên bắt buộc phải xử lý thủ công các ký hiệu đánh dấu xung đột (`<<<<<<<`, `=======`, `>>>>>>>`) bên trong file.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Kiểm tra lịch sử commit dưới dạng nhánh:
    ```bash
    git log --graph --oneline
    ```
- **Kết quả mong đợi:**
  * Hiển thị nhánh `feature-update` tách ra từ `main`, sau đó gộp lại với một commit gộp (merge commit) có 2 nhánh tổ tiên.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Tệp `README.md` đã được giải quyết xung đột sạch sẽ (không còn chứa các ký tự đánh dấu xung đột của Git).
  * Lịch sử Git chứa commit merge hoàn chỉnh.
- **Yêu cầu không được có:**
  * Không sử dụng tùy chọn `--abort` để hủy bỏ quá trình gộp nhánh.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_04/ex2/`
* **Cơ chế nộp:** Học viên nộp tệp tin `README.md` sau khi đã giải quyết xung đột hoàn chỉnh, kèm theo báo cáo ngắn ghi rõ các bước giải quyết xung đột thủ công và hình chụp lịch sử commit hiển thị đồ thị nhánh chạy từ lệnh `git log --graph --oneline`.

#### Gợi ý/Bệ đỡ
1. Tạo một nhánh tính năng mới và di chuyển sang nhánh đó:
   ```bash
   git checkout -b feature-update
   ```
2. Sửa đổi dòng cuối cùng trong file `README.md` thành: `Sua doi dong cuoi tu nhanh feature-update`. Tiến hành commit thay đổi này:
   ```bash
   git add README.md
   git commit -m "Cap nhat noi dung tren nhanh feature-update"
   ```
3. Chuyển về nhánh `main`:
   ```bash
   git checkout main
   ```
4. Chỉnh sửa dòng cuối cùng trong file `README.md` (ở nhánh `main`) thành một nội dung khác: `Sua doi dong cuoi tu nhanh main`. Tiến hành commit:
   ```bash
   git add README.md
   git commit -m "Cap nhat dong cuoi tu nhanh main de tao xung dot"
   ```
5. Thực hiện gộp nhánh `feature-update` vào `main`:
   ```bash
   git merge feature-update
   ```
   *Kết quả:* Terminal báo lỗi xảy ra Merge Conflict ở file `README.md`.
6. Mở file `README.md`, thảo luận chọn lọc dòng code cần giữ lại, xóa toàn bộ các ký hiệu đánh dấu `<<<<<<< HEAD`, `=======`, và `>>>>>>> feature-update`.
7. Đánh dấu file đã giải quyết xung đột và hoàn thành commit:
   ```bash
   git add README.md
   git commit -m "Giai quyet xung dot va hoan tat gop nhanh feature-update"
   ```

---

### EX3 — Cấu hình xác thực SSH và Đẩy dự án lên GitHub
- **tier:** guided
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_03]
- **owns_skills:** []
- **assumes:** [git-local-basics]

#### Mục tiêu
- Khởi tạo cặp khóa SSH bảo mật phục vụ mục đích xác thực kết nối từ xa.
- Cấu hình liên kết an toàn giữa repository cục bộ với máy chủ GitHub.
- Đẩy (push) mã nguồn và lịch sử commit thành công lên GitHub bằng giao thức SSH.

#### Yêu cầu
- **Bối cảnh:** Học viên cần đưa dự án cục bộ lên kho lưu trữ đám mây GitHub để lưu trữ và cộng tác nhóm.
- **Ràng buộc:** Bắt buộc sử dụng giao thức SSH và thuật toán `Ed25519` để sinh khóa (không sử dụng giao thức HTTPS để tránh phải nhập password/token thủ công).

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Kiểm tra kết nối SSH tới GitHub:
    ```bash
    ssh -T git@github.com
    ```
  * Kiểm tra cấu hình remote URL:
    ```bash
    git remote -v
    ```
- **Kết quả mong đợi:**
  * Lệnh ssh trả về thông báo xác nhận danh tính tài khoản GitHub của bạn thành công.
  * Đường dẫn URL của remote `origin` có dạng dạng SSH: `git@github.com:username/repository.git`.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Tệp tin khóa public `id_ed25519.pub` nằm trong thư mục `~/.ssh/`.
  * Có remote có tên là `origin` liên kết đúng tới repository trên GitHub.
- **Yêu cầu không được có:**
  * Không chia sẻ hoặc nộp tệp khóa private `id_ed25519` lên Git.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_04/ex3/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` mô tả quá trình tạo khóa SSH Ed25519, liên kết remote repository và cung cấp đường dẫn URL của kho lưu trữ GitHub công khai/riêng tư đã được cấu hình thành công (không nộp khóa private).

#### Gợi ý/Bệ đỡ
1. Mở terminal, sinh cặp khóa SSH mới bằng thuật toán Ed25519:
   ```bash
   ssh-keygen -t ed25519 -C "email_cua_ban@example.com"
   ```
   *Lưu ý:* Nhấn Enter liên tiếp để sử dụng đường dẫn lưu mặc định và bỏ qua mật khẩu passphrase nếu muốn nhanh.
2. Đọc nội dung của file khóa công khai vừa tạo:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
3. Copy toàn bộ chuỗi ký tự hiển thị, truy cập website GitHub cá nhân, chọn **Settings -> SSH and GPG keys -> New SSH Key**, điền tên và dán nội dung vào rồi bấm Add.
4. Tạo một repository trống hoàn toàn trên GitHub có tên là `git-basics` (không chọn tích hợp README hay license).
5. Liên kết repository local hiện tại với GitHub:
   ```bash
   git remote add origin git@github.com:username/git-basics.git
   ```
   *Lưu ý:* Thay thế `username` bằng tên tài khoản thật của bạn.
6. Đẩy mã nguồn từ nhánh `main` lên GitHub và thiết lập theo dõi mặc định:
   ```bash
   git push -u origin main
   ```

---

### EX4 — Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)
- **tier:** guided
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_04]
- **owns_skills:** []
- **assumes:** [git-local-basics]

#### Mục tiêu
- Cấu hình tệp tin ẩn `.gitignore` để tự động bỏ qua các file nhạy cảm hoặc file rác hệ thống.
- Sử dụng lệnh gỡ bỏ file đã commit ra khỏi cache theo dõi của Git một cách an toàn.
- Chỉnh sửa thông điệp hoặc nội dung của commit gần nhất thông qua tùy chọn amend.

#### Yêu cầu
- **Bối cảnh:** Học viên vô tình commit nhầm file chứa thông tin bảo mật `credentials.txt` lên Git. Học viên cần gỡ bỏ file này khỏi sự theo dõi mà không làm mất file vật lý trên đĩa cứng, cấu hình để Git bỏ qua file này trong tương lai, và sửa lại tin nhắn commit gần nhất cho sạch sẽ.
- **Ràng buộc:** Không sử dụng lệnh xóa vật lý file trên hệ điều hành, phải giữ lại tệp tin ở thư mục làm việc cục bộ.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Kiểm tra trạng thái file:
    ```bash
    git status
    ```
  * Kiểm tra lịch sử commit gần nhất:
    ```bash
    git log -n 1
    ```
- **Kết quả mong đợi:**
  * File `credentials.txt` không còn xuất hiện trong danh sách theo dõi của Git (không ở dạng Staged hay Modified).
  * Lịch sử commit gần nhất hiển thị thông điệp đã sửa đổi thành công.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Có tệp `.gitignore` chứa dòng khai báo `credentials.txt`.
  * Tệp `credentials.txt` vẫn tồn tại ở Working Directory cục bộ nhưng không có trong cơ sở dữ liệu commit mới nhất.
- **Yêu cầu không được có:**
  * Không chứa các ký tự/dòng rác dư thừa trong `.gitignore`.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_04/ex4/`
* **Cơ chế nộp:** Học viên nộp tệp `.gitignore` đã tạo và tệp báo cáo `README.md` giải thích cách gỡ bỏ file khỏi cache của Git bằng lệnh `git rm --cached` cùng kết quả hiển thị của lệnh `git log -n 1` chứng minh đã sử dụng `--amend` để sửa đổi thông điệp commit thành công.

#### Gợi ý/Bệ đỡ
1. Tạo một tệp mới tên là `credentials.txt` chứa nội dung dummy bảo mật: `PASSWORD=super_secret_123`.
2. Thực hiện add và commit nhầm file này lên local:
   ```bash
   git add credentials.txt
   ```
   ```bash
   git commit -m "Them credentials.txt nhay cam"
   ```
3. Chạy lệnh gỡ tệp tin ra khỏi cache theo dõi của Git (nhưng giữ nguyên file ở Working Directory cục bộ):
   ```bash
   git rm --cached credentials.txt
   ```
4. Tạo tệp `.gitignore` trong thư mục gốc dự án và ghi dòng chữ sau vào bên trong:
   ```
   credentials.txt
   ```
5. Đưa `.gitignore` vào vùng chuẩn bị và thực hiện sửa đổi ghi đè commit gần nhất (gộp chung tệp .gitignore mới tạo và sửa đổi thông điệp commit lỗi cũ):
   ```bash
   git add .gitignore
   ```
   ```bash
   git commit --amend -m "Them cau hinh .gitignore va loai bo file mat khau nhay cam"
   ```
6. Kiểm tra lại trạng thái tệp tin bằng `git status`.

---

### EX5 — Khôi phục trạng thái và Đảo ngược commit (Reset vs Revert)
- **tier:** hints
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_04]
- **owns_skills:** []
- **assumes:** [git-local-basics]

#### Mục tiêu
- Ứng dụng thành thạo hai cơ chế reset và revert để sửa chữa sai sót trong lịch sử dự án.
- Phân biệt sự khác nhau giữa khôi phục lịch sử cục bộ và đảo ngược lịch sử an toàn khi làm việc nhóm.

#### Yêu cầu
- **Bối cảnh:** Học viên đã tạo ra một commit chứa mã nguồn bị lỗi ở local. Học viên cần thực hành hai kỹ thuật khác nhau để xử lý lỗi này:
  * **Trường hợp 1 (Sửa đổi cục bộ):** Di chuyển lịch sử cục bộ lùi lại 1 commit và giữ lại các tệp tin thay đổi ở dạng chưa chuẩn bị để viết lại code.
  * **Trường hợp 2 (Sửa đổi công cộng):** Đảo ngược thay đổi của một commit cũ bằng cách tạo thêm một commit mới đối lập để đẩy lên remote an toàn.
- **Ràng buộc:** 
  * Trong trường hợp 1, không được làm mất mã nguồn hiện hành (không dùng reset hard).
  * Trong trường hợp 2, bắt buộc tạo ra một commit mới để ghi lại lịch sử đảo ngược rõ ràng.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Xem log lịch sử commit:
    ```bash
    git log --oneline -n 5
    ```
- **Kết quả mong đợi:**
  * Trường hợp 1: Con trỏ HEAD lùi lại, thay đổi nằm trong Working Directory dưới dạng Modified.
  * Trường hợp 2: Có một commit mới có tiêu đề bắt đầu bằng `Revert ...` xuất hiện trên đầu nhánh.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Nhánh lịch sử chứa commit revert hợp lệ có chứa nội dung đảo ngược đúng đắn.
- **Yêu cầu không được có:**
  * Tránh sử dụng reset hard trên các nhánh đã push lên remote chung để không làm đứt gãy code của đồng nghiệp.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_04/ex5/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` trình bày chi tiết cách thực hiện hai trường hợp (Reset và Revert), đồng thời giải thích rõ sự khác biệt của hai cơ chế này khi làm việc cá nhân so với khi làm việc nhóm trên nhánh chung. Kèm theo ảnh chụp lịch sử commit chứng minh đã tạo commit revert thành công.

#### Gợi ý/Bệ đỡ
- Sử dụng lệnh `git reset --mixed HEAD~1` (hoặc `HEAD^`) để di chuyển con trỏ nhánh lùi về quá khứ và đưa code của commit bị hủy về Working Directory.
- Sử dụng lệnh `git revert <commit_hash>` để Git tự động tạo một commit mới đảo ngược các thay đổi dòng code của commit có mã hash tương ứng.

---

### EX6 — Tích hợp Quy trình Teamwork (Cherry-pick, Pull và Xử lý xung đột từ xa)
- **tier:** independent
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_02, ss04_lesson_03, ss04_lesson_04]
- **owns_skills:** []
- **assumes:** [git-branching-conflicts, git-remote-github, git-advanced-history]

#### Mục tiêu
- Vận dụng phối hợp tổng hợp các kỹ năng Git nâng cao để giải quyết bài toán teamwork thực tế.
- Tự chủ trong việc chọn lọc commit (cherry-pick), đồng bộ từ xa (pull) và xử lý xung đột phát sinh từ xa.

#### Yêu cầu
- **Bối cảnh:** Học viên đang đứng ở nhánh `main`. Nhánh phụ `hotfix-security` có chứa 3 commit thử nghiệm, trong đó chỉ có commit thứ 2 (sửa lỗi rò rỉ dữ liệu) là cần thiết để gộp vào nhánh chính. Tuy nhiên, sau khi học viên sao chép thành công commit này sang `main` local và chuẩn bị đẩy lên GitHub, hệ thống GitHub từ chối do một thành viên khác trong nhóm đã đẩy commit mới lên trước. Học viên phải kéo code mới về, xử lý xung đột local một cách an toàn và đẩy hoàn thành dự án lên remote.
- **Ràng buộc:** 
  * Không gộp (merge) cả nhánh `hotfix-security` vào `main`. Chỉ lấy duy nhất một commit sửa lỗi chọn lọc.
  * Không sử dụng tùy chọn push force (`-f` hoặc `--force`) để ghi đè lịch sử trên GitHub.
  * Mọi lịch sử gộp và đồng bộ phải thẳng đẹp, không chứa tệp rác dư thừa.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Xem log và kiểm tra trạng thái remote:
    ```bash
    git log --graph --oneline
    git status
    ```
- **Kết quả mong đợi:**
  * Nhánh `main` trên local và remote đồng bộ hoàn toàn.
  * Lịch sử chứa commit được cherry-pick từ nhánh hotfix và có commit gộp đồng bộ khi pull từ remote về.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Commit sửa lỗi hotfix được tích hợp thành công vào nhánh `main` mà không mang theo các commit rác từ nhánh `hotfix-security`.
  * Xử lý và giải quyết triệt để mọi xung đột gộp nhánh phát sinh khi pull từ remote.
- **Yêu cầu không được có:**
  * Tuyệt đối không dùng push force để tránh xóa lịch sử code của thành viên nhóm.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_04/ex6/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` ghi nhận lại toàn bộ nhật ký các lệnh đã thực hiện (cherry-pick, pull, giải quyết xung đột, push), kèm ảnh chụp đồ thị lịch sử `git log --graph --oneline` để chứng minh tiến trình nhánh `main` đã tích hợp đúng và đồng bộ hoàn tất với remote.

#### Gợi ý/Bệ đỡ
- Không có hướng dẫn chi tiết. Học viên cần tự nhớ lại cú pháp `git cherry-pick <hash>`, `git pull` để tải về và gộp nhánh remote, sửa conflict thủ công và thực thi `git push` để hoàn tất nhiệm vụ.

