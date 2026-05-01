# Solopreneur Skill

Claude skill สำหรับ Solo Entrepreneur ที่ต้องการพัฒนา Digital Product อย่างเป็นระบบ ตั้งแต่ไอเดียจนถึง launch

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

---

## วิธีติดตั้ง

### วิธีที่ 1 — ติดตั้งจาก .skill file (แนะนำ)

1. ดาวน์โหลดไฟล์ [solopreneur-skill.skill](https://github.com/nattaponra/solopreneur-skill/releases/latest)
2. เปิด **Claude Desktop**
3. ไปที่ **Settings → Skills**
4. คลิก **Install from file** แล้วเลือกไฟล์ `.skill` ที่ดาวน์โหลดมา
5. ติดตั้งเสร็จ — พร้อมใช้งานทันที

### วิธีที่ 2 — ติดตั้งจาก Source

```bash
# Clone repository
git clone https://github.com/nattaponra/solopreneur-skill.git

# เปิด Claude Desktop → Settings → Skills → Install from folder
# เลือก folder: solopreneur-skill/solopreneur-skill
```

---

## ตัวอย่างการใช้งาน

### 🌱 เริ่มจากศูนย์ — มีแค่ไอเดีย

**คุณพิมพ์:**
```
ฉันมีไอเดียอยากสร้าง app ช่วยให้ freelancer ออก invoice ได้เร็วขึ้น
```

**Skill จะ:**
1. ถามคำถามเพื่อ define problem statement ให้ชัด
2. ช่วยระบุ customer segment และ value proposition
3. บันทึก `01-problem-solution.md` ให้อัตโนมัติ
4. พาไปต่อที่ Lean Canvas ใน Phase 2

---

### 📊 Phase 2 — ทำ Business Model

**คุณพิมพ์:**
```
ช่วยทำ Lean Canvas ให้หน่อย product ของฉันคือ SaaS สำหรับ freelancer
```

**Skill จะ:**
1. กรอก Lean Canvas ทีละ block พร้อมถามข้อมูลที่ขาด
2. แนะนำ revenue model ที่เหมาะสม (subscription, freemium ฯลฯ)
3. ประมาณ unit economics เบื้องต้น (CAC, LTV)
4. บันทึก `02-lean-canvas.md` และ `02-business-model.md`

---

### 🧪 Phase 3 — Validate ก่อนสร้าง

**คุณพิมพ์:**
```
อยากทดสอบว่ามีคนต้องการ product นี้จริงไหม ก่อนจะเริ่มสร้าง
```

**Skill จะ:**
1. ช่วยกำหนด hypothesis ที่ต้อง validate
2. สร้าง user interview guide พร้อมคำถาม Mom Test
3. แนะนำ MVP type ที่เร็วที่สุด (landing page, concierge ฯลฯ)
4. บันทึก `03-validation-plan.md` และ `03-interview-guide.md`
5. หลัง validate เสร็จ สรุปผลใน `03-validation-results.md`

---

### 🚀 Phase 4 — เริ่มพัฒนาด้วย Scrum

**คุณพิมพ์:**
```
validate แล้ว พร้อมสร้างแล้ว อยากเริ่ม sprint แรก
```

**Skill จะ:**
1. ช่วยเขียน PRD และ System Architecture
2. สร้าง Product Backlog พร้อม user stories และ acceptance criteria
3. วาง Sprint 1 Plan พร้อม story points
4. บันทึก `04-prd.md`, `04-architecture.md`, `04-backlog.md`, `04-sprint-1-plan.md`

---

### ✅ Sprint Review — คุณตรวจงานในฐานะ PO

**คุณพิมพ์:**
```
Sprint 1 เสร็จแล้ว ช่วยเตรียม checklist สำหรับ review หน่อย
```

**Skill จะ:**
1. สร้าง Sprint Review checklist ตาม acceptance criteria ที่กำหนดไว้
2. บันทึกผลการ review ว่า story ไหน Accepted / Rejected
3. อัปเดต backlog ตามผล review
4. บันทึก `04-sprint-1-review.md` และ `04-sprint-1-retro.md`
5. เริ่ม Sprint 2 Planning ทันที

---

### 📄 เอกสารที่ได้รับตลอด Journey

```
my-product/
├── 01-problem-solution.md      ← Phase 1
├── 02-lean-canvas.md           ← Phase 2
├── 02-business-model.md        ← Phase 2
├── 03-validation-plan.md       ← Phase 3
├── 03-interview-guide.md       ← Phase 3
├── 03-validation-results.md    ← Phase 3
├── 04-prd.md                   ← Phase 4
├── 04-architecture.md          ← Phase 4
├── 04-tech-stack.md            ← Phase 4
├── 04-definition-of-done.md    ← Phase 4
├── 04-backlog.md               ← Phase 4 (อัปเดตทุก sprint)
├── 04-test-plan.md             ← Phase 4
├── 04-bug-log.md               ← Phase 4 (อัปเดตต่อเนื่อง)
├── 04-sprint-1-plan.md         ← Sprint 1
├── 04-sprint-1-review.md       ← Sprint 1
├── 04-sprint-1-retro.md        ← Sprint 1
└── 04-release-v1.0.md          ← เมื่อ launch
```

Skill จะทำงานอัตโนมัติเมื่อ Claude ตรวจพบว่าคุณกำลังพัฒนา product

---

## โครงสร้างไฟล์

```
solopreneur-skill/
├── SKILL.md                        # ไฟล์หลักของ skill
└── references/
    ├── problem-solution.md         # รายละเอียด Phase 1
    ├── business-model.md           # รายละเอียด Phase 2
    ├── research-validation.md      # รายละเอียด Phase 3
    └── sdlc-scrum.md               # รายละเอียด Phase 4
```

---

## License

MIT
