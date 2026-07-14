---
schema_version: 1
id: skill_course_factory_v1
type: meta
meta_kind: skill
title: "Skill: Course Factory (universal)"
status: approved
language: vi
---

# Skill — Course Factory v1

LLM **bắt buộc** tuân thủ skill này khi gen tài nguyên course qua MCP.  
Mục tiêu: đúng flow, đúng dependency, chống trùng, có human gate.

**Repo này (`devops-course`)** chỉ chứa:

- `course-spec/pm.curriculum.md` — PM **nguyên sơ** (list Session/Lesson)
- `course-spec/guidelines/*` — chuẩn format
- `course-spec/skills/this file`
- `workspace/` — **output** gen (ban đầu trống)

MCP engine nằm repo khác (`devops-rag-mcp`). Không gen vào folder MCP.

---

## 0. Nguồn được dùng

| Nguồn | Dùng? |
|-------|--------|
| `course-spec/pm.curriculum.md` | Bắt buộc |
| `course-spec/guidelines/*` | Bắt buộc |
| Unit `workspace/...` `status: approved` | Inherit (session ≥ 2) |
| Domain (`course-spec/domain/`) | **Không** bật mặc định |
| Draft / needs_fix | Không inherit |

---

## 0.1 Bước 0 — PM primitive → structured (bắt buộc trước Session 1 đầy đủ)

PM hiện `format: primitive`. Agent:

1. `get_writing_rules("pm")` → đọc `PM_CURRICULUM_FORMAT.md`
2. Chuẩn hóa PM: thêm `session_kind` (`theory`|`practice`), `practice_of`, `depends_on_sessions`, `owns`/`assumes` từng lesson, concept registry
3. Ghi **cập nhật** `pm.curriculum.md` (hoặc tạo `pm.curriculum.structured.md` rồi thay thế) — **human review PM** nếu policy yêu cầu
4. `verify_pm(N)` chỉ tin cậy anti-redundancy sau khi có owns/assumes

Session *"Hệ thống kiến thức Session X, Y"* → `session_kind: practice`, `lessons: []`, chỉ homework 6 bài.

MCP primitive parse vẫn cho `get_build_plan` / skeleton; **không** thay bước chuẩn hóa owns/assumes.

---

## 1. Tools (hợp đồng — map MCP)

Tên có thể alias; **ý nghĩa** giữ nguyên:

| Tool | Khi gọi |
|------|---------|
| `get_course_spec` | Đầu việc: PM + standards list |
| `get_writing_rules` | Trước khi viết body / quiz / homework |
| `verify_pm` | Trước gen session N (reasoning V1–V5) |
| `get_build_plan` | Liệt kê unit còn thiếu theo PM |
| `list_progress` | status draft/review/approved |
| `get_session_blueprint` | PM slice session N + depends + owns/assumes |
| `get_prior_content` | Summary unit **approved** prerequisite |
| `search_concepts` | Tìm đoạn đã gen (anti-dup + hook) |
| `read_section` | Đọc section cụ thể file approved |
| `start_unit` | Tạo file + frontmatter (`lesson`/`tutorial`/`homework`/quiz/…) |
| `write_section` | Ghi từng section |
| `validate_unit` | frontmatter + section ids + depends |
| `reembed` | Sau gen/fix (`scope=workspace` / `only_path`) |
| `get_review_packet` | Cho human |
| `set_review_status` | draft→…→approved |

**Unit `tutorial` (step-by-step):** 1 lab / **theory session only** — `unit_type=tutorial` (alias `step_by_step`).  
**Cấm** tutorial trên `session_kind: practice` (practice = homework only).  
Guideline: `TUTORIAL_DESIGN.md`. DevOps: `> **[IMAGE NEEDED]** ...` khi cần screenshot.

Nếu tool chưa implement: **mô phỏng bằng file ops + checklist** nhưng vẫn ghi reasoning như đã gọi.

---

## 2. Flow chuẩn

