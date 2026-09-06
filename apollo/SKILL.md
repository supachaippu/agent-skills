---
name: apollo
description: Master skill for building new features with top-tier Tremor Blocks UI/UX and rigorous tests. Orchestrates ui-ux-pro-max, tremor-blocks, implement-spec, tdd, web-design-guidelines, and impeccable. Triggers on /apollo, "new feature", "build feature", "ui design", "ทำฟีเจอร์ใหม่", "สร้างหน้าเว็บ", "ทำ ui", "tremor".
---

# Apollo: Feature Creation & Tremor UI/UX Excellence Pipeline

เมื่อผู้ใช้ต้องการสร้างฟีเจอร์ใหม่, พัฒนาหน้าจอผู้ใช้ (UI/UX), หน้า Dashboard, หรือพิมพ์ `/apollo`, "ทำฟีเจอร์ใหม่", "สร้างหน้าเว็บ", "ทำ ui", "tremor":
AI **ต้องแสดงกล่องติดตามสถานะ (Pipeline Tracker) ในคำตอบแรกเสมอ** และปฏิบัติตามลำดับขั้นตอนดังนี้:

---

## 📊 กฎเหล็ก: แสดงกล่อง Pipeline Tracker ทุกครั้ง
ในทุกๆ ข้อความตอบกลับ AI **ต้องพิมพ์กล่องสถานะนี้ไว้บนสุดของคำตอบเสมอ**:

```text
══════════════════════════════════════════════════════
🏛️ [Apollo Feature Creation Pipeline Tracker]
[1/5] Aegis & Design Tokens: [✅ ตรวจสอบความปลอดภัย & โทนสี Zinc/ฟอนต์]
[2/5] Tremor Blocks Plan: [🛑 หยุดเสนอผัง Wireframe เพื่อรอป๋าอนุมัติ]
[3/5] Spec Implementation: [⏸️/✅ สร้างคอมโพเนนต์ตามบล็อกที่ตกลง]
[4/5] TDD & Web Standards: [⏸️/✅ รันเทสต์ & ตรวจสอบ Accessibility]
[5/5] Impeccable Polish: [⏸️/✅ ขัดเกลา Dark/Light & Micro-interactions]
══════════════════════════════════════════════════════
```

---

## ขั้นตอนที่ 1: ตรวจสอบความปลอดภัยและดีไซน์โทเคน (Aegis & Tokens)
- ตรวจสอบขอบเขตโฟลเดอร์โครงการ และยืนยันความปลอดภัย SAP Read-Only 100%
- **ประสานงานสกิล:** `ui-ux-pro-max` กำหนดฟอนต์ (Inter/Prompt + JetBrains Mono) และโทนสี Zinc (`zinc-50` / `zinc-950`)
- อัปเดตข้อ [1/5] เป็น ✅

---

## ขั้นตอนที่ 2: จุดเบรกที่ 1 — นำเสนอผังโครงสร้าง UI และรออนุมัติ (MANDATORY WIREFRAME APPROVAL)
- **มาตรฐานคอมโพเนนต์:** ยึดรูปแบบ **[Tremor Blocks](https://blocks.tremor.so/)** (KPI Cards, Status Banners, Clean Tables, Dark Mode)
- 🛑 **คำสั่งเบรกแตก:**
  1. อัปเดตข้อ [2/5] ใน Tracker เป็น `🛑 หยุดรออนุมัติผัง UI`
  2. **ห้ามกระโดดไปเขียนโค้ด HTML/React เด็ดขาด**
  3. สรุปผังหน้าจอให้ผู้ใช้เห็นภาพ: รายชื่อบล็อก, ตัวเลขที่จะแสดง, และปุ่ม Action
  4. **หยุดรอคำยืนยันอนุมัติจากผู้ใช้ก่อน จึงจะเริ่มขั้นตอนเขียนโค้ด**

---

## ขั้นตอนที่ 3: ลงมือพัฒนาตามบล็อกที่ตกลง (Spec Implementation)
- **ประสานงานสกิล:** `implement-spec`
- เมื่อผู้ใช้อนุมัติ อัปเดตข้อ [2/5] เป็น ✅ และข้อ [3/5] เป็น ⏳
- สร้างคอมโพเนนต์และประกอบหน้าจอตามผัง Tremor Blocks ที่ตกลงกันไว้

---

## ขั้นตอนที่ 4: พัฒนาควบคู่การทดสอบและมาตรฐานเว็บ (TDD & Web Audit)
- **ประสานงานสกิล:** `tdd` และ `web-design-guidelines`
- เขียนและรัน Unit Test / Integration Test ยืนยันว่าโค้ดทำงานถูกต้อง
- ตรวจสอบความถูกต้องด้าน Accessibility (ARIA, Semantic HTML, Keyboard Navigation)
- อัปเดตข้อ [4/5] เป็น ✅

---

## ขั้นตอนที่ 5: ขัดเกลารายละเอียดขั้นสูงสุด (Impeccable Micro-Polish)
- **ประสานงานสกิล:** `impeccable`
- อัปเดตข้อ [5/5] เป็น ✅
- ตรวจสอบ Empty states, Loading states, Error states และความลื่นไหลของการสลับโหมด Dark/Light
