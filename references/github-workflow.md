# GitHub Workflow — Solopreneur Skill

## ภาพรวม

ทุกอย่างใน product development อยู่บน GitHub:
- **Issues** = tasks, user stories, bugs ทั้งหมด
- **Milestones** = sprints
- **Labels** = ประเภทของ issue
- **Docs** = committed เข้า repo เสมอ

---

## Step 0: GitHub Setup (ก่อน Intake)

ทุกครั้งที่ skill เริ่มต้นครั้งแรก ให้ตรวจสอบก่อนว่ามี GitHub repo แล้วหรือยัง

### ถ้ายังไม่มี repo → ให้ผู้ใช้สร้างก่อน

แนะนำผู้ใช้ด้วยขั้นตอนนี้:

```
1. ไปที่ github.com/new
2. ตั้งชื่อ repo ตามชื่อ product (lowercase, ใช้ - แทนเว้นวรรค)
   เช่น: my-freelance-app
3. เลือก Public หรือ Private ตามต้องการ
4. ✅ เลือก "Add a README file"
5. คลิก "Create repository"
6. Copy URL repo มาให้ครับ เช่น https://github.com/username/my-freelance-app
```

### เมื่อได้ repo URL แล้ว ให้ทำทันที

**1. Initialize โครงสร้างโฟลเดอร์ใน repo:**
```
docs/
├── 01-problem-solution.md
├── 02-lean-canvas.md
└── ... (สร้างเมื่อถึงแต่ละ phase)
```

**2. สร้าง Labels ใน GitHub:**

| Label | Color | ใช้สำหรับ |
|-------|-------|---------|
| `phase-1` | #0075ca | Problem/Solution |
| `phase-2` | #e4e669 | Business Model |
| `phase-3` | #d93f0b | Research/Validation |
| `phase-4` | #0e8a16 | SDLC |
| `user-story` | #5319e7 | Feature ที่ต้องพัฒนา |
| `bug` | #ee0701 | Bug ที่พบ |
| `docs` | #c2e0c6 | งาน documentation |
| `future` | #bfd4f2 | Future Backlog (ยังไม่ทำ) |
| `blocked` | #b60205 | ติดขัด รอ dependency |

**3. สร้าง Milestone สำหรับแต่ละ Sprint:**
```
Milestone: Sprint 1
Due date: [วันที่สิ้นสุด sprint]
Description: [Sprint Goal]
```

**วิธีสร้าง Labels และ Milestones ผ่าน GitHub CLI (ถ้ามี):**
```bash
gh label create "phase-1" --color "0075ca" --repo username/repo
gh milestone create "Sprint 1" --due-date "2025-06-01" --repo username/repo
```

---

## การสร้าง GitHub Issues

### ทุก User Story = 1 GitHub Issue

**Template สำหรับ User Story Issue:**

```markdown
Title: [US-001] As a [user] I want to [action]

## User Story
As a [user type]
I want to [action]
So that [outcome]

## Acceptance Criteria
- [ ] Given [...] When [...] Then [...]
- [ ] Given [...] When [...] Then [...]

## Technical Notes
[Agent Dev จะเติมส่วนนี้]

## QA Results
[Agent QA จะเติมส่วนนี้]

## Story Points
[X] points

## Sprint
Sprint [N]
```

**Labels ที่ต้องติด:** `user-story`, `phase-4`, และ priority label
**Milestone:** Sprint ที่จะทำ

---

### Bug = GitHub Issue

**Template สำหรับ Bug Issue:**

```markdown
Title: [BUG] [คำอธิบายสั้น]

## คำอธิบาย
[อธิบายปัญหา]

## Steps to Reproduce
1. [ขั้นตอน]
2. [ขั้นตอน]

## Expected Behavior
[ควรเป็นอย่างไร]

## Actual Behavior
[เป็นอย่างไรจริงๆ]

## Severity
- [ ] Critical
- [ ] High
- [ ] Medium
- [ ] Low

## Found by
Agent QA / Sprint Review / PO
```

