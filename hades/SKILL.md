---
name: hades
description: Master skill for database design, migrations, RLS policies, and safe data operations. Orchestrates supabase-postgres-best-practices, migrate-to-shoehorn, supabase-audit-rls with SAP SQL read-only and Cloud D1 anti-seeding guards. Triggers on /hades, "database", "db migration", "rls", "ฐานข้อมูล", "ย้าย db", "supabase sql".
---

# Hades: Database Architecture, Security & Safe Migration Pipeline

เมื่อต้องทำงานกับฐานข้อมูล, ปรับเปลี่ยนโครงสร้างตาราง (Schema Migration), กำหนดสิทธิ์ RLS, หรือพิมพ์ `/hades`, "ฐานข้อมูล", "migration", "rls", "supabase sql":
ให้ปฏิบัติตามมาตรฐานความปลอดภัยและ **จุดเบรกบังคับหยุด (Hard Blocking Gates)** อย่างเคร่งครัดดังนี้:

---

## กฎเหล็กด้านความปลอดภัยของฐานข้อมูล (Database Guardrails)

### 1. ฐานข้อมูล SAP SQL Server: Read-Only 100%
- **คำสั่งที่อนุญาต:** เฉพาะคำสั่ง `SELECT` หรือการดึงข้อมูลเพื่ออ่านเท่านั้น
- **คำสั่งต้องห้ามเด็ดขาด:** ห้ามรันคำสั่ง `INSERT`, `UPDATE`, `DELETE`, `DROP`, `ALTER`, `CREATE`, `TRUNCATE` บน SAP Server SQL เด็ดขาด (ยกเว้นกรณีพิเศษการอัปเดต EnbApprDI ใน OADM ที่ได้รับคำสั่งตรงจากป๋า)

### 2. ฐานข้อมูล Cloud D1: ห้าม Remote Seeding
- **ห้ามรันสคริปต์ล้าง/เขียนทับฐานข้อมูล:** ห้ามรันคำสั่งประเภท `npx wrangler d1 execute ... --file=seed.sql` บน Cloud D1 เด็ดขาด เพื่อป้องกันความเสี่ยงในการทำ Database Cleansing ที่ทำให้ข้อมูลจริงสูญหาย

### 3. มาตรฐาน n8n PostgreSQL Node
- เมื่อสร้างหรือแก้ไขโหนด PostgreSQL ใน n8n:
  - ต้องใช้ `"operation": "executeQuery"` เสมอ (ห้ามใช้ "executeLikeSource")
  - ต้องใช้ `"query": "<sql query>"` ตัวพิมพ์เล็กเสมอ (ห้ามใช้ "Query" ตัวพิมพ์ใหญ่)

### 4. นโยบายฐานข้อมูลและระบบแคช (Database, Storage & Cached Egress)
- **ยึด Supabase เป็นศูนย์กลางข้อมูลและแคชหลัก:** อะไรที่เกี่ยวข้องกับ Database, Data Storage, หรือการเก็บสถานะของระบบ ให้ใช้ **Supabase (PostgreSQL)** เป็นหลัก
- **การใช้งาน Cached & Storage:** เนื่องจาก Supabase มีระบบ **Cached Egress** และ **Storage** สำหรับการแคชและเสิร์ฟข้อมูลในตัวอยู่แล้วที่มีประสิทธิภาพและตรวจสอบปริมาณการใช้งานได้ชัดเจน ให้ใช้ฟีเจอร์นี้ของ Supabase ในการจัดการแคชข้อมูล
- **หลีกเลี่ยงการพึ่งพา Cloudflare KV:** หลีกเลี่ยงการนำ Cloudflare KV มาใช้เป็น Database หรือที่เก็บแคชหลักของระบบ เนื่องจากขีดจำกัดความจุ โควตาการอ่าน/เขียน และพฤติกรรมการแคชของ Cloudflare KV ยังมีความไม่แน่นอนและตรวจสอบขีดจำกัดได้ยาก การรวมศูนย์ข้อมูลและแคชไว้ที่ Supabase จะทำให้ระบบมีความเสถียร ตรวจสอบง่าย และลดความซับซ้อนของสถาปัตยกรรม

---

## ขั้นตอนที่ 1: วางมาตรฐานโครงสร้างฐานข้อมูล (Postgres Best Practices)
- **ประสานงานสกิล:** `supabase-postgres-best-practices`
- เลือกใช้ Data types ที่เหมาะสม (`timestamptz`, `uuid`, `text` แทน `varchar` ไร้ขนาด)
- กำหนด Primary Keys, Foreign Keys พร้อม Index ป้องกัน Table Scan

---

## ขั้นตอนที่ 2: จุดเบรกที่ 1 — แสดงสคริปต์ SQL Migration และขอคำยืนยัน (MANDATORY SQL REVIEW)
- 🛑 **คำสั่งเบรกแตก (CRITICAL HARD STOP):**
  - **ห้าม AI นำสคริปต์ SQL DDL ไปรันหรือยิงเข้าฐานข้อมูลจริงโดยไม่แสดงให้ผู้ใช้ตรวจเด็ดขาด**
  - AI ต้องแสดงบล็อกคำสั่ง SQL อย่างครบถ้วน:
    ```sql
    -- ตัวอย่างสคริปต์ Migration
    ALTER TABLE ... ADD COLUMN ...;
    CREATE INDEX CONCURRENTLY ...;
    ```
  - อธิบายว่าคำสั่งนี้จะกระทบกับตารางใด และมีผลต่อข้อมูลเดิมอย่างไร
  - **หยุดรอคำยืนยันอนุมัติจากผู้ใช้ก่อน จึงจะเริ่มดำเนินการรันหรือนำไปใส่ใน Migration File ได้**

---

## ขั้นตอนที่ 3: สร้าง Mock และ Type Assertion ที่ปลอดภัย (Type Safety)
- **ประสานงานสกิล:** `migrate-to-shoehorn`
- สำหรับชุดทดสอบที่มีการจำลองข้อมูลฐานข้อมูล ให้ใช้การยืนยัน Type-safe เพื่อป้องกัน Mock แตกเมื่อ Schema เปลี่ยนแปลง

---

## ขั้นตอนที่ 4: จุดเบรกที่ 2 — ตรวจสอบและบังคับใช้นโยบายความปลอดภัย RLS (RLS Policy Audit)
- **ประสานงานสกิล:** `supabase-audit-rls`
- ตรวจสอบให้แน่ใจว่าตารางเปิดใช้งาน `ALTER TABLE ... ENABLE ROW LEVEL SECURITY;`
- แสดงและตรวจสอบนโยบาย (Policies) แยกตาม Action: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
- ป้องกันช่องโหว่บายพาส เช่น `auth.uid() IS NULL` หรือการเข้าถึงข้าม Tenant

---

## ขั้นตอนที่ 5: ตรวจสอบและทดสอบผลลัพธ์ (Verification & Testing)
- รันการทดสอบ Query เพื่อวัดประสิทธิภาพและยืนยันผลลัพธ์
- ทดสอบสิทธิ์การเข้าถึงทั้งในฐานะ Authenticated User และ Anonymous User เพื่อยืนยันว่า RLS ป้องกันข้อมูลได้จริง 100%
