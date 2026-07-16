# DÀN Ý CHI TIẾT - SESSION 2: VIRTUAL PRIVATE SERVER (VPS) & ẢO HÓA
*(Tổng số slide: 22 slides - Đầy đủ chi tiết cho toàn bộ Session 2)*

---

## SLIDE 1: TIÊU ĐỀ CHÍNH
* **Tiêu đề**: Virtual Private Server (VPS)
* **Phần phụ**: Ảo Hóa & Thiết Lập Hạ Tầng Máy Chủ Cloud
* **Bố cục (Layout)**: Center (Tiêu đề căn giữa, nền tối sang trọng)
* **Ghi chú**: Rikkei Education · HSSF Deck

---

## SLIDE 2: MỤC TIÊU BUỔI HỌC (OBJECTIVES)
* **Tiêu đề**: Mục tiêu Session 02
* **Bố cục (Layout)**: Trái (Nội dung) | Phải (Ảnh minh họa/Card thông số)
* **Nội dung chính**:
  - Nắm vững cơ chế hoạt động của công nghệ ảo hóa (Virtualization) và Hypervisor.
  - Tự khởi tạo và cấu hình thành công Cloud VM (Ubuntu Server) qua SSH Key.
  - Vận hành tường lửa host-based (UFW) bảo vệ cổng kết nối máy chủ.
  - Cài đặt và triển khai thành công Web Server Nginx để phục vụ ứng dụng.

---

## SLIDE 3: LỘ TRÌNH CHI TIẾT (AGENDA)
* **Tiêu đề**: Lộ trình bài học
* **Bố cục (Layout)**: Timeline / Step list
* **Nội dung**:
  1. **Bài 1**: Khái niệm ảo hóa (Virtualization Basics)
  2. **Bài 2**: Khởi tạo Cloud Server thực tế
  3. **Bài 3**: Cơ chế bảo mật cho Infrastructure
  4. **Bài 4**: Cài đặt và cấu hình Web Server Nginx

---

## SLIDE 4: BÀI 1 - ĐẶT VẤN ĐỀ: MÁY CHỦ BARE-METAL TRUYỀN THỐNG
* **Tiêu đề**: Hạn chế của máy chủ vật lý (Bare-metal)
* **Bố cục (Layout)**: Split (Trái: Vấn đề | Phải: Tác hại/Hậu quả)
* **Nội dung**:
  - **Lãng phí tài nguyên**: Một ứng dụng thường chỉ dùng 10-15% CPU/RAM của server vật lý.
  - **Triển khai chậm chạp**: Phải mua sắm phần cứng, đi dây mạng, lắp tủ rack mất nhiều tuần.
  - **Thiếu tính độc lập (Isolation)**: Các ứng dụng chung máy chủ dễ bị xung đột thư viện và sập hàng loạt khi có sự cố.

---

## SLIDE 5: BÀI 1 - ĐỊNH NGHĨA CÔNG NGHỆ ẢO HÓA (VIRTUALIZATION)
* **Tiêu đề**: Ảo hóa là gì?
* **Bố cục (Layout)**: Center + Sơ đồ khối đơn giản
* **Nội dung**:
  - Là công nghệ tạo ra phiên bản ảo (logical) trên nền tảng hạ tầng vật lý.
  - Chèn một lớp phần mềm trung gian để trừu tượng hóa CPU, RAM, Disk, Network thành nhiều phần độc lập.
  - **Lịch sử**: Ra đời năm 1967 (Hệ điều hành CP-40 trên IBM Mainframe), bùng nổ năm 1998 nhờ VMware trên hệ x86.

---

## SLIDE 6: BÀI 1 - THÀNH PHẦN CỐT LÕI: HYPERVISOR (VMM)
* **Tiêu đề**: Bộ quản lý máy ảo (Hypervisor)
* **Bố cục (Layout)**: Content + Callout
* **Nội dung**:
  - Là phần mềm thực thi nhiệm vụ trừu tượng hóa và phân phối tài nguyên phần cứng.
  - **Quản lý phân quyền lệnh (CPU Rings)**: Kiểm soát lệnh nhạy cảm của hệ điều hành máy ảo (Guest OS) bằng phần mềm hoặc phần cứng hỗ trợ (Intel VT-x, AMD-V) để tránh phá vỡ an toàn tài nguyên vật lý.

---

## SLIDE 7: BÀI 1 - PHÂN LOẠI HYPERVISOR (TYPE 1 VS TYPE 2)
* **Tiêu đề**: So sánh Hypervisor Type 1 & Type 2
* **Bố cục (Layout)**: Compare (So sánh song song 2 cột)
* **Nội dung**:
  - **Type 1 (Bare-metal)**: Cài trực tiếp lên phần cứng (KVM, VMware ESXi). Hiệu năng cao, dùng cho Data Center/Cloud.
  - **Type 2 (Hosted)**: Chạy trên một OS có sẵn (VirtualBox, VMware Workstation). Dễ cài đặt, phù hợp cho môi trường phát triển/thực hành cá nhân.

