# Frontmatter Schema v1 (universal)

Mục tiêu: mọi unit (lesson, quiz, homework, review) là file Markdown + YAML frontmatter kiểu Obsidian — **parse được, index được, query được** không cần đọc full body.

`schema_version: 1` bắt buộc trên mọi file content.

---

## 1. Trường chung (mọi loại unit)

```yaml
---
schema_version: 1
id: ss07_lesson_02                 # unique trong course; snake/kebab OK
type: lesson                       # lesson | quiz | homework | revision_questions | review | meta | other
status: draft                      # draft | in_review | needs_fix | approved | deprecated

# Định vị trong curriculum
course_id: devops-microservices    # slug course
session: 7
unit: 2                            # lesson number / quiz set index / homework index
title: "Cấu trúc và cú pháp .gitlab-ci.yml"

# Loại session (bắt buộc trên mọi unit thuộc session)
session_kind: theory               # theory | practice
# theory   = tiết lý thuyết / dạy concept (có lesson ± quiz ± homework)
# practice = tiết thực hành / ôn tập (KHÔNG lesson content; chỉ homework tổng hợp)

# Phân loại
tags:                              # free-form + controlled (xem §3)
  - cicd
  - gitlab-ci
  - yaml
concepts:                          # concept IDs ổn định (slug)
  - pipeline-stage
  - job-script
  - gitlab-runner

# Phụ thuộc (graph)
depends_on:                        # unit/concept phải có TRƯỚC (approved)
  - ss01_lesson_02                 # unit id
  - concept:ci-cd-basics           # hoặc concept:slug
builds_on:                         # mềm hơn depends: tham chiếu/ôn, không block gen
  - ss01_lesson_02
enables:                           # unit/concept mà bài này MỞ RA (forward)
  - ss08_lesson_01
  - concept:docker-in-ci

# Chống trùng / ranh giới nội dung
owns:                              # concept bài này ĐƯỢC GIỚI THIỆU / ĐỊNH NGHĨA
  - pipeline-stage
  - job-script
assumes:                           # concept coi như ĐÃ BIẾT — chỉ nhắc, không dạy lại
  - ci-cd-basics
  - build-test-deploy
does_not_cover:                    # ranh giới: để session sau / ngoài scope
  - docker-image-push
  - vps-deploy

# Vận hành gen
source: generated                  # generated | human | hybrid
pm_ref: "Session 07 / Lesson 02"   # neo về PM
language: vi
created: 2026-07-10
updated: 2026-07-10
---
```

### Ý nghĩa graph

| Field | Dùng để |
|-------|---------|
| `depends_on` | Hard edge: gen/verify fail nếu prerequisite chưa `approved` (trừ session bootstrap) |
| `builds_on` | Soft edge: gợi ý ôn / narrative hook |
| `enables` | Forward link: session sau có thể `depends_on` ngược lại |
| `owns` | Ownership concept → chống 2 lesson cùng “dạy mới” 1 concept |
| `assumes` | LLM chỉ reference, không re-explain dài |
| `does_not_cover` | Explicit scope cut → giảm redundancy với PM verify |

---

## 2. Mở rộng theo `type`

### `type: lesson`

```yaml
type: lesson
lesson_mode: theory                # theory | practical  (BẮT BUỘC — xem MARKDOWN_SYNTAX)
# theory    = thiên lý thuyết (objectives → problem → core → optional practice/pitfalls/references)
# practical = thiên thực hành (problem → core gọn → steps → optional pitfalls/references)
# Companion BẮT BUỘC (file riêng): quiz_lesson + revision_questions cùng unit#
lesson_role: teach
estimated_minutes: 45
artifacts:
  - ".gitlab-ci.yml (build stage)"
```

**Cấm** section `essay` trong body lesson.

### `type: revision_questions`

```yaml
type: revision_questions
question_count: 2                  # 2 hoặc 3
maps_to: [ss07_lesson_02]          # BẮT BUỘC — đúng 1 lesson
lesson_mode: theory                # khớp lesson
```

Xem `REVISION_QUESTIONS.md`. Mỗi lesson **phải** có đúng 1 unit revision.

### `type: quiz`

```yaml
type: quiz
quiz_kind: lesson                  # lesson | warm_up | exit
question_count: 5
# optional matrix ids from QUIZ_FORMAT
matrix_id: lesson_default
```

### `type: homework`