### 2.1 Bootstrap / theory session (vd Session 2)

```
get_course_spec
get_writing_rules  # gồm tutorial
verify_pm(session=N)
get_build_plan(session=N)
# Order: lessons → tutorial → homework → quiz phase
for each lesson:
  start_unit(lesson) → write → validate → reembed → review → approved
  (+ revision + quiz_lesson theo skill nếu bật)
start_unit(unit_type="tutorial", step_count=6)
  write steps + [IMAGE NEEDED] where UI matters
  validate → reembed → human review → approved
start_unit(homework) → … → approved
# quiz warm_up / exit nếu plan
```

**Tutorial ≠ homework:** tutorial = happy-path lab (theory only); homework = 6 EX.  
**Practice:** không gen tutorial.

### 2.2 Session N (N ≥ 2) — inherit approved

```
verify_pm(session=N)             # móc depends + anti-redundancy
get_session_blueprint(N)
get_prior_content(depends)       # approved only
search_concepts(owns/assumes)    # tránh dạy lại
# optional read_section for exact config/code to extend
start_unit → write_section* → validate → reembed
→ human review loop → approved
```

### 2.3 Quiz / Homework sau lessons — session `theory`

```
get_writing_rules(quiz|homework)
maps_to approved lessons of CURRENT session only
validate → reembed → human → approved
```

### 2.4 Session `practice` (ôn tập — chỉ 6 homework, vd ss03, ss06)

```
verify_pm(session=N)                    # session_kind: practice, lessons: []
# FAIL nếu PM còn lesson titles hoặc thiếu practice_of
assert all sessions in practice_of are approved
get_session_blueprint(N)                # homework_only: true
get_prior_content / search              # CHỈ units ∈ practice_of (approved)
get_writing_rules(homework)             # HOMEWORK_DESIGN §5 practice
start_unit type=homework
# Gen đúng 6 EX:
#   coverage mọi session trong practice_of
#   ≥1 EX multi-session nếu |practice_of|≥2
#   owns concept mới: cấm
validate_unit → reembed → human → approved
# CẤM start_unit type=lesson trong session này
```

---

## 3. Reasoning bắt buộc (viết ra, không chỉ “nghĩ thầm”)

Trước khi viết body lesson, agent **in** block:

```markdown
### Authoring rationale — {unit_id}
- PM owns: ...
- PM assumes: ...
- Prior approved loaded: ...
- Will NOT re-teach: ...
- Will teach (owns): ...
- Hooks: 1 short para max for assumes
- does_not_cover respected: ...
- Dup check (search): hits=... → action=skip/merge/reference
```

Sau `verify_pm`:

```markdown
### PM verify — Session {N}
- ...
- verdict: PASS|FAIL
```

---

## 4. Anti-redundancy rules (enforce)

1. Không tạo heading/section định nghĩa concept ∈ `assumes` dài hơn 1 short paragraph.  
2. Không `owns` concept đã `introduced_in` unit khác (trừ errata + deprecate cũ).  
3. Session triển khai cụ thể (vd CI GitLab) **phải** `assumes` concept nền (vd ci-cd-basics) và cite unit prior.  
4. Session `practice`: `owns` rỗng; không lesson; homework tổng hợp `practice_of` only.  

---

## 4.1 Quy chuẩn định dạng & hành văn (Formatting & Writing Standards)