---

## SLIDE 8: BÀI 2 - ĐẶT VẤN ĐỀ: TRIỂN KHAI TRÊN CLOUD
* **Tiêu đề**: Giải pháp Cloud VPS thay thế
* **Bố cục (Layout)**: Content + Tiêu đề phụ
* **Nội dung**:
  - Không cần lo lắng lắp đặt phần cứng, mua IP tĩnh hay cấu hình router vật lý.
  - Chỉ cần vài click chuột để có ngay một hệ điều hành máy chủ chạy độc lập, sẵn sàng trực tuyến trên Internet.

---

## SLIDE 9: BÀI 2 - KHÁI NIỆM VPS & CLOUD PROVIDERS
* **Tiêu đề**: Thuê máy chủ Cloud ở đâu?
* **Bố cục (Layout)**: Split (Trái: VPS là gì | Phải: Danh sách nhà cung cấp)
* **Nội dung**:
  - **VPS**: Phân chia từ máy vật lý lớn bằng KVM ảo hóa, cấp IP tĩnh công cộng riêng biệt.
  - **Nhà cung cấp quốc tế**: DigitalOcean, AWS, GCP, Azure, Linode.
  - **Nhà cung cấp Việt Nam**: VNG Cloud, Viettel IDC, FPT Smart Cloud.

---

## SLIDE 10: BÀI 2 - CÁC THÔNG SỐ KỸ THUẬT CỦA VPS
* **Tiêu đề**: Thông số cấu hình của Cloud Server
* **Bố cục (Layout)**: Grid (Mạng lưới 4 ô thông số)
* **Nội dung**:
  1. **vCPU**: Đơn vị xử lý ảo hóa.
  2. **RAM**: Bộ nhớ trong (Thiếu RAM sẽ bị kích hoạt cơ chế Out-Of-Memory (OOM) killer tắt ứng dụng).
  3. **Storage**: SSD/NVMe ảo hóa đọc ghi tốc độ cao.
  4. **Region/Zone**: Vị trí vật lý của Data Center (chọn gần Việt Nam như Singapore để giảm độ trễ).

---

## SLIDE 11: BÀI 2 - SSH KEY: CƠ CHẾ XÁC THỰC BẢO MẬT
* **Tiêu đề**: Xác thực SSH an toàn
* **Bố cục (Layout)**: Content với sơ đồ tương tác
* **Nội dung**:
  - Password dễ bị brute-force bằng botnet. SSH Key giải quyết triệt để lỗi bảo mật này.
  - Cơ chế dựa trên mật mã khóa công khai:
    - **Private Key (`id_ed25519`)**: Giữ bí mật tuyệt đối trên máy cá nhân.
    - **Public Key (`id_ed25519.pub`)**: Đẩy lên máy chủ VPS để xác minh kết nối.

---

## SLIDE 12: BÀI 3 - ĐẶT VẤN ĐỀ: MỐI ĐE DỌA KHÔNG GIAN MẠNG
* **Tiêu đề**: Nguy hiểm khi online mặc định
* **Bố cục (Layout)**: Center Callout (Cảnh báo nguy hiểm)
* **Nội dung**:
  - Ngay khi có IP Public, VPS của bạn sẽ bị quét bởi hàng triệu botnet tự động dò tìm lỗ hổng hoặc mật khẩu SSH mặc định.
  - Một máy chủ "thô" (unhardened) có thể bị hack chỉ sau vài giờ.

---

## SLIDE 13: BÀI 3 - GIA CỐ BẢO MẬT SSH (SSH HARDENING)
* **Tiêu đề**: Cấu hình bảo mật file sshd_config
* **Bố cục (Layout)**: Trái (Giải thích chỉ thị) | Phải (Code cấu hình mẫu)
* **Nội dung**:
  - `PasswordAuthentication no`: Cấm tuyệt đối đăng nhập bằng mật khẩu thường.
  - `PermitRootLogin no`: Không cho phép đăng nhập trực tiếp bằng tài khoản tối cao `root`. Phải đăng nhập qua non-root user và dùng `sudo`.

---

## SLIDE 14: BÀI 3 - CƠ CHẾ HOẠT ĐỘNG CỦA TƯỜNG LỬA (FIREWALL)
* **Tiêu đề**: Nguyên tắc hoạt động của Firewall
* **Bố cục (Layout)**: Content + Sơ đồ cổng kết nối
* **Nội dung**:
  - **Default Deny Incoming**: Chặn toàn bộ kết nối đi vào, trừ những cổng được mở tường minh.
  - **Default Allow Outgoing**: Cho phép máy chủ tự do kết nối ra ngoài tải bản cập nhật phần mềm.
  - **Phân loại**: Tường lửa cấp hệ điều hành (Host-based - UFW) và Tường lửa cấp đám mây (Network-based - Security Group).

---

