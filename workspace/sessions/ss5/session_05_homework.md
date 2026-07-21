---
schema_version: 1
id: ss05_homework
type: homework
status: approved
course_id: devops-basic
session: 5
unit: 0
title: Bài tập thực hành Git và GitHub nâng cao
session_kind: practice
tags: []
concepts: []
depends_on:
- ss04_homework
builds_on: []
enables: []
owns: []
assumes:
- git-local-basics
- git-branching-conflicts
- git-remote-github
- git-advanced-history
does_not_cover: []
source: generated
pm_ref: Session 05
language: vi
created: '2026-07-19'
updated: '2026-07-19'
exercise_count: 6
difficulty_mix:
  guided: 4
  hints: 1
  independent: 1
practice_of:
- 4
maps_to_sessions:
- 4
---

# Bài tập thực hành Git và GitHub nâng cao

### EX1 — Khôi phục commit đã mất bằng Git Reflog
- **tier:** guided
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_04]
- **owns_skills:** []
- **assumes:** [git-local-basics]

#### Mục tiêu
- Hiểu được cách Git lưu trữ lịch sử hoạt động cục bộ thông qua Reflog.
- Sử dụng thành thạo lệnh `git reflog` để truy vết các tham chiếu commit cũ.
- Khôi phục thành công một commit đã bị xóa mất khỏi nhánh làm việc sau khi thực thi lệnh reset hard.

#### Yêu cầu
- **Bối cảnh:** Học viên vô tình chạy lệnh `git reset --hard HEAD~1` trên repository cục bộ, khiến cho commit quan trọng nhất chứa mã nguồn vừa chỉnh sửa bị biến mất và không hiển thị trên `git log`.
- **Ràng buộc:** Không được viết lại code thủ công, bắt buộc phải dùng cơ chế Reflog của Git để kéo lại commit trạng thái cũ.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Xem log lịch sử commit hiện tại:
    ```bash
    git log --oneline
    ```
  * Xem nhật ký tham chiếu Reflog:
    ```bash
    git reflog
    ```
- **Kết quả mong đợi:**
  * Lịch sử `git log` khôi phục lại đúng commit có tiêu đề và nội dung ban đầu (trước khi bị reset).

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Tệp báo cáo `README.md` chỉ ra mã băm (SHA-1 hash) của commit trước và sau khi khôi phục.
  * Lịch sử Git chứa đúng nội dung tệp tin đã khôi phục.
