---
schema_version: 1
id: ss01_lesson_01
type: lesson
status: approved
course_id: devops-basic
session: 1
unit: 1
title: Định hướng môn học DevOps in Action
session_kind: theory
tags:
- devops
- introduction
concepts:
- devops-introduction
depends_on: []
builds_on: []
enables:
- ss02_lesson_01
owns:
- devops-introduction
assumes: []
does_not_cover: []
source: generated
pm_ref: Session 01 / Lesson 01
language: vi
created: '2026-07-15'
updated: '2026-07-15'
lesson_mode: theory
---

# Định hướng môn học DevOps in Action

<!-- section: objectives -->
## 1. Mục tiêu
*   Hiểu rõ định nghĩa cơ bản và vai trò của văn hóa **DevOps** trong chu kỳ phát triển phần mềm hiện đại.
*   Nắm bắt lộ trình học tập, cấu trúc các session và các công cụ thực hành chính trong khóa học.
*   Biết cách thiết lập tâm thế và chuẩn bị môi trường học tập hiệu quả.

<!-- section: problem -->
## 2. Đặt vấn đề
Trong mô hình phát triển phần mềm truyền thống, hai bộ phận **Development (Phát triển - Dev)** và **Operations (Vận hành - Ops)** thường hoạt động cô lập (mô hình Silo):
*   **Dev:** Tập trung vào viết tính năng mới thật nhanh và chuyển giao cho Ops.
*   **Ops:** Tập trung vào sự ổn định của hệ thống, dẫn đến việc e ngại thay đổi và hạn chế triển khai mã nguồn mới.

Sự thiếu đồng bộ này tạo ra "bức tường hoang mang" (Wall of Confusion), kéo dài thời gian phát hành ứng dụng (Time-to-market) và làm giảm chất lượng phần mềm. Để giải quyết nút thắt này, văn hóa và phương pháp luận **DevOps** đã ra đời.

<!-- section: core -->
## 3. Kiến thức cốt lõi

### 3.1. DevOps là gì?
**DevOps** không phải là một công cụ cụ thể hay một chức danh công việc đơn thuần. DevOps là sự kết hợp của **Văn hóa (Culture)**, **Quy trình (Process)** và **Công cụ (Tools)** nhằm rút ngắn chu kỳ phát triển, tăng tần suất triển khai và đảm bảo chất lượng phần mềm ổn định.

Mô hình DevOps thường được biểu diễn bằng hình vô cực (infinity loop) bao gồm các giai đoạn liên tục:
1.  **Plan:** Lên kế hoạch và định nghĩa yêu cầu.
2.  **Code:** Phát triển mã nguồn ứng dụng.
3.  **Build:** Biên dịch và đóng gói ứng dụng.
4.  **Test:** Kiểm thử chất lượng phần mềm.
5.  **Release:** Đóng gói phiên bản phát hành.
6.  **Deploy:** Triển khai ứng dụng lên môi trường chạy thực tế (Cloud, Server).
7.  **Operate:** Vận hành và giám sát hệ thống.
8.  **Monitor:** Theo dõi hiệu năng và phản hồi của người dùng để tiếp tục cải tiến.

### 3.2. Lộ trình học tập khóa học DevOps Basics
Khóa học này tập trung cung cấp các kiến thức thực chiến nền tảng bao gồm:
*   **Hạ tầng (Infrastructure):** Virtual Private Server (VPS), quản trị người dùng, bảo mật tường lửa UFW và máy chủ Web Nginx.
*   **Quản lý mã nguồn (Source Control):** Thành thạo Git, xử lý xung đột nhánh (conflict) và làm việc nhóm qua GitHub.
*   **Tự động hóa (Automation/CI-CD):** Tự động hóa kiểm thử, đóng gói ứng dụng Java Spring Boot bằng Docker và xây dựng quy trình CI/CD qua GitHub Actions.
*   **Giám sát (Monitoring):** Cài đặt công nghệ giám sát hệ thống thời gian thực với Prometheus và Grafana.

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
*   **Đồng nhất DevOps chỉ là cài đặt công cụ:** Việc cài đặt Jenkins, Docker hay Kubernetes mà không thay đổi quy trình làm việc phối hợp giữa Dev và Ops sẽ không đem lại hiệu quả DevOps thực tế.
*   **Học thụ động không thực hành:** DevOps là kỹ năng thực chiến. Nếu không tự tay gõ lệnh, thiết lập máy chủ và debug lỗi, học viên sẽ không thể làm chủ được kỹ năng này.

<!-- section: references -->
## 5. Tài liệu tham khảo
*   [The Phoenix Project (Sách về văn hóa DevOps)](https://itrevolution.com/book/the-phoenix-project/)
*   [Atlassian DevOps Overview](https://www.atlassian.com/devops)
