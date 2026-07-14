---
schema_version: 1
id: quiz_format_v1
type: meta
meta_kind: quiz_format
title: "Quiz Format Specification"
status: approved
language: vi
---

# Quiz Format Specification v1

Spec bắt buộc khi gen quiz qua Course Factory MCP.  
Tham chiếu thiết kế gốc (`QUIZ_FORMAT` lesson / đầu giờ / cuối giờ) + siết các rule dễ bị agent lạm dụng.

**Ngôn ngữ:** toàn bộ stem, options, EXP viết **tiếng Việt** (trừ identifier / code).

---

## 1. Nguyên tắc cốt lõi (5 “NÊN / KHÔNG”)

1. **Đơn nhiệm** — Mỗi câu đánh giá **đúng 1** kiến thức/kỹ năng. Không nhồi nhiều lỗi (cú pháp + logic + hiệu năng) vào cùng một stem.
2. **Ngữ cảnh hóa** — Ưu tiên **tình huống / scenario** thực tế; hạn chế hỏi định nghĩa suông.
3. **Nhiễu thông minh** — Phương án sai bắt nguồn từ **lỗi phổ biến** (off-by-one, nhầm stage pipeline, nhầm env, v.v.).  
   Cấm: “Cả 3 đều sai”, “Tất cả đều đúng”, đáp án vô nghĩa / ngoài phạm vi bài, đáp án “tếu”.
4. **Đồng nhất (BẮT BUỘC)** — Bốn options **cùng kiểu**: độ dài tương đương, cấu trúc ngữ pháp tương đương, **cùng phạm vi kiến thức**.  
   - Không được để đáp án đúng **dài hơn hẳn** (hoặc ngắn hơn hẳn) các đáp án sai.  
   - Không “leak” bằng wording (lặp keyword stem chỉ ở đáp án đúng).
5. **Sắc bén (No clues)** — Stem không gợi đáp án; options không lộ bằng formal/không formal lệch nhau.

### Bổ sung bắt buộc (siết từ thực tế gen)

| Rule | Chi tiết |
|------|----------|
| **Độ dài options** | **Bắt buộc** xấp xỉ bằng nhau (không phải “cố gắng”). Sai lệch độ dài rõ → phải viết lại. Đáp án đúng **không** được là option dài nhất một mình. |
| **Random `@correct`** | Phân bố A/B/C/D **khách quan**. Cấm chuỗi dài cùng một đáp án (vd. 5 câu liên tiếp cùng `C`). **Tối đa 2 câu liên tiếp** cùng `@correct`. Với 30 câu: mỗi letter khoảng 6–9 lần, không letter nào > 10. |
| **Loại trừ khó** | Distractor **không** quá lệch kiến thức để học viên loại trừ ngay; cũng **không** “bẫy bẩn” ngoài scope bài. Mỗi sai phải giải thích được bằng misconception cụ thể trong `[EXP]`. |
| **`@difficulty` = số** | **Chỉ** số nguyên theo bảng quy đổi §3. **Cấm** slug Bloom (`apply`, `understand`, …) trong field `@difficulty`. |

---

## 2. Ba loại quiz (`quiz_kind`)

| `quiz_kind` | Mục đích | Số câu | Scope |
|-------------|----------|--------|--------|
| `lesson` | Sau 1 lesson | **5** | owns/assumes của lesson đó |
| `warm_up` | Đầu buổi | **30** | **15 bài cũ + 15 bài mới** (50/50) |
| `exit` | Cuối buổi | **30** | **Chỉ bài mới** (`@category: 1`) |

Tạo **đúng** `question_count` theo kind — không thiếu/thừa.

**Thời gian gợi ý**

- `lesson` / `exit`: ≤ **44 giây**/câu  
- `warm_up`: ≤ **45 giây**/câu  

---

## 3. Bảng `@difficulty` (bắt buộc — số 1…11)

`@difficulty` **luôn là số nguyên** trong `1..11`. Map nhận thức:

