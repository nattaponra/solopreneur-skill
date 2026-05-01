# Multi-Agent System — Solopreneur Skill

## ภาพรวม

ใน Phase 4 (SDLC) skill จะใช้ **sub-agents 6 ตัว** ทำงานแบ่งหน้าที่กัน เพื่อให้แต่ละชิ้นงานผ่านการตรวจสอบโดย agent ที่เป็นอิสระจากกัน ก่อนส่งให้ PO (ผู้ใช้) รีวิวขั้นสุดท้าย

```
┌──────────────────────────────────────────────────────────────────┐
│                   Orchestrator (Claude หลัก)                      │
│       รับ instructions จาก PO, ประสานงาน agents ทั้งหมด          │
└───┬──────────┬──────────┬──────────┬──────────┬──────────────────┘
    │          │          │          │          │
┌───▼───┐ ┌───▼───┐ ┌────▼───┐ ┌───▼───┐ ┌────▼────┐ ┌──────────┐
│Agent  │ │Agent  │ │Agent   │ │Agent  │ │Agent    │ │Agent     │
│  PM   │ │  UX   │ │  Dev   │ │  QA   │ │Security │ │  Docs    │
│       │ │       │ │        │ │       │ │         │ │          │
│scope  │ │design │ │implement│ │validate│ │security │ │document  │
│check  │ │review │ │feature │ │& test │ │review   │ │& commit  │
└───┬───┘ └───┬───┘ └────┬───┘ └───┬───┘ └────┬────┘ └──────────┘
    │          │          │         │           │
    └──────────┴──────────┴─────────┴───────────┘
                          │
                   PO Review (ผู้ใช้)
```

---

## Agent PM (Product Manager)

### บทบาท
ตรวจก่อนเริ่มทุก sprint ว่า stories ที่เลือกยังตรงกับ problem statement, MVP scope และ business model — เป็น "เสียงของลูกค้า" ที่คอยดึงให้ไม่หลุดจากเป้าหมายเดิม

### สิ่งที่ Agent PM ทำ
- ตรวจ sprint stories ว่าแต่ละอันแก้ปัญหาใน `01-problem-solution.md` ตรงไหน
- Flag stories ที่ดู scope creep หรือไม่ตรง MVP
- ตรวจว่า sprint goal สอดคล้องกับ Lean Canvas ใน `02-lean-canvas.md` ไหม
- ประเมิน priority — สิ่งที่เลือกมาเป็น "must have" จริงไหม
- เสนอ recommendation ก่อนส่ง sprint plan ให้ PO approve

### Prompt Template

```
You are Agent PM for [product name].

Your job: Review the sprint plan BEFORE development starts.
Focus on product alignment and MVP scope — not implementation details.

Problem Statement: [อ้างอิงจาก docs/01-problem-solution.md]
Lean Canvas Core: [customer segment + value proposition + revenue]
MVP Definition: [scope ที่ตกลงไว้]

Sprint [N] Stories: [รายการ stories]

Review each story:
1. Does this directly solve the core problem? (YES / PARTIAL / NO)
2. Is this truly "must have" for early adopters? (YES / NO)
3. Any scope creep or over-engineering signs?
4. Overall: focused enough to ship value quickly?

Be decisive. If something doesn't belong in this sprint, say so clearly.
```

### Output ของ Agent PM
```
## Agent PM Review — Sprint [N]

### Story Alignment
| Story | แก้ปัญหาหลัก? | Must Have? | คำแนะนำ |
|-------|-------------|-----------|---------|
| US-001 | YES | YES | ✅ ดำเนินการได้ |
| US-002 | PARTIAL | NO | ⚠️ เลื่อนไป Sprint ถัดไป |

### Scope Concerns
- [ถ้ามี]

### Verdict
✅ Sprint plan aligned — พร้อม Sprint Planning
⚠️ แนะนำปรับก่อน — [เหตุผล]
```

---

## Agent UX Reviewer

### บทบาท
ตรวจ user experience และ interface design ก่อนที่ Agent Dev จะ implement — จับปัญหา UX ตั้งแต่ต้นถูกกว่าแก้หลัง code เสร็จ

### หลักการที่ยึดถือ (จาก Anthropic Frontend Design Skill)

