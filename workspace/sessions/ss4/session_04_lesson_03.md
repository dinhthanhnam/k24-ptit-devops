---
schema_version: 1
id: ss04_lesson_03
type: lesson
status: approved
course_id: devops-basic
session: 4
unit: 3
title: Làm việc Từ xa với GitHub và quy trình Teamwork
session_kind: theory
tags: []
concepts: &id001
- git-remote-github
depends_on: []
builds_on: []
enables: []
owns: *id001
assumes:
- git-branching-conflicts
does_not_cover: []
source: generated
pm_ref: Session 04 / Lesson 03
language: vi
created: '2026-07-17'
updated: '2026-07-17'
lesson_mode: practical
---

# Làm việc Từ xa với GitHub và quy trình Teamwork

<!-- section: problem -->
## 1. Đặt vấn đề
Khi làm việc trên máy tính cá nhân (local), dự án của bạn luôn đối mặt với các rủi ro lớn:
* **Hỏng hóc thiết bị:** Nếu ổ cứng máy tính bị hỏng, toàn bộ mã nguồn và lịch sử commit của bạn sẽ biến mất hoàn toàn.
* **Cản trở cộng tác:** Việc gửi mã nguồn cho đồng nghiệp qua email, Zalo, hay USB rất cồng kềnh, dễ nhầm lẫn và không thể gộp các thay đổi của mọi người theo thời gian thực.

Để làm việc nhóm và bảo vệ mã nguồn, chúng ta cần một máy chủ lưu trữ Git từ xa (Remote Repository), phổ biến nhất là **GitHub**. Tuy nhiên, để bảo vệ tài khoản người dùng, kể từ tháng 8/2021, GitHub đã chính thức khai tử phương thức xác thực bằng mật khẩu tài khoản thông thường (HTTPS Password) khi thao tác qua Git CLI. 

Nếu học viên cố gắng kết nối qua HTTPS bằng mật khẩu, Git sẽ báo lỗi từ chối truy cập. Do đó, việc thiết lập phương thức xác thực an toàn không dùng mật khẩu thông qua **SSH Key** là bắt buộc đối với mọi kỹ sư DevOps để làm việc với GitHub.

<!-- section: core -->
## 2. Kiến thức cốt lõi

### 2.1. Remote Repository (Kho lưu trữ từ xa)
Remote Repository là phiên bản dự án của bạn được lưu trữ trên một máy chủ kết nối internet (như GitHub, GitLab, Bitbucket). Nó giúp đồng bộ hóa các commit từ máy local lên đám mây và chia sẻ mã nguồn với các thành viên khác trong nhóm.

### 2.2. Cơ chế xác thực qua SSH Key
SSH (Secure Shell) Key là một phương thức xác thực mã hóa cực kỳ an toàn, cho phép bạn kết nối máy tính của mình với GitHub mà không cần nhập tên đăng nhập và mật khẩu mỗi lần đẩy code. Cơ chế này dựa trên một cặp khóa:
* **Private Key (Khóa riêng tư):** Lưu trữ bí mật tại máy tính cá nhân của bạn (thư mục `~/.ssh/id_ed25519`). **Tuyệt đối không được chia sẻ file này cho bất kỳ ai.**
* **Public Key (Khóa công khai):** Tải lên và cấu hình trên tài khoản GitHub của bạn. Bất kỳ ai cũng có thể nhìn thấy khóa này nhưng không thể dùng nó để giải mã ngược lại khóa riêng tư.

Khi bạn thực hiện thao tác Git kết nối đến GitHub, máy tính sẽ dùng Private Key để ký nhận diện, GitHub dùng Public Key đã cấu hình để đối chiếu xác thực.

