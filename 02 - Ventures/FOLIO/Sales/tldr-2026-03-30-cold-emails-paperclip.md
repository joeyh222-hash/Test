# FOLIO Session Summary — 2026-03-30

## What Was Done

### Cold Email Series (補習班)
- All 5 emails updated with FOLIO-branded rotating subject lines:
  1. `FOLIO · 學測英文作文 AI 批改服務｜把批改時間還給老師`
  2. `FOLIO · 學測英文作文 AI 批改｜讓每位學生拿到個人化回饋`
  3. `FOLIO · 學測英文作文 AI 批改服務｜3~5 工作天，全班個人化報告`
  4. Repeats format 1 (Email 4)
  5. Repeats format 2 (Email 5)
- Added website line to all 5 emails: `歡迎到我們的官網逛逛，了解 FOLIO 的各項服務！https://foliopath.me`
- Added meeting invite line to all 5 emails: `如果您想先直接跟我們聊聊您的需求及需要的服務，也歡迎來信安排一個線上會議，我們非常樂意直接在視訊上討論。`
- Email 2 rewritten: removed confrontational opener + rhetorical questions; replaced with observation from FOLIO development research. Authority comes from "talking to many cram school teachers and students" not "I was a tutor."
- Email 3 rewritten: removed punchy ad-copy lines; softer observational opening; tone now matches Email 1.
- Scheduling table updated with subject line column.
- Emails 1–3 + header exported to Google Docs: https://docs.google.com/document/d/1aDZpbRcsWur7xvaahdyKnv7SOkLrkAbPOgC6igveLJ8/edit

### Paperclip Setup
- Learned Paperclip: open-source AI agent orchestration platform (MIT). Runs teams of AI agents like a company. Claude Code is the employee; Paperclip is the company structure.
- Created knowledge base: `02 - Ventures/FOLIO/Technical/Paperclip/Paperclip — Overview.md`
- Designed FOLIO org chart on Paperclip:
  - CEO → COO (6 pipeline agents) + CFO + CMO (2 agents)
- Created `folio-context` skill with 4 reference files:
  - `company-overview.md`, `service-overview.md`, `pricing.md`, `brand-voice.md`
- CEO hired COO, CFO, CMO. Pipeline agents next.

## Key Decisions

- Email authority: do NOT mention personal tutoring as the source of insight. Use "during FOLIO's development, we talked with cram school teachers and students" instead.
- Tone rule: emails should lead with concrete observations, not rhetorical questions. State structural problems, don't blame the teacher.
- Paperclip skills system: folio-context skill is shared across all agents; pipeline agents each get their own skill (gsat-grading, html-report-formatting, etc.)

## Next Actions

- [ ] Write pipeline skills: `gsat-grading`, `html-report-formatting`, `dual-ocr-merge`, `report-qa-checklist`, `batch-intake`, `cold-email-cram-schools`
- [ ] Install Paperclip: `npx paperclipai onboard --yes`
- [ ] Create FOLIO company in Paperclip dashboard
- [ ] Brief each agent with FOLIO context before first task
- [ ] Review/refine Emails 4 and 5 (not touched this session)