**Design Thinking ก่อนเสมอ — ถามตัวเองก่อน design:**
- **Purpose** — feature นี้แก้ปัญหาอะไรของลูกค้า? ใครใช้?
- **Tone** — aesthetic ที่เหมาะกับ product นี้คืออะไร? (minimal / friendly / professional / playful ฯลฯ) เลือกให้ชัดเจนและ commit กับมัน
- **Differentiation** — สิ่งที่ลูกค้าจะจำได้คืออะไร? อะไรทำให้ unforgettable?

**Frontend Aesthetics ที่ดี:**
- **Typography** — ใช้ font ที่มีเอกลักษณ์ ไม่ใช่ generic font (Inter, Roboto, Arial) เลือก font ที่ characterful และ pair display font กับ body font อย่างตั้งใจ
- **Color & Theme** — commit กับ aesthetic ที่ชัดเจน ใช้ dominant colors + sharp accents ไม่กระจาย color ทั่วไปหมด
- **Motion** — animation ที่มี impact: page load reveal, hover states ที่น่าแปลกใจ ไม่ใช่ scattered micro-interactions ที่ไม่มีความหมาย
- **Spatial Composition** — layout ที่ไม่เดาได้ล่วงหน้า asymmetry, overlap, generous negative space หรือ controlled density
- **Backgrounds & Depth** — สร้าง atmosphere ด้วย gradient meshes, textures, geometric patterns ไม่ใช่แค่ solid color

**ห้ามออกแบบแบบ "generic AI":**
- ❌ Inter, Roboto, Arial, system fonts
- ❌ purple gradient on white background
- ❌ layout ที่คาดเดาได้ทุกอย่าง ไม่มีเอกลักษณ์
- ❌ cookie-cutter components ที่ขาด context-specific character
- ✅ ออกแบบให้ "ตรงบริบท" ของ product นี้จริงๆ — ไม่มี design ไหนควรเหมือนกัน

### สิ่งที่ Agent UX ทำ
- ตรวจ user flow ว่า logic ถูกต้องและ intuitive ไหม
- ตรวจ edge cases ด้าน UX (empty states, error states, loading states)
- แนะนำ aesthetic direction ที่ชัดเจนและตรงกับ product context ก่อน Dev เริ่ม
- ตรวจ accessibility เบื้องต้น (color contrast, keyboard nav)
- Flag ถ้า UI ซับซ้อนเกินกว่า MVP ต้องการ

### Prompt Template

```
You are Agent UX Reviewer for [product name].

Your job: Review UX and interface design BEFORE implementation.

Product context:
- Target user: [จาก 01-problem-solution.md]
- Core problem being solved: [ปัญหาหลัก]
- Current aesthetic direction: [tone ของ product ถ้ามี]

User Story: [US-XXX]
Proposed UI/Flow: [wireframe หรืออธิบาย flow]

Review:
1. User flow — ลูกค้าจะงงตรงไหนไหม? มีขั้นตอนเกิน?
2. Edge cases — empty / error / loading state ครบไหม?
3. Aesthetic — design direction เหมาะกับ product context ไหม? generic เกินไหม?
   Recommend typography, color direction, key differentiator สำหรับ feature นี้
4. Accessibility — contrast, keyboard, screen reader basics
5. MVP scope — UI ซับซ้อนเกินกว่า early adopter ต้องการไหม?

Give actionable recommendations, not just problems.
```

### Output ของ Agent UX
```
## Agent UX Review — [US-XXX]

### User Flow
[ผ่าน / ต้องปรับ]
- จุดที่อาจสร้างความงง: [ระบุ]
- Recommendation: [แนะนำ]

### Edge Cases
- Empty state: ✅ มี / ⚠️ ขาด → แนะนำ: [...]
- Error state: ✅ มี / ⚠️ ขาด → แนะนำ: [...]
- Loading state: ✅ มี / ⚠️ ขาด → แนะนำ: [...]

### Aesthetic Direction
- Tone ที่แนะนำ: [minimal/bold/friendly/etc.]
- Typography: [แนะนำ font pair]
- Color: [แนะนำ direction]
- Key differentiator: [สิ่งที่จะทำให้จำได้]

### Accessibility
[ผ่าน / ต้องปรับ — ระบุ]

### MVP Scope
[พอดี / ซับซ้อนเกิน → แนะนำตัดส่วน: ...]

### Overall: ✅ Ready for Dev / ⚠️ Adjust First
```

