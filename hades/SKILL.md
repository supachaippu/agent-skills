---
name: hades
description: Master skill for database design, migrations, RLS policies, and safe data operations. Orchestrates supabase-postgres-best-practices, migrate-to-shoehorn, supabase-audit-rls with SAP SQL read-only and Cloud D1 anti-seeding guards. Triggers on /hades, "database", "db migration", "rls", "ฐานข้อมูล", "ย้าย db", "supabase sql".
---

# Hades: Database Architecture, Security & Safe Migration Pipeline

เมื่อต้องทำงานกับฐานข้อมูล, ปรับเปลี่ยนโครงสร้างตาราง (Schema Migration), กำหนดสิทธิ์ RLS, หรือพิมพ์ `/hades`, "ฐานข้อมูล", "migration", "rls", "supabase sql":
AI **ต้องแสดงกล่องติดตามสถานะ (Pipeline Tracker) ในคำตอบแรกเสมอ** และปฏิบัติตามลำดับขั้นตอนดังนี้:

---

## 📊 กฎเหล็ก: แสดงกล่อง Pipeline Tracker ทุกครั้ง
ในทุกๆ ข้อความตอบกลับ AI **ต้องพิมพ์กล่องสถานะนี้ไว้บนสุดของคำตอบเสมอ**:

```text
══════════════════════════════════════════════════════
🏛️ [Hades Database Architecture Pipeline Tracker]
[1/5] Database Guardrails: [✅ SAP Read-Only 100% + Supabase First Policy]
[2/5] Schema & DDL Review: [🛑 หยุดแสดงโค้ด SQL Migration เพื่อรอป๋าตรวจ]
[3/5] Type Safety & Mocks: [⏸️/✅ ทำ Mocks Type-safe ด้วย Shoehorn]
[4/5] RLS Security Audit: [⏸️/✅ ตรวจสอบนโยบายความปลอดภัยแยก Action]
[5/5] Query Verification: [⏸️/✅ ทดสอบประสิทธิภาพ Query จริง]
══════════════════════════════════════════════════════
```

---

## กฎเหล็กด้านความปลอดภัยของฐานข้อมูล (Database Guardrails)
1. **SAP SQL Server: Read-Only 100%:** อนุญาตเฉพาะ `SELECT` ห้ามรันคำสั่งแก้ไขหรือทำลายข้อมูลเด็ดขาด
2. **Cloud D1: ห้าม Remote Seeding:** ห้ามรัน `npx wrangler d1 execute ... --file=seed.sql` ป้องกันล้างข้อมูลทิ้ง
3. **n8n PostgreSQL Node:** บังคับใช้ `"operation": "executeQuery"` และ `"query"` ตัวพิมพ์เล็กเสมอ
4. **นโยบาย Supabase First & Cached Egress:** รวมศูนย์ DB และ Cache ไว้ที่ Supabase (ใช้ประโยชน์จาก Cached Egress และ Storage ในตัว) หลีกเลี่ยง Cloudflare KV
- อัปเดตข้อ [1/5] เป็น ✅

---

## ขั้นตอนที่ 1: วางมาตรฐานโครงสร้างฐานข้อมูล (Postgres Best Practices)
- **ประสานงานสกิล:** `supabase-postgres-best-practices`
- เลือกใช้ Data types ที่เหมาะสม (`timestamptz`, `uuid`) และกำหนด Index บน Foreign Key

---

## ขั้นตอนที่ 2: จุดเบรกที่ 1 — แสดงสคริปต์ SQL Migration และขอคำยืนยัน (MANDATORY SQL REVIEW)
- 🛑 **คำสั่งเบรกแตก:**
  1. อัปเดตข้อ [2/5] ใน Tracker เป็น `🛑 หยุดรอตรวจสอบโค้ด SQL Migration`
  2. **ห้ามนำคำสั่ง SQL ไปรันในฐานข้อมูลจริงโดยไม่แสดงให้ผู้ใช้ตรวจเด็ดขาด**
  3. แสดงบล็อกโค้ด SQL DDL เต็มรูปแบบ และอธิบายผลกระทบต่อตารางเดิม
  4. **หยุดรอคำยืนยันอนุมัติจากผู้ใช้ก่อน จึงจะเริ่มดำเนินการรันจริงได้**

---

## ขั้นตอนที่ 3: สร้าง Mock และ Type Assertion ที่ปลอดภัย (Type Safety)
- **ประสานงานสกิล:** `migrate-to-shoehorn`
- เมื่อได้รับอนุมัติ อัปเดตข้อ [2/5] เป็น ✅ และข้อ [3/5] เป็น ⏳
- ทำ Type-safe fixtures สำหรับชุดทดสอบเพื่อป้องกัน Mock แตกเมื่อ Schema เปลี่ยนแปลง
- อัปเดตข้อ [3/5] เป็น ✅

---

## ขั้นตอนที่ 4: จุดเบรกที่ 2 — ตรวจสอบและบังคับใช้นโยบายความปลอดภัย RLS (RLS Policy Audit)
- **ประสานงานสกิล:** `supabase-audit-rls`
- ยืนยันว่าตารางเปิดใช้งาน `ENABLE ROW LEVEL SECURITY`
- ตรวจสอบนโยบายแยก Action (`SELECT`, `INSERT`, `UPDATE`, `DELETE`) ป้องกันช่องโหว่บายพาส
- อัปเดตข้อ [4/5] เป็น ✅

---

## ขั้นตอนที่ 5: ตรวจสอบและทดสอบผลลัพธ์ (Verification & Testing)
- ทดสอบสิทธิ์การเข้าถึงทั้งแบบ Authenticated และ Anonymous เพื่อยืนยันว่า RLS ป้องกันข้อมูลได้จริง 100%
- อัปเดตข้อ [5/5] เป็น ✅
