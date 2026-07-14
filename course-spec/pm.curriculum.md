---
schema_version: 1
id: pm_curriculum
type: meta
meta_kind: pm_curriculum
course_id: devops-basic
title: "DevOps Basics"
language: vi
version: 1
status: approved
format: structured
---

# PM — Course Curriculum

## Session 02: Virtual Private Server (VPS)

```yaml
session: 2
id: ss02
title: "Virtual Private Server (VPS)"
session_kind: theory
depends_on_sessions: []
builds_on_sessions: []
enables_sessions: [3, 6, 9, 10]
owns_concepts:
  - virtualization-basics
  - cloud-server-provisioning
  - infrastructure-security
  - nginx-basic-setup
assumes_concepts: []
does_not_cover:
  - vps-deploy
redundancy_rules:
  - "Chỉ hướng dẫn khởi tạo cloud server và cấu hình Nginx cơ bản; không dạy deploy code thủ công hay tự động ở session này."
lessons:
  - unit: 1
    id: ss02_lesson_01
    title: "Khái niệm ảo hóa (Virtualization)"
    owns: [virtualization-basics]
    assumes: []
  - unit: 2
    id: ss02_lesson_02
    title: "Khởi tạo Cloud Server thực tế"
    owns: [cloud-server-provisioning]
    assumes: [virtualization-basics]
  - unit: 3
    id: ss02_lesson_03
    title: "Cơ chế bảo mật cho Infrastructure"
    owns: [infrastructure-security]
    assumes: [cloud-server-provisioning]
  - unit: 4
    id: ss02_lesson_04
    title: "Cài đặt và cấu hình Web Server Nginx"
    owns: [nginx-basic-setup]
    assumes: [infrastructure-security]
tutorial:
  required: true
  step_count: 6
homework:
  required: true
  exercise_count: 6
```

## Session 03: Thực hành thao tác với Virtual Private Server (VPS)

```yaml
session: 3
id: ss03
title: "Thực hành thao tác với Virtual Private Server (VPS)"
session_kind: practice
practice_of: [2]
depends_on_sessions: [2]
owns_concepts: []
assumes_concepts: []
does_not_cover: []
lessons: []
homework:
  required: true
  exercise_count: 6
  only_artifact: true
  coverage_rule: "every session in practice_of appears in >=1 EX"
  difficulty: "harder and longer than theory sessions"
  design_notes:
    - "Độ khó và thời lượng làm bài phải cao hơn so với các bài tập của session lý thuyết (Session 02)."
    - "Tập trung vào các kịch bản thực tế phức tạp, cấu hình nâng cao và tự động xử lý/khắc phục sự cố (troubleshooting)."

```

## Session 04: Git, GitHub

```yaml
session: 4
id: ss04
title: "Git, GitHub"
session_kind: theory
depends_on_sessions: []
builds_on_sessions: []
enables_sessions: [5, 11]
owns_concepts:
  - git-local-basics
  - git-branching-conflicts
  - git-remote-github
  - git-advanced-history
assumes_concepts: []
does_not_cover: []
lessons:
  - unit: 1
    id: ss04_lesson_01
    title: "Khởi tạo và thao tác cơ bản với Git (Local)"
    owns: [git-local-basics]
    assumes: []
  - unit: 2
    id: ss04_lesson_02
    title: "Quản lý Nhánh (Branching) và xử lý Xung đột"
    owns: [git-branching-conflicts]
    assumes: [git-local-basics]
  - unit: 3
    id: ss04_lesson_03
    title: "Làm việc Từ xa với GitHub và quy trình Teamwork"
    owns: [git-remote-github]
    assumes: [git-branching-conflicts]
  - unit: 4
    id: ss04_lesson_04
    title: "Kỹ thuật Git nâng cao và quản lý lịch sử"
    owns: [git-advanced-history]
    assumes: [git-remote-github]
tutorial:
  required: true
  step_count: 6
homework:
  required: true
  exercise_count: 6
```

## Session 05: Thực hành thao tác với Git, GitHub

