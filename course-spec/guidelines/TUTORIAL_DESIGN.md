---
schema_version: 1
id: tutorial_design_v1
type: meta
meta_kind: tutorial_design
title: "Tutorial / Step-by-step Lab Design"
status: approved
language: vi
course_note: "DevOps Basics (k24-ptit-devops) — tutorial CHỈ session theory; practice = homework only"
---

# Tutorial Design v1 — Step-by-step lab

Mỗi session **`session_kind: theory`** có **đúng 1** unit `type: tutorial` (lab cầm tay chỉ việc), **ngoài** homework 6 EX.

### Nguyên tắc cốt lõi (Core Principles)
1. **Happy-path cực đơn giản:** Lab tutorial chỉ đi theo một con đường duy nhất thành công (happy path) với các bước cơ bản nhất. **Không cần bao quát toàn bộ nội dung lý thuyết hay tất cả các khía cạnh bảo mật/nâng cao của session**.
2. **Trực quan & thú vị:** Tập trung vào kết quả hiển thị trực quan nhanh nhất (ví dụ: nhìn thấy trang web hoạt động ngay) để tạo cảm hứng và động lực học tập cho học viên.
3. **Phân chia vai trò rõ ràng:** 
   * **Tutorial:** Trải nghiệm cơ bản, nhanh chóng, ít rào cản.
   * **Homework:** Nơi thực hành chuyên sâu, bao hàm tất cả các ràng buộc bảo mật, các góc khuất kỹ thuật và các lỗi thực tế.

| | **Tutorial** | **Homework** |
|--|--------------|--------------|
| Scope | **Theory session only** (Happy-path cơ bản, trực quan) | Theory + practice (Bao phủ đầy đủ nội dung & nâng cao) |
| / session theory | **1 file** `session_NN_tutorial.md` | 1 file, **6 EX** |
| Practice session | **Không có** | **6 EX** (only artifact) |
| MCP | `unit_type: tutorial` (alias `step_by_step`) | `homework` |

## Thứ tự gen (theory)

Lessons → **tutorial** → homework → quiz phase  

## Practice

**Không tutorial.** Chỉ homework 6 EX. Không lesson.

## PM (theory only)

```yaml
tutorial:
  required: true
  title: "Lab: Khởi tạo VPS và Nginx cơ bản"
  step_count: 6
```

Session practice: **không** khai `tutorial` (hoặc `required: false`).

## Body sections

`overview` · `prerequisites` · `step_01`…`step_NN` (≥3) · `verify` · `pitfalls` · `next`

## Ảnh — DevOps Basics

Agent **không** generate ảnh. Chèn:

```markdown
> **[IMAGE NEEDED]** Mô tả: ví dụ trang tạo droplet sau khi chọn region.
> Gợi ý path: `assets/ss02/step_02_create_droplet.png`
```

## MCP

```
start_unit(session_number=2, unit_type="tutorial", step_count=6)
# session practice → error nếu gọi tutorial
```
