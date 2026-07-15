# k24-ptit-devops

Repo **nội dung học phần DevOps Basics** (K24 PTIT).

> Không nhầm với `devops-course` (repo test cũ).

## Layout

```
k24-ptit-devops/
  course-spec/     # PM + guidelines + skill
  workspace/       # OUTPUT gen
  assets/          # ảnh chèn tay (optional)
```

## MCP (course-factory)

Env bắt buộc trỏ **repo này**:

| Biến | Path |
|------|------|
| `COURSE_SPEC` | `.../k24-ptit-devops/course-spec` |
| `WORKSPACE` | `.../k24-ptit-devops/workspace` |

File cấu hình Antigravity: `~/.gemini/config/mcp_config.json`  
(Engine `.env` cũng nên trùng: `COURSE_SPEC=../k24-ptit-devops/course-spec`.)

**Lưu ý:** `env` trong `mcp_config.json` **ghi đè** `.env` của engine. Nếu MCP vẫn trỏ `devops-course`, agent sẽ ghi nhầm sang project test.

## Kiểm tra nhanh

```powershell
cd ...\devops-rag-mcp
# sau khi mcp_config đúng — hoặc set env rồi:
.\.venv\Scripts\python.exe -c "from src.config import COURSE_SPEC, WORKSPACE; print(COURSE_SPEC); print(WORKSPACE)"
```

Phải thấy `k24-ptit-devops`.
