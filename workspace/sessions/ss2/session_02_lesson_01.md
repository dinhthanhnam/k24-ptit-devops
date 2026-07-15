---
schema_version: 1
id: ss02_lesson_01
type: lesson
status: approved
course_id: devops-basic
session: 2
unit: 1
title: Khái niệm ảo hóa (Virtualization)
session_kind: theory
tags: []
concepts:
- virtualization-basics
depends_on: []
builds_on: []
enables: []
owns:
- virtualization-basics
assumes: []
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / Lesson 01
language: vi
created: '2026-07-14'
updated: '2026-07-15'
lesson_mode: theory
---

# Khái niệm ảo hóa (Virtualization)

<!-- section: objectives -->
## 1. Mục tiêu
- Hiểu rõ định nghĩa và cơ chế hoạt động của công nghệ ảo hóa (Virtualization).
- Phân biệt cấu trúc kiến trúc giữa máy chủ vật lý truyền thống (Bare-metal) và hệ thống sử dụng ảo hóa.
- Phân loại và so sánh được Hypervisor Type 1 (Bare-metal) và Hypervisor Type 2 (Hosted).
- Nhận thức được các ưu điểm vượt trội và vai trò nền tảng của ảo hóa đối với điện toán đám mây (Cloud Computing).

<!-- section: problem -->
## 2. Đặt vấn đề
Trước khi công nghệ ảo hóa xuất hiện, cách duy nhất để triển khai một ứng dụng trong môi trường sản xuất (production) là cài đặt trực tiếp hệ điều hành lên một máy chủ vật lý (Bare-metal server), sau đó chạy ứng dụng trên hệ điều hành đó. Cách tiếp cận truyền thống này bộc lộ nhiều hạn chế nghiêm trọng:

1. **Lãng phí tài nguyên phần cứng cực kỳ lớn**: Một máy chủ vật lý mạnh mẽ thường chỉ sử dụng khoảng 10% - 15% năng lực xử lý của CPU và RAM cho một ứng dụng đơn lẻ. Tuy nhiên, doanh nghiệp vẫn phải trả chi phí vận hành, điện năng và làm mát cho toàn bộ hệ thống vật lý đó.
2. **Thời gian triển khai chậm chạp**: Để có thêm một máy chủ mới chạy môi trường thử nghiệm hoặc ứng dụng mới, doanh nghiệp phải mất nhiều ngày, thậm chí nhiều tuần để mua sắm thiết bị phần cứng, lắp đặt tủ rack, đi dây mạng và cài đặt thủ công.
3. **Thiếu tính độc lập và bảo mật (Isolation)**: Nếu cài đặt nhiều ứng dụng khác nhau lên cùng một máy vật lý để tiết kiệm chi phí, các ứng dụng này dễ dàng xung đột thư viện phần mềm (dependency conflict). Hơn nữa, nếu một ứng dụng bị tấn công hoặc gặp sự cố crash, nó có thể làm ảnh hưởng hoặc làm sập toàn bộ các dịch vụ khác trên máy chủ đó.

Để vượt qua các rào cản này, ngành công nghệ thông tin cần một giải pháp cho phép chia nhỏ một máy chủ vật lý mạnh mẽ thành nhiều máy chủ ảo độc lập, hoạt động an toàn và tối ưu tài nguyên. Đó chính là lý do công nghệ **ảo hóa (Virtualization)** ra đời.

<!-- section: core -->
## 3. Kiến thức cốt lõi

### 3.1. Ảo hóa là gì?
**Ảo hóa (Virtualization)** là công nghệ cho phép tạo ra các phiên bản ảo (logical representation) chạy trên nền tảng hạ tầng phần cứng vật lý của máy tính (physical resources). Công nghệ này hoạt động bằng cách chèn một lớp phần mềm đặc biệt lên trên phần cứng vật lý để trừu tượng hóa (abstract) và phân chia các tài nguyên vật lý như CPU, RAM, ổ cứng (Storage) và card mạng (Network) thành nhiều phần độc lập.

*Lịch sử phát triển:* 
Công nghệ ảo hóa có nguồn gốc từ những năm 1960 trên các dòng máy tính lớn (Mainframe) của IBM. Dẫn chứng lịch sử nổi bật nhất là dự án phát triển hệ điều hành **CP-40** vào năm **1967** trên hệ thống IBM System/360 Model 40. Sau một thời gian thoái trào, ảo hóa bùng nổ trở lại trên kiến trúc máy tính cá nhân x86 nhờ giải pháp dịch nhị phân bằng phần mềm của **VMware** năm **1998** (bằng sáng chế US6397242B1), và sau đó là các hỗ trợ phần cứng tăng tốc từ Intel (Intel VT-x, 2005) và AMD (AMD-V, 2006).

