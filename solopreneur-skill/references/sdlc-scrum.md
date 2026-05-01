# Phase 4: SDLC with Scrum

## เป้าหมาย
พัฒนา Digital Product อย่างเป็นระบบผ่าน Scrum Framework โดยผู้ใช้ทำหน้าที่ Product Owner (PO) ตรวจงานทุก Sprint

---

## โครงสร้าง Scrum สำหรับ Solo Entrepreneur

| บทบาท | ใคร | หน้าที่ |
|--------|-----|---------|
| **Product Owner** | คุณ (ผู้ใช้) | กำหนด priority, ตรวจงาน, approve sprint |
| **Scrum Master** | Claude | อำนวยความสะดวก, track progress, ชี้ blockers |
| **Development Team** | Claude + นักพัฒนาของคุณ | วางแผนและส่งมอบ features |

---

## Sprint Cycle (2 สัปดาห์)

```
Week 1: Sprint Planning → Development
Week 2: Development → Sprint Review (PO ตรวจ) → Retrospective

Timeline:
วันที่ 1: Sprint Planning
วันที่ 2-9: Development
วันที่ 10: Sprint Review (PO Review)
วันที่ 10: Sprint Retrospective
→ วนซ้ำ
```

---

## Product Backlog

### การสร้าง Backlog จาก MVP

หลังจาก Phase 3 ให้แปลง features ทั้งหมดเป็น User Stories ใน Backlog

**User Story Format:**
```
As a [ประเภทผู้ใช้]
I want to [สิ่งที่ต้องการทำ]
So that [ผลลัพธ์ที่ต้องการ]
```

**ตัวอย่าง:**
```
As a Freelance Designer
I want to generate a proposal from a template
So that I can send it to clients within 10 minutes
```

### Backlog Template

| ID | User Story | Priority | Story Points | Status |
|----|-----------|----------|--------------|--------|
| US-001 | As a… I want… So that… | High | 5 | To Do |
| US-002 | … | Medium | 3 | To Do |

**Priority Levels:**
- **Must Have** — MVP ต้องมี ไม่มีไม่ได้
- **Should Have** — สำคัญมาก แต่ไม่ block MVP
- **Could Have** — ดีถ้ามี แต่ตัดได้
- **Won't Have (this sprint)** — ไว้ sprint หน้า

### Story Points (ประมาณเวลา)
- **1 point** = งานเล็กมาก ใช้เวลาไม่เกิน 1 วัน
- **2 points** = งานเล็ก 1-2 วัน
- **3 points** = งานกลาง 2-3 วัน
- **5 points** = งานใหญ่ 3-5 วัน
- **8 points** = งานใหญ่มาก ควรแตกออก

---

## Sprint Planning

### สิ่งที่ต้องทำในการ Planning

**1. กำหนด Sprint Goal:**
```
Sprint [N] Goal:
ภายใน 2 สัปดาห์นี้ เราจะ [ผลลัพธ์ที่ต้องการ]
เพื่อ [เหตุผลทางธุรกิจ]
```

**2. เลือก Stories จาก Backlog:**
- ดู velocity จาก sprint ที่แล้ว (sprint แรก ประมาณ 20-30 points)
- เลือก stories ที่ match Sprint Goal
- ตรวจว่าทุก story มี Acceptance Criteria ชัดเจน

**3. Acceptance Criteria Template:**
```
User Story: [ชื่อ story]

Acceptance Criteria:
- Given [สถานการณ์เริ่มต้น]
  When [ผู้ใช้ทำอะไร]
  Then [ผลลัพธ์ที่เกิดขึ้น]

- Given […]
  When […]
  Then […]

Definition of Done:
- [ ] Code เขียนเสร็จและ review แล้ว
- [ ] Test ผ่าน
- [ ] Deploy to staging
- [ ] PO review และ approve
```

### Sprint Planning Output Template
```
## Sprint [N] Plan
วันที่: [start] → [end]
Sprint Goal: [เป้าหมาย]

Stories ใน Sprint นี้:
| Story | Points | Owner |
|-------|--------|-------|
| US-001 | 5 | |
| US-002 | 3 | |
Total: [X] points

Dependencies & Risks:
- [dependency หรือ risk]

Definition of Done for this Sprint:
- [ ] [เงื่อนไข]
```

---

## Daily Progress Tracking

แม้จะเป็น Solo Entrepreneur ควรมี daily check-in:

