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

| | **Tutorial** | **Homework** |
|--|--------------|--------------|
| Scope | **Theory session only** | Theory + practice |
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
