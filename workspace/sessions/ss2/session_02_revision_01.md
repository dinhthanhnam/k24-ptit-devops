---
schema_version: 1
id: ss02_revision_01
type: revision_questions
status: approved
course_id: devops-basic
session: 2
unit: 1
title: Ôn sau bài — Khái niệm ảo hóa (Virtualization)
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_01
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / revision L01
language: vi
created: '2026-07-14'
updated: '2026-07-14'
question_count: 2
maps_to:
- ss02_lesson_01
lesson_mode: theory
---

# Ôn sau bài — Khái niệm ảo hóa (Virtualization)

## RQ1
Hãy phân tích và so sánh sự khác biệt cốt lõi về mặt kiến trúc phần cứng và hiệu năng giữa **Hypervisor Type 1 (Bare-metal)** và **Hypervisor Type 2 (Hosted)**. Cho ví dụ thực tế về các công nghệ thuộc mỗi loại.

*Hướng dẫn trả lời:*
*   **Về mặt kiến trúc:** 
    *   *Type 1:* Cài đặt trực tiếp lên phần cứng vật lý của máy chủ, không cần hệ điều hành máy chủ (Host OS) làm trung gian. 
    *   *Type 2:* Hoạt động giống như một phần mềm ứng dụng thông thường, chạy trên nền tảng của một hệ điều hành Host (như Windows, macOS, Linux).
*   **Về mặt hiệu năng:** 
    *   *Type 1:* Hiệu năng tối đa, độ trễ cực thấp do không phải chia sẻ tài nguyên hay đi qua lớp chuyển đổi trung gian của Host OS. 
    *   *Type 2:* Hiệu năng thấp hơn do tài nguyên hệ thống phải phân bổ cho cả Host OS và đi qua các lớp trung gian của hệ điều hành này trước khi đến máy ảo.
*   **Ví dụ thực tế:** 
    *   *Type 1:* VMware ESXi, KVM, Microsoft Hyper-V. 
    *   *Type 2:* Oracle VM VirtualBox, VMware Workstation, Parallels Desktop.

## RQ2
Tại sao công nghệ ảo hóa (Virtualization) lại được coi là nền tảng cốt lõi của điện toán đám mây (Cloud Computing)? Hãy nêu 3 lợi ích kinh tế/kỹ thuật lớn nhất mà ảo hóa mang lại cho doanh nghiệp khi triển khai dịch vụ.

*Hướng dẫn trả lời:*
*   **Lý do ảo hóa là nền tảng của Cloud Computing:** Ảo hóa cung cấp khả năng trừu tượng hóa phần cứng vật lý, cho phép chia nhỏ tài nguyên của một máy chủ vật lý khổng lồ thành nhiều môi trường ảo cô lập. Nhờ đó, các nhà cung cấp đám mây mới có thể triển khai mô hình cung cấp tài nguyên theo yêu cầu (On-demand resource allocation) cho nhiều khách hàng khác nhau.
*   **3 lợi ích lớn nhất:**
    1.  *Tối ưu hóa chi phí (Consolidation):* Gom nhiều máy chủ tải thấp vào một máy chủ vật lý mạnh, giảm chi phí mua sắm thiết bị, điện năng và diện tích phòng máy.
    2.  *Tính cô lập an toàn (Isolation):* Sự cố bảo mật hoặc treo hệ thống ở một máy ảo hoàn toàn không ảnh hưởng đến các máy ảo khác hoạt động trên cùng một phần cứng.
    3.  *Quản lý linh hoạt và nhanh chóng (Flexibility & Portability):* Khởi tạo máy ảo mới chỉ trong vài giây, dễ dàng sao lưu (Snapshot), nhân bản (Clone) hoặc di chuyển máy ảo sang phần cứng vật lý khác mà không làm gián đoạn dịch vụ.