### 2.3. Các lệnh tương tác với Remote chính
* `git remote add <name> <url>`: Thiết lập liên kết giữa repository local với repository remote. Tên remote mặc định thường là `origin`.
* `git push`: Đẩy các commit mới từ nhánh local lên nhánh tương ứng trên remote repository.
* `git fetch`: Tải về các thông tin commit mới nhất từ remote repository về máy local nhưng chưa tiến hành gộp (merge) vào code của bạn.
* `git pull`: Tải về các commit mới nhất và tự động thực hiện gộp (merge) vào nhánh hiện hành ở local (Lưu ý: `git pull` = `git fetch` + `git merge`).
* `git clone <url>`: Sao chép toàn bộ mã nguồn và lịch sử commit của một remote repository về máy local lần đầu tiên.

<!-- section: steps -->
## 3. Các bước thực hành

### Bước 1 — Kiểm tra và tạo mới cặp khóa SSH (SSH Keypair)
Kiểm tra xem máy tính cá nhân đã có sẵn khóa SSH chưa, nếu chưa tiến hành sinh khóa mới.

1. Kiểm tra các khóa hiện có:
   ```bash
   ls -la ~/.ssh
   ```
   *(Nếu bạn thấy các tệp tin như `id_ed25519` và `id_ed25519.pub`, có nghĩa là bạn đã có khóa SSH. Hãy bỏ qua bước tạo mới và dùng luôn khóa đó).*
2. Nếu chưa có khóa, tiến hành tạo mới bằng thuật toán bảo mật Ed25519:
   ```bash
   ssh-keygen -t ed25519 -C "email_cua_ban@example.com"
   ```
   *Khi hệ thống hỏi nơi lưu và mật khẩu (passphrase), hãy nhấn **Enter** liên tiếp 3 lần để chọn mặc định và không cài mật khẩu.*

### Bước 2 — Sao chép Public Key và cấu hình lên GitHub
Đưa khóa công khai lên tài khoản GitHub để máy chủ nhận diện máy local của bạn.