**Labels:** `bug`, severity label
**Milestone:** Sprint ที่จะ fix

---

### Phase Gate = GitHub Issue

สร้าง issue สำหรับ checklist ก่อนผ่านแต่ละ phase:

```markdown
Title: [PHASE GATE] Phase 1 → Phase 2 Checklist

## Checklist
- [ ] Problem Statement ชัดเจน
- [ ] Customer Segment เจาะจง
- [ ] Solution Hypothesis กำหนดแล้ว
- [ ] Value Proposition เขียนแล้ว
- [ ] `docs/01-problem-solution.md` committed แล้ว

## ผู้อนุมัติ
@[username] (PO)
```

---

## Issue Lifecycle

```
Open → In Progress → In Review (QA) → Done (PO Approved) → Closed
```

**Labels ตาม status:**
- เปิดใหม่ = ไม่มี status label
- กำลังทำ = `in-progress`
- QA ตรวจ = `in-review`
- PO อนุมัติ = ปิด issue + comment "Approved by PO"

---

## Document Workflow — Commit ทุกครั้ง

### กฎสำคัญ: เอกสารทุกชิ้นต้องอยู่ใน repo เสมอ

หลังสร้างหรืออัปเดตเอกสาร Agent Docs ต้อง commit ทันที

**Commit Message Convention:**
```
docs(phase-1): add problem-solution statement
docs(phase-2): update lean-canvas with revenue model
docs(phase-4): add sprint-1-plan
docs(phase-4): update backlog after sprint-1-review
fix(docs): correct acceptance criteria in sprint-1-plan
```

**โครงสร้าง docs/ ใน repo:**
```
docs/
├── 01-problem-solution.md
├── 02-lean-canvas.md
├── 02-business-model.md
├── 03-validation-plan.md
├── 03-interview-guide.md
├── 03-validation-results.md
├── 04-prd.md
├── 04-architecture.md
├── 04-tech-stack.md
├── 04-definition-of-done.md
├── 04-backlog.md
├── 04-test-plan.md
├── 04-bug-log.md
├── 04-sprint-1-plan.md
├── 04-sprint-1-review.md
├── 04-sprint-1-retro.md
└── 04-release-v1.0.md
```

---

## Sprint Workflow บน GitHub

### Sprint Planning
1. สร้าง Milestone สำหรับ Sprint ใหม่
2. สร้าง Issue สำหรับแต่ละ User Story
3. Assign issues เข้า Milestone
4. สร้าง `docs/04-sprint-N-plan.md` → commit

### During Sprint
- Agent Dev: comment implementation plan ใน Issue
- Agent QA: comment QA Report ใน Issue พร้อม verdict
- ถ้า QA FAIL → reopen issue + label `needs-fix`
- ถ้า QA PASS → label `in-review` รอ PO

### Sprint Review
- PO ตรวจ Issue ที่ label `in-review` ทีละอัน
- ถ้า approve → close issue + comment "✅ Approved"
- ถ้า reject → comment เหตุผล + label `needs-fix` + reopen
- Agent Docs สร้าง `docs/04-sprint-N-review.md` → commit

### Sprint Retrospective
- Agent Docs สร้าง `docs/04-sprint-N-retro.md` → commit
- สร้าง Milestone สำหรับ Sprint ถัดไป

---

## คำถามที่ต้องถามผู้ใช้ตอน Setup

```
1. GitHub repo URL คืออะไร?
2. คุณมี GitHub CLI (gh) ติดตั้งอยู่ไหม?
   (ถ้ามี จะช่วยสร้าง labels/milestones/issues ผ่าน command ได้เลย)
3. repo เป็น Public หรือ Private?
```

ถ้าไม่มี GitHub CLI → ให้ link ไปที่ GitHub web UI พร้อม instructions ทีละขั้น
ถ้ามี GitHub CLI → สร้าง labels, milestones, issues ผ่าน `gh` commands เลย
