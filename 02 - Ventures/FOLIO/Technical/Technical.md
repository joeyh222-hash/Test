---
area: FOLIO
---

# FOLIO — Technical Overview

[[FOLIO — Venture Overview|FOLIO]]

*Architecture, pipeline, and AI prompts for the FOLIO GSAT grading system.*

---

## Pipeline

### Part 1 — OCR

```
Student essay (scanned image)
    ↓
Google Cloud Vision (一號機)  ──┐
                                ├──→ OCR Merger Bot (OpenAI or Claude)
OpenAI Vision (二號機)        ──┘
    ↓
Plain text transcript:
    [SECTION:TRANSLATION]
    [SECTION:ESSAY]
    (3 Google Docs saved: Merged, 一號機, 二號機)
```

**Why dual OCR:** Google Cloud Vision is highly accurate at the character level; OpenAI Vision has stronger context awareness and handles handwriting better. The Merger Bot uses the image as ground truth, GCV output as the draft, and produces one faithful transcript preserving all student errors.

### Part 2 — Grading & Output

```
Essay question image + OCR transcript (Merged)
    ↓
Grading Bot (Claude Sonnet)
→ outputs strict JSON (6 sections, no text outside JSON)
    ↓
Formatting Bot (Claude Sonnet)
→ parses JSON, converts correction markers to HTML spans
→ outputs complete inline-styled HTML doc
    ↓
Create document from HTML → Google Docs
    ↓
Organize to folder
```

---

## Bot Interface: JSON Schema

The JSON produced by the Grading Bot is the exact interface consumed by the Formatting Bot.

```json
{
  "總分": { "總分": number, "內容": number, "組織": number, "文法句構": number, "字彙拼字": number },
  "作文批改": { "題目": string, "原始作文": string, "修改後作文": string },
  "修改建議": { "段落結構": string, "單字片語訂正": string, "文法訂正": string },
  "延伸補充": { "升級詞彙與搭配": string, "萬用句型框架": string, "詞彙升級梯": string },
  "閱卷評語": string,
  "延伸練習": [{ "英文題目": string, "中文說明": string, "練習重點": string, "實用價值": string, "內容延伸素材": string }]
}
```

---

## Correction Markup System

Inline correction markers used in `修改後作文` (written by Grading Bot, rendered by Formatting Bot):

| Type | Syntax | Meaning | Rendered as |
|------|--------|---------|-------------|
| Tier 1 — Grammar error | `~~wrong~~[correct]` | Actually wrong | Red strikethrough + blue bold bracket |
| Tier 2 — Style improvement | `__original__[better]` | Not wrong, but improvable | Purple underline + blue bold bracket |

Rule: edits are surgical — max ~6 words per marked span. No full sentence replacements.

---

## Bots

| Bot | Model | Input | Output |
|-----|-------|-------|--------|
| [[OCR Merger Bot]] | OpenAI or Claude | Scanned image + GCV transcript | Plain text with `[SECTION:TRANSLATION]` / `[SECTION:ESSAY]` markers |
| [[Grading Bot]] | Claude Sonnet | Essay question image + merged transcript | Strict JSON (6 sections) |
| [[Formatting Bot]] | Claude Sonnet | Grading Bot JSON | Complete inline-styled HTML for Google Docs |

---

## Report Structure (Final Output)

The Formatting Bot generates a ~20-page student-facing learning report:

| Section | Content |
|---------|---------|
| Score block | 總分/20 + 4 sub-scores with justifications |
| 二、作文批改 | Essay question image, original essay, 逐句訂正, legend |
| 三、修改建議 | 段落結構, 單字片語訂正, 文法重點訂正 |
| 四、延伸補充 | 升級詞彙與搭配, 萬用句型框架, 詞彙升級梯 |
| 五、閱卷評語 | 150–220 word evaluative prose (Traditional Chinese) |
| 六、延伸練習 | 2 practice exercises with skill focus and idea frameworks |

---

## Paperclip Orchestration

The processing pipeline is being rebuilt on [[Paperclip/Paperclip — Overview|Paperclip]] — an open-source AI agent orchestration platform. See the Paperclip subfolder for full knowledge base and company design.

- [[Paperclip/Paperclip — Overview|Paperclip — Overview]]
- [[Paperclip/Paperclip — FOLIO Company Design|Paperclip — FOLIO Company Design]] *(planned)*

---

## APIs Used

| Service | Purpose |
|---------|---------|
| Google Cloud Vision | OCR 一號機 — high character accuracy |
| OpenAI Vision | OCR 二號機 — context-aware handwriting reading |
| Google Docs API | Generate OCR result docs + final HTML report |
| Google Drive API | Organize output files to folder |