```yaml
session: 5
id: ss05
title: "Thực hành thao tác với Git, GitHub"
session_kind: practice
practice_of: [4]
depends_on_sessions: [4]
owns_concepts: []
assumes_concepts: []
does_not_cover: []
lessons: []
homework:
  required: true
  exercise_count: 6
  only_artifact: true
  coverage_rule: "every session in practice_of appears in >=1 EX"
  difficulty: "harder and longer than theory sessions"
  design_notes:
    - "Độ khó và thời lượng làm bài phải cao hơn so với các bài tập của session lý thuyết (Session 04)."
    - "Tập trung vào giải quyết các bài toán teamwork thực tế, giải quyết xung đột (conflict resolution) và các kịch bản Git nâng cao."
```

## Session 06: Linux CLI & Networking

```yaml
session: 6
id: ss06
title: "Linux CLI & Networking"
session_kind: theory
depends_on_sessions: [2]
builds_on_sessions: []
enables_sessions: [7, 9]
owns_concepts:
  - linux-architecture
  - linux-user-group-management
  - linux-networking-basics
  - linux-process-management
assumes_concepts:
  - cloud-server-provisioning
does_not_cover: []
lessons:
  - unit: 1
    id: ss06_lesson_01
    title: "Kiến trúc hệ điều hành Linux"
    owns: [linux-architecture]
    assumes: [cloud-server-provisioning]
  - unit: 2
    id: ss06_lesson_02
    title: "Quản lý User, Group trên Ubuntu Server"
    owns: [linux-user-group-management]
    assumes: [linux-architecture]
  - unit: 3
    id: ss06_lesson_03
    title: "Quản lý Network trên Ubuntu Server"
    owns: [linux-networking-basics]
    assumes: [linux-architecture]
  - unit: 4
    id: ss06_lesson_04
    title: "Quản lý Process trên Ubuntu Server"
    owns: [linux-process-management]
    assumes: [linux-architecture]
tutorial:
  required: true
  step_count: 6
homework:
  required: true
  exercise_count: 6
```

## Session 07: Thực hành thao tác với Linux CLI, Networking

```yaml
session: 7
id: ss07
title: "Thực hành thao tác với Linux CLI, Networking"
session_kind: practice
practice_of: [6]
depends_on_sessions: [6]
owns_concepts: []
assumes_concepts: []
does_not_cover: []
lessons: []
homework:
  required: true
  exercise_count: 6
  only_artifact: true
  coverage_rule: "every session in practice_of appears in >=1 EX"
  difficulty: "harder and longer than theory sessions"
  design_notes:
    - "Độ khó và thời lượng làm bài phải cao hơn so với các bài tập của session lý thuyết (Session 06)."
    - "Thiết kế các bài toán quản trị hệ thống phức tạp, tối ưu hóa mạng và xử lý sự cố Process/Network trên môi trường Ubuntu Server thực tế."
```

## Session 08: Hackathon

```yaml
session: 8
id: ss08
title: "Hackathon (Thi giữa môn)"
session_kind: practice
practice_of: []
depends_on_sessions: []
owns_concepts: []
assumes_concepts: []
does_not_cover: []
lessons: []
homework:
  required: false
  exercise_count: 0
  note: "Tạm thời để trống - Thi giữa môn"
```

## Session 09: Docker & Containerization

```yaml
session: 9
id: ss09
title: "Docker & Containerization"
session_kind: theory
depends_on_sessions: [2, 6]
builds_on_sessions: []
enables_sessions: [10, 11]
owns_concepts:
  - docker-vs-vm
  - dockerfile-single-stage
  - dockerfile-multi-stage
  - docker-networks-volumes
  - docker-compose-orchestration
assumes_concepts:
  - virtualization-basics
  - linux-architecture
does_not_cover: []
lessons:
  - unit: 1
    id: ss09_lesson_01
    title: "Khác biệt giữa Virtual Machine và Container"
    owns: [docker-vs-vm]
    assumes: [virtualization-basics]
  - unit: 2
    id: ss09_lesson_02
    title: "Viết Dockerfile để đóng gói ứng dụng Single-stage"
    owns: [dockerfile-single-stage]
    assumes: [docker-vs-vm]
  - unit: 3
    id: ss09_lesson_03
    title: "Viết Dockerfile để đóng gói ứng dụng Multi-stage"
    owns: [dockerfile-multi-stage]
    assumes: [dockerfile-single-stage]
  - unit: 4
    id: ss09_lesson_04
    title: "Quản lý Docker Networking, lưu trữ dữ liệu với Docker Volumes"
    owns: [docker-networks-volumes]
    assumes: [docker-vs-vm, linux-networking-basics]
  - unit: 5
    id: ss09_lesson_05
    title: "Định nghĩa và điều phối hệ thống đa thành phần với Docker Compose"
    owns: [docker-compose-orchestration]
    assumes: [docker-networks-volumes, dockerfile-single-stage]
tutorial:
  required: true
  step_count: 6
homework:
  required: true
  exercise_count: 6
```

