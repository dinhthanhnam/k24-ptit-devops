---
schema_version: 1
id: ss02_lesson_02
type: lesson
status: approved
course_id: devops-basic
session: 2
unit: 2
title: Khởi tạo Cloud Server thực tế
session_kind: theory
tags: []
concepts:
- cloud-server-provisioning
depends_on: []
builds_on: []
enables: []
owns:
- cloud-server-provisioning
assumes:
- virtualization-basics
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / Lesson 02
language: vi
created: '2026-07-14'
updated: '2026-07-14'
lesson_mode: practical
---

# Khởi tạo Cloud Server thực tế

<!-- section: problem -->
## 1. Đặt vấn đề
Trong môi trường phát triển phần mềm truyền thống, khi cần triển khai một ứng dụng lên internet, các kỹ sư thường phải đối mặt với quy trình cài đặt và cấu hình phần cứng vật lý vô cùng phức tạp:
*   **Mua sắm và lắp đặt:** Mua máy chủ vật lý, tủ rack, thiết lập hệ thống điện và làm mát.
*   **Cấu hình mạng:** Thiết lập router, switch, mua IP tĩnh (Public IP) và cấu hình tường lửa mạng vật lý.
*   **Thời gian chuẩn bị lâu:** Quá trình chuẩn bị hạ tầng có thể kéo dài từ vài ngày đến vài tuần.

Để giải quyết vấn đề này, điện toán đám mây (Cloud Computing) cung cấp giải pháp **Cloud Server** (hoặc VPS). Người dùng có thể khởi tạo một hoặc nhiều máy chủ ảo hoạt động độc lập trên hạ tầng của nhà cung cấp chỉ sau vài cú click chuột, sẵn sàng để cài đặt ứng dụng ngay lập tức mà không cần quan tâm đến phần cứng vật lý bên dưới.

<!-- section: core -->
## 2. Kiến thức cốt lõi
*   **Virtual Private Server (VPS):** Là một máy chủ ảo được phân chia từ một máy chủ vật lý mạnh mẽ bằng công nghệ ảo hóa (thường sử dụng Hypervisor Type 1 như KVM). Mỗi VPS có hệ điều hành, tài nguyên (CPU, RAM, Disk) và IP tĩnh riêng biệt, hoàn toàn cô lập với các VPS khác trên cùng một máy chủ vật lý.
*   **Cloud Provider (Nhà cung cấp đám mây):** Các công ty sở hữu các trung tâm dữ liệu (Data Center) khổng lồ và cung cấp dịch vụ cho thuê tài nguyên ảo hóa qua internet.
    *   *Quốc tế:* AWS (Amazon Web Services), Google Cloud Platform (GCP), Microsoft Azure, DigitalOcean, Linode/Akamai.
    *   *Trong nước:* VNG Cloud, Viettel IDC, FPT Smart Cloud, CMC Cloud.
*   **Các thông số kỹ thuật cốt lõi của một VPS:**
    *   **vCPU (Virtual CPU):** Đơn vị xử lý trung tâm ảo hóa. Càng nhiều vCPU, khả năng xử lý song song càng mạnh.
    *   **RAM (Random Access Memory):** Bộ nhớ trong của máy chủ ảo. Thiếu RAM sẽ khiến hệ điều hành kích hoạt cơ chế Out-Of-Memory (OOM) killer và tắt ứng dụng.
    *   **Storage (Lưu trữ):** Thường sử dụng ổ cứng SSD hoặc NVMe ảo hóa để đảm bảo tốc độ đọc/ghi (IOPS) cao.
    *   **Region / Zone:** Vị trí vật lý của trung tâm dữ liệu chứa máy chủ ảo. Cần chọn Region gần người dùng nhất (ví dụ: Singapore đối với người dùng tại Việt Nam) để giảm độ trễ (latency).
    *   **OS Image:** Bản cài đặt hệ điều hành mẫu. Trong khóa học này, chúng ta sử dụng **Ubuntu Server 24.04 LTS** (phiên bản tiêu chuẩn mới nhất).
