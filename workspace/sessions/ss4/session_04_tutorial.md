---
schema_version: 1
id: ss04_tutorial
type: tutorial
status: approved
course_id: devops-basic
session: 4
unit: 0
title: 'Lab: Đưa dự án đầu tiên lên GitHub'
session_kind: theory
tags:
- tutorial
- step-by-step
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
pm_ref: Session 04 / tutorial
language: vi
created: '2026-07-17'
updated: '2026-07-17'
step_count: 6
maps_to:
- ss04_lesson_01
- ss04_lesson_02
- ss04_lesson_03
- ss04_lesson_04
image_policy: placeholder
---

# Lab: Đưa dự án đầu tiên lên GitHub

<!-- section: overview -->
## 0. Tổng quan lab
* **Mục tiêu hoàn thành:** Xây dựng một trang web HTML giới thiệu cá nhân đơn giản ở máy local, khởi tạo Git để quản lý phiên bản, tạo khóa SSH Key an toàn để liên kết với tài khoản GitHub và thực hiện đẩy (push) dự án lên đám mây GitHub.
* **Thời lượng ước tính:** 25 phút.
* **Ánh xạ lessons/sessions:** `ss04_lesson_01`, `ss04_lesson_02`, `ss04_lesson_03`, `ss04_lesson_04`.
* **Môi trường / prerequisites:** Máy tính cá nhân chạy hệ điều hành Windows, macOS hoặc Linux đã cài đặt sẵn Git CLI, và trình duyệt web có tài khoản GitHub cá nhân hoạt động.

<!-- section: prerequisites -->
## 1. Chuẩn bị
Trước khi thực hành, hãy đảm bảo bạn đã hoàn thành các bước chuẩn bị sau:
- [ ] Mở Terminal/Git Bash và kiểm tra Git đã được cài đặt thành công:
  ```bash
  git --version
  ```
  *(Phải hiển thị phiên bản Git đã cài đặt, ví dụ: `git version 2.45.0`).*
