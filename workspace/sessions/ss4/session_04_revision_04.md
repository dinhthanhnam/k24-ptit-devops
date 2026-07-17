---
schema_version: 1
id: ss04_revision_04
type: revision_questions
status: approved
course_id: devops-basic
session: 4
unit: 4
title: "Ôn tập - Kỹ thuật Git nâng cao và quản lý lịch sử"
session_kind: theory
tags:
  - git
  - revision
concepts: []
depends_on:
  - ss04_lesson_04
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: "Session 04 / revision L04"
language: vi
created: '2026-07-17'
updated: '2026-07-17'
question_count: 3
maps_to:
  - ss04_lesson_04
lesson_mode: practical
---

# Ôn tập - Kỹ thuật Git nâng cao và quản lý lịch sử

## RQ1
Hãy so sánh sự khác nhau về mặt cơ chế hoạt động đối với 3 vùng làm việc (Working Directory, Staging Area, Git Directory) khi thực hiện lệnh hủy commit ở 3 chế độ: `git reset --soft`, `git reset --mixed` và `git reset --hard`. Trong trường hợp nào việc sử dụng `git reset --hard` có thể gây mất mát mã nguồn vĩnh viễn?

*Hướng dẫn trả lời:*
* **Cơ chế hoạt động:**
  * `git reset --soft`: Chỉ dịch chuyển con trỏ nhánh về commit cũ. Các thay đổi của commit bị hủy vẫn được giữ nguyên vẹn ở **Staging Area** (sẵn sàng để commit lại). Working Directory không thay đổi.
  * `git reset --mixed` (mặc định): Dịch chuyển con trỏ nhánh về commit cũ và xóa các thay đổi đó khỏi Staging Area. Tuy nhiên, các file thay đổi vẫn được giữ lại tại **Working Directory** dưới dạng tệp tin chưa được theo dõi/chỉnh sửa (Untracked/Modified).
  * `git reset --hard`: Dịch chuyển con trỏ nhánh về commit cũ, đồng thời xóa sạch toàn bộ các file thay đổi ở cả **Staging Area** và **Working Directory**.
* **Nguy cơ mất mát vĩnh viễn:** Chế độ `--hard` ghi đè trực tiếp lên thư mục làm việc vật lý trên ổ cứng. Nếu học viên có các đoạn code mới viết đang dang dở ở Working Directory mà chưa thực hiện commit (hoặc chưa add vào stash), lệnh `--hard` sẽ xóa sạch hoàn toàn các file này và không thể phục hồi lại bằng Git được nữa.

## RQ2
Tại sao khi làm việc nhóm trên một nhánh chung (như `main`), lập trình viên tuyệt đối không nên sử dụng `git reset` để xóa bỏ các commit đã push lên remote, mà thay vào đó phải sử dụng `git revert`? Giải thích cơ chế của `git revert`.

*Hướng dẫn trả lời:*
* **Tại sao không dùng `git reset` trên nhánh chung:**
  * Lệnh `git reset` viết lại lịch sử commit ở local (xóa commit cũ). Nếu bạn đã push các commit đó lên remote và đồng nghiệp đã kéo (pull) về máy họ, việc bạn reset ở local rồi push ép buộc (`git push -f`) sẽ tạo ra sự sai lệch lịch sử nghiêm trọng. Đồng nghiệp của bạn khi pull tiếp theo sẽ gặp lỗi xung đột lịch sử commit chồng chéo và có thể lỡ tay push ngược lại commit bạn đã xóa lên remote.
* **Cơ chế của `git revert`:**
  * Lệnh `git revert` không hề xóa bỏ commit lỗi trong quá khứ. Thay vào đó, nó tạo ra một **commit mới** hoàn toàn độc lập, chứa các thay đổi có nội dung đảo ngược hoàn toàn so với commit lỗi đó. Vì đây là một commit mới nằm ở đỉnh lịch sử, nó không hề viết lại lịch sử cũ mà chỉ đi tiếp về phía trước, giúp việc push/pull đồng bộ giữa các thành viên diễn ra trơn tru mà không gây xung đột lịch sử.

## RQ3
Giải thích vai trò của lệnh `git cherry-pick`. Hãy nêu một tình huống thực tế mà bạn bắt buộc phải dùng `git cherry-pick` thay vì dùng `git merge` thông thường.

*Hướng dẫn trả lời:*
* **Vai trò của `git cherry-pick`:** Cho phép chọn lọc và sao chép chính xác một commit cụ thể từ bất kỳ nhánh nào trong repository để áp dụng lên nhánh hiện hành dưới dạng một commit mới.
* **Tình huống thực tế:**
  * Bạn đang phát triển một loạt các tính năng mới lớn trên nhánh `feature-app`. Nhánh này chứa hàng chục commit khác nhau và hầu hết chúng đều chưa hoàn thiện, chưa chạy được thử nghiệm.
  * Đột nhiên, khách hàng báo lỗi bảo mật nghiêm trọng trên production. Bạn đã viết mã sửa lỗi này thành công trong commit duy nhất ký hiệu là `C5` trên nhánh `feature-app`.
  * Lúc này, bạn chỉ muốn đưa duy nhất bản sửa lỗi của commit `C5` vào nhánh chính `main` để deploy lập tức cho khách hàng. Bạn không thể dùng `git merge feature-app` vì nó sẽ kéo theo hàng chục commit tính năng chưa hoàn thiện kia làm hỏng bản chạy ổn định. Giải pháp duy nhất là chuyển sang `main` và chạy `git cherry-pick C5` để chỉ lấy đúng bản vá lỗi.