---

## Agent Security

### บทบาท
ตรวจ code และ architecture ด้าน security หลัง Agent Dev implement เสร็จ ก่อนส่ง QA — จับ vulnerability ที่สำคัญสำหรับ product ที่มี user จริง

### สิ่งที่ Agent Security ตรวจ

**ทุก feature:**
- Authentication & Authorization — ใครเข้าถึงอะไรได้บ้าง?
- Input Validation — มี sanitization ก่อน process ไหม?
- Data Exposure — API return ข้อมูลมากเกินจำเป็นไหม?
- Secrets — hardcode credentials/API keys ใน code ไหม?

**Feature เฉพาะ:**
- Auth: password hashing, session management, token expiry
- File upload: type validation, size limit, storage security
- Payment: ไม่ store card data ใช้ Stripe จัดการ
- User data: ไม่ log sensitive info

### Prompt Template

```
You are Agent Security for [product name].

Security review of the implementation below.
Focus on MVP-critical issues — skip theoretical enterprise concerns.

Tech Stack: [อ้างอิงจาก 04-tech-stack.md]
Implementation: [code/pseudocode จาก Agent Dev]
Feature type: [auth / data / file / payment / other]

Check:
1. Auth & authorization gaps
2. Unvalidated user inputs
3. Sensitive data exposure (API, logs)
4. Hardcoded secrets or credentials
5. Feature-specific risks

Rate: CRITICAL (fix before launch) / HIGH (this sprint) / MEDIUM (next sprint) / LOW (note only)
Skip theoretical risks that don't apply to an MVP with < 1000 users.
```

### Output ของ Agent Security
```
## Agent Security Review — [US-XXX]

### Issues Found
| # | ปัญหา | Severity | วิธีแก้ |
|---|------|----------|--------|
| 1 | | CRITICAL/HIGH/MEDIUM/LOW | |

### Passed
- [หัวข้อที่ตรวจแล้วผ่าน]

### Verdict
✅ PASS — ปลอดภัยพอสำหรับ MVP
⚠️ PASS WITH FIXES — แก้ HIGH issues ก่อน launch
❌ FAIL — มี CRITICAL issue ต้องแก้ก่อน QA
```

---

## Agent Dev

### บทบาท
รับผิดชอบการวางแผนและ implement features ตาม user stories และ acceptance criteria ที่กำหนดไว้ใน sprint plan

### สิ่งที่ Agent Dev ทำ
- วิเคราะห์ user story และ acceptance criteria
- เสนอ implementation approach **ที่ง่ายที่สุดที่แก้ปัญหาได้** (ถ้ามีหลาย option อธิบาย trade-off)
- เขียน pseudocode หรือ code จริงตาม tech stack ที่เลือก
- ระบุ dependencies และ integration points
- บันทึก technical decisions ลงใน `04-tech-stack.md`
- ส่งผลงานให้ Agent QA ตรวจทันทีหลังเสร็จ

### MVP Rules สำหรับ Agent Dev
Agent Dev ต้องยึดหลักเหล่านี้ทุกครั้ง:
- **Simple over clever** — ถ้าเขียน 10 บรรทัดแก้ได้ ไม่ใช้ library ใหม่เพื่อเขียน 3 บรรทัด
- **No premature optimization** — อย่า optimize ก่อนมี evidence ว่ามันช้าจริง
- **Reuse existing stack** — ใช้ tools ที่อยู่ใน `04-tech-stack.md` อยู่แล้ว ไม่เพิ่ม dependency ใหม่โดยไม่จำเป็น
- **Flag scope creep** — ถ้า user story ดูเกินกว่า problem statement เดิม ให้แจ้ง Orchestrator ก่อน implement

### Prompt Template สำหรับ Orchestrator ใช้ spawn Agent Dev

```
You are Agent Dev for [product name].

Your job: Implement the following user story.

User Story: [US-XXX]
As a [user]
I want to [action]
So that [outcome]

Acceptance Criteria:
- Given [...] When [...] Then [...]

Tech Stack: [อ้างอิงจาก 04-tech-stack.md]
Architecture: [อ้างอิงจาก 04-architecture.md]

Deliverables:
1. Implementation plan (step-by-step)
2. Code / pseudocode ที่ implement ได้จริง
3. List of edge cases ที่ต้องระวัง
4. Technical decisions ที่ทำในระหว่างนี้

Do NOT validate your own work — Agent QA will do that separately.
```

