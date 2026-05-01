# Multi-Agent System — Solopreneur Skill

## ภาพรวม

ใน Phase 4 (SDLC) skill จะใช้ **sub-agents 3 ตัว** ทำงานแบ่งหน้าที่กัน เพื่อให้แต่ละชิ้นงานผ่านการตรวจสอบโดย agent ที่เป็นอิสระจากกัน ก่อนส่งให้ PO (ผู้ใช้) รีวิวขั้นสุดท้าย

```
┌─────────────────────────────────────────────────────┐
│                   Orchestrator (Claude หลัก)         │
│  รับ instructions จาก PO, ประสานงาน agents ทั้งหมด  │
└──────────┬──────────────┬──────────────┬────────────┘
           │              │              │
     ┌─────▼─────┐  ┌─────▼─────┐  ┌───▼──────┐
     │ Agent Dev │  │ Agent QA  │  │Agent Docs│
     │           │  │           │  │          │
     │ implement │  │ validate  │  │ document │
     │ features  │  │ & test    │  │ & update │
     └─────┬─────┘  └─────┬─────┘  └───┬──────┘
           │              │              │
           └──────────────▼──────────────┘
                    PO Review (ผู้ใช้)
```

---

## Agent Dev

### บทบาท
รับผิดชอบการวางแผนและ implement features ตาม user stories และ acceptance criteria ที่กำหนดไว้ใน sprint plan

### สิ่งที่ Agent Dev ทำ
- วิเคราะห์ user story และ acceptance criteria
- เสนอ implementation approach (ถ้ามีหลาย option อธิบาย trade-off)
- เขียน pseudocode หรือ code จริงตาม tech stack ที่เลือก
- ระบุ dependencies และ integration points
- บันทึก technical decisions ลงใน `04-tech-stack.md`
- ส่งผลงานให้ Agent QA ตรวจทันทีหลังเสร็จ

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
- บันทึก bugs ที่พบลงใน `04-bug-log.md`
- ออก QA Report ก่อนส่งให้ PO

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

## Sprint Workflow พร้อม Agents

```
Sprint Planning (Orchestrator + PO)
        │
        ▼
Agent Dev implements stories
        │
        ▼
Agent QA validates (อิสระจาก Dev)
        │
   ┌────▼────┐
   │ PASS?   │
   └────┬────┘
        │ YES                    NO → Dev แก้ → QA ตรวจซ้ำ
        ▼
Agent Docs อัปเดตเอกสาร
(ทำคู่ขนาน หรือหลัง QA)
        │
        ▼
Orchestrator สรุปรายงาน Sprint Review
        │
        ▼
PO (ผู้ใช้) ตรวจ Sprint Review Report
        │
   ┌────▼────┐
   │Approve? │
   └────┬────┘
        │ YES → Sprint Retrospective → Sprint ถัดไป
        │ NO  → เปิด issue → บันทึกใน bug log → แก้ใน sprint ถัดไป
```

---

## กฎการใช้ Agents

1. **ทุก sprint ต้องมีทั้ง 3 agents** — ไม่ข้าม QA แม้งานจะดูง่าย
2. **Agent QA ต้องเป็นอิสระ** — spawn หลัง Dev เสร็จ ไม่ให้ context การตัดสินใจของ Dev
3. **Agent Docs ทำงานจาก fact** — document เฉพาะสิ่งที่เกิดขึ้นจริง ไม่ใช่สิ่งที่ตั้งใจ
4. **PO เป็น final decision maker เสมอ** — agents เสนอ verdict แต่ PO approve
5. **ถ้า QA FAIL ให้ Dev แก้ก่อน** — ไม่ส่ง FAIL ให้ PO โดยไม่มีแผนแก้ไข
