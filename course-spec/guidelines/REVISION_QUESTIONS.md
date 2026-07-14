---
schema_version: 1
id: revision_questions_format_v1
type: meta
meta_kind: revision_questions
title: "Revision Questions (post-lesson)"
status: approved
language: vi
---

# Revision Questions v1

File **bắt buộc** đi kèm mỗi lesson (`maps_to` đúng 1 lesson).  
**Không** optional, **không** nhúng trong body lesson.

---

## 1. Mục đích (duy nhất)

Sau khi sinh viên **đọc xong lesson**, họ trả lời vài câu **mở** để:

- kiểm tra đã nắm ý chính / áp dụng được ý chính;
- chuẩn bị thảo luận hoặc tự ôn.

Không thay quiz MCQ (`QUIZ_FORMAT`). Không cần ma trận Bloom / rubric cứng.

---

## 2. Số lượng

- **2 hoặc 3 câu** (`## RQ1` … `## RQ2` hoặc `## RQ3`).  
- Không bắt buộc đúng 3; không bắt buộc “3 mức”.  
- Đủ để trả lời **vấn đề/câu hỏi cốt lõi** sau khi đọc lesson — không nhồi quá nhiều.

---

## 3. Cách viết (lỏng)

- Tiếng Việt; gắn `owns` / nội dung lesson `maps_to`.  
- Open-ended (không A/B/C/D).  
- `theory` lesson → giải thích / liên hệ / áp dụng khái niệm.  
- `practical` lesson → mô tả làm gì, xử lý tình huống lab, hoặc giải thích step.  
- Có thể thêm gợi ý ngắn tùy ý — **không** bắt buộc `@level` / `@rubric` / `@concept`.

---

## 4. Cú pháp tối thiểu

```markdown
---
schema_version: 1
id: ss01_revision_01
type: revision_questions
status: draft
session: 1
session_kind: theory
unit: 1
title: "Ôn — Lesson 01 …"
maps_to: [ss01_lesson_01]
lesson_mode: theory
question_count: 2                  # 2 hoặc 3
language: vi
---

# Ôn sau bài: {lesson title}

## RQ1

{câu hỏi}

## RQ2

{câu hỏi}

## RQ3

{optional — nếu question_count: 3}
```

---

## 5. Path / id

```
sessions/ss{NN}/session_{NN}_revision_{MM}.md
id: ss{NN}_revision_{MM}
```

`start_unit(session, unit_type=revision_questions, unit=MM)`.

---

## 6. Indexing

Mỗi `## RQn` = 1 chunk; metadata: `maps_to`, `lesson_mode`.
