---
name: gaia
description: Master skill for greenfield project setup and initialization. Orchestrates domain-modeling, deep modular architecture, pre-commit hooks, git rules, project paths, and telemetry. Triggers on /gaia, "start project", "setup project", "เริ่มโปรเจกต์", "สร้างโปรเจกต์ใหม่".
---

# Gaia: Greenfield Project Initialization & Architecture Seeding

เมื่อผู้ใช้เริ่มต้นโครงการใหม่ (Greenfield Project) หรือพิมพ์ `/gaia`, "เริ่มโปรเจกต์ใหม่", "setup project":
ให้ปฏิบัติตามขั้นตอนและ **จุดเบรกบังคับหยุด (Hard Blocking Gates)** ดังต่อไปนี้:

---

## ขั้นตอนที่ 1: ตรวจสอบขอบเขตและเปิดเกราะป้องกัน (Aegis Activation)
1. **ล็อกขอบเขตโฟลเดอร์โครงการ:** ตรวจสอบโฟลเดอร์ของโครงการย่อยเป้าหมาย (เช่น `/Users/bart/ไฟล์ดิบ/<subproject>`)
2. **กฎเหล็กโฟลเดอร์ Root:** **ห้ามรันคำสั่ง `git init`, `npm init`, หรือสคริปต์ใดๆ บน Root `/Users/bart/ไฟล์ดิบ` เด็ดขาด** ต้องทำงานอยู่ภายในโฟลเดอร์ของโครงการย่อยนั้นๆ เสมอ
3. **เปิดเกราะความปลอดภัย `aegis`:** บังคับใช้มาตรการ SAP Read-Only และ Directory Containment ทันที

---

## ขั้นตอนที่ 2: จุดเบรกที่ 1 — ซักถามวิสัยทัศน์โครงการและเทคโนโลยี (MANDATORY PROJECT ALIGNMENT)
- 🛑 **คำสั่งเบรกแตก (CRITICAL HARD STOP):**
  - **ห้าม AI คิดชื่อโดเมน หรือสร้างไฟล์โครงสร้างโครงการเองโดยไม่ถามผู้ใช้เด็ดขาด**
  - AI ต้องหยุดเพื่อถามผู้ใช้สั้นๆ 3 ประเด็นสำคัญ:
    1. **เป้าหมายหลักของโปรเจกต์:** ระบบนี้ทำหน้าที่อะไร มีฟังก์ชันหลักอะไรบ้าง?
    2. **เทคโนโลยีและภาษาที่ต้องการ:** (เช่น Python, TypeScript, Node.js, Next.js, Cloudflare Worker ฯลฯ)
    3. **ฐานข้อมูลและระบบจัดเก็บ:** (ยึด Supabase เป็นหลักตามนโยบายระบบ)
  - **หยุดรอคำตอบจากผู้ใช้ก่อน จึงจะเริ่มสร้างไฟล์และวางโครงสร้างระบบ**

---

## ขั้นตอนที่ 3: วางโมเดลโดเมนและบริบทระบบ (Domain Modeling)
- **ประสานงานสกิล:** `domain-modeling`
- สร้างเอกสาร `CONTEXT.md` ภายในโฟลเดอร์โครงการตามข้อมูลที่ได้รับจากผู้ใช้:
  - กำหนดคำศัพท์เฉพาะทาง (Ubiquitous Language)
  - กำหนดขอบเขตระบบ (System Boundaries) และ Entities หลัก

---

## ขั้นตอนที่ 4: ออกแบบสถาปัตยกรรมโมดูลเชิงลึก (Deep Modular Architecture)
- **ประสานงานสกิล:** `setup-ts-deep-modules` (หรือเทียบเท่าสำหรับภาษาอื่น)
- จัดวางโครงสร้างแบบ Deep Modules:
  - อินเทอร์เฟซภายนอกเรียบง่าย (Narrow Interface)
  - ซ่อนความซับซ้อนไว้ภายในโมดูล (Deep Implementation)

---

## ขั้นตอนที่ 5: วางระบบตรวจสอบคุณภาพอัตโนมัติ (Pre-Commit & Quality Hooks)
- **ประสานงานสกิล:** `setup-pre-commit`
- ติดตั้ง Husky, lint-staged, Linter, และ Type-checking เพื่อป้องกันข้อผิดพลาดตั้งแต่ก่อน Commit

---

## ขั้นตอนที่ 6: ติดตั้ง Git และระบบ Dual-Push คู่ขนาน (Git Rules & Dual Remote)
- **ประสานงานสกิล:** `git-rules`
- รัน `git init` เฉพาะในโฟลเดอร์โครงการย่อยนั้น
- สร้าง `.gitignore` ครอบคลุม `.env`, `node_modules`, `.DS_Store`
- ตั้งค่า Git Dual-Push ไปยังทั้ง 2 บัญชี (`supachaippu` + `ocrsparepart`)
- แสดงรายการไฟล์และขอคำยืนยันก่อนทำ Initial Commit & Push เสมอ

---

## ขั้นตอนที่ 7: กำหนดโครงสร้างพาธผลลัพธ์และระบบติดตาม (Paths & Beacon)
- **ประสานงานสกิล:** `project-paths` และ `project-beacon`
- วางมาตรฐานโฟลเดอร์ผลลัพธ์ตามชื่อไฟล์อินพุตภายในโฟลเดอร์รันเนอร์
- บันทึก telemetry event ลงทะเบียนโปรเจกต์เข้าสู่ระบบกลาง