## SLIDE 15: BÀI 3 - THỰC HÀNH CẤU HÌNH UFW TRÊN UBUNTU
* **Tiêu đề**: Quản trị tường lửa với UFW
* **Bố cục (Layout)**: Trái (Các bước thực thi) | Phải (Khối code bash shell)
* **Nội dung**:
  - Cho phép SSH trước khi bật UFW: `sudo ufw allow 22/tcp` hoặc `sudo ufw allow ssh`
  - Cho phép HTTP/HTTPS: `sudo ufw allow 80/tcp`, `sudo ufw allow 443/tcp`
  - Kích hoạt tường lửa: `sudo ufw enable`
  - Xem trạng thái: `sudo ufw status verbose`

---

## SLIDE 16: BÀI 4 - ĐẶT VẤN ĐỀ: PHÂN PHỐI LƯU LƯỢNG WEB
* **Tiêu đề**: Tại sao không chạy trực tiếp Application Server?
* **Bố cục (Layout)**: Split (Vấn đề và Giải pháp)
* **Nội dung**:
  - Các máy chủ ứng dụng thô (Node.js port 3000, Python Flask port 5000) xử lý file tĩnh rất kém và không chịu được tải lớn.
  - Phơi bày trực tiếp cổng ứng dụng nội bộ ra ngoài rất mất an toàn.
  - Khó chạy nhiều web app cùng chung cổng tiêu chuẩn 80/443.

---

## SLIDE 17: BÀI 4 - GIỚI THIỆU NGINX WEB SERVER
* **Tiêu đề**: Nginx - Engine X
* **Bố cục (Layout)**: Content + Callout
* **Nội dung**:
  - Là phần mềm Web Server mã nguồn mở, hoạt động theo cơ chế hướng sự kiện (event-driven) cực nhẹ.
  - Đóng vai trò là Reverse Proxy, HTTP Cache và bộ cân bằng tải (Load Balancer).
  - **Cổng tiêu chuẩn**: Port 80 (HTTP không mã hóa) và Port 443 (HTTPS mã hóa SSL/TLS).

---

## SLIDE 18: BÀI 4 - CẤU TRÚC THƯ MỤC NGINX TRÊN UBUNTU
* **Tiêu đề**: Cấu trúc cấu hình Nginx
* **Bố cục (Layout)**: List + Ghi chú
* **Nội dung**:
  - `/etc/nginx/nginx.conf`: File cấu hình chính toàn hệ thống.
  - `/etc/nginx/sites-available/`: File cấu hình cho từng site riêng biệt.
  - `/etc/nginx/sites-enabled/`: Chứa các symlink liên kết sang sites-available để active website.
  - `/var/www/html/`: Thư mục chứa code/HTML tĩnh mặc định.

---

## SLIDE 19: BÀI 4 - CẤU HÌNH SERVER BLOCK (VIRTUAL HOST)
* **Tiêu đề**: Chạy nhiều website trên 1 địa chỉ IP
* **Bố cục (Layout)**: Trái (Giải thích chỉ thị) | Phải (Nginx Server Block mẫu)
* **Nội dung**:
  - `listen 80`: Lắng nghe ở cổng 80.
  - `server_name`: Tên miền trỏ tới (ví dụ: `mywebsite.com`).
  - `root`: Đường dẫn thư mục chứa code tĩnh trên máy.
  - `index`: Xác định file ưu tiên chạy trước (như `index.html`).

---

## SLIDE 20: BÀI 4 - THIẾT LẬP HTTP BASIC AUTHENTICATION
* **Tiêu đề**: Bảo mật lớp ngoài bằng Basic Auth
* **Bố cục (Layout)**: Content + Code shell
* **Nội dung**:
  - Yêu cầu điền tài khoản và mật khẩu trực tiếp trên popup của trình duyệt trước khi vào trang web.
  - Dùng chỉ thị: `auth_basic` và `auth_basic_user_file`.
  - Tạo file lưu thông tin mật khẩu băm thông qua công cụ `htpasswd` (`sudo apt install apache2-utils`).

---

## SLIDE 21: NGUYÊN TẮC GIỚI HẠN (REDUNDANCY RULE)
* **Tiêu đề**: Giới hạn phạm vi Session 02
* **Bố cục (Layout)**: Center Callout (Cảnh báo đỏ)
* **Nội dung**:
  - *Chỉ tập trung hướng dẫn khởi tạo cloud server, bảo mật SSH/Firewall cơ bản và cấu hình web tĩnh bằng Nginx.*
  - **TUYỆT ĐỐI KHÔNG triệt tiêu**: Không dạy viết script hoặc dùng CI/CD tự động deploy ứng dụng Java/Node.js lên VPS trong buổi này để tránh loãng nội dung.

---

## SLIDE 22: KẾT THÚC BUỔI HỌC
* **Tiêu đề**: Rikkei Academy - Rikkei Education
* **Nội dung**: Học viện đào tạo lập trình chất lượng Nhật Bản. Hẹn gặp lại trong Session 3!
* **Bố cục (Layout)**: Brand End Slide chuẩn.