- **Yêu cầu không được có:**
  * Tránh thực hiện commit mới đè lên với nội dung gõ lại thủ công.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_05/ex1/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` mô tả từng bước thực hiện từ khi phát hiện mất commit, chạy lệnh tra cứu reflog đến khi khôi phục thành công bằng lệnh checkout hoặc reset.

#### Gợi ý/Bệ đỡ
1. Khởi tạo một dự án thử nghiệm, tạo file `feature.txt` có nội dung `Day la tinh nang quan trong`.
2. Commit thay đổi: `git add .` và `git commit -m "Them tinh nang quan trong"`.
3. Giả lập lỗi bằng cách lùi commit và xóa sạch working directory:
   ```bash
   git reset --hard HEAD~1
   ```
4. Kiểm tra `git log` để xác nhận commit đã biến mất.
5. Tra cứu reflog để tìm mã hash của commit vừa bị xóa:
   ```bash
   git reflog
   ```
   *Kết quả hiển thị dạng:* `e3a5b2c HEAD@{1}: commit: Them tinh nang quan trong`
6. Khôi phục lại commit đó về nhánh hiện tại:
   ```bash
   git reset --hard e3a5b2c
   ```
   *(Thay `e3a5b2c` bằng mã hash thật tìm được trong reflog của bạn).*

---

### EX2 — Tái cấu trúc lịch sử commit bằng Interactive Rebase
- **tier:** guided
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_04]
- **owns_skills:** []
- **assumes:** [git-local-basics, git-advanced-history]

#### Mục tiêu
- Sử dụng công cụ tương tác Interactive Rebase để chỉnh sửa lịch sử cục bộ.
- Thực hiện gộp nhiều commit nhỏ lẻ (squash) thành một commit duy nhất có ý nghĩa.
- Đổi tên thông điệp commit (reword) và xóa bỏ một commit không cần thiết (drop).

#### Yêu cầu
- **Bối cảnh:** Nhánh tính năng của học viên trước khi đẩy lên remote chứa nhiều commit thử nghiệm vụn vặt và thông điệp không rõ ràng (ví dụ: "fix typo", "temp", "adds file").
- **Ràng buộc:** 
  * Gộp 3 commit nhỏ cuối cùng thành 1 commit duy nhất.
  * Thay đổi thông điệp commit sau khi gộp thành: `feat: hoan thien module authentication`.
  * Xóa bỏ hoàn toàn một commit chứa file rác thử nghiệm (`temp.txt`).

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Xem log lịch sử chi tiết:
    ```bash
    git log --oneline
    ```
- **Kết quả mong đợi:**
  * Lịch sử chỉ hiển thị duy nhất một commit sạch sẽ đại diện cho tính năng, không còn các commit phụ rác.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Lịch sử commit sạch sẽ, thông điệp tuân thủ định dạng chuẩn (`feat:...`).
  * File rác `temp.txt` biến mất khỏi cả thư mục làm việc và lịch sử Git.
- **Yêu cầu không được có:**
  * Tuyệt đối không để sót các commit thử nghiệm trung gian trong lịch sử sau rebase.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_05/ex2/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` chụp lại màn hình giao diện soạn thảo Interactive Rebase (giao diện cấu hình pick, squash, reword, drop) và log lịch sử commit sạch sẽ sau khi hoàn tất.

#### Gợi ý/Bệ đỡ
1. Tạo lần lượt 4 commit trên nhánh làm việc hiện tại:
   - Commit 1: Tạo `auth.js` -> `feat: khoi tao module auth`
   - Commit 2: Sửa `auth.js` -> `fix typo`
   - Commit 3: Sửa `auth.js` -> `adds utility functions`
   - Commit 4: Tạo `temp.txt` -> `add temp file for debug`
2. Chạy lệnh Interactive Rebase lùi về 4 commit trước:
   ```bash
   git rebase -i HEAD~4
   ```
3. Trong trình soạn thảo mở ra, cấu hình các dòng như sau:
   - Commit 1: Giữ nguyên `pick`
   - Commit 2: Thay `pick` thành `squash` (hoặc `s`)
   - Commit 3: Thay `pick` thành `squash` (hoặc `s`)
   - Commit 4: Thay `pick` thành `drop` (hoặc `d` để xóa bỏ commit này)
4. Lưu và đóng trình soạn thảo. Git sẽ yêu cầu soạn thảo lại thông điệp cho commit gộp. Sửa lại thành: `feat: hoan thien module authentication`.

---

### EX3 — Xử lý xung đột phức tạp trong quá trình Rebase
- **tier:** guided
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_02, ss04_lesson_04]
- **owns_skills:** []
- **assumes:** [git-branching-conflicts, git-advanced-history]

#### Mục tiêu
- Hiểu được sự khác biệt giữa giải quyết xung đột khi Merge và khi Rebase.
- Áp dụng quy trình giải quyết xung đột từng bước (step-by-step conflict resolution) trong Rebase.
- Đưa lịch sử nhánh tính năng lên trên đầu nhánh chính một cách thẳng hàng.

