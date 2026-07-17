---
schema_version: 1
id: ss04_revision_03
type: revision_questions
status: approved
course_id: devops-basic
session: 4
unit: 3
title: "Ôn tập - Làm việc Từ xa với GitHub và quy trình Teamwork"
session_kind: theory
tags:
  - git
  - revision
concepts: []
depends_on:
  - ss04_lesson_03
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: "Session 04 / revision L03"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
question_count: 3
maps_to:
  - ss04_lesson_03
lesson_mode: practical
---

# Ôn tập - Làm việc Từ xa với GitHub và quy trình Teamwork

## RQ1
Tại sao GitHub lại ngừng hỗ trợ xác thực bằng mật khẩu tài khoản thông thường (HTTPS Password) khi thực hiện các thao tác push/pull mã nguồn qua Git CLI? Hãy giải thích lợi ích về mặt bảo mật của cơ chế xác thực bằng SSH Key.

*Hướng dẫn trả lời:*
* **Lý do ngừng hỗ trợ HTTPS Password:** Mật khẩu thông thường dễ bị rò rỉ (qua các đợt tấn công brute-force, keylogger hoặc do người dùng đặt mật khẩu yếu). Hơn nữa, việc lưu mật khẩu dưới dạng văn bản thô trên máy tính local rất kém an toàn.
* **Lợi ích bảo mật của SSH Key:**
  * Cơ chế SSH Key sử dụng mật mã khóa công khai (khóa bất đối xứng) với thuật toán phức tạp, khiến hacker không thể giải mã ngược lại từ khóa công khai để lấy khóa riêng tư.
  * Khóa riêng tư (`id_ed25519`) luôn nằm an toàn ở local và không bao giờ được gửi qua internet. GitHub chỉ nhận khóa công khai và chữ ký số được ký bởi khóa riêng tư để xác nhận quyền truy cập.
  * Người dùng có thể dễ dàng quản lý, thu hồi hoặc thêm mới các khóa SSH độc lập cho từng thiết bị mà không cần đổi mật khẩu gốc của tài khoản.

## RQ2
Một lập trình viên lỡ tay sao chép nội dung của khóa riêng tư (`id_ed25519`) và dán vào mục cấu hình SSH Key trên GitHub Console. Điều này có giúp họ kết nối được không và nó gây ra mối nguy hại bảo mật nào? Khóa nào mới là khóa chính xác cần đưa lên GitHub?

*Hướng dẫn trả lời:*
* **Kết quả kết nối:** Không thể kết nối được. GitHub yêu cầu Khóa công khai (Public Key) để đối chiếu chữ ký số từ máy local gửi lên. Nếu bạn cung cấp Khóa riêng tư cho GitHub, GitHub sẽ không thể giải mã chữ ký được tạo từ chính khóa đó (vì nguyên tắc khóa bất đối xứng là dữ liệu mã hóa bằng khóa này phải được giải mã bằng khóa kia).
* **Nguy cơ bảo mật:** Đây là lỗ hổng bảo mật cực kỳ nghiêm trọng. Khi khóa riêng tư bị đưa lên internet hoặc bên thứ ba, bất kỳ ai có được khóa này đều có thể mạo danh bạn để truy cập, sửa đổi, xóa sạch toàn bộ mã nguồn trên tất cả các kho chứa của bạn trên GitHub.
* **Khóa chính xác:** Học viên bắt buộc phải copy nội dung của khóa công khai, tệp tin có đuôi `.pub` (`~/.ssh/id_ed25519.pub`).

## RQ3
Phân biệt sự khác biệt về vai trò và kết quả thực thi giữa hai lệnh `git fetch` và `git pull`. Trong trường hợp nào học viên nên dùng `git fetch` thay vì `git pull`?

*Hướng dẫn trả lời:*
* **Phân biệt:**
  * `git fetch`: Chỉ tải toàn bộ lịch sử commit mới nhất từ remote repository về local repository nhưng **không tự động gộp (merge)** các thay đổi này vào mã nguồn đang viết ở Working Directory. Nhánh local của bạn vẫn giữ nguyên trạng thái cũ.
  * `git pull`: Thực hiện hai hành động liên tiếp: Tải về các thay đổi mới (`git fetch`) và ngay lập tức **tự động gộp** (`git merge`) các thay đổi đó vào nhánh hiện hành ở Working Directory của bạn.
* **Trường hợp nên dùng `git fetch`:**
  * Khi làm việc nhóm và bạn muốn kiểm tra xem đồng nghiệp đã commit những gì lên remote trước khi quyết định gộp code để tránh làm hỏng hoặc xung đột với code hiện tại của mình.
  * Khi bạn muốn so sánh sự khác biệt (`git diff origin/main`) trước khi chính thức merge.