1. Hiển thị nội dung của khóa công khai (Public Key):
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
2. Bôi đen và sao chép toàn bộ nội dung hiển thị (dòng chữ bắt đầu bằng `ssh-ed25519 ...` cho đến hết email của bạn).
3. Đăng nhập vào [GitHub](https://github.com), truy cập vào **Settings** (ở góc phải trên cùng) -> **SSH and GPG keys** -> chọn **New SSH Key**.
4. Nhập tiêu đề tùy chọn (ví dụ: `My Laptop`) và dán toàn bộ nội dung khóa công khai đã copy vào ô **Key**, sau đó nhấn **Add SSH Key**.

### Bước 3 — Kiểm tra kết nối SSH tới GitHub
Xác nhận rằng máy tính local của bạn đã có thể nói chuyện và xác thực thành công với GitHub.

Chạy lệnh kiểm tra kết nối từ Terminal:
```bash
ssh -T git@github.com
```

*Kết quả:* Terminal sẽ hỏi bạn có muốn tin tưởng máy chủ GitHub hay không, gõ `yes` và nhấn Enter. Tiếp theo, terminal hiển thị thông điệp chào mừng:
`Hi username! You've successfully authenticated, but GitHub does not provide shell access.`
Có nghĩa là bạn đã cấu hình SSH thành công!

### Bước 4 — Tạo Repository trống trên GitHub
Tạo nơi chứa dự án trên đám mây để chuẩn bị liên kết.

1. Truy cập trang chủ GitHub, nhấn nút **New** (hoặc nút **Create repository**).
2. Đặt tên kho chứa (ví dụ: `git-practice-remote`).
3. Chọn chế độ hiển thị là **Public** hoặc **Private**.
4. **Lưu ý quan trọng:** Không tích chọn bất kỳ mục nào như *Add a README file*, *Add .gitignore* hay *Choose a license* để tránh tạo ra commit ban đầu gây lệch nhánh.
5. Nhấn **Create repository**.
6. Tại giao diện hiển thị, chọn tab **SSH** (không chọn HTTPS) và sao chép đường dẫn repository có dạng: `git@github.com:username/git-practice-remote.git`.

### Bước 5 — Liên kết Local Repository với GitHub
Khai báo đường dẫn remote cho dự án local mà chúng ta đã làm việc ở bài trước.

Mở thư mục dự án `git-practice` ở local trên Terminal và chạy lệnh:
```bash
git remote add origin git@github.com:username/git-practice-remote.git
```
*(Thay thế `git@github.com:username/git-practice-remote.git` bằng đường dẫn SSH repository bạn vừa copy ở Bước 4).*

Để kiểm tra xem liên kết đã được thiết lập chính xác hay chưa:
```bash
git remote -v
```

### Bước 6 — Đẩy mã nguồn lên GitHub (Git Push)
Thực hiện đẩy toàn bộ lịch sử commit local lên repository remote.

Chạy lệnh đẩy nhánh `main` lên remote:
```bash
git push -u origin main
```
*(Tham số `-u` giúp thiết lập luồng theo dõi (upstream tracking) giữa nhánh main ở local và main ở remote. Trong các lần tiếp theo, bạn chỉ cần gõ đơn giản `git push` hoặc `git pull`).*

F5 lại trang GitHub của bạn, bạn sẽ thấy toàn bộ các tệp tin và lịch sử commit ở local đã được đồng bộ lên giao diện web của GitHub.

### Bước 7 — Giả lập Clone và đồng bộ hóa (Git Pull)
Giả lập việc một thành viên khác tải code về máy và cập nhật dữ liệu.

1. Di chuyển ra khỏi thư mục dự án hiện tại và thực hiện clone dự án về một thư mục mới có tên là `git-practice-member`:
   ```bash
   cd ..
   git clone git@github.com:username/git-practice-remote.git git-practice-member
   ```
2. Vào thư mục mới và tạo thay đổi giả lập:
   ```bash
   cd git-practice-member
   echo "Dong gop tu thanh vien nhom" >> README.md
   git add README.md
   git commit -m "Thanh vien cap nhat README"
   git push
   ```
3. Quay lại thư mục dự án ban đầu của bạn và kéo thay đổi mới về để đồng bộ:
   ```bash
   cd ../git-practice
   git pull
   ```
   *Kết quả:* Kiểm tra file `README.md` của bạn, dòng chữ đóng góp của thành viên đã được đồng bộ về máy local của bạn một cách nhanh chóng.

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
* **Sử dụng link HTTPS dẫn đến lỗi xác thực:** Khi chạy lệnh `git remote add origin`, nếu học viên copy nhầm link HTTPS thay vì link SSH, Git sẽ liên tục yêu cầu nhập Username/Password của GitHub trên CLI khi push/pull, và sau đó báo lỗi authentication do cơ chế nhập pass trực tiếp đã bị ngừng hỗ trợ.
* **Upload nhầm khóa riêng tư (Private Key) lên GitHub:** Lập trình viên hay bị nhầm lẫn giữa hai tệp tin `id_ed25519` (Private Key) và `id_ed25519.pub` (Public Key), sau đó upload nhầm Private Key lên GitHub Console. Việc này không giúp kết nối hoạt động mà còn gây rò rỉ khóa bảo mật nghiêm trọng. Chỉ có khóa công khai `.pub` mới được tải lên GitHub.
* **Xảy ra lỗi Non-Fast-Forward khi push:** Nếu remote repository đã có những commit mới của người khác mà bạn chưa đồng bộ về máy local, lệnh `git push` sẽ bị từ chối. Học viên bắt buộc phải chạy `git pull` để gộp các thay đổi mới nhất về máy local (và xử lý xung đột nếu có) trước khi thực hiện push lại.

<!-- section: references -->
## 5. Tài liệu tham khảo
* [GitHub Docs: Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
* [Sách Pro Git - Chương 2.5: Làm việc với các Kho Chứa Từ Xa (Remotes)](https://git-scm.com/book/vi/v2/Git-C%C4%83n-B%E1%BA%A3n-L%C3%A0m-Vi%E1%BB%87c-v%E1%BB%9Bi-c%C3%A1c-Kho-Ch%E1%BB%A9a-T%E1%BB%AB-Xa)
* [GitHub Blog: Token authentication requirements for Git operations](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)