#### Yêu cầu
- **Bối cảnh:** Nhánh `main` đã có thêm 2 commit mới từ các thành viên khác sửa đổi tệp tin cấu hình `config.json`. Nhánh `feature-api` của học viên cũng sửa đổi cùng các dòng trong tệp tin đó qua 2 commit khác nhau. Khi học viên rebase nhánh `feature-api` lên `main`, xung đột sẽ xảy ra ở từng commit trong tiến trình rebase.
- **Ràng buộc:** Học viên phải giải quyết xung đột thủ công ở từng chặng, không được dùng merge thông thường và không được phá hỏng code của nhánh chính.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Kiểm tra trạng thái rebase:
    ```bash
    git status
    ```
  * Kiểm tra lịch sử sau khi hoàn thành:
    ```bash
    git log --graph --oneline
    ```
- **Kết quả mong đợi:**
  * Lịch sử Git thẳng tắp, không có merge commit phụ. Các commit của nhánh `feature-api` nằm nối tiếp ngay sau các commit mới nhất của `main`.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Tệp `config.json` hợp nhất đúng đắn code của cả hai bên.
  * Lịch sử commit dạng đồ thị thẳng đẹp.
- **Yêu cầu không được có:**
  * Không sử dụng tùy chọn `--abort` giữa chừng để trốn tránh giải quyết conflict.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_05/ex3/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` chi tiết các lần phát sinh conflict trong quá trình rebase và cách giải quyết cho từng chặng, kèm ảnh chụp `git log --graph --oneline` sau cùng.

#### Gợi ý/Bệ đỡ
1. Đứng ở `main`, tạo file `config.json` với nội dung ban đầu:
   ```json
   {
     "port": 8080,
     "debug": false
   }
   ```
   Commit: `git add config.json && git commit -m "init config"`.
2. Tạo nhánh `feature-api` từ `main`: `git checkout -b feature-api`.
3. Ở nhánh `feature-api`, sửa `"port": 9000` rồi commit `feat: change port`. Tiếp tục sửa tiếp `"debug": true` rồi commit `feat: enable debug`.
4. Quay lại `main`: `git checkout main`. Sửa `"port": 8081` rồi commit `update port on main`. Sửa tiếp `"env": "production"` rồi commit `add env config`.
5. Quay lại `feature-api`: `git checkout feature-api`. Tiến hành rebase lên `main`:
   ```bash
   git rebase main
   ```
6. Khi gặp conflict lần 1 ở file `config.json`, mở file ra sửa thủ công phần port, lưu lại, chạy `git add config.json` rồi tiếp tục:
   ```bash
   git rebase --continue
   ```
7. Lặp lại việc sửa conflict lần 2 nếu có cho commit tiếp theo cho đến khi rebase hoàn tất.

---

### EX4 — Mô phỏng quy trình Hotfix & Gitflow thực tế
- **tier:** guided
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_02, ss04_lesson_03]
- **owns_skills:** []
- **assumes:** [git-branching-conflicts, git-remote-github]

#### Mục tiêu
- Áp dụng mô hình phân nhánh Gitflow chuẩn trong quản lý vòng đời phần mềm.
- Thực hành tạo, kiểm thử và tích hợp nhánh Hotfix trực tiếp vào hệ thống đang chạy.
- Đồng bộ hóa bản vá nóng về nhánh phát triển (develop) để tránh trôi lỗi.

#### Yêu cầu
- **Bối cảnh:** Hệ thống đang chạy trên nhánh `main` (phiên bản stable `v1.0.0`) gặp lỗi nghiêm trọng lộ dữ liệu người dùng. Nhánh `develop` đang phát triển dở dang các tính năng mới cho phiên bản tương lai và không thể deploy ngay được.
- **Ràng buộc:** 
  * Tạo nhánh sửa lỗi khẩn cấp `hotfix/v1.0.1` tách ra trực tiếp từ `main`.
  * Sau khi sửa lỗi xong, gộp nhánh hotfix này vào `main`, tạo tag phiên bản `v1.0.1` để chuẩn bị release.
  * Bắt buộc phải gộp ngược lại nhánh hotfix này vào nhánh `develop` để đảm bảo code phát triển tương lai cũng được sửa lỗi này.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Kiểm tra các nhánh hiện có và danh sách tag:
    ```bash
    git branch -a
    git tag
    ```
  * Kiểm tra sơ đồ lịch sử gộp nhánh:
    ```bash
    git log --graph --oneline --all
    ```
- **Kết quả mong đợi:**
  * Có tag `v1.0.1` chỉ vào commit mới trên nhánh `main`. Lịch sử nhánh `develop` chứa commit sửa lỗi từ hotfix.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Nhánh `main` và `develop` đều chứa bản vá sửa lỗi.
  * Tag `v1.0.1` tồn tại trên Git.
- **Yêu cầu không được có:**
  * Tránh việc merge trực tiếp nhánh `develop` vào `main` tại thời điểm này vì sẽ làm lẫn các tính năng chưa hoàn thiện lên production.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_05/ex4/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` giải thích sơ đồ phân nhánh Gitflow đã sử dụng và vẽ lại sơ đồ merge bằng ASCII hoặc ảnh chụp màn hình đồ thị commit của repository.

