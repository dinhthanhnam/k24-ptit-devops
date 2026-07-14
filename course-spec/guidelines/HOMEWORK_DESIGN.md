---
schema_version: 1
id: homework_design_v1
type: meta
meta_kind: homework_design
title: "Homework Design Specification (universal)"
status: approved
language: vi
---

# Homework Design Specification v1 (universal)

Spec **khách quan** — không gắn sản phẩm/domain cụ thể.  
Môn học có thể thêm file `homework.design.override.md` (số bài, context, tiêu chí bảo mật riêng).

---

## 1. Mục tiêu

Homework kiểm tra **kỹ năng thực hành** đã teach trong session, không kiểm tra thuộc lòng định nghĩa.

Nguyên tắc:

1. **Actionable** — động từ hành động: cấu hình được, chạy được, sửa được, đo được.  
2. **Verifiable** — có bước kiểm tra + evidence rõ.  
3. **Scaffolded** — giảm dần scaffolding theo độ khó.  
4. **Domain-pluggable** — ngữ cảnh (tên app, stack) do course override, không hard-code trong core.  

---

## 2. Hai loại session → hai cách dùng homework

| `session_kind` | Vai trò session | Nội dung gen | Homework |
|----------------|-----------------|--------------|----------|
| `theory` | Dạy concept / skill mới | Lessons (+ optional quiz) + homework | Ôn **trong** session đó |
| `practice` | Tiết thực hành / ôn tập (vd ss03, ss06) | **Không lesson, không “bài giảng”** | **6 bài = toàn bộ session** — tổng hợp các session trong `practice_of` |

Cùng một **cơ cấu 6 bài / 3 tier** (§3). Khác nhau ở **phạm vi `maps_to_*`** và **nguồn prior**.

---

## 3. Cơ cấu mặc định (có thể override)

Mọi session (cả `theory` và `practice`) mặc định **6 exercises**:

| Tier | id | Số bài | Scaffolding | Đánh giá |
|------|-----|--------|-------------|----------|
| Guided | `guided` | 4 | Step-by-step | Pass / Fail |
| Hints | `hints` | 1 | Gợi ý / keywords only | Pass / Fail |
| Independent | `independent` | 1 | Chỉ outcome + constraints | Pass / Fail |

Override example (trong course-spec):

```yaml
homework_defaults:
  exercise_count: 6
  mix: { guided: 4, hints: 1, independent: 1 }
```

---

## 4. Homework cho session `theory`

- Scope: skill/concept **owns** trong session hiện tại (lessons đã teach, ideally approved).  
- Mỗi EX: `maps_to_lessons` ⊆ lessons của **cùng** session.  
- Independent: được `assumes` nhẹ session trước (approved only).  
- File: `sessions/ss{NN}/session_{NN}_homework.md` với `session_kind: theory`.

---

## 5. Homework cho session `practice` (tiết ôn / lab tổng hợp)

Đây là trường hợp **ss03 ôn ss01+ss02**, **ss06 ôn ss04+ss05**, v.v.

### 5.1 Định nghĩa

- Session **không** có file lesson / quiz nội dung giảng.  
- Artifact duy nhất cần gen + review: **`session_{NN}_homework.md`** (6 EX).  
- PM: `session_kind: practice`, `practice_of: [A, B, …]` (các session lý thuyết được tổng hợp).  
- Mọi concept/skill trong bài tập phải lấy từ **union** nội dung đã **approved** của `practice_of` — **không** introduce concept mới (`owns: []` ở cấp file).

### 5.2 Phân bổ coverage (khuyến nghị, có thể override)

Mục tiêu: **bao phủ cả các session được ôn**, không lệch hết sang một session.

| Pattern | Khi `practice_of` có 2 sessions (phổ biến) |
|---------|------------------------------------------|
| Guided EX1–EX2 | Thiên về session A (session nhỏ hơn / sớm hơn) |
| Guided EX3–EX4 | Thiên về session B |
| Hints EX5 | **Xâu chuỗi A+B** (một bài đụng cả hai) |
| Independent EX6 | **Tích hợp A+B** (outcome gộp, ít scaffold) |

Khi `practice_of` có 3+ sessions: chia guided theo round-robin hoặc theo trọng số PM; **ít nhất 1 EX** phải multi-session (hints hoặc independent).

