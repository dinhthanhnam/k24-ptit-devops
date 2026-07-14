# PM Curriculum Format v1 (index-friendly)

Thay plain list “Session 01 … Lesson 01 …” bằng Markdown + YAML **parse được** để:

1. Index / tools đọc cấu trúc  
2. LLM **verify** dependency & chống trùng  
3. Gen `depends_on` / `owns` / `assumes` cho từng unit  

File chuẩn: `course-spec/pm.curriculum.md`

---

## 1. Frontmatter course-level

```yaml
---
schema_version: 1
id: pm_curriculum
type: meta
meta_kind: pm_curriculum
course_id: devops-microservices
title: "DevOps thực chiến với Microservices"
language: vi
version: 1
status: approved
---
```

---

## 2. Body structure (bắt buộc)

Mỗi session = một heading `##` + YAML block fenced `yaml` (machine-readable) + optional prose.

### Template một session

````markdown
## Session 07 — Tự động hóa biên dịch với GitLab CI

```yaml
session: 7
id: ss07
title: "Tự động hóa biên dịch với GitLab CI"
session_kind: theory           # theory | practice  (bắt buộc)
# kind: teach                  # legacy alias → theory
depends_on_sessions: [1, 2, 4] # hard: session-level
builds_on_sessions: [1]        # soft: ôn ý tưởng (CI/CD khái niệm ở ss01)
enables_sessions: [8, 10]
owns_concepts:
  - gitlab-ci-architecture
  - gitlab-ci-yml-syntax
  - pipeline-stages
  - maven-gradle-in-ci
assumes_concepts:
  - ci-cd-basics               # từ ss01
  - docker-image-basics        # nếu pipeline đụng image later — chỉ assume nếu đã teach
does_not_cover:
  - docker-build-in-pipeline   # để ss08
  - registry-push              # để ss08
  - vps-deploy                 # để ss10
redundancy_rules:
  - "Không dạy lại định nghĩa CI/CD (ss01); chỉ 1 đoạn hook 'đã học build-test-deploy'."
  - "Không hướng dẫn Dockerfile production (ss08)."
lessons:
  - unit: 1
    id: ss07_lesson_01
    title: "Tổng quan GitLab CI/CD và kiến trúc GitLab Runner"
    owns: [gitlab-ci-architecture]
    assumes: [ci-cd-basics]
  - unit: 2
    id: ss07_lesson_02
    title: "Cấu trúc và cú pháp file .gitlab-ci.yml"
    owns: [gitlab-ci-yml-syntax]
    assumes: [gitlab-ci-architecture, ci-cd-basics]
  - unit: 3
    id: ss07_lesson_03
    title: "Pipeline stages và cơ chế chạy job"
    owns: [pipeline-stages]
    assumes: [gitlab-ci-yml-syntax]
  - unit: 4
    id: ss07_lesson_04
    title: "Build ứng dụng bằng Maven/Gradle trong CI"
    owns: [maven-gradle-in-ci]
    assumes: [pipeline-stages]
  - unit: 5
    id: ss07_lesson_05
    title: "Đọc log pipeline và xử lý lỗi build"
    owns: [pipeline-log-debug]
    assumes: [maven-gradle-in-ci]
homework:
  required: true
  exercise_count: 6
```
````

### Session `practice` (ôn tập / lab — chỉ homework)

Ví dụ Session 03 = tổng hợp Session 01 + 02: **không lesson**, đúng 6 bài tập theo `HOMEWORK_DESIGN` §5.

```yaml
session: 3
id: ss03
title: "Hệ thống kiến thức Session 01, 02"
session_kind: practice         # tiết thực hành / ôn tập
practice_of: [1, 2]            # bắt buộc: các session theory được ôn
depends_on_sessions: [1, 2]    # phải approved trước khi gen homework
owns_concepts: []              # không concept mới
assumes_concepts: []           # verify: = union owns của practice_of
does_not_cover: []             # không mở topic session 4+
lessons: []                    # BẮT BUỘC rỗng
homework:
  required: true
  exercise_count: 6
  only_artifact: true          # session = homework file duy nhất
  coverage_rule: "every session in practice_of appears in ≥1 EX; ≥1 multi-session EX"
```