#### Gợi ý/Bệ đỡ
1. Giả sử nhánh `main` giữ code production ổn định; nhánh `develop` giữ code đang phát triển. Khi cần sửa lỗi gấp, tách nhánh `hotfix/` từ `main`.
2. Sau khi fix xong trên `hotfix/v1.0.1`, chuyển về `main`: `git checkout main` -> `git merge hotfix/v1.0.1` -> `git tag -a v1.0.1 -m "Release Hotfix 1.0.1"`.
3. Cuối cùng, chuyển về `develop`: `git checkout develop` -> `git merge hotfix/v1.0.1`. Xóa nhánh hotfix cục bộ sau khi hoàn tất để dọn dẹp.

---

### EX5 — Kiểm tra chất lượng code tự động trước commit bằng Git Hooks
- **tier:** hints
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_04]
- **owns_skills:** []
- **assumes:** [git-local-basics]

#### Mục tiêu
- Tìm hiểu cơ chế hoạt động của Git Hooks cục bộ (local hooks).
- Viết và kích hoạt tệp tin script pre-commit hook.
- Tự động hóa việc quét mã nguồn để chặn các commit vi phạm chính sách bảo mật của dự án.

#### Yêu cầu
- **Bối cảnh:** Đội ngũ phát triển muốn thiết lập một cơ chế tự động bảo vệ cục bộ, không cho phép thành viên commit bất kỳ đoạn code nào có chứa từ khóa nhạy cảm `TODO` (chỉ định công việc chưa hoàn thành) hoặc chứa chuỗi `AWS_SECRET_ACCESS_KEY` (bí mật đám mây dễ bị lộ).
- **Ràng buộc:** 
  * Viết một file script bash/shell đặt tại `.git/hooks/pre-commit` (cần cấp quyền thực thi cho file này).
  * Khi lập trình viên chạy lệnh `git commit`, hook sẽ tự động quét các file trong Staging Area.
  * Nếu phát hiện bất kỳ file nào chứa các từ khóa trên, in ra thông báo lỗi chi tiết và chặn quá trình commit (trả về mã thoát non-zero). Nếu không phát hiện lỗi, cho phép commit bình thường.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Tạo file `test.txt` có chứa dòng chữ `TODO: need to fix this later` và thực hiện commit.
  * Tạo file `test.txt` không chứa từ khóa cấm và thực hiện commit.
- **Kết quả mong đợi:**
  * Trường hợp chứa từ khóa cấm: Lệnh `git commit` bị từ chối ngay lập tức và in ra thông báo cảnh báo lỗi trên màn hình.
  * Trường hợp sạch: Lệnh `git commit` diễn ra thành công.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Tệp script `pre-commit` hoạt động đúng logic yêu cầu.
  * Báo cáo kiểm thử chụp lại cả 2 tình huống (bị chặn và được cho phép commit).