| Số | Tên (nhãn soạn thảo) | Khi dùng |
|----|----------------------|----------|
| **1** | Nhận diện / định nghĩa | `lesson` — cú pháp, thuật ngữ |
| **2** | Thông hiểu cơ bản | `lesson` — luồng chạy đơn giản |
| **3** | Vận dụng nhẹ / đọc code | `lesson` — snippet, so sánh nhẹ |
| **4** | Vận dụng chuyên sâu | `warm_up` bài cũ |
| **5** | Phân tích chuyên sâu | `warm_up` bài cũ (debug, luồng dữ liệu) |
| **6** | Sáng tạo / best practice | `warm_up` bài cũ **và** `exit` (best practice) |
| **7** | Thông hiểu (bài mới) | `warm_up` bài mới — khái niệm E-learning |
| **8** | Vận dụng sơ bộ (bài mới) | `warm_up` bài mới — cú pháp/triển khai cơ bản |
| **9** | Phân tích sơ bộ (bài mới) | `warm_up` bài mới — so sánh với cái đã biết |
| **10** | Vận dụng (cuối giờ) | `exit` — triển khai đúng chức năng bài mới |
| **11** | Phân tích (cuối giờ) | `exit` — đọc luồng, bắt lỗi logic bài mới |

**Cấm:** `@difficulty: apply`, `understand`, `analyze`, …  
**Đúng:** `@difficulty: 4`

---

## 4. Cú pháp một câu (machine-friendly)

```markdown
## Q1

{Stem — tiếng Việt; scenario-first}

```{lang}
{optional: code mẫu trong stem — fenced, được xuống dòng, indent chuẩn}
```

[A]
{option — nếu có code: cực ngắn / pseudo; TUYỆT ĐỐI không xuống dòng trong option}
[EXP]
{giải thích vì sao A đúng hoặc sai — misconception cụ thể}
[B]
...
[EXP]
...
[C]
...
[EXP]
...
[D]
...
[EXP]
...

@correct: B
@point: 20
@difficulty: 4
@concept: pipeline-stages
@category: 0
```

### Fields

| Field | Bắt buộc | Giá trị |
|-------|----------|---------|
| `@correct` | Có | `A` \| `B` \| `C` \| `D` |
| `@point` | `lesson` (default 20); warm_up/exit optional | số |
| `@difficulty` | **Có** (mọi kind) | số nguyên `1`…`11` theo §3 |
| `@concept` | Nên có | concept id ∈ owns ∪ assumes (prior approved khi ôn cũ) |
| `@category` | `warm_up` + `exit` bắt buộc | `0` = bài cũ (prior), `1` = bài mới (current) |

### Code

| Vị trí | Rule |
|--------|------|
| **Stem** | Fenced code block riêng; được xuống dòng; indent rõ |
| **Options [A]–[D]** | Code ngắn / pseudo; **cấm xuống dòng** trong nội dung option |

---

## 5. Ma trận theo kind

### 5.1 `lesson` — 5 câu

| # | Mục tiêu | `@difficulty` gợi ý |
|---|----------|---------------------|
| Q1 | Định nghĩa / cú pháp | 1 |
| Q2 | Luồng thực thi | 2 |
| Q3 | Đọc hiểu code mẫu | 3 |
| Q4 | Phân biệt / so sánh | 2 hoặc 3 |
| Q5 | Dự đoán kết quả (bẫy nhẹ) | 3 |

`@category`: có thể omit hoặc `1` (nội dung lesson hiện tại).

---

### 5.2 `warm_up` — 30 câu — **15 cũ + 15 mới (50/50)**

> **Không** dùng tỉ lệ 2/3–1/3 hay 20/10. **Đúng: 15 prior + 15 current.**

