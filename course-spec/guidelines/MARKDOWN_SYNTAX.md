# Markdown Syntax Standard v1 (lesson body)

Universal structure sau frontmatter. Heading tiếng Việt tự do; **`<!-- section: id -->` bắt buộc** để index / `read_section` / validate.

> Phân biệt:  
> - `session_kind: theory | practice` = loại **buổi** (practice = chỉ homework, không lesson/tutorial).  
> - `lesson_mode: theory | practical` = loại **bài lesson** trong session theory.  
> - `type: tutorial` = 1 lab step-by-step / **theory session only** — xem `TUTORIAL_DESIGN.md`.

---

## 1. Hai mode lesson

| `lesson_mode` | Khi nào | Skeleton body |
|---------------|---------|----------------|
| **`theory`** | Thiên khái niệm, mô hình | §2 |
| **`practical`** | Thiên lab / thao tác | §3 |

**Companion bắt buộc (file riêng — không nhúng trong lesson):**

| Unit | Rule |
|------|------|
| `type: quiz` (`quiz_kind: lesson`) | 1 quiz MCQ / lesson — `QUIZ_FORMAT` |
| `type: revision_questions` | 1 file tự luận / lesson — `REVISION_QUESTIONS` |

Cứ **có lesson** → phải có **cả** quiz lesson **và** revision questions (gate plan / skill).

Session `session_kind: practice` (ôn tập): **không** lesson / quiz / revision / **tutorial** — chỉ homework.

Mỗi session **theory**: **1** `session_NN_tutorial.md`, trừ khi PM `tutorial.required: false`.

---

## 2. Lesson `theory` — body (không chứa essay)

```markdown
# {title}

<!-- section: objectives -->
## 1. Mục tiêu
- ...

<!-- section: problem -->
## 2. Đặt vấn đề
...

<!-- section: core -->
## 3. Kiến thức cốt lõi
...

<!-- section: practice -->
## 4. Thực hành và minh hoạ
...
_(Optional — bỏ nếu bài không code / không demo)_

<!-- section: pitfalls -->
## 5. Lỗi sai thường gặp
_(Optional)_

<!-- section: references -->
## 6. Tài liệu tham khảo
_(Optional)_
```

| id | Bắt buộc? |
|----|-----------|
| `objectives` | **yes** |
| `problem` | **yes** |
| `core` | **yes** |
| `practice` | no (minh hoạ; bỏ nếu không code) |
| `pitfalls` | no |
| `references` | no |

**Không** dùng `<!-- section: essay -->` trong lesson — tự luận = file `revision_questions`.

---

## 3. Lesson `practical` — body

```markdown
# {title}

<!-- section: problem -->
## 1. Đặt vấn đề
...

<!-- section: core -->
## 2. Kiến thức cốt lõi
_(gọn)_

<!-- section: steps -->
## 3. Các step thực hành
### Step 1 — ...
...

<!-- section: pitfalls -->
## 4. Lỗi sai thường gặp
_(Optional)_

<!-- section: references -->
## 5. Tài liệu tham khảo
_(Optional)_
```

| id | Bắt buộc? |
|----|-----------|
| `problem` | **yes** |
| `core` | **yes** |
| `steps` | **yes** |
| `pitfalls` | no |
| `references` | no |

---

## 4. Quy tắc chống trùng

1. **`assumes`:** tối đa 1 short paragraph hook.  
2. **`owns`:** định nghĩa chính thức một lần.  
3. Code: fenced + language tag.  
4. **Cấm** nhúng quiz MCQ hoặc revision/essay vào body lesson.  
5. **Cấm** nhét 6 EX homework vào lesson.

---

## 5. File naming

```
sessions/ss{NN}/session_{NN}_lesson_{MM}.md
sessions/ss{NN}/session_{NN}_revision_{MM}.md   # bắt buộc companion
sessions/ss{NN}/session_{NN}_quiz_lesson_{MM}.md
sessions/ss{NN}/session_{NN}_quiz_warm_up.md    # session-level
sessions/ss{NN}/session_{NN}_quiz_exit.md
sessions/ss{NN}/session_{NN}_tutorial.md        # 1 lab step-by-step / session
sessions/ss{NN}/session_{NN}_homework.md
assets/ss{NN}/...                               # ảnh chèn tay (human); tutorial chỉ [IMAGE NEEDED]
```

### Ảnh trong tutorial / practical lesson (DevOps)

```markdown
> **[IMAGE NEEDED]** Mô tả ảnh cần chèn.
> Gợi ý path: `assets/ss02/step_03_....png`
```

Không generate binary; human thêm file vào `assets/` sau.