- **Yêu cầu không được có:**
  * Script không được gây lỗi treo terminal hoặc chặn nhầm các commit hợp lệ khác.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_05/ex5/`
* **Cơ chế nộp:** Do thư mục `.git/` không được đẩy lên GitHub mặc định, học viên hãy copy nội dung file script `pre-commit` của mình lưu vào file `pre-commit.sh` đặt trong thư mục `homework/session_05/ex5/` kèm theo tệp hướng dẫn sử dụng và báo cáo kiểm thử `README.md`.

#### Gợi ý/Bệ đỡ
- Học viên cần tự tìm hiểu cách lấy danh sách các file đang staged (ví dụ sử dụng lệnh `git diff --cached --name-only`) và dùng lệnh `grep` hoặc các công cụ quét chuỗi tương tự trong shell script để kiểm tra nội dung file, sau đó dùng `exit 1` nếu muốn chặn commit và `exit 0` để cho phép đi tiếp.
- Đừng quên cấp quyền thực thi cho script trên Linux/macOS bằng lệnh: `chmod +x .git/hooks/pre-commit`.

---

### EX6 — Tự động hóa tìm kiếm commit gây lỗi bằng Git Bisect
- **tier:** independent
- **maps_to_sessions:** [4]
- **maps_to_lessons:** [ss04_lesson_04]
- **owns_skills:** []
- **assumes:** [git-local-basics, git-advanced-history]

#### Mục tiêu
- Vận dụng công cụ tìm kiếm nhị phân `git bisect` trên lịch sử dự án để tìm lỗi.
- Định vị chính xác và nhanh chóng commit đầu tiên làm phát sinh lỗi (bug) trong một chuỗi lịch sử commit dài.

#### Yêu cầu
- **Bối cảnh:** Sau một chuỗi 15 commit liên tiếp được đẩy lên dự án, ứng dụng đột ngột phát sinh lỗi (lỗi logic hoặc crash) tại một hàm chức năng. Học viên cần tìm ra chính xác commit nào là thủ phạm gây ra lỗi đó.
- **Ràng buộc:** Bắt buộc sử dụng tiến trình `git bisect` để tìm kiếm, không dò tay hay kiểm tra từng file thủ công.

#### Kiểm tra
- **Lệnh kiểm tra:**
  * Xem tiến trình tìm kiếm nhị phân của Git:
    ```bash
    git bisect log
    ```
- **Kết quả mong đợi:**
  * Git hiển thị thông báo chỉ mặt gọi tên chính xác commit đầu tiên gây lỗi: `<commit_hash> is the first bad commit`.

#### Tiêu chí chấm
- **Yêu cầu phải có:**
  * Log hoặc kết quả xuất của `git bisect` xác định chính xác commit hash gây lỗi.
  * Tệp `README.md` báo cáo giải thích các bước chạy test code ở mỗi chặng nhị phân.
- **Yêu cầu không được có:**
  * Không dùng các phương pháp thủ công không sử dụng lệnh `git bisect`.

#### Hướng dẫn nộp bài
* **Đường dẫn trên GitHub:** `homework/session_05/ex6/`
* **Cơ chế nộp:** Học viên nộp tệp báo cáo `README.md` mô tả tiến trình điều tra bằng `git bisect`, chỉ ra các commit được đánh giá là `good`/`bad` qua từng bước kiểm thử và mã băm commit lỗi cuối cùng tìm thấy.

#### Gợi ý/Bệ đỡ
- Không có hướng dẫn chi tiết. Học viên cần bắt đầu tiến trình bằng `git bisect start`, sau đó đánh dấu commit hiện tại là lỗi bằng `git bisect bad` và tìm về một commit cũ ổn định trong quá khứ đánh dấu `git bisect good <stable_commit_hash>`.
- Tiến hành chạy thử nghiệm ứng dụng ở mỗi bước do Git gợi ý, điền `git bisect good` hoặc `git bisect bad` tương ứng cho đến khi Git kết luận. Kết thúc tiến trình bằng `git bisect reset` để trả con trỏ HEAD về vị trí cũ.