---

## 3. Concept registry (cuối file PM — khuyến nghị)

Giúp index + verify ownership duy nhất:

````markdown
## Concept registry

```yaml
concepts:
  - id: ci-cd-basics
    label: "Khái niệm CI/CD (build, test, deploy)"
    introduced_in: ss01_lesson_02
  - id: gitlab-ci-yml-syntax
    label: "Cú pháp .gitlab-ci.yml"
    introduced_in: ss07_lesson_02
```
````

Rule: mỗi `id` chỉ **một** `introduced_in`.

---

## 4. Reasoning cho LLM — verify PM (bắt buộc trong skill)

Khi `verify_pm` / trước khi gen session N, LLM (và tool checklist) chạy các bước sau và **ghi reasoning** ra review packet:

### Bước V1 — Coverage
- Mọi lesson title trong PM có `id` unique?  
- Mọi `owns` lesson có trong registry / không trùng owner?

### Bước V2 — Dependency chain (ví dụ ss01 ↔ ss07)
- ss01 owns `ci-cd-basics`  
- ss07 `assumes` / `depends_on` phải **móc** `ci-cd-basics`  
- ss07 **không** `owns` lại `ci-cd-basics`  
- Narrative: ss07 được **1 hook** tối đa ~1 đoạn (“Ở Session 1 ta đã…”) rồi vào GitLab cụ thể  

### Bước V3 — Redundancy
- Giao `owns(ssA) ∩ owns(ssB)` phải **rỗng**  
- Giao `does_not_cover(ssA)` với `owns(ssB)` nên **khớp** (A cắt scope → B nhận)  
- Nếu PM ss01 lesson “CI/CD khái niệm” và ss07 lesson “CI/CD là gì” → **FAIL verify**, yêu cầu sửa PM hoặc gộp title  

### Bước V4 — Ordering
- Nếu `depends_on_sessions` chứa X, session X phải có số nhỏ hơn (hoặc explicit parallel flag)  
- Mọi `assumes_concepts` phải có `introduced_in` session < current (hoặc same session earlier unit)

### Bước V5 — Gen readiness
- Session N chỉ gen khi mọi `depends_on_sessions` đã **approved** (trừ N=1 bootstrap)  
- Unit chỉ inherit body từ unit `approved`

### Output reasoning (template)

```markdown
## PM verify — Session 07
- depends_on_sessions: [1,2,4] → status: all approved? ...
- assumes: ci-cd-basics ← ss01_lesson_02 (OK)
- owns overlap with ss01: none (OK)
- redundancy_rules applied: no re-definition of CI/CD
- risk: lesson_01 title có thể đụng "tổng quan CI" → mitigate by assumes + short hook only
- verdict: PASS | FAIL + fixes
```

---

## 5. Migrate từ PM plain-text hiện tại

PM cũ:

```text
Session 01    Tổng quan DevOps & Quy trình CI/CD
Lesson 01    ...
```

→ Script/LLM convert một lần sang format §2, **bổ sung tay** `depends_on_sessions`, `owns_concepts`, `assumes_concepts`, `does_not_cover` (đây là giá trị thật của PM mới — không infer mù).

---

## 6. Indexing hints (cho MCP)

| Chunk kind | Key metadata |
|------------|----------------|
| `pm.session` | session, id, kind, depends_on_sessions, owns_concepts |
| `pm.lesson` | parent session, unit id, owns, assumes |
| `pm.concept` | concept id, introduced_in |

Search “gitlab ci” → hit `pm.session` ss07 + lessons; graph walk `assumes` → ss01.