## Session 10: Thực hành thao tác với Docker, Containerization

```yaml
session: 10
id: ss10
title: "Thực hành thao tác với Docker, Containerization"
session_kind: practice
practice_of: [9]
depends_on_sessions: [9]
owns_concepts: []
assumes_concepts: []
does_not_cover: []
lessons: []
homework:
  required: true
  exercise_count: 6
  only_artifact: true
  coverage_rule: "every session in practice_of appears in >=1 EX"
  difficulty: "harder and longer than theory sessions"
  design_notes:
    - "Độ khó và thời lượng làm bài phải cao hơn so với các bài tập của session lý thuyết (Session 09)."
    - "Các bài tập yêu cầu tối ưu hóa Dockerfile, debug lỗi container, cấu hình volume/network phức tạp và triển khai multi-container qua Docker Compose."
```

## Session 11: CI/CD Pipeline

```yaml
session: 11
id: ss11
title: "CI/CD Pipeline"
session_kind: theory
depends_on_sessions: [4, 9]
builds_on_sessions: []
enables_sessions: [12]
owns_concepts:
  - cicd-core-concepts
  - ci-workflow-design
  - cd-workflow-design
  - pipeline-scripting
assumes_concepts:
  - git-remote-github
  - docker-compose-orchestration
does_not_cover: []
lessons:
  - unit: 1
    id: ss11_lesson_01
    title: "Khái niệm cốt lõi của CI và CD"
    owns: [cicd-core-concepts]
    assumes: []
  - unit: 2
    id: ss11_lesson_02
    title: "Thiết kế quy trình CI tự động"
    owns: [ci-workflow-design]
    assumes: [cicd-core-concepts, git-remote-github]
  - unit: 3
    id: ss11_lesson_03
    title: "Thiết kế quy trình CD tự động"
    owns: [cd-workflow-design]
    assumes: [cicd-core-concepts, git-remote-github]
  - unit: 4
    id: ss11_lesson_04
    title: "Viết file kịch bản Pipeline hoàn chỉnh"
    owns: [pipeline-scripting]
    assumes: [ci-workflow-design, cd-workflow-design, docker-compose-orchestration]
tutorial:
  required: true
  step_count: 6
homework:
  required: true
  exercise_count: 6
```

## Session 12: Thực hành thao tác với CI/CD Pipeline (GitHub Actions)

```yaml
session: 12
id: ss12
title: "Thực hành thao tác với CI/CD Pipeline (GitHub Actions)"
session_kind: practice
practice_of: [11]
depends_on_sessions: [11]
owns_concepts: []
assumes_concepts: []
does_not_cover: []
lessons: []
homework:
  required: true
  exercise_count: 6
  only_artifact: true
  coverage_rule: "every session in practice_of appears in >=1 EX"
  difficulty: "harder and longer than theory sessions"
  design_notes:
    - "Độ khó và thời lượng làm bài phải cao hơn so với các bài tập của session lý thuyết (Session 11)."
    - "Bài tập tập trung vào việc tự động hóa hoàn chỉnh quy trình CI/CD tích hợp Docker, xử lý lỗi pipeline thực tế trên GitHub Actions."
```

## Session 13: Mini Project tổng hợp

```yaml
session: 13
id: ss13
title: "Mini Project tổng hợp"
session_kind: practice
practice_of: [2, 4, 6, 9, 11]
depends_on_sessions: [3, 5, 7, 10, 12]
owns_concepts: []
assumes_concepts: []
does_not_cover: []
lessons: []
homework:
  required: true
  exercise_count: 6
  only_artifact: true
  coverage_rule: "every session in practice_of appears in >=1 EX"
  difficulty: "harder and longer than theory sessions"
  design_notes:
    - "Mini Project tổng hợp kiểm tra khả năng tích hợp toàn bộ các kỹ năng cốt lõi đã học (VPS, Git, Linux, Docker, CI/CD)."
    - "Yêu cầu xây dựng và vận hành một luồng phân phối tự động hóa end-to-end hoàn chỉnh."
```