Mỗi phần tài nguyên độc lập này được đóng gói lại để tạo thành một **Máy ảo (Virtual Machine - VM)**.

```text
+-------------------------------------------------------------+
| Máy ảo A (Guest OS) | Máy ảo B (Guest OS) | Máy ảo C (Guest OS) |
+-------------------------------------------------------------+
|             Lớp ảo hóa (Hypervisor / VMM)                  |
+-------------------------------------------------------------+
|             Phần cứng vật lý (Host Hardware)                |
+-------------------------------------------------------------+
```

### 3.2. Thành phần cốt lõi: Hypervisor
**Hypervisor** (hay còn gọi là **VMM - Virtual Machine Monitor**) là thành phần phần mềm quan trọng nhất trong công nghệ ảo hóa. Nhiệm vụ của Hypervisor bao gồm:
*   Trừu tượng hóa tài nguyên phần cứng vật lý.
*   Phân phối tài nguyên (CPU, RAM, Disk) một cách linh hoạt cho từng máy ảo.
*   Đảm bảo tính cô lập và an toàn giữa các máy ảo, không để máy ảo này truy cập trái phép vào bộ nhớ hay tài nguyên của máy ảo khác.
*   **Quản lý phân quyền lệnh (CPU Rings):** CPU phân chia quyền chạy lệnh từ Ring 0 (Quyền tối cao của OS) đến Ring 3 (Quyền thấp của ứng dụng). Để máy ảo (Guest OS) không can thiệp trực tiếp làm hỏng tài nguyên vật lý, Hypervisor kiểm soát và dịch các lệnh nhạy cảm của máy ảo thông qua phần mềm (Binary Translation) hoặc nhờ sự hỗ trợ của phần cứng CPU (VT-x/AMD-V giúp tự động gạt nút chuyển quyền VM-Exit/VM-Entry).

Hypervisor được chia làm hai loại chính:

#### 3.2.1. Hypervisor Type 1 (Bare-metal Hypervisor)
Loại Hypervisor này được cài đặt **trực tiếp lên phần cứng vật lý** của máy chủ mà không cần thông qua bất kỳ hệ điều hành trung gian nào.
*   **Cơ chế hoạt động**: Chạy trực tiếp trên phần cứng, quản lý trực tiếp CPU, RAM và thiết bị ngoại vi.
*   **Đặc điểm**: Hi năng cực kỳ cao, độ trễ thấp, tính ổn định và bảo mật tối đa do giảm thiểu được lớp trung gian OS.
*   **Ví dụ thực tế**: VMware ESXi, Microsoft Hyper-V, KVM (Kernel-based Virtual Machine), Citrix XenServer.
*   **Ứng dụng**: Thường được dùng trong các trung tâm dữ liệu (Data Center), các nhà cung cấp dịch vụ đám mây (AWS, Azure, Google Cloud, các nhà cung cấp VPS) đòi hỏi hiệu năng cao và quy mô lớn.

#### 3.2.2. Hypervisor Type 2 (Hosted Hypervisor)
Loại Hypervisor này được cài đặt và vận hành như **một phần mềm ứng dụng thông thường** chạy trên một hệ điều hành máy chủ có sẵn (Host OS).
*   **Cơ chế hoạt động**: Phần cứng vật lý -> Hệ điều hành Host (Windows, macOS, Linux) -> Hypervisor -> Các máy ảo (Guest OS).
*   **Đặc điểm**: Dễ dàng cài đặt và sử dụng, giao diện thân thiện. Tuy nhiên, hiệu năng thấp hơn Type 1 do tài nguyên phải đi qua lớp trung gian của Host OS.
*   **Ví dụ thực tế**: Oracle VM VirtualBox, VMware Workstation, Parallels Desktop.
*   **Ứng dụng**: Phù hợp cho môi trường học tập, nghiên cứu, phát triển phần mềm thử nghiệm của lập trình viên ngay trên máy tính cá nhân.

