---
schema_version: 1
id: ss04_lesson_02
type: lesson
status: approved
course_id: devops-basic
session: 4
unit: 2
title: "Quản lý Nhánh (Branching) và xử lý Xung đột"
session_kind: theory
tags:
  - git
  - branching
  - merge-conflicts
concepts:
  - git-branching-conflicts
depends_on:
  - ss04_lesson_01
builds_on: []
enables:
  - ss04_lesson_03
owns:
  - git-branching-conflicts
assumes:
  - git-local-basics
does_not_cover:
  - git-remote-github
  - git-advanced-history
source: generated
pm_ref: "Session 04 / Lesson 02"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
lesson_mode: practical
lesson_role: teach
estimated_minutes: 45
artifacts:
  - "Git Branching Structure"
---

# Quản lý Nhánh (Branching) và xử lý Xung đột

<!-- section: problem -->
## 1. Đặt vấn đề
Trong quá trình làm việc thực tế, nếu toàn bộ thành viên trong nhóm phát triển hoặc thậm chí một lập trình viên làm việc độc lập chỉ commit trực tiếp lên một nhánh duy nhất (như nhánh chính `main` hoặc `master`), hệ thống sẽ gặp các rủi ro lớn:
* **Ảnh hưởng đến mã nguồn đang chạy ổn định (Production):** Một đoạn code lỗi mới commit lên có thể làm hỏng toàn bộ ứng dụng đang hoạt động bình thường của khách hàng.
* **Cản trở làm việc song song:** Các lập trình viên không thể phát triển các tính năng khác nhau một cách độc lập mà không can thiệp hoặc ghi đè lên công việc của nhau.
* **Khó khăn khi thử nghiệm:** Khi muốn thử nghiệm một giải pháp công nghệ mới, lập trình viên không có môi trường cô lập an toàn để tự do thử nghiệm.

Bên cạnh đó, khi gộp các phần mã nguồn được phát triển song song lại với nhau, nếu hai người cùng sửa đổi một dòng code trên cùng một file, Git sẽ không thể tự đưa ra quyết định dòng code của ai là chính xác. Git sẽ báo lỗi **Merge Conflict (Xung đột gộp)** và dừng quá trình gộp để yêu cầu lập trình viên can thiệp xử lý.

Để giải quyết vấn đề này, cơ chế **Nhánh (Branching)** và kỹ năng **xử lý Xung đột (Conflict Resolution)** ra đời.

<!-- section: core -->
## 2. Kiến thức cốt lõi

### 2.1. Nhánh (Branch) trong Git là gì?
Trong Git, nhánh không phải là một thư mục riêng biệt sao chép code ra, mà bản chất thực sự của một nhánh chỉ là một **con trỏ di động (movable pointer)** trỏ đến một commit cụ thể trong lịch sử.
* Nhánh mặc định khi khởi tạo dự án thường là `main` (hoặc `master`).
* Mỗi khi bạn tạo một commit mới, con trỏ của nhánh hiện tại sẽ tự động di chuyển tiến lên phía trước để trỏ vào commit mới nhất đó.
* Con trỏ **HEAD** là một con trỏ đặc biệt của Git dùng để xác định bạn đang trực tiếp đứng làm việc ở nhánh nào.

### 2.2. Hai cơ chế gộp nhánh (Merge) phổ biến
Khi gộp nhánh phụ (ví dụ `feature`) vào nhánh chính (`main`), Git sử dụng hai cơ chế gộp chính tùy thuộc vào lịch sử commit:

1. **Fast-forward Merge:**
   * **Điều kiện:** Nhánh chính `main` không phát sinh thêm commit mới nào kể từ khi nhánh `feature` được tách ra.
   * **Cách hoạt động:** Git không cần tạo commit gộp mới, mà chỉ đơn giản là dời con trỏ của nhánh `main` tiến thẳng về phía trước để trỏ vào commit mới nhất của nhánh `feature`.