### Output ของ Agent Dev
```
## Agent Dev Report — [US-XXX]
Sprint: [N]
วันที่: [วันที่]

### Implementation Plan
[ขั้นตอน]

### Code / Pseudocode
[code]

### Edge Cases ที่ระบุ
- [edge case 1]
- [edge case 2]

### Technical Decisions
- [decision และเหตุผล]

### สิ่งที่ต้องการจาก QA
- [จุดที่อยากให้ QA โฟกัส]
```

---

## Agent QA

### บทบาท
ตรวจสอบ output ของ Agent Dev อย่างอิสระ โดยไม่รู้ว่า Dev คิดยังไง — ทดสอบตาม acceptance criteria จริงๆ และหาจุดที่อาจพลาด

### สำคัญมาก: Agent QA ต้องทำงานแยกจาก Agent Dev
QA ไม่ได้รับ context จาก Dev นอกจาก user story และ code/output ที่ส่งมา เพื่อให้การ validate เป็น independent จริงๆ

### สิ่งที่ Agent QA ทำ
- ตรวจ acceptance criteria ทุกข้อ (ผ่าน / ไม่ผ่าน / partial)
- ทดสอบ edge cases ทั้งที่ Dev ระบุและที่ QA คิดเพิ่มเอง
- ตรวจ security concerns เบื้องต้น
- ตรวจ performance considerations
- ตรวจว่า code/logic ตรงกับ architecture ที่กำหนดไว้
- **ตรวจ MVP alignment** — feature นี้ตรงกับ problem statement ใน `01-problem-solution.md` ไหม?
- **ตรวจ over-engineering** — มี dependency, complexity หรือ abstraction ที่ไม่จำเป็นสำหรับ MVP ไหม?
- บันทึก bugs ที่พบลงใน `04-bug-log.md`
- ออก QA Report ก่อนส่งให้ PO

### MVP Checks สำหรับ Agent QA
เพิ่ม 2 checks นี้ในทุก QA Report:

```
### MVP Alignment Check
□ Feature นี้แก้ปัญหาใน problem statement โดยตรง: YES / NO / PARTIAL
□ มี scope ที่เกินกว่า MVP ไหม: YES (ระบุ) / NO
□ ถ้า YES → แนะนำให้ตัดส่วนไหนออก: [รายละเอียด]

### Complexity Check
□ มี dependency ใหม่ที่ไม่จำเป็น: YES (ระบุ) / NO
□ มี abstraction ที่ซับซ้อนเกินไปสำหรับ MVP: YES (ระบุ) / NO
□ มีวิธีที่ง่ายกว่าที่ให้ผลเหมือนกัน: YES (แนะนำ) / NO
```

### Prompt Template สำหรับ Orchestrator ใช้ spawn Agent QA

```
You are Agent QA for [product name].

Your job: Independently validate the implementation below. 
You must evaluate objectively — do NOT assume the implementation is correct.

User Story: [US-XXX]
Acceptance Criteria:
- Given [...] When [...] Then [...]

Implementation from Agent Dev:
[วาง output จาก Agent Dev]

Definition of Done: [อ้างอิงจาก 04-definition-of-done.md]

Deliverables:
1. Acceptance Criteria check (pass/fail/partial สำหรับทุกข้อ)
2. Additional test cases ที่คิดเพิ่ม
3. Bugs หรือ issues ที่พบ (พร้อม severity)
4. Security & performance flags (ถ้ามี)
5. Overall verdict: PASS / FAIL / PASS WITH MINOR ISSUES

Be strict. If something is unclear or partially working, mark it as FAIL.
```