```yaml
type: homework
session_kind: theory               # theory | practice — phải khớp PM session
exercise_count: 6
difficulty_mix:                    # align HOMEWORK_DESIGN
  guided: 4
  hints: 1
  independent: 1

# --- Chỉ bắt buộc khi session_kind: practice (tiết ôn / lab tổng hợp) ---
# Không có lesson file trong session này; homework là TOÀN BỘ nội dung session.
practice_of: [1, 2]                # session numbers được ôn (vd ss03 ôn ss01+ss02)
maps_to_sessions: [1, 2]           # alias rõ nghĩa; nên = practice_of
# maps_to_lessons trên từng EX* phải ∈ union lessons của practice_of (approved)
```

Ví dụ homework session thực hành (ss03):

```yaml
---
schema_version: 1
id: ss03_homework
type: homework
status: draft
course_id: example-course
session: 3
unit: 0
title: "Bài tập tổng hợp Session 01–02"
session_kind: practice
practice_of: [1, 2]
maps_to_sessions: [1, 2]
exercise_count: 6
difficulty_mix: { guided: 4, hints: 1, independent: 1 }
depends_on: [ss01_homework, ss02_homework]   # hoặc list lesson approved; tối thiểu depends sessions
owns: []                                     # practice không introduce concept mới
assumes: []                                  # fill từ union owns của ss01+ss02 khi gen
source: generated
pm_ref: "Session 03"
language: vi
---
```

### `type: lesson` + `session_kind`

```yaml
type: lesson
session_kind: theory               # lesson CHỈ tồn tại khi session_kind: theory
# session_kind: practice → CẤM type: lesson trong session đó
```

### Session-level (trong PM; mirror lên unit)

| `session_kind` | Tên gọi | Có lesson? | Có quiz? | Có homework? |
|----------------|---------|------------|----------|--------------|
| `theory` | Lý thuyết / teach | Có (theo PM) | Optional | Có (6 EX, scope = session đó) |
| `practice` | Thực hành / ôn tập | **Không** | Thường không | **Có — là artifact duy nhất** (6 EX, scope = `practice_of`) |

> `kind: teach | review | capstone` trong PM cũ map sang:  
> `teach`/`capstone` → `session_kind: theory` · `review` → `session_kind: practice`.

### `type: meta` (PM, design specs trong course-spec)

```yaml
type: meta
meta_kind: pm_curriculum           # pm_curriculum | homework_design | quiz_format | guideline | skill
```

---

## 3. Tags (universal conventions)

**Controlled prefixes** (khuyến nghị):

| Prefix | Ví dụ | Ý nghĩa |
|--------|--------|---------|
| (none) | `docker`, `cicd` | topic |
| `skill:` | `skill:debug`, `skill:deploy` | kỹ năng |
| `bloom:` | `bloom:apply`, `bloom:analyze` | mức nhận thức |
| `artifact:` | `artifact:dockerfile` | loại sản phẩm |
| `level:` | `level:intro`, `level:prod` | độ sâu |

Tags **không** thay `depends_on`. Tags phục vụ filter/search; depends phục vụ graph.

---

## 4. Concept ID

- Slug: `lowercase-kebab`, ổn định xuyên course  
- Khai báo lần đầu khi unit `owns` nó  
- Unit sau chỉ `assumes` / `depends_on: concept:…`  

Indexer có thể build bảng:

`concept → owned_by unit → assumed_by units[]`

---

## 5. Status lifecycle (gate kế thừa)

```
draft → in_review → needs_fix ⇄ in_review → approved
                         ↘ deprecated
```

**Quy tắc MCP/skill:**

- `get_prior_content` / inherit search **chỉ** unit `status: approved`  
- Session 1 unit đầu: `depends_on: []` cho phép  
- Không promote `approved` nếu `validate` fail hoặc human chưa sign-off  

---

## 6. Minimal valid example (lesson)

```yaml
---
schema_version: 1
id: ss01_lesson_01
type: lesson
status: draft
course_id: example-course
session: 1
unit: 1
title: "Tổng quan DevOps và hạn chế triển khai thủ công"
tags: [devops, intro]
concepts: [devops-overview, manual-deploy-pain]
depends_on: []
builds_on: []
enables: [ss01_lesson_02, concept:ci-cd-basics]
owns: [devops-overview, manual-deploy-pain]
assumes: []
does_not_cover: [gitlab-ci-syntax, docker-basics]
source: generated
pm_ref: "Session 01 / Lesson 01"
language: vi
---
```
