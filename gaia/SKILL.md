---
name: gaia
description: Master skill for greenfield project setup and initialization. Orchestrates domain-modeling, deep modular architecture, pre-commit hooks, git rules, project paths, and telemetry. Triggers on /gaia, "start project", "setup project", "เริ่มโปรเจกต์", "สร้างโปรเจกต์ใหม่".
---

# Gaia: Greenfield Project Initialization & Architecture Seeding

เมื่อผู้ใช้เริ่มต้นโครงการใหม่ (Greenfield Project) หรือพิมพ์ `/gaia`, "เริ่มโปรเจกต์ใหม่", "setup project":
AI **ต้องแสดงกล่องติดตามสถานะ (Pipeline Tracker) ในคำตอบแรกเสมอ** และปฏิบัติตามลำดับขั้นตอนดังนี้:

---

## 📊 กฎเหล็ก: แสดงกล่อง Pipeline Tracker ทุกครั้ง
ในทุกๆ ข้อความตอบกลับ AI **ต้องพิมพ์กล่องสถานะนี้ไว้บนสุดของคำตอบเสมอ**:

```text
══════════════════════════════════════════════════════
🏛️ [Gaia Project Initialization Pipeline Tracker]
[1/5] Aegis Guard & Scope: [✅ ล็อกขอบเขตโฟลเดอร์ & SAP Read-Only]
[2/5] Project Alignment: [🛑 หยุดถามเป้าหมายระบบและ Tech Stack จากป๋า]
[3/5] Domain Modeling: [⏸️/✅ สร้าง CONTEXT.md กำหนดคำศัพท์เฉพาะ]
[4/5] Architecture & Hooks: [⏸️/✅ วาง Deep Modules + Git Pre-commit Hooks]
[5/5] Git Dual-Push & Beacon: [⏸️/✅ ตั้งค่า Remote คู่ขนาน 2 บัญชี & Telemetry]
══════════════════════════════════════════════════════
```

---

## ขั้นตอนที่ 1: ตรวจสอบขอบเขตและเปิดเกราะป้องกัน (Aegis Activation)
1. **ล็อกขอบเขตโฟลเดอร์โครงการ:** ตรวจสอบโฟลเดอร์ย่อยเป้าหมาย
2. **กฎเหล็กโฟลเดอร์ Root:** **ห้ามรันคำสั่ง `git init`, `npm init` บน Root `/Users/bart/ไฟล์ดิบ` เด็ดขาด**
3. อัปเดตข้อ [1/5] เป็น ✅

---

## ขั้นตอนที่ 2: จุดเบรกที่ 1 — ซักถามวิสัยทัศน์โครงการและเทคโนโลยี (MANDATORY ALIGNMENT)
- 🛑 **คำสั่งเบรกแตก:**
  1. อัปเดตข้อ [2/5] ใน Tracker เป็น `🛑 หยุดถามเป้าหมายและ Stack จากผู้ใช้`
  2. **ห้าม AI คิดชื่อโดเมน หรือสร้างไฟล์โครงการเองโดยไม่ถามผู้ใช้เด็ดขาด**
  3. ถามผู้ใช้ 3 ประเด็นสำคัญ:
     - เป้าหมายหลักของระบบ
     - ภาษาและ Tech Stack ที่ต้องการ
     - ฐานข้อมูล (ยึด Supabase เป็นหลัก)
  4. **หยุดรอคำตอบจากผู้ใช้ก่อน จึงจะเริ่มสร้างไฟล์จริงได้**

---

## ขั้นตอนที่ 3: วางโมเดลโดเมนและบริบทระบบ (Domain Modeling)
- **ประสานงานสกิล:** `domain-modeling`
- เมื่อได้รับคำตอบ อัปเดตข้อ [2/5] เป็น ✅ และข้อ [3/5] เป็น ⏳
- สร้างเอกสาร `CONTEXT.md` ภายในโฟลเดอร์โครงการ (Ubiquitous Language, Boundaries, Entities)
- อัปเดตข้อ [3/5] เป็น ✅

---

## ขั้นตอนที่ 4: ออกแบบสถาปัตยกรรมโมดูลเชิงลึกและ Git Hooks (Deep Modules & Hooks)
- **ประสานงานสกิล:** `setup-ts-deep-modules` และ `setup-pre-commit`
- จัดวางโครงสร้างแบบ Deep Modules (Minimal Public API)
- ติดตั้ง Pre-commit hooks (Husky, lint-staged, Linter, Type-checking)
- อัปเดตข้อ [4/5] เป็น ✅

---

## ขั้นตอนที่ 5: ติดตั้ง Git Dual-Push และระบบติดตาม (Git Dual-Push & Beacon)
- **ประสานงานสกิล:** `git-rules`, `project-paths`, และ `project-beacon`
- รัน `git init` ในโฟลเดอร์ย่อย, สร้าง `.gitignore`
- ตั้งค่า Git Dual-Push ไปยังทั้ง 2 บัญชี (`supachaippu` + `ocrsparepart`)
- แสดงรายการไฟล์และขอคำยืนยันก่อนทำ Initial Push เสมอ
- อัปเดตข้อ [5/5] เป็น ✅