*   **Xác thực SSH (Secure Shell Authentication):**
    *   *Mật khẩu (Password):* Dễ bị tấn công Brute-force (dò tìm mật khẩu bằng botnet).
    *   *Khóa SSH (SSH Key):* Phương pháp xác thực dựa trên mật mã khóa công khai (Public-key cryptography). Gồm 2 phần:
        *   **Khóa riêng tư (Private Key - `id_ed25519`):** Giữ bí mật trên máy tính cá nhân.
        *   **Khóa công khai (Public Key - `id_ed25519.pub`):** Đưa lên máy chủ ảo để xác thực kết nối.

> [!TIP]
> **Về chi phí thực hành (Free Credit):**
> Hầu hết các nhà cung cấp đám mây lớn (như DigitalOcean, AWS, GCP) đều có chương trình dùng thử miễn phí dành cho tài khoản mới. 
> *   **DigitalOcean Free Trial:** Tặng **$200 credit** miễn phí sử dụng trong 60 ngày khi đăng ký tài khoản mới qua link giới thiệu (referral link) hoặc liên kết thẻ ngân hàng (chỉ để xác thực, không bị trừ tiền nếu dùng trong hạn mức).
> *   **GitHub Student Developer Pack:** Nếu các bạn có email sinh viên (`@student...` hoặc `@ptit.edu.vn`), các bạn có thể đăng ký gói này để nhận thêm **$200 credit** của DigitalOcean và nhiều công cụ lập trình khác miễn phí hoàn toàn.

<!-- section: steps -->
## 3. Các bước thực hành

### Bước 1 — Tạo cặp khóa SSH (SSH Key Pair) trên máy cá nhân
Trước khi khởi tạo máy chủ, các bạn cần chuẩn bị sẵn một cặp khóa SSH trên máy tính của mình để đảm bảo kết nối an toàn. Chúng ta sử dụng thuật toán **Ed25519** vì độ bảo mật cao, hiệu năng tốt và cú pháp gọn nhẹ hơn so với RSA truyền thống.

Mở Terminal (trên Linux/macOS) hoặc PowerShell/Git Bash (trên Windows) và chạy lệnh sau:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
*   Nhấn **Enter** để lưu khóa ở đường dẫn mặc định (`~/.ssh/id_ed25519`).
*   Hệ thống sẽ yêu cầu nhập *passphrase* (mật khẩu bảo vệ khóa riêng tư). Các bạn có thể nhấn **Enter** hai lần để bỏ qua nếu muốn đăng nhập nhanh không cần mật khẩu.

Kiểm tra và copy nội dung của **Public Key** vừa tạo:
```bash
cat ~/.ssh/id_ed25519.pub
```
*(Hãy copy toàn bộ nội dung xuất hiện, bắt đầu bằng `ssh-ed25519` và kết thúc bằng email của các bạn).*

### Bước 2 — Đăng nhập và chọn dịch vụ tại Cloud Provider
Truy cập vào trang quản trị của nhà cung cấp cloud (ở đây lấy ví dụ là **DigitalOcean**). Nhấn nút **Create** ở góc trên bên phải màn hình và chọn **Droplets** (tên gọi của VPS trên DigitalOcean).

> **[IMAGE NEEDED]** Mô tả: Trang bảng điều khiển (Dashboard) của DigitalOcean với nút Create Droplets nổi bật.
> Gợi ý path: `assets/ss02/step_02_do_dashboard.png`

### Bước 3 — Cấu hình vị trí máy chủ (Region)
Chọn khu vực địa lý cho máy chủ. Đối với người dùng tại Việt Nam, hãy ưu tiên chọn **Singapore** để có tốc độ truyền tải nhanh nhất và độ trễ thấp nhất.

> **[IMAGE NEEDED]** Mô tả: Giao diện chọn Region trong trang tạo Droplet, chọn Singapore.
> Gợi ý path: `assets/ss02/step_03_select_region.png`

### Bước 4 — Chọn Hệ điều hành và cấu hình phần cứng (Droplet Type)
*   **OS Image:** Chọn **Ubuntu**, phiên bản **24.04 LTS (x64)**.
*   **Droplet Type:** Chọn gói **Basic** (Shared CPU).
*   **CPU Options:** Chọn gói rẻ nhất để thực hành (ví dụ: Regular với giá trị 4GB / 2 vCPUs hoặc gói 1 vCPU / 512MB hoặc 1GB RAM tùy thuộc vào mục đích sử dụng hiện tại).

