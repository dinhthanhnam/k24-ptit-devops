---
schema_version: 1
id: ss04_lesson_01
type: lesson
status: approved
course_id: devops-basic
session: 4
unit: 1
title: "Khởi tạo và thao tác cơ bản với Git (Local)"
session_kind: theory
tags:
  - git
  - source-control
  - local
concepts:
  - git-local-basics
depends_on: []
builds_on: []
enables:
  - ss04_lesson_02
owns:
  - git-local-basics
assumes: []
does_not_cover:
  - git-branching-conflicts
  - git-remote-github
  - git-advanced-history
source: generated
pm_ref: "Session 04 / Lesson 01"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
lesson_mode: practical
lesson_role: teach
estimated_minutes: 45
artifacts:
  - "Local Git Repository"
---

# Khởi tạo và thao tác cơ bản với Git (Local)

<!-- section: problem -->
## 1. Đặt vấn đề
Khi phát triển phần mềm, việc quản lý các phiên bản mã nguồn là cực kỳ quan trọng. Nếu không sử dụng các công cụ quản lý chuyên nghiệp, lập trình viên thường tự sao lưu thủ công bằng cách:
* Sao chép thư mục dự án và đặt tên theo kiểu: `project_v1`, `project_v2_final`, `project_v2_final_fixed`.
* Nén file zip gửi qua email, chat hoặc lưu trữ đám mây cá nhân.

Cách làm thủ công này gây ra hàng loạt vấn đề nghiêm trọng:
* **Hỗn loạn phiên bản:** Không biết phiên bản nào là mới nhất hoặc ổn định nhất.
* **Mất mát dữ liệu:** Rất khó khôi phục lại một dòng code cũ đã bị ghi đè cách đây vài tuần.
* **Mất dấu lịch sử:** Không biết ai đã thay đổi dòng code nào, thay đổi vào thời gian nào và vì lý do gì.

Để giải quyết triệt để vấn đề này, **Git** — một hệ thống quản lý phiên bản phân tán (Distributed Version Control System - DVCS) — đã được tạo ra và trở thành tiêu chuẩn công nghiệp toàn cầu.

<!-- section: core -->
## 2. Kiến thức cốt lõi

### 2.1. Git là gì?
Git là hệ thống quản lý phiên bản mã nguồn phân tán. "Phân tán" có nghĩa là mỗi máy tính của lập trình viên đều chứa một bản sao đầy đủ (Clone) của toàn bộ lịch sử commit, chứ không chỉ tải về phiên bản mới nhất từ máy chủ trung tâm. Điều này giúp lập trình viên có thể làm việc offline và thực hiện mọi thao tác (commit, xem lịch sử, phân nhánh) cực nhanh ngay trên máy local.

### 2.2. Mô hình 3 vùng làm việc của Git (Three-State Architecture)
Đây là kiến trúc cốt lõi giúp hiểu cách Git lưu trữ dữ liệu. Một dự án sử dụng Git sẽ có 3 vùng vật lý/logic:

1. **Working Directory (Thư mục làm việc):** Thư mục chứa các file mã nguồn hiện tại bạn đang trực tiếp chỉnh sửa trên đĩa cứng.
2. **Staging Area / Index (Vùng đệm):** Một file đóng vai trò vùng chuẩn bị chứa danh sách các thay đổi (thêm, sửa, xóa) bạn muốn đưa vào lịch sử trong lần commit tiếp theo.
3. **Git Directory / Repository (Thư mục lưu trữ Git):** Thư mục `.git` (ẩn), nơi Git lưu trữ toàn bộ cơ sở dữ liệu metadata và các snapshot lịch sử đã commit của dự án.

### 2.3. Vòng đời các trạng thái của file trong Git
Mỗi tệp tin trong thư mục dự án có Git sẽ nằm ở một trong bốn trạng thái chính:
* **Untracked (Chưa theo dõi):** File mới tạo, Git chưa hề biết đến sự tồn tại của nó.
* **Unmodified (Chưa chỉnh sửa):** File đã có trong commit trước và chưa có bất kỳ sửa đổi nào ở Working Directory.
* **Modified (Đã chỉnh sửa):** File đã được theo dõi nhưng có thay đổi mới chưa được đưa vào Staging Area.
* **Staged (Đã đưa vào vùng đệm):** File đã chỉnh sửa và đã được đánh dấu để chuẩn bị đưa vào commit tiếp theo.

<!-- section: steps -->
## 3. Các bước thực hành

### Bước 1 — Khởi tạo Git Repository
Tạo một thư mục dự án mới và biến nó thành một Git repository.

Mở Terminal và chạy các lệnh sau:
```bash
# Tạo thư mục dự án mới
mkdir git-practice
cd git-practice

# Khởi tạo repository local
git init
```

*Kết quả:* Terminal sẽ hiển thị dòng thông báo: `Initialized empty Git repository in /path/to/git-practice/.git/`. Thư mục ẩn `.git/` đã được tạo ra để quản lý dự án.

