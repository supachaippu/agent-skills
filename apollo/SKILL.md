---
name: apollo
description: Master skill for building new features with top-tier Tremor Blocks UI/UX and rigorous tests. Orchestrates ui-ux-pro-max, tremor-blocks, implement-spec, tdd, web-design-guidelines, and impeccable. Triggers on /apollo, "new feature", "build feature", "ui design", "ทำฟีเจอร์ใหม่", "สร้างหน้าเว็บ", "ทำ ui", "tremor".
---

# Apollo: Feature Creation & Tremor UI/UX Excellence Pipeline

เมื่อผู้ใช้ต้องการสร้างฟีเจอร์ใหม่, พัฒนาหน้าจอผู้ใช้ (UI/UX), หน้า Dashboard, หรือพิมพ์ `/apollo`, "ทำฟีเจอร์ใหม่", "สร้างหน้าเว็บ", "ทำ ui", "tremor":
ให้ปฏิบัติตามขั้นตอนและ **จุดเบรกบังคับหยุด (Hard Blocking Gates)** ดังต่อไปนี้:

---

## ขั้นตอนที่ 1: ตรวจสอบเกราะความปลอดภัย (Aegis Verification)
- ยืนยันว่างานทั้งหมดทำอยู่ภายในโฟลเดอร์ของโปรเจกต์ย่อยนั้นๆ
- ยืนยันว่าไม่มีการแตะต้องฐานข้อมูล SAP ในเชิงแก้ไข (ยึดหลัก Read-Only 100%)

---

## ขั้นตอนที่ 2: วางแนวทางการออกแบบอัจฉริยะ (Design Intelligence)
- **ประสานงานสกิล:** `ui-ux-pro-max`
- เลือกคู่ฟอนต์: Inter + Prompt + JetBrains Mono (สำหรับตัวเลขและโค้ด)
- กำหนดโทนสีเน้นความสะอาด คมชัดระดับโปรดักชัน (Zinc Palette: `zinc-50` / `zinc-950`)
- วางระบบ Spacing และ Layout Grid ที่มี Contrast Ratio ได้มาตรฐานการเข้าถึง (Accessibility)

---

## ขั้นตอนที่ 3: สถาปัตยกรรม UI สไตล์ Tremor Blocks (Tremor Dashboard Standard)
- **มาตรฐานคอมโพเนนต์:** ยึดรูปแบบ **[Tremor Blocks](https://blocks.tremor.so/)** เป็นหลัก:
  - **KPI & Metric Cards:** แสดง Category, ค่าตัวเลขเด่นชัด (`tabular-nums`), Subtitle, Progress Bar, Delta Badge พร้อม Micro-chart
  - **Status Banners & Callouts:** แถบสถานะระบบพร้อมไอคอน Shield/Check, Badge สีสุขภาพระบบ (Emerald/Amber/Rose) และข้อความสรุปกระชับ
  - **Navigation & Controls:** แถบ Header คมชัด, Dark/Light Mode สลับนุ่มนวล, และปุ่ม Action สไตล์มินิมอล
  - **Data Density & Tone:** โทน Zinc เรียบหรู ขอบบางเบา (`ring-1 ring-zinc-950/5 dark:ring-white/10`), ไร้กราเดียนต์สีม่วงฟุ้งโหลแบบ AI

---

## ขั้นตอนที่ 4: จุดเบรกที่ 1 — นำเสนอโครงสร้าง UI และรอรับอนุมัติ (MANDATORY UI PLAN APPROVAL)
- 🛑 **คำสั่งเบรกแตก (CRITICAL HARD STOP):**
  - **ห้ามกระโดดไปเขียนโค้ด HTML/React ทันทีเด็ดขาด**
  - AI ต้องสรุป **ผังโครงสร้างหน้าจอ (Tremor Blocks Wireframe)** ให้ผู้ใช้เห็นภาพก่อน:
    1. รายการบล็อกที่จะมีในหน้าเว็บ (Header ➡️ Banners ➡️ Metric Cards ➡️ Charts/Tables)
    2. รายการข้อมูลหรือตัวเลขที่จะแสดงในแต่ละการ์ด
    3. ปุ่มหรือ Action ที่ผู้ใช้สามารถกดได้
  - **หยุดรอคำยืนยันอนุมัติจากผู้ใช้ก่อน จึงจะเริ่มขั้นตอนการเขียนโค้ดได้**

---

## ขั้นตอนที่ 5: พัฒนาตามสเปกและทดสอบเข้มงวด (Spec Implementation & TDD)
- **ประสานงานสกิล:** `implement-spec` และ `tdd`
- ลงมือสร้างคอมโพเนนต์และฟังก์ชันตามบล็อกที่ตกลงกันไว้
- เขียน Unit Test / Integration Test ประกบฟังก์ชันสำคัญตามวงจร Red-Green-Refactor

---

## ขั้นตอนที่ 6: ตรวจสอบมาตรฐานเว็บสากล (Web Interface Audit)
- **ประสานงานสกิล:** `web-design-guidelines`
- ตรวจสอบความถูกต้องด้าน Accessibility (ARIA, Semantic HTML, Keyboard Navigation)
- ตรวจสอบการแสดงผลแบบ Responsive บนหน้าจอขนาดต่างๆ

---

## ขั้นตอนที่ 7: ขัดเกลารายละเอียดขั้นสูงสุด (Impeccable Micro-Polish)
- **ประสานงานสกิล:** `impeccable`
- ตรวจสอบสถานะขอบเขต: Loading states, Empty states, Error states, และ Hover states
- ปรับแต่ง Transition การสลับโหมด Dark/Light ให้ออกมาเนียนตาไร้รอยต่อ