> **[IMAGE NEEDED]** Mô tả: Chọn OS Image Ubuntu 24.04 và gói cấu hình phần cứng tối thiểu cho Droplet.
> Gợi ý path: `assets/ss02/step_04_select_os_spec.png`

### Bước 5 — Thiết lập cơ chế xác thực (Authentication)
Tại phần **Authentication Method**, chọn **SSH Keys**. 
*   Nhấn nút **New SSH Key** (hoặc **Add SSH Key**).
*   Dán toàn bộ nội dung Public Key (`id_ed25519.pub`) đã copy ở **Bước 1** vào ô nhập liệu.
*   Đặt tên gợi nhớ cho khóa SSH đó (ví dụ: `my-laptop-key`) và nhấn **Add SSH Key**.

> **[IMAGE NEEDED]** Mô tả: Cửa sổ popup dán SSH Public Key vào giao diện cấu hình của DigitalOcean.
> Gợi ý path: `assets/ss02/step_05_add_ssh_key.png`

Sau đó, cuộn xuống dưới cùng và nhấn nút **Create Droplet**.

### Bước 6 — Kết nối tới Cloud Server qua SSH
Đợi khoảng 1-2 phút để nhà cung cấp khởi tạo hệ thống. Sau khi quá trình hoàn tất, các bạn sẽ thấy Droplet hiển thị một địa chỉ **IP Public** dạng `12.34.56.78`.

Mở Terminal/PowerShell trên máy cá nhân và tiến hành kết nối:
```bash
ssh root@<IP_ADDRESS_CỦA_DROPLET>
```
Nếu hệ thống hỏi xác nhận độ tin cậy của máy chủ (*Are you sure you want to continue connecting?*), hãy gõ `yes` và nhấn **Enter**. 

Nếu thành công, giao diện Terminal của các bạn sẽ chuyển sang dấu nhắc lệnh của máy chủ Ubuntu từ xa:
```bash
root@ubuntu-s-1vcpu-1gb-sgp1:~#
```

> **[IMAGE NEEDED]** Mô tả: Màn hình Terminal kết nối thành công vào server Ubuntu từ xa qua giao thức SSH.
> Gợi ý path: `assets/ss02/step_06_ssh_connected.png`

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
*   **Sử dụng mật khẩu đơn giản (Password Authentication):** Đây là lỗi nghiêm trọng nhất. Các botnet trên internet liên tục quét các cổng SSH (mặc định là cổng 22) và thực hiện dò mật khẩu (brute-force). Nếu các bạn dùng mật khẩu dễ nhớ, server có thể bị chiếm quyền điều khiển chỉ trong vài giờ. **Khuyến nghị luôn dùng SSH Key**.
*   **Lộ khóa riêng tư (Private Key):** Tuyệt đối không được chia sẻ file `id_ed25519` hoặc nội dung bên trong nó cho bất kỳ ai. Nếu mất Private Key, bất cứ ai có file đó đều có thể đăng nhập vào server mà không cần mật khẩu.
*   **Quên xóa tài nguyên (Resources Cleanup):** Các nhà cung cấp dịch vụ đám mây tính tiền theo thời gian tài nguyên được bật (thường tính theo giờ). Kể cả khi các bạn tắt máy ảo trong bảng điều khiển nhưng không xóa (Destroy), ổ đĩa và địa chỉ IP vẫn được giữ riêng và các bạn vẫn bị tính phí. **Nhớ bấm Destroy Droplet sau khi không dùng nữa**.

<!-- section: references -->
## 5. Tài liệu tham khảo
*   [DigitalOcean - How to Create a Droplet](https://docs.digitalocean.com/products/droplets/how-to/create/)
*   [DigitalOcean - How to Connect to Droplets with SSH](https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/)
*   [OpenSSH Documentation](https://www.openssh.com/)

<!-- companions: sau khi lesson approved → revision `ss02_revision_02` + quiz `ss02_quiz_lesson_02` (get_quiz_plan) -->