- [ ] Có tài khoản đăng nhập đang hoạt động trên trang web [GitHub](https://github.com).
- [ ] Một trình soạn thảo mã nguồn gọn nhẹ (khuyên dùng VS Code) để chỉnh sửa file.

<!-- section: step_01 -->
## Step 1: Khởi tạo dự án local và commit đầu tiên
**Mục tiêu step:** Tạo cấu trúc dự án HTML cơ bản tại máy local và khởi tạo Git repository để quản lý lịch sử.

**Thao tác:**
1. Tạo một thư mục dự án mới tên là `my-profile` trên máy tính và di chuyển vào thư mục đó:
   ```bash
   mkdir my-profile
   cd my-profile
   ```
2. Tạo một file `index.html` chứa nội dung giới thiệu bản thân đơn giản:
   ```bash
   echo "<h1>Xin chao, toi la Hoc Vien DevOps!</h1>" > index.html
   ```
3. Kiểm tra xem máy tính cá nhân của bạn đã cấu hình danh tính Git chưa bằng lệnh:
   ```bash
   git config --global user.name
   git config --global user.email
   ```
   *(Nếu terminal đã in ra tên và email thật của bạn, hãy chuyển ngay sang bước 4. Nếu chưa có thông tin, tiến hành thiết lập bằng tên và email của bạn):*
   ```bash
   git config --global user.name "Ten Cua Ban"
   git config --global user.email "email_cua_ban@example.com"
   ```
4. Khởi tạo kho chứa Git local, thêm file `index.html` vào Staging Area và tạo commit đầu tiên:
   ```bash
   git init
   git add index.html
   git commit -m "Commit khoi tao: Them file index.html"
   ```

**Kết quả mong đợi / kiểm tra:**
Chạy lệnh `git status` và `git log --oneline`. Hệ thống hiển thị thông báo `nothing to commit, working tree clean` và hiển thị lịch sử có đúng 1 commit đầu tiên.

<!-- section: step_02 -->
## Step 2: Khởi tạo cặp khóa SSH (SSH Keypair)
**Mục tiêu step:** Sinh cặp khóa mã hóa SSH tại máy local để làm cơ sở đăng nhập tự động vào GitHub.

**Thao tác:**
1. Sinh khóa SSH mới bằng thuật toán mã hóa hiện đại Ed25519 (thay thế bằng địa chỉ email đăng ký tài khoản GitHub của bạn):
   ```bash
   ssh-keygen -t ed25519 -C "email_github_cua_ban@example.com"
   ```
2. Khi terminal hỏi `Enter file in which to save the key...`, nhấn **Enter** để chọn đường dẫn mặc định.
3. Khi terminal hỏi `Enter passphrase...`, tiếp tục nhấn **Enter** liên tiếp 2 lần để không thiết lập mật khẩu bảo vệ khóa (giúp thao tác tự động hóa sau này nhanh hơn).
4. Kiểm tra sự tồn tại của khóa riêng tư và khóa công khai vừa sinh ra:
   ```bash
   ls -la ~/.ssh
   ```

**Kết quả mong đợi / kiểm tra:**
Trong thư mục `~/.ssh/` xuất hiện hai tệp tin mới:
* `id_ed25519` (Khóa riêng tư - Private Key)
* `id_ed25519.pub` (Khóa công khai - Public Key)

> **[IMAGE NEEDED]** Minh họa kết quả terminal sau khi chạy lệnh tạo khóa ssh-keygen thành công.
> Gợi ý path: `assets/ss04/step_02_ssh_keygen_output.png`

<!-- section: step_03 -->
## Step 3: Đăng ký khóa công khai lên GitHub và kiểm tra kết nối
**Mục tiêu step:** Liên kết khóa công khai (Public Key) local với tài khoản GitHub và xác thực đường truyền bảo mật.

**Thao tác:**
1. In nội dung của khóa công khai ra terminal để sao chép:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
2. Dùng chuột bôi đen toàn bộ nội dung hiển thị (bắt đầu bằng `ssh-ed25519` cho đến hết địa chỉ email) và sao chép.
3. Mở trình duyệt, đăng nhập vào GitHub, click vào ảnh đại diện ở góc phải trên cùng và chọn **Settings**.
4. Tại menu bên trái, tìm mục **SSH and GPG keys**, nhấn nút **New SSH key** màu xanh.
5. Đặt tên gợi nhớ tại mục **Title** (ví dụ: `My DevOps Machine`), chọn loại key là `Authentication Key` và dán (paste) nội dung đã copy ở bước 1 vào ô **Key**. Nhấn **Add SSH key**.
6. Quay lại terminal local để kiểm tra xác thực bằng lệnh kết nối:
   ```bash
   ssh -T git@github.com
   ```
7. Nếu terminal hiển thị câu hỏi `Are you sure you want to continue connecting (yes/no/[fingerprint])?`, gõ `yes` và nhấn Enter.

**Kết quả mong đợi / kiểm tra:**
Terminal phản hồi lời chào mừng thành công từ GitHub:
`Hi username! You've successfully authenticated, but GitHub does not provide shell access.`

> **[IMAGE NEEDED]** Giao diện thêm SSH Key mới trên trang cài đặt của GitHub.
> Gợi ý path: `assets/ss04/step_03_github_ssh_key_settings.png`

<!-- section: step_04 -->
## Step 4: Tạo một kho chứa trống (Repository) trên GitHub
**Mục tiêu step:** Tạo một không gian lưu trữ dự án tương ứng trên đám mây GitHub.

**Thao tác:**
1. Truy cập vào trang chủ [GitHub](https://github.com), nhấn nút **New** ở góc trái màn hình (hoặc truy cập nhanh qua đường dẫn `https://github.com/new`).
2. Điền tên kho chứa tại ô **Repository name**: `my-profile`.
3. Chọn chế độ hiển thị là **Public** (hoặc **Private** tùy chọn).
4. **Lưu ý cực kỳ quan trọng:** Không tích chọn vào các mục *Add a README file*, *Add .gitignore*, hoặc *Choose a license*. Chúng ta cần một repository hoàn toàn trống rỗng để tránh lệch lịch sử commit với local.
5. Nhấn nút **Create repository** ở cuối trang.
6. Tại trang giao diện tiếp theo hiện ra, chọn tab **SSH** (không chọn HTTPS) và sao chép địa chỉ repository có dạng: `git@github.com:username/my-profile.git`.

**Kết quả mong đợi / kiểm tra:**
Tạo thành công repository và nhận được dòng địa chỉ kết nối dạng SSH của repo đó để chuẩn bị liên kết.

> **[IMAGE NEEDED]** Giao diện trang khởi tạo repository trống trên GitHub, làm nổi bật việc không chọn README/gitignore.
> Gợi ý path: `assets/ss04/step_04_create_empty_repo.png`

<!-- section: step_05 -->
## Step 5: Kết nối local repository với GitHub và thực hiện push code
**Mục tiêu step:** Liên kết thư mục dự án local của bạn với repository trên GitHub và đẩy dữ liệu lên đám mây.

**Thao tác:**
1. Đứng tại thư mục dự án `my-profile` ở local trên Terminal, chạy lệnh liên kết remote (thay thế địa chỉ URL SSH bằng địa chỉ của bạn đã copy ở Step 4):
   ```bash
   git remote add origin git@github.com:username/my-profile.git
   ```
2. Đổi tên nhánh mặc định hiện tại của bạn thành nhánh `main` (nếu nhánh hiện tại đang là `master`):
   ```bash
   git branch -M main
   ```
3. Đẩy (push) mã nguồn từ local lên remote repository và thiết lập luồng theo dõi mặc định:
   ```bash
   git push -u origin main
   ```

**Kết quả mong đợi / kiểm tra:**
Terminal sẽ hiển thị tiến trình đẩy code và thông báo hoàn tất kết nối:
`Branch 'main' set up to track remote branch 'main' from 'origin'.`
Chạy lệnh `git remote -v` hiển thị đúng 2 dòng cấu hình trỏ tới link SSH của GitHub.

<!-- section: step_06 -->
## Step 6: Kiểm tra kết quả trực quan trên website GitHub
**Mục tiêu step:** Xem kết quả hiển thị trực quan của mã nguồn và lịch sử commit của dự án trực tuyến trên đám mây.

**Thao tác:**
1. Quay lại trình duyệt web và tải lại (F5) trang repository GitHub `my-profile` của bạn.
2. Kiểm tra xem file `index.html` đã xuất hiện trong danh sách tệp tin của repository chưa.
3. Nhấp chuột vào liên kết **1 commit** (hoặc biểu tượng lịch sử commit) để kiểm tra lịch sử commit đã được đẩy lên từ local.

**Kết quả mong đợi / kiểm tra:**
* Mã nguồn file `index.html` hiển thị chuẩn xác trên giao diện web của GitHub.
* Lịch sử commit hiển thị đầy đủ thông điệp `"Commit khoi tao: Them file index.html"`.

> **[IMAGE NEEDED]** Giao diện website GitHub hiển thị file index.html và lịch sử commit sau khi push code thành công.
> Gợi ý path: `assets/ss04/step_06_github_repo_success.png`

<!-- section: verify -->
## Kiểm tra tổng kết
Hãy chắc chắn rằng bạn đã đạt được các kết quả sau trước khi kết thúc lab:
- [ ] Thư mục local `my-profile` được quản lý bởi Git (có thư mục ẩn `.git/`).
- [ ] Cặp khóa SSH được sinh ra thành công trong thư mục ẩn `~/.ssh/`.
- [ ] Lệnh `ssh -T git@github.com` hiển thị lời chào xác thực thành công từ GitHub.
- [ ] Chạy `git remote -v` hiển thị liên kết remote dạng SSH trỏ đúng đến repository của bạn trên GitHub.
- [ ] Website GitHub hiển thị đầy đủ nội dung tệp `index.html` và lịch sử commit.

<!-- section: pitfalls -->
## Lỗi thường gặp
* **Copy nhầm Private Key (`id_ed25519`) đưa lên GitHub:** Khi cấu hình SSH Key trên GitHub Console, học viên thường nhầm lẫn dán khóa riêng tư thay vì khóa công khai. Hãy luôn nhớ chỉ mở và copy file có đuôi `.pub` (`id_ed25519.pub`).
* **Sử dụng link HTTPS dẫn đến lỗi hỏi mật khẩu CLI:** Nếu cấu hình link HTTPS cho remote, GitHub sẽ hỏi mật khẩu tài khoản của bạn và báo lỗi không hỗ trợ. Hãy kiểm tra lại bằng lệnh `git remote -v`, nếu thấy link bắt đầu bằng `https://` hãy xóa đi bằng `git remote remove origin` và add lại bằng link SSH bắt đầu bằng `git@github.com:`.
* **Lỡ tích chọn tạo file README khi tạo repo trên GitHub:** Việc này làm phát sinh commit đầu tiên trên remote mà local không có, dẫn đến lỗi xung đột lịch sử (non-fast-forward) khi push. Hãy tạo lại một repository trống khác trên GitHub.

<!-- section: next -->
## Bước tiếp theo
Chúc mừng bạn đã đưa thành công dự án đầu tiên của mình lên GitHub!
Hãy chuyển sang phần **Homework** của Session này để thực hành chuyên sâu các bài tập gộp nhánh, xử lý conflict nâng cao, và kỹ thuật dọn dẹp lịch sử commit.