1. **Cách xưng hô:** Tuyệt đối không dùng từ "Bạn" đơn lẻ khi xưng hô với người học. Phải dùng các từ thân thiện và chuyên nghiệp hơn như: **"các bạn"**, **"các học viên"**, hoặc **"học viên"**.
2. **Cấu trúc Heading (Heading Level Hierarchy):** Phải đi tuần tự theo thứ tự cấp bậc tiêu đề (H1 -> H2 -> H3 -> H4), tuyệt đối **CẤM nhảy cóc tiêu đề** (ví dụ: nhảy từ H2 sang H4 hoặc bỏ qua H2 khi viết nội dung các section con). Mỗi section lớn như `<!-- section: core -->` hoặc `<!-- section: problem -->` phải giữ nguyên tiêu đề H2 mặc định của skeleton trước khi triển khai các tiêu đề H3, H4 bên trong.
3. **Hình ảnh minh họa & Workflow:** Đối với các vị trí phù hợp trong bài học (mô tả quy trình, luồng dữ liệu, kiến trúc):
   - Phải thiết kế và thêm **Workflow bằng sơ đồ ASCII** (sử dụng text blocks) hoặc sơ đồ **Mermaid** trực quan.
   - Phải cung cấp chi tiết **Prompt gợi ý sinh hình ảnh minh họa** tương ứng để người dùng có thể dùng làm tài liệu tham khảo/sinh ảnh thực tế.
4. **Tài liệu tham khảo (References):** Bắt buộc phải gắn link liên kết (Markdown link) kèm tiêu đề tài liệu làm ưu tiên hàng đầu, không cần ghi tên tác giả.
5. **Câu hỏi ôn tập (Revision Questions):** Mỗi câu hỏi tự luận ôn tập (RQ) phải đi kèm một phần gợi ý đáp án/định hướng trả lời ngắn gọn (ví dụ: `*Gợi ý đáp án:*` hoặc `*Hướng dẫn trả lời:*`) ngay phía dưới câu hỏi để hỗ trợ học viên tự đánh giá kiến thức.

---

## 5. Human gate

- **QUY TẮC BẮT BUỘC (STRICT RULE):** Agent chỉ được phép khởi tạo và sinh nội dung cho **đúng 1 unit (1 lesson/homework/quiz) duy nhất tại một thời điểm**. Tuyệt đối CẤM sinh hàng loạt nhiều bài học/bài tập cùng một lúc trong một turn hoặc tự động chuyển sang unit tiếp theo khi unit hiện tại chưa được người dùng kiểm tra và phê duyệt (`approved`).
- Cấm tự `approved` nếu policy require_human=true (default).  
- `needs_fix` phải kèm note cụ thể (frontmatter / review log).  
- Sau fix: luôn `validate` + `reembed` trước review lại.  

---

## 6. Out of scope skill này

- Sinh slide/video  
- Sửa PM khi FAIL: **đề xuất** diff PM, chờ human merge  
- Domain architecture storytelling (QuickBite, …) trừ khi course-spec/domain được load  

---

## 7. Definition of done (một session)

### `session_kind: theory`
- [ ] `verify_pm` PASS  
- [ ] Mọi lesson PM → file + frontmatter → `approved`  
- [ ] Quiz (nếu plan) + homework 6 EX `approved`  
- [ ] reembed mới nhất · `list_progress` complete  

### `session_kind: practice`
- [ ] `verify_pm` PASS · `lessons: []` · `practice_of` đủ  
- [ ] **Zero** lesson files  
- [ ] Đúng 1 file homework · 6 EX · coverage `practice_of` · ≥1 multi-session EX  
- [ ] `approved` + reembed · `list_progress` complete  

---

## 8. Quản lý Context Window & Trí nhớ (Memory Optimization)

- **Quy tắc chủ động quên (Forgetting Rule):** Sau khi mỗi session hoàn thành và được phê duyệt (`approved`), Agent chủ động giải phóng bộ nhớ (không lưu giữ chi tiết nội dung các bài học, bài tập của session đó trong context của lượt hội thoại tiếp theo) nhằm tối ưu hóa không gian context window.
- **Truy xuất động qua MCP:** Khi cần kết nối ngữ cảnh hoặc tham chiếu cấu hình của các session trước đó cho session hiện tại, Agent bắt buộc phải sử dụng các công cụ MCP chuyên trách (`get_prior_content`, `search_concepts`, `read_section`) để kéo thông tin về một cách chính xác thay vì tự suy đoán hoặc yêu cầu người dùng cung cấp lại.