2. **3-Way Merge (Recursive Merge):**
   * **Điều kiện:** Nhánh chính `main` đã phát sinh thêm các commit mới song song với các commit của nhánh `feature`.
   * **Cách hoạt động:** Git sẽ tìm commit tổ tiên chung gần nhất (Common Ancestor) của cả hai nhánh, sau đó tạo một commit gộp mới (Merge Commit) kết hợp mã nguồn của cả hai nhánh lại với nhau.

### 2.3. Merge Conflict (Xung đột gộp) là gì?
Xung đột xảy ra khi Git cố gắng tự động gộp (3-way merge) nhưng phát hiện ra có sự thay đổi chồng chéo trên cùng một dòng của cùng một tệp tin ở cả hai nhánh. Khi đó, Git sẽ đánh dấu xung đột trực tiếp vào file bằng các ký tự đặc biệt:
```html
<<<<<<< HEAD
Mã nguồn hiện tại trên nhánh bạn đang đứng (HEAD)
=======
Mã nguồn từ nhánh bạn đang gộp vào
>>>>>>> tên_nhánh_phụ
```
Lập trình viên bắt buộc phải mở file, thảo luận với đồng nghiệp (nếu làm nhóm), lựa chọn đoạn code chính xác cần giữ lại, xóa các ký tự đánh dấu của Git, sau đó add và commit để hoàn tất quá trình gộp.

<!-- section: steps -->
## 3. Các bước thực hành

### Bước 1 — Kiểm tra và Tạo nhánh mới
Kiểm tra danh sách nhánh hiện có và tạo một nhánh tính năng mới tên là `feature-login`.

1. Kiểm tra danh sách các nhánh local:
   ```bash
   git branch
   ```
   *(Nhánh có dấu sao `*` và hiển thị màu xanh là nhánh bạn đang đứng làm việc).*
2. Tạo một nhánh mới:
   ```bash
   git branch feature-login
   ```
3. Chuyển sang nhánh mới vừa tạo:
   ```bash
   git checkout feature-login
   ```
   *(Mẹo nhanh: Bạn có thể gộp hai lệnh tạo và chuyển nhánh bằng một lệnh duy nhất: `git checkout -b feature-login` hoặc `git switch -c feature-login`).*

### Bước 2 — Thực hiện Commit trên nhánh mới
Tạo sự thay đổi mã nguồn trên nhánh `feature-login` để kiểm tra tính cô lập.

1. Tạo file `login.html`:
   ```bash
   echo "<h3>Giao dien dang nhap</h3>" > login.html
   ```
2. Đưa vào Staging Area và thực hiện commit:
   ```bash
   git add login.html
   git commit -m "Them file login.html tren nhanh feature-login"
   ```
3. Quay lại nhánh chính `main`:
   ```bash
   git checkout main
   ```
4. Kiểm tra thư mục dự án: File `login.html` hoàn toàn biến mất ở nhánh `main` vì các thay đổi trên nhánh `feature-login` được cô lập hoàn toàn.

### Bước 3 — Thực hiện Fast-forward Merge
Tiến hành gộp nhánh `feature-login` vào nhánh `main` khi nhánh `main` chưa có thay đổi nào mới.

Đang đứng ở nhánh `main`, chạy lệnh gộp nhánh:
```bash
git merge feature-login
```

*Kết quả:* Terminal hiển thị dòng chữ `Updating ... Fast-forward`. Con trỏ nhánh `main` đã được dời tiến thẳng lên bằng con trỏ nhánh `feature-login`. File `login.html` xuất hiện an toàn trong thư mục của nhánh `main`.

### Bước 4 — Tạo kịch bản xung đột (Merge Conflict Setup)
Tạo hai nhánh cùng chỉnh sửa một dòng trong file `login.html` để kích hoạt xung đột.

1. Tạo một nhánh mới tên là `feature-facebook`:
   ```bash
   git checkout -b feature-facebook
   ```
2. Sửa nội dung file `login.html` thành:
   ```html
   <h3>Giao dien dang nhap bang Facebook</h3>
   ```
3. Commit thay đổi:
   ```bash
   git add login.html
   git commit -m "Cau hinh dang nhap bang Facebook"
   ```