Mỗi EX bắt buộc khai báo:

```markdown
- **maps_to_sessions:** [1, 2]          # subset của practice_of; multi-session nếu tích hợp
- **maps_to_lessons:** [ss01_lesson_02, ss02_lesson_04]
```

- `maps_to_sessions` ⊆ `practice_of`  
- `maps_to_lessons` phải thuộc các session đó (unit approved)  
- Cấm `maps_to_lessons` trỏ session ngoài `practice_of`

### 5.3 Nguồn prior khi gen (skill / MCP)

```
get_prior_content / search  →  CHỈ units approved ∈ practice_of
get_session_blueprint(practice session) → lessons: [] ; homework_only: true
```

LLM **không** viết lại lý thuyết; chỉ thiết kế đề bài vận dụng.

### 5.4 Frontmatter file (practice)

Xem `FRONTMATTER_SCHEMA` — các field: `session_kind: practice`, `practice_of`, `maps_to_sessions`, `owns: []`.

### 5.5 Anti-patterns (FAIL validate)

1. Tạo `session_*_lesson_*.md` trong session `practice`.  
2. EX chỉ cover 1 session trong khi `practice_of` có 2+ **và** không có EX nào multi-session.  
3. EX yêu cầu skill/concept **chưa** taught trong `practice_of`.  
4. Dạy concept mới trong phần Requirements (“trước hết hãy tìm hiểu X…” dài → thuộc theory session khác).  
5. Trùng nguyên đề EX đã có trong homework của session A/B (được **biến tấu / gộp**, không copy nguyên).

### 5.6 Definition of done — session practice

- [ ] Không có lesson files  
- [ ] Đúng 6 EX, mix tier mặc định  
- [ ] Coverage: mọi session trong `practice_of` xuất hiện trong ≥1 EX  
- [ ] ≥1 EX multi-session nếu `|practice_of| ≥ 2`  
- [ ] validate + reembed + human → `approved`  

---

## 6. Cấu trúc một exercise (format nộp/gen)

Mỗi exercise trong `session_NN_homework.md` (dùng chung theory & practice):

```markdown
### EX{n} — {title}
- **tier:** guided | hints | independent
- **maps_to_sessions:** [7]                 # theory: [current]; practice: subset of practice_of
- **maps_to_lessons:** [ss07_lesson_02, ss07_lesson_03]
- **owns_skills:** [edit-ci-yaml]           # skill vận dụng; practice: không dual-own concept registry
- **assumes:** [ci-cd-basics]

#### Objectives
- ...

#### Requirements
- Context: {placeholder: course_context}
- Constraints: ...

#### Verification
- Commands / checks: ...
- Expected signals: ...
- Evidence: screenshot | log | file path

#### Submission
- Path: `homework/session_NN/ex{n}/...`
- Required files: ...

#### Scaffolding
<!-- guided: steps; hints: bullet hints; independent: omit or "none" -->
```

Frontmatter file homework: xem `FRONTMATTER_SCHEMA` (`type: homework`).

---

## 7. Pass / Fail criteria (universal)

Pass khi **tất cả** đúng:

1. **Runs** — artifact chạy/áp dụng được trên môi trường chuẩn course (định nghĩa per-course).  
2. **Meets constraints** — không vi phạm ràng buộc (secrets, path, tool allowlist).  
3. **Evidence complete** — đủ minh chứng Verification yêu cầu.  
4. **Structure** — đúng layout submission.  

Per-course **được** thêm criterion (ví dụ non-root user) trong override — không đưa vào core như bắt buộc toàn cục.

---

## 8. Anti-redundancy với lesson

### Theory session
- `maps_to_lessons` ⊆ session hiện tại.  
- Không yêu cầu skill thuộc `does_not_cover` của session.  
- Independent: chạm nhẹ session trước (**assumes** approved only).  

### Practice session
- `maps_to_lessons` ⊆ union lessons của `practice_of` (approved).  
- Không mở rộng ra session sau `practice_of`.  
- Ưu tiên bài **tích hợp / vận dụng**, không nhái 100% EX đã giao ở session lý thuyết.

---

## 9. Indexing

Chunk theo `EX{n}`; metadata: `tier`, `maps_to_lessons`, `maps_to_sessions`, `session`, `session_kind`.