| STT | `@category` | `@difficulty` | Số câu | Mục tiêu |
|-----|-------------|---------------|--------|----------|
| Q1–Q6 | `0` bài cũ | **4** Vận dụng chuyên sâu | 6 | Hiện thực hóa vào bài toán nhỏ / fix phản xạ |
| Q7–Q11 | `0` bài cũ | **5** Phân tích chuyên sâu | 5 | Đọc luồng, debug logic |
| Q12–Q15 | `0` bài cũ | **6** Sáng tạo | 4 | Kiến trúc nhẹ, tối ưu, chọn hướng xử lý |
| Q16–Q21 | `1` bài mới | **7** Thông hiểu | 6 | Khái niệm, thuật ngữ, mục đích (E-learning) |
| Q22–Q27 | `1` bài mới | **8** Vận dụng sơ bộ | 6 | Cú pháp chuẩn, triển khai cơ bản |
| Q28–Q30 | `1` bài mới | **9** Phân tích sơ bộ | 3 | So sánh công nghệ mới với cái đã biết |

**Nguồn tham chiếu khi gen**

- `category: 0` → unit **approved** session trước / `depends_on` / `assumes`  
- `category: 1` → lesson sắp dạy / E-learning bài mới (PM owns session hiện tại)

---

### 5.3 `exit` — 30 câu — chỉ bài mới

| STT | `@difficulty` | Số câu | Mục tiêu |
|-----|---------------|--------|----------|
| Q1–Q12 | **10** Vận dụng | 12 | Triển khai đúng cú pháp / chức năng bài mới |
| Q13–Q22 | **11** Phân tích | 10 | Đọc luồng, bắt lỗi logic, cơ chế vận hành |
| Q23–Q30 | **6** Sáng tạo | 8 | Best practice / chọn giải pháp tối ưu |

- `@category: 1` cho **mọi** câu exit.  
- Chỉ kiến thức **vừa học** trong session; tham lesson/homework approved của session đó.

---

## 6. Checklist QA trước khi `validate` / review

- [ ] Đúng số câu theo `quiz_kind`  
- [ ] Mọi `@difficulty` là số `1..11` khớp ma trận kind  
- [ ] `warm_up`: đúng 15×`@category:0` + 15×`@category:1`  
- [ ] `exit`: 30×`@category:1`; difficulty mix 12×10 + 10×11 + 8×6  
- [ ] Không >2 câu liên tiếp cùng `@correct`; phân bố A/B/C/D cân  
- [ ] Bốn options **cùng độ dài/cấu trúc**; đáp án đúng không “lồ lộ” vì dài nhất  
- [ ] Distractor = misconception thật, không lệch scope  
- [ ] Option không có code xuống dòng; stem code (nếu có) fenced chuẩn  
- [ ] Toàn bộ tiếng Việt  

---

## 7. File + frontmatter

```text
sessions/ss{NN}/session_{NN}_quiz_lesson.md
sessions/ss{NN}/session_{NN}_quiz_lesson_{MM}.md   # optional per-lesson
sessions/ss{NN}/session_{NN}_quiz_warm_up.md
sessions/ss{NN}/session_{NN}_quiz_exit.md
```

```yaml
---
schema_version: 1
id: ss07_quiz_warm_up
type: quiz
status: draft
session: 7
session_kind: theory
title: "Quiz đầu giờ — Session 07"
quiz_kind: warm_up                 # lesson | warm_up | exit
question_count: 30
maps_to: [ss06_lesson_01, ss07_lesson_01]   # prior + upcoming refs
---
```

---

## 8. Indexing (RAG)

Mỗi `## Qn` = 1 chunk. Metadata tối thiểu: `quiz_kind`, `@difficulty` (số), `@category`, `@concept`, `@correct`.

---

## 9. Những lỗi agent thường mắc (CẤM lặp lại)

| Lỗi | Đúng |
|-----|------|
| `@difficulty: apply` / bloom slug | `@difficulty: 4` (số) |
| warm_up ~20 cũ / 10 mới hoặc 2/3–1/3 | **15 / 15** |
| “Cố gắng” options dài tương đương | **Bắt buộc** ngang nhau; đúng không dài nhất một mình |
| 4–5 câu liên tiếp `@correct: C` | Random; max 2 liên tiếp cùng letter |
| Distractor “Cả A và B”, “Không có đáp án” | Lỗi phổ biến trong scope |
| Code xuống dòng trong `[A]`…`[D]` | Chỉ pseudo/một dòng |
| Quiz concept ∈ `does_not_cover` | Chỉ owns ∪ assumes (prior approved) |