```text
SO SÁNH HAI LOẠI HYPERVISOR

        [ Hypervisor Type 1 ]                    [ Hypervisor Type 2 ]
  +-------------------------------+        +-------------------------------+
  |   VM 1 (OS)  |   VM 2 (OS)    |        |   VM 1 (OS)  |   VM 2 (OS)    |
  +-------------------------------+        +-------------------------------+
  |      Hypervisor (Type 1)      |        |      Hypervisor (Type 2)      |
  +-------------------------------+        +-------------------------------+
  |       Phần cứng vật lý        |        |  Hệ điều hành Host (Win/Mac)  |
  +-------------------------------+        +-------------------------------+
                                           |       Phần cứng vật lý        |
                                           +-------------------------------+
```

### 3.3. Khái niệm Máy ảo (Virtual Machine - VM)
Một **Máy ảo (VM)** là một hệ thống máy tính ảo hóa hoạt động độc lập như một máy tính vật lý thật. Một máy ảo tiêu chuẩn bao gồm:
*   **Cấu hình phần cứng ảo hóa**: CPU ảo (vCPU), RAM ảo, ổ đĩa ảo, card mạng ảo được Hypervisor cấp phát.
*   **Hệ điều hành khách (Guest OS)**: Hệ điều hành cài đặt bên trong máy ảo (ví dụ: Ubuntu Server, Windows Server). Guest OS này hoàn toàn tin rằng nó đang chạy trên phần cứng vật lý thực tế.
*   **Ứng dụng và Thư viện**: Toàn bộ ứng dụng và môi trường chạy code của người dùng.

### 3.4. Lợi ích vượt trội của công nghệ ảo hóa
Nhờ sự cách ly và quản lý tập trung của Hypervisor, ảo hóa mang lại các giá trị cốt lõi:
1. **Tối ưu hóa chi phí (Consolidation)**: Gom nhiều máy chủ ứng dụng tải thấp vào chạy trên một máy chủ vật lý mạnh duy nhất, giảm thiểu số lượng thiết bị phần cứng phải mua sắm và bảo trì.
2. **Khả năng cách ly an toàn (Isolation)**: Sự cố sập hệ thống hoặc nhiễm mã độc trên một máy ảo sẽ bị giới hạn hoàn toàn trong máy ảo đó, không lây lan sang các máy ảo khác hay ảnh hưởng tới hệ điều hành Host.
3. **Quản lý linh hoạt (Flexibility & Portability)**: Máy ảo thực chất được lưu trữ dưới dạng các tệp tin cấu hình và ổ đĩa trên bộ nhớ. Do đó, quản trị viên dễ dàng tạo bản sao (Clone), chụp ảnh trạng thái tức thời (Snapshot) để rollback khi lỗi, hoặc di chuyển máy ảo sang một phần cứng vật lý khác mà không cần cài đặt lại từ đầu.

> [!NOTE]
> **Gợi ý Prompt sinh hình minh họa (AI Image Prompt):**
> *A high-tech diagram showcasing hardware virtualization architecture. At the bottom, a powerful physical server rack made of hardware components glows with blue light. In the middle, a clean software layer representing the Hypervisor abstracts the resources. At the top, three transparent virtual machines float, each containing its own operating system icon (like Linux or Windows) and applications. Isometric flat design style, professional neon accents, cyan and dark blue color scheme.*

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
*   **Nhầm lẫn giữa Ảo hóa (Virtualization) và Giả lập (Emulation)**:
    *   *Ảo hóa*: Các máy ảo chia sẻ trực tiếp kiến trúc tập lệnh phần cứng của Host (ví dụ: máy ảo x86 chạy trên phần cứng x86). Hiệu năng đạt gần tương đương bare-metal nhờ cơ chế pass-through trực tiếp thông qua Hypervisor.
    *   *Giả lập*: Phần mềm phải dịch chuyển toàn bộ tập lệnh từ kiến trúc này sang kiến trúc khác bằng code (ví dụ: giả lập game console ARM trên máy tính x86). Quá trình này tiêu tốn cực kỳ nhiều tài nguyên và hiệu năng rất thấp.
*   **Nghĩ rằng tài nguyên ảo hóa là vô hạn**: Một lỗi phổ biến của quản trị viên là cấp phát vCPU và RAM ảo vượt xa năng lực vật lý thực tế (overcommitting). Khi các máy ảo đồng loạt chịu tải cao, hệ thống vật lý sẽ bị quá tải dẫn đến treo hoặc crash hàng loạt máy ảo.

<!-- section: references -->
## 5. Tài liệu tham khảo
- [VMware Virtualization Basics](https://www.vmware.com/topics/glossary/content/virtualization.html)
- [IBM Cloud: What is Virtualization?](https://www.ibm.com/topics/virtualization)
