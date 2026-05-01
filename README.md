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

## วิธีใช้งาน

หลังติดตั้งแล้ว พิมพ์ใน Claude ได้เลย เช่น:

```
ฉันมีไอเดียอยากสร้าง app สำหรับ freelancer ช่วยวางแผน product ให้หน่อย
```

```
ช่วยทำ Lean Canvas ให้หน่อย ฉันจะสร้าง SaaS สำหรับร้านอาหาร
```

```
อยากเริ่ม sprint แรก ช่วย sprint planning ให้หน่อย
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