### Bước 2 — Cấu hình thông tin danh tính (Identity Config)
Trước khi ghi lại bất kỳ thay đổi nào, bạn phải khai báo tên và email của mình để Git ghi nhận ai là tác giả của các commit.

Chạy lệnh cấu hình phạm vi local (chỉ áp dụng cho dự án này):
```bash
git config user.name "Nguyen Van A"
git config user.email "anguyen@example.com"
```
*(Nếu muốn áp dụng cho tất cả các dự án trên máy cá nhân, thêm tham số `--global` vào sau config).*

Để kiểm tra lại cấu hình hiện tại:
```bash
git config --list
```

### Bước 3 — Tạo file mới và kiểm tra trạng thái (Status checking)
Tạo một file văn bản đơn giản và theo dõi cách Git nhận diện file mới.

Tạo file `README.md`:
```bash
echo "# Hoc Git Local" > README.md
```

Kiểm tra trạng thái dự án:
```bash
git status
```

*Kết quả:* Git sẽ báo file `README.md` đang ở trạng thái **Untracked files** (màu đỏ trên terminal) vì Git chưa được yêu cầu theo dõi file này.

### Bước 4 — Đưa file vào vùng đệm (Staging Area)
Yêu cầu Git đưa thay đổi của tệp tin vào vùng chuẩn bị trước khi commit.

Chạy lệnh:
```bash
git add README.md
```
*(Nếu muốn thêm toàn bộ các file mới hoặc có thay đổi trong thư mục hiện tại, dùng lệnh `git add .`)*

Kiểm tra lại trạng thái:
```bash
git status
```

*Kết quả:* File `README.md` chuyển sang màu xanh lá cây dưới mục **Changes to be committed**. Trạng thái của file lúc này là **Staged**.

### Bước 5 — Thực hiện Commit lưu snapshot
Ghi lại snapshot của các file trong Staging Area vào lịch sử Git Directory.

Chạy lệnh commit kèm thông điệp (message) mô tả ngắn gọn thay đổi:
```bash
git commit -m "Khoi tao du an va them file README.md"
```

*Kết quả:* Git hiển thị thông tin tóm tắt của commit bao gồm mã băm SHA-1 rút gọn, thông điệp commit và số lượng file thay đổi. File `README.md` lúc này đã chuyển sang trạng thái an toàn trong Git Directory. Nếu chạy `git status`, hệ thống sẽ báo `nothing to commit, working tree clean`.

### Bước 6 — Sửa đổi file, xem sự khác biệt và lịch sử commit
Thực hiện thay đổi nội dung file đã có, so sánh và kiểm tra lịch sử.

1. Sửa đổi nội dung file `README.md`:
   ```bash
   echo "Hoc các lenh Git co ban: init, status, add, commit, log." >> README.md
   ```
2. Xem sự khác biệt giữa Working Directory và Staging Area:
   ```bash
   git diff
   ```
   *Kết quả:* Terminal hiển thị các dòng thay đổi có dấu `+` màu xanh.
3. Đưa thay đổi mới vào Staging Area và commit:
   ```bash
   git add README.md
   git commit -m "Cap nhat noi dung huong dan cac lenh Git co ban"
   ```
4. Xem lịch sử các commit đã thực hiện:
   ```bash
   git log
   ```
   *Kết quả:* Hiển thị danh sách các commit gồm mã hash SHA-1 đầy đủ, tác giả, ngày giờ thực hiện và thông điệp commit.

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
* **Chưa cấu hình tên/email:** Nếu bạn chạy `git commit` lần đầu tiên trên một máy tính mới mà chưa chạy lệnh `git config`, Git sẽ báo lỗi và ngăn chặn hành động commit.
* **Sửa đổi file sau khi `git add` nhưng quên chạy lại `git add` trước khi commit:**
  Nếu bạn `git add file.txt`, sau đó mở file ra sửa tiếp rồi chạy thẳng `git commit`, thì chỉ có phần thay đổi *trước khi* chạy lệnh `git add` được lưu vào commit mới. Những thay đổi sau đó vẫn nằm ở Working Directory dưới dạng Modified.
* **Commit message quá chung chung:** Viết message như `fix`, `update`, `code` sẽ làm lịch sử commit trở nên vô dụng khi cần tìm kiếm hoặc khôi phục mã nguồn cũ. Hãy viết tin nhắn ngắn gọn nhưng mô tả rõ mục đích thay đổi (ví dụ: `git commit -m "Them trang 404 tuy bien cho website"`).

<!-- section: references -->
## 5. Tài liệu tham khảo
* [Sách Pro Git - Chương 1 & Chươg 2 (Bản dịch tiếng Việt)](https://git-scm.com/book/vi/v2)
* [Atlassian Git Tutorials: Git Init & Git Add](https://www.atlassian.com/git/tutorials/saving-changes)