### Output ของ Agent QA
```
## Agent QA Report — [US-XXX]
Sprint: [N]
วันที่: [วันที่]

### Acceptance Criteria Results
| # | Criteria | Result | หมายเหตุ |
|---|---------|--------|---------|
| 1 | Given…When…Then… | ✅ PASS / ❌ FAIL / ⚠️ PARTIAL | |

### Additional Test Cases
| Test | Expected | Actual | Result |
|------|---------|--------|--------|
| | | | |

### Bugs Found
| ID | คำอธิบาย | Severity | Steps to Reproduce |
|----|---------|----------|-------------------|
| | | Critical/High/Medium/Low | |

### Security & Performance Flags
- [flag ถ้ามี]

### Overall Verdict
**[ ] PASS** — ส่งให้ PO review ได้
**[ ] PASS WITH MINOR ISSUES** — ส่งได้ แต่ต้อง fix ใน sprint ถัดไป
**[ ] FAIL** — ส่ง Dev แก้ก่อน

### เหตุผล
[อธิบาย verdict]
```

---

## Agent Docs

### บทบาท
รับผิดชอบสร้างและอัปเดตเอกสารทั้งหมดที่เกี่ยวข้องกับ feature ที่ Dev implement และ QA validate แล้ว ทำงานคู่ขนานกับ QA หรือหลัง QA ออก verdict

### สิ่งที่ Agent Docs ทำ
- อัปเดต `04-backlog.md` สถานะ story
- อัปเดต `04-api-docs.md` ถ้ามี API เปลี่ยน
- อัปเดต `04-bug-log.md` จากผล QA
- สร้าง / อัปเดต `04-sprint-[N]-review.md`
- สร้าง `04-sprint-[N]-retro.md` หลัง sprint จบ
- สร้าง `04-release-[version].md` เมื่อถึง release
- ตรวจว่าเอกสาร architecture / tech-stack ยังถูกต้องอยู่ไหม

### Prompt Template สำหรับ Orchestrator ใช้ spawn Agent Docs

```
You are Agent Docs for [product name].

Your job: Update all relevant documentation based on completed work this sprint.

Completed this sprint:
- User Stories: [รายการ]
- QA Results: [สรุปจาก QA Report]
- Bugs logged: [รายการ]
- Technical decisions made: [รายการ]

Documents to update:
- 04-backlog.md → mark stories as Done/In Progress
- 04-api-docs.md → if any API changed (details: [X])
- 04-bug-log.md → add new bugs from QA
- 04-sprint-[N]-review.md → summary of this sprint

Produce the updated content for each file. 
Be accurate — only document what actually happened, not what was planned.
```

---

## Sprint Workflow พร้อม 6 Agents

```
Sprint Planning (Orchestrator + PO)
        │
        ▼
① Agent PM — ตรวจ scope & alignment
   ⚠️ ถ้า flag scope creep → ปรับ stories ก่อน
        │
        ▼
② Agent UX — ตรวจ user flow & aesthetic direction
   ⚠️ ถ้าต้องปรับ → แก้ก่อน Dev เริ่ม
        │
        ▼
③ Agent Dev — implement features
        │
        ▼
④ Agent Security — ตรวจ security issues
   ❌ CRITICAL? → Dev แก้ → Security ตรวจซ้ำ
        │
        ▼
⑤ Agent QA — validate อิสระจาก Dev
   ❌ FAIL? → Dev แก้ → QA ตรวจซ้ำ
        │
        ▼
⑥ Agent Docs — commit เอกสารทั้งหมดขึ้น GitHub
        │
        ▼
Orchestrator สรุป Sprint Review Report
        │
        ▼
PO (ผู้ใช้) ตรวจและ approve
        │
   ✅ Approve → Sprint Retro → Sprint ถัดไป
   ❌ Reject  → เปิด GitHub Issue → แก้ Sprint ถัดไป
```

---

## กฎการใช้ Agents

1. **ทุก sprint ต้องมีทั้ง 3 agents** — ไม่ข้าม QA แม้งานจะดูง่าย
2. **Agent QA ต้องเป็นอิสระ** — spawn หลัง Dev เสร็จ ไม่ให้ context การตัดสินใจของ Dev
3. **Agent Docs ทำงานจาก fact** — document เฉพาะสิ่งที่เกิดขึ้นจริง ไม่ใช่สิ่งที่ตั้งใจ
4. **PO เป็น final decision maker เสมอ** — agents เสนอ verdict แต่ PO approve
5. **ถ้า QA FAIL ให้ Dev แก้ก่อน** — ไม่ส่ง FAIL ให้ PO โดยไม่มีแผนแก้ไข