```
วันที่: [วัน]
เมื่อวาน:
- ✅ ทำอะไรไปบ้าง

วันนี้:
- 🎯 จะทำอะไร

Blockers:
- ⚠️ มีอะไรติดขัดไหม
```

---

## Sprint Review (PO Review)

นี่คือ checkpoint สำคัญที่สุด — **คุณในฐานะ PO ตรวจและ approve งาน**

### Sprint Review Checklist สำหรับ PO

**ก่อน Review:**
- [ ] ได้รับ demo/delivery จาก dev team แล้ว
- [ ] ทราบ Sprint Goal และ stories ที่กำหนดไว้

**ระหว่าง Review — ทดสอบแต่ละ Story:**

สำหรับแต่ละ User Story ให้ตรวจ:
```
Story: [US-XXX]
□ Acceptance Criteria ข้อ 1: [ผ่าน/ไม่ผ่าน]
□ Acceptance Criteria ข้อ 2: [ผ่าน/ไม่ผ่าน]
□ UX เป็นที่ยอมรับได้: [ผ่าน/ไม่ผ่าน]
□ Performance ดีพอ: [ผ่าน/ไม่ผ่าน]

ผลสรุป: ✅ Accepted / ❌ Rejected / 🔄 Needs Revision
หมายเหตุ: [feedback]
```

**หลัง Review:**
```
## Sprint [N] Review Summary
วันที่: [วัน]
Velocity: [points ที่ทำเสร็จ] / [points ที่วางแผน]

Stories ที่ Accepted: [รายการ]
Stories ที่ Rejected/Revision: [รายการ + เหตุผล]

Backlog Updates:
- เพิ่ม: [stories ใหม่ที่ค้นพบ]
- ลบ: [stories ที่ไม่จำเป็นแล้ว]
- ปรับ priority: [เหตุผล]

Sprint Goal: ✅ Achieved / ❌ Not Achieved
เหตุผล: [อธิบาย]
```

---

## Sprint Retrospective

ทำหลัง Sprint Review ทันที — ใช้เวลา 30-45 นาที

**Format: Start / Stop / Continue**

```
## Sprint [N] Retrospective
วันที่: [วัน]

🟢 START — สิ่งที่ควรเริ่มทำ:
- [สิ่งที่เรียนรู้และควรเพิ่ม]

🔴 STOP — สิ่งที่ควรหยุดทำ:
- [สิ่งที่ไม่ work]

🔵 CONTINUE — สิ่งที่ดีอยู่แล้ว:
- [สิ่งที่ทำได้ดี]

Action Items สำหรับ Sprint ถัดไป:
- [ ] [action] → Owner: [ใคร]

Velocity Trend:
Sprint [N-1]: [X] points
Sprint [N]: [Y] points
```

---

## Release Planning

ทุก 3-4 Sprints ให้ทำ Release Review:

```
## Release [Version] Plan
Sprints: [N] ถึง [N+3]

Features ที่จะ release:
- [Feature 1]
- [Feature 2]

Release Criteria:
- [ ] Performance targets met
- [ ] Security review done
- [ ] User testing completed
- [ ] Documentation ready

Go-live Plan:
- วันที่ release: [วัน]
- Rollback plan: [วิธี rollback ถ้าปัญหา]
- Communication: [แจ้งลูกค้ายังไง]
```

---

## Metrics Dashboard (ติดตามทุก Sprint)

```
## Product Metrics — Sprint [N]
วันที่: [วัน]

User Metrics:
- Active Users: [X]
- New Signups: [X]
- Churn Rate: [X%]

Product Health:
- Feature Adoption: [X%]
- Bug Count (Open): [X]
- Avg Response Time: [Xms]

Business Metrics:
- MRR: [฿X]
- CAC: [฿X]
- NPS Score: [X]

Trend: ⬆️ / ⬇️ / ➡️ เทียบ Sprint ที่แล้ว
```

---

## Checklist Sprint แต่ละรอบ ✓

**Planning:**
- [ ] Sprint Goal ชัดเจน
- [ ] Stories มี Acceptance Criteria
- [ ] Team acknowledge scope

**During Sprint:**
- [ ] Daily tracking สม่ำเสมอ
- [ ] Blockers ถูก escalate ทันที

**Review:**
- [ ] PO ตรวจทุก story ด้วยตัวเอง
- [ ] Accepted/Rejected ชัดเจน
- [ ] Backlog update แล้ว

**Retrospective:**
- [ ] Action items มีชัดเจน
- [ ] Velocity บันทึกแล้ว

→ วนซ้ำ Sprint ถัดไป จนถึง Release