## Session 14: Ôn tập cuối môn

```yaml
session: 14
id: ss14
title: "Ôn tập cuối môn"
session_kind: practice
practice_of: [2, 4, 6, 9, 11]
depends_on_sessions: [13]
owns_concepts: []
assumes_concepts: []
does_not_cover: []
lessons: []
homework:
  required: true
  exercise_count: 6
  only_artifact: true
  coverage_rule: "every session in practice_of appears in >=1 EX"
  difficulty: "harder and longer than theory sessions"
  design_notes:
    - "Ôn tập cuối môn kiểm tra toàn diện, mô phỏng các dạng đề thi lý thuyết và thực hành chính thức với yêu cầu khắt khe về thời gian và độ chuẩn xác."
```

## Concept registry

```yaml
concepts:
  - id: virtualization-basics
    label: "Khái niệm ảo hóa (Virtualization)"
    introduced_in: ss02_lesson_01
  - id: cloud-server-provisioning
    label: "Khởi tạo Cloud Server thực tế"
    introduced_in: ss02_lesson_02
  - id: infrastructure-security
    label: "Cơ chế bảo mật cho Infrastructure"
    introduced_in: ss02_lesson_03
  - id: nginx-basic-setup
    label: "Cài đặt và cấu hình Web Server Nginx"
    introduced_in: ss02_lesson_04
  - id: git-local-basics
    label: "Khởi tạo và thao tác cơ bản với Git (Local)"
    introduced_in: ss04_lesson_01
  - id: git-branching-conflicts
    label: "Quản lý Nhánh (Branching) và xử lý Xung đột"
    introduced_in: ss04_lesson_02
  - id: git-remote-github
    label: "Làm việc Từ xa với GitHub và quy trình Teamwork"
    introduced_in: ss04_lesson_03
  - id: git-advanced-history
    label: "Kỹ thuật Git nâng cao và quản lý lịch sử"
    introduced_in: ss04_lesson_04
  - id: linux-architecture
    label: "Kiến trúc hệ điều hành Linux"
    introduced_in: ss06_lesson_01
  - id: linux-user-group-management
    label: "Quản lý User, Group trên Ubuntu Server"
    introduced_in: ss06_lesson_02
  - id: linux-networking-basics
    label: "Quản lý Network trên Ubuntu Server"
    introduced_in: ss06_lesson_03
  - id: linux-process-management
    label: "Quản lý Process trên Ubuntu Server"
    introduced_in: ss06_lesson_04
  - id: docker-vs-vm
    label: "Khác biệt giữa Virtual Machine và Container"
    introduced_in: ss09_lesson_01
  - id: dockerfile-single-stage
    label: "Viết Dockerfile để đóng gói ứng dụng Single-stage"
    introduced_in: ss09_lesson_02
  - id: dockerfile-multi-stage
    label: "Viết Dockerfile để đóng gói ứng dụng Multi-stage"
    introduced_in: ss09_lesson_03
  - id: docker-networks-volumes
    label: "Quản lý Docker Networking, lưu trữ dữ liệu với Docker Volumes"
    introduced_in: ss09_lesson_04
  - id: docker-compose-orchestration
    label: "Định nghĩa và điều phối hệ thống đa thành phần với Docker Compose"
    introduced_in: ss09_lesson_05
  - id: cicd-core-concepts
    label: "Khái niệm cốt lõi của CI và CD"
    introduced_in: ss11_lesson_01
  - id: ci-workflow-design
    label: "Thiết kế quy trình CI tự động"
    introduced_in: ss11_lesson_02
  - id: cd-workflow-design
    label: "Thiết kế quy trình CD tự động"
    introduced_in: ss11_lesson_03
  - id: pipeline-scripting
    label: "Viết file kịch bản Pipeline hoàn chỉnh"
    introduced_in: ss11_lesson_04
```