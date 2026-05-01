# Solopreneur Skill

Claude skill สำหรับ Solo Entrepreneur ที่ต้องการพัฒนา Digital Product อย่างเป็นระบบ ตั้งแต่ไอเดียจนถึง launch — พร้อมระบบ 8 sub-agents ตรวจสอบคุณภาพทุก sprint

---

## ครอบคลุมอะไรบ้าง

| Phase | หัวข้อ | รายละเอียด |
|-------|--------|-----------|
| 1 | Problem / Solution Fit | Problem statement, value proposition, customer segment |
| 2 | Business Model | Lean Canvas, revenue model, unit economics, go-to-market |
| 3 | Research & Validation | User interview, hypothesis testing, MVP definition |
| 4 | SDLC with Scrum | Backlog, sprint planning, sprint review (คุณเป็น PO), retrospective |

- **ภาษา:** ไทย / English
- **Framework:** Scrum — คุณรับบทบาท Product Owner ตรวจงานทุก Sprint
- **MVP-focused:** มี guardrails ป้องกัน scope creep และ over-engineering ตลอดเวลา
- **GitHub-first:** tasks ทุกอย่างผ่าน GitHub Issues, เอกสารทั้งหมด commit ขึ้น repo

---

## 8-Agent System

ใน Phase 4 ทุก sprint ผ่านการตรวจสอบโดย sub-agents 8 ตัวตามลำดับ ก่อนส่งให้คุณ (PO) approve:

```
① Agent PM            → ตรวจ scope & MVP alignment ก่อน Dev เริ่ม
② Agent UX            → ตรวจ user flow & aesthetic direction
③ Agent Dev           → implement features
④ Agent Code Reviewer → ตรวจ code smells & clean code
⑤ Agent Security      → ตรวจ security issues
⑥ Agent QA            → validate อิสระ — PASS / FAIL
⑦ Agent Docs     ┐    → commit เอกสารขึ้น GitHub
⑧ Agent Manual   ┘    → อัปเดต User Manual + screenshot placeholders
        ↓
  PO (คุณ) approve
```

---

## วิธีติดตั้งบน Claude Code

### วิธีที่ 1 — Clone โดยตรง (แนะนำ)

```bash
# Personal skill — ใช้ได้ทุก project
git clone https://github.com/nattaponra/solopreneur-skill.git \
  ~/.claude/skills/solopreneur-skill
```

```bash
# Project skill — ใช้เฉพาะ project นั้น
git clone https://github.com/nattaponra/solopreneur-skill.git \
  .claude/skills/solopreneur-skill
```

### วิธีที่ 2 — Copy ด้วยตัวเอง

```bash
mkdir -p ~/.claude/skills/solopreneur-skill
cp SKILL.md ~/.claude/skills/solopreneur-skill/
cp -r references ~/.claude/skills/solopreneur-skill/
```

### เรียกใช้งาน

```
/solopreneur-skill
```

หรือให้ Claude เรียกอัตโนมัติเมื่อตรวจพบว่าคุณกำลัง develop product

---

## ตัวอย่างการใช้งาน

### 🌱 เริ่มจากศูนย์ — มีแค่ไอเดีย

```
ฉันมีไอเดียอยากสร้าง app ช่วยให้ freelancer ออก invoice ได้เร็วขึ้น
```

Skill จะ: ถาม → define problem statement → ระบุ customer segment → บันทึก `01-problem-solution.md` → พาไป Phase 2

---

### 📊 Phase 2 — Business Model

```
ช่วยทำ Lean Canvas ให้หน่อย product ของฉันคือ SaaS สำหรับ freelancer
```

Skill จะ: กรอก Lean Canvas ทีละ block → แนะนำ revenue model → ประมาณ unit economics → บันทึก `02-lean-canvas.md`

---

### 🧪 Phase 3 — Validate ก่อนสร้าง

```
อยากทดสอบว่ามีคนต้องการ product นี้จริงไหม ก่อนจะเริ่มสร้าง
```

Skill จะ: กำหนด hypothesis → สร้าง user interview guide (Mom Test) → แนะนำ MVP type → บันทึก `03-validation-plan.md`

---

### 🚀 Phase 4 — เริ่มพัฒนา Sprint แรก

```
validate แล้ว พร้อมสร้างแล้ว อยากเริ่ม sprint แรก
```

Skill จะ: เขียน PRD + Architecture → สร้าง Product Backlog + User Stories → วาง Sprint 1 Plan → ส่ง agents ทั้ง 8 ทำงาน

---

### 🤖 Sprint ทุกอัน — 8 Agents ทำงานอัตโนมัติ

```
Sprint 1 เริ่มเลย feature แรกคือ user login
```

| Agent | สิ่งที่ทำ |
|-------|---------|
| PM | ตรวจว่า login ตรง MVP scope ไหม |
| UX | ตรวจ user flow + แนะนำ aesthetic direction |
| Dev | implement login feature |
| Code Reviewer | ตรวจ code smells, naming, DRY |
| Security | ตรวจ auth, password hashing, token expiry |
| QA | ตรวจ acceptance criteria ทุกข้อ — PASS/FAIL |
| Docs | commit sprint plan, review, bug log ขึ้น GitHub |
| Manual | อัปเดต User Manual + `[SCREENSHOT: login form]` |

ถ้า QA **FAIL** → Dev แก้ → QA ตรวจซ้ำ → ผ่านแล้วค่อยส่งคุณ review

---

### 📄 เอกสารที่ได้ตลอด Journey (commit ขึ้น GitHub ทั้งหมด)

```
docs/
├── 01-problem-solution.md       ← Phase 1
├── 02-lean-canvas.md            ← Phase 2
├── 02-business-model.md         ← Phase 2
├── 03-validation-plan.md        ← Phase 3
├── 03-interview-guide.md        ← Phase 3
├── 03-validation-results.md     ← Phase 3
├── 04-prd.md                    ← Phase 4
├── 04-architecture.md           ← Phase 4
├── 04-tech-stack.md             ← Phase 4
├── 04-definition-of-done.md     ← Phase 4
├── 04-backlog.md                ← Phase 4 (อัปเดตทุก sprint)
├── 04-test-plan.md              ← Phase 4
├── 04-bug-log.md                ← Phase 4 (อัปเดตต่อเนื่อง)
├── 04-user-manual.md            ← Phase 4 (อัปเดตทุก sprint + screenshots)
├── 04-sprint-1-plan.md          ← Sprint 1
├── 04-sprint-1-review.md        ← Sprint 1
├── 04-sprint-1-retro.md         ← Sprint 1
└── 04-release-v1.0.md           ← เมื่อ launch
```

---

## โครงสร้างไฟล์

```
solopreneur-skill/
├── SKILL.md                        # ไฟล์หลัก — frontmatter + instructions
└── references/
    ├── problem-solution.md         # Phase 1 templates & checklist
    ├── business-model.md           # Phase 2 — Lean Canvas, revenue model
    ├── research-validation.md      # Phase 3 — hypothesis, interview guide, MVP
    ├── sdlc-scrum.md               # Phase 4 — Scrum workflow + SDLC document templates
    ├── agents.md                   # 8-agent system — roles, prompts, outputs
    └── github-workflow.md          # GitHub setup, Issues, Labels, Milestones
```

---

## License

MIT
