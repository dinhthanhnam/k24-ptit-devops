# Session 02 — Virtual Private Server (VPS)

Deck giảng dạy theo **HSSF charter** (thin deck):

- **HSSF** — chrome + teaching blocks (header, list, callout, code, compare, steps, term, figure…)
- **Tailwind** — layout only (`flex`, `gap`, `flex-1`, …), CDN, **`preflight: false`**
- **`deck.css`** — chỉ token stage font-size

**Runtime:** [hssf-slides@0.5.0](https://www.npmjs.com/package/hssf-slides) (advance-slide toaster when fragments done)

## Serve

```bash
cd workspace/sessions/ss2/html/session_02_slide
npx serve .
```

Keyboard: `←` `→` `Space` · `F` fullscreen · hash `#2` · click term để mở glossary.

## Files

| Path | Role |
|------|------|
| `index.html` | **22 slides** — arc Session 02 |
| `styles/deck.css` | Chỉ `--hssf-stage-font-size` (+ code color) |
| `assets/images/` | Diagram ảo hóa (nếu có) |
| `AGENTS.md` | Quy tắc authoring (scaffold) |

## Nội dung (map nhanh)

1 Title · 2 Objectives · 3 Agenda  
4–8 Ảo hóa (bare-metal → hypervisor types)  
9–12 Cloud VPS / provider / SSH Key  
13–16 Security (threats, SSH harden, UFW)  
17–20 Nginx (why, config, auth + scope)  
21 Summary · 22 Brand end  

## Charter notes

- Layout: **Tailwind**, không `hssf-columns` / `hssf-grid` cho bố cục  
- Brand: header, list, callout, compare, steps, code, agenda, defs, figure, term  
- Compare columns: `data-hssf-fragment="hold"`  
- Không flow architecture, không kit `deck-*`  