4. Quay trở về nhánh `main`:
   ```bash
   git checkout main
   ```
5. Sửa nội dung file `login.html` trên nhánh `main` thành một dòng khác:
   ```html
   <h3>Giao dien dang nhap bang Google</h3>
   ```
6. Commit thay đổi trên nhánh `main`:
   ```bash
   git add login.html
   git commit -m "Cau hinh dang nhap bang Google"
   ```

Lúc này, cả hai nhánh `main` và `feature-facebook` đều có commit mới kể từ điểm tách nhánh, và cả hai đều sửa đổi dòng số 1 trong file `login.html`.

### Bước 5 — Tiến hành Merge và Nhận diện Conflict
Gộp nhánh phụ vào nhánh chính và quan sát thông báo lỗi xung đột của Git.

Đang đứng ở nhánh `main`, chạy lệnh gộp nhánh `feature-facebook` vào:
```bash
git merge feature-facebook
```

*Kết quả:* Git hiển thị thông báo lỗi:
```text
CONFLICT (content): Merge conflict in login.html
Automatic merge failed; fix conflicts and then commit the result.
```
Nếu chạy lệnh `git status`, bạn sẽ thấy file `login.html` nằm dưới mục **Both modified**.

### Bước 6 — Giải quyết xung đột thủ công (Conflict Resolution)
Mở tệp tin bị xung đột, chỉnh sửa nội dung và kết thúc quá trình gộp.

1. Mở file `login.html` bằng trình soạn thảo (ví dụ: VS Code hoặc Nano). Nội dung file hiển thị dạng:
   ```html
   <<<<<<< HEAD
   <h3>Giao dien dang nhap bang Google</h3>
   =======
   <h3>Giao dien dang nhap bang Facebook</h3>
   >>>>>>> feature-facebook
   ```
2. Hãy xóa toàn bộ các ký hiệu đánh dấu (`<<<<<<< HEAD`, `=======`, `>>>>>>> feature-facebook`) và chỉnh sửa dòng code thành phiên bản mong muốn cuối cùng. Ví dụ giữ lại cả hai hoặc gộp chung:
   ```html
   <h3>Giao dien dang nhap bang Google hoac Facebook</h3>
   ```
3. Lưu file lại.
4. Đánh dấu file đã giải quyết xung đột bằng lệnh:
   ```bash
   git add login.html
   ```
5. Hoàn tất commit merge:
   ```bash
   git commit -m "Merge branch feature-facebook and resolve conflict in login.html"
   ```
6. Kiểm tra lại lịch sử commit đồ họa:
   ```bash
   git log --graph --oneline
   ```
   *Kết quả:* Biểu đồ hiển thị luồng nhánh tách ra và nhập lại thành công.

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
* **Xóa nhầm các ký tự đánh dấu xung đột mà không sửa code:** Nếu lập trình viên để nguyên các ký hiệu `<<<<<<<`, `=======` và `>>>>>>>` rồi commit, các ký tự này sẽ trở thành một phần của mã nguồn và gây lỗi cú pháp/giao diện khi chạy ứng dụng.
* **Hoảng loạn và xóa thư mục dự án khi gặp Conflict:** Merge conflict là hiện tượng hết sức bình thường khi làm việc nhóm. Nếu muốn hủy bỏ hoàn toàn lệnh merge đang lỗi và quay về trạng thái sạch sẽ trước khi chạy lệnh merge, chỉ cần gõ lệnh:
  ```bash
  git merge --abort
  ```
* **Quên chạy lệnh commit sau khi `git add`:** Sau khi sửa xong file bị conflict và chạy `git add`, quá trình merge vẫn chưa kết thúc cho đến khi bạn thực thi lệnh `git commit`.

<!-- section: references -->
## 5. Tài liệu tham khảo
* [Sách Pro Git - Chương 3: Nhánh trong Git (Branching)](https://git-scm.com/book/vi/v2/Nnh-trong-Git-C-Bản-Về-Phn-Nhnh-V-Gộp-Nhnh)
* [Atlassian Git Tutorials: Using Branches & Resolving Merge Conflicts](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts)
