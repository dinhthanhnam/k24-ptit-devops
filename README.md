# devops-course

Repo **nội dung học phần** (tách khỏi MCP engine).

## Chỉ có input chuẩn

```
course-spec/
  pm.curriculum.md              # PM nguyên sơ (plain list)
  guidelines/                   # chuẩn format + homework/quiz
  skills/SKILL_COURSE_FACTORY.md
workspace/                      # OUTPUT — agent gen markdown vào đây
  sessions/
```

**Không** nhúng domain QuickBite / Evolution Map (optional sau, `course-spec/domain/`).

## Quan hệ với MCP

| Repo | Vai trò |
|------|---------|
| `devops-rag-mcp` | Engine MCP (tools, embed, index) |
| `devops-course` (repo này) | Course-spec + workspace |

Antigravity mở **workspace = repo này**, MCP trỏ env:

- `COURSE_SPEC` → `.../k24-ptit-devops/course-spec`
- `WORKSPACE` → `.../k24-ptit-devops/workspace`

## Flow test Antigravity

1. `get_course_spec` / `get_writing_rules`
2. **Chuẩn hóa PM** primitive → YAML theo `guidelines/PM_CURRICULUM_FORMAT.md` (ghi đè hoặc `pm.curriculum.structured.md` rồi merge)
3. `verify_pm(1)` → gen Session 1 → review → approved → reembed
4. Tiếp session sau; Session 3/6/… = `practice` chỉ 6 homework

## PM primitive

File hiện tại: list Session/Lesson gốc.  
Session kiểu *"Hệ thống kiến thức Session X, Y"* = **practice** (không lesson body).
