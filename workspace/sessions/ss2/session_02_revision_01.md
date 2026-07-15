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
created: '2026-07-15'
updated: '2026-07-15'
question_count: 3
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
Giải thích khái niệm phân quyền lệnh (**CPU Rings**) trong kiến trúc máy tính. Tại sao việc quản lý CPU Rings lại là yếu tố sống còn để Hypervisor duy trì tính cô lập an toàn giữa các máy ảo?

*Hướng dẫn trả lời:*
*   **Khái niệm CPU Rings:** CPU phân chia quyền thực thi lệnh từ cao xuống thấp: Ring 0 (Quyền tối cao dành cho Nhân hệ điều hành - Kernel, can thiệp trực tiếp phần cứng) và Ring 3 (Quyền thấp dành cho ứng dụng người dùng, muốn kết nối phần cứng phải xin phép Ring 0).
*   **Lý do quản lý CPU Rings là sống còn:** Trong máy ảo, Guest OS luôn tin rằng nó có quyền tối cao và muốn chạy ở Ring 0. Tuy nhiên, nếu cho phép Guest OS kiểm soát Ring 0 vật lý, nó sẽ can thiệp và làm sập hoặc đọc trộm dữ liệu của các máy ảo khác chạy chung phần cứng. Do đó, Hypervisor phải chiếm giữ Ring 0 thật, đẩy Guest OS xuống Ring thấp hơn và kiểm soát toàn bộ các lệnh nhạy cảm của Guest OS (thông qua dịch nhị phân hoặc dùng công nghệ hỗ trợ phần cứng VT-x/AMD-V để thực hiện bẫy chuyển quyền VM-Exit/VM-Entry) nhằm bảo đảm tính cô lập tuyệt đối.

## RQ3
Trình bày các mốc dẫn chứng lịch sử quan trọng đánh dấu sự phát triển của công nghệ ảo hóa từ máy tính lớn (Mainframe) đến kiến trúc x86 thương mại phổ thông ngày nay.

*Hướng dẫn trả lời:*
*   **Thập niên 1960s (IBM Mainframe):** Khởi đầu từ dự án phát triển hệ điều hành **CP-40** vào năm **1967** trên hệ thống IBM System/360 Model 40 tại Trung tâm Khoa học Cambridge của IBM, thiết lập khái niệm máy ảo thương mại đầu tiên để chia sẻ máy tính lớn đắt đỏ.
*   **Năm 1998 (VMware và cuộc cách mạng x86):** VMware nộp bằng sáng chế Hoa Kỳ số **US6397242B1** năm 1998 về giải pháp dịch nhị phân bằng phần mềm, giải quyết bài toán ảo hóa trên kiến trúc x86 (vốn không được thiết kế hỗ trợ ảo hóa ban đầu).
*   **Năm 2005 - 2006 (Ảo hóa phần cứng):** Các nhà sản xuất vi xử lý ra mắt các công nghệ tích hợp trực tiếp trên chip: Intel giới thiệu **Intel VT-x** năm **2005** và AMD giới thiệu **AMD-V** năm **2006**, đưa hiệu năng ảo hóa tiệm cận phần cứng thật.
