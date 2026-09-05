---
name: gaia
description: Master skill for greenfield project setup and initialization. Orchestrates domain-modeling, deep modular architecture, pre-commit hooks, git rules, project paths, and telemetry. Triggers on /gaia, "start project", "setup project", "เริ่มโปรเจกต์", "สร้างโปรเจกต์ใหม่".
---

# Gaia: Greenfield Project Initialization & Architecture Seeding

เมื่อผู้ใช้เริ่มต้นโครงการใหม่ (Greenfield Project) หรือพิมพ์ `/gaia`, "เริ่มโปรเจกต์ใหม่", "setup project":
ให้เรียกใช้และประสานงานชุดสกิลสถาปัตยกรรมรากฐานตามลำดับขั้นตอนดังนี้:

---

## ขั้นตอนที่ 1: ตรวจสอบขอบเขตและเปิดเกราะป้องกัน (Aegis Activation)
1. **ล็อกขอบเขตโฟลเดอร์โครงการ:** ตรวจสอบโฟลเดอร์ของโครงการย่อยเป้าหมาย (เช่น `/Users/bart/ไฟล์ดิบ/<subproject>`)
2. **กฎเหล็กโฟลเดอร์ Root:** ห้ามรันคำสั่ง `git init`, `npm init`, หรือสคริปต์ใดๆ บนไดเรกทอรี Root `/Users/bart/ไฟล์ดิบ` เป็นอันขาด ต้องทำงานอยู่ภายในโฟลเดอร์ของโครงการย่อยนั้นๆ เสมอ
3. **เปิดเกราะความปลอดภัย `aegis`:** บังคับใช้มาตรการ SAP Read-Only และ Directory Containment ตั้งแต่วินาทีแรก

---

## ขั้นตอนที่ 2: วางโมเดลโดเมนและบริบทระบบ (Domain Modeling)
- **ประสานงานสกิล:** `domain-modeling`
- ร่วมกับผู้ใช้กำหนดคำศัพท์เฉพาะ (Ubiquitous Language), ขอบเขตระบบ (System Boundaries), และ Entities หลัก
- สร้างเอกสาร `CONTEXT.md` ภายในโฟลเดอร์โครงการเพื่อบันทึก Architecture Decision Records (ADR) และศัพท์เทคนิคของโดเมน

---

## ขั้นตอนที่ 3: ออกแบบสถาปัตยกรรมโมดูลเชิงลึก (Deep Modular Architecture)
- **ประสานงานสกิล:** `setup-ts-deep-modules` (หรือเทียบเท่าสำหรับภาษาอื่น)
- จัดวางโครงสร้างแบบ Deep Modules:
  - อินเทอร์เฟซภายนอกเรียบง่าย ชัดเจน (Narrow Interface)
  - ซ่อนความซับซ้อนและการทำงานจริงไว้ภายในโมดูล (Deep Implementation)
  - ลดการ Coupling ระหว่างโมดูลให้น้อยที่สุด

---

## ขั้นตอนที่ 4: วางระบบตรวจสอบคุณภาพอัตโนมัติ (Pre-Commit & Quality Hooks)
- **ประสานงานสกิล:** `setup-pre-commit`
- ติดตั้งและตั้งค่า Husky, lint-staged, Prettier/Linter, และ Type-checking
- กำหนดให้ตรวจสอบอัตโนมัติทุกครั้งที่มีการ commit เพื่อป้องกันโค้ดที่มีข้อผิดพลาดหลุดขึ้นระบบ

---

## ขั้นตอนที่ 5: ติดตั้ง Git และระบบ Dual-Push คู่ขนาน (Git Rules & Dual Remote)
- **ประสานงานสกิล:** `git-rules`
- ตรวจสอบและรัน `git init` เฉพาะในโฟลเดอร์โครงการย่อยนั้น
- สร้าง `.gitignore` ที่ครอบคลุมไฟล์ `.env`, `node_modules`, `.DS_Store`, และ build artifacts
- ตั้งค่า Git Dual-Push ไปยังสองบัญชีคู่ขนาน:
  - Primary: `https://<GITHUB_TOKEN>@github.com/supachaippu/<repo_name>.git`
  - Secondary: `https://<SECONDARY_GITHUB_TOKEN>@github.com/ocrsparepart/<repo_name>.git`
- ใช้ชื่อ repository เป็นภาษาอังกฤษตัวพิมพ์เล็ก กระชับ และไม่มีช่องว่าง

---

## ขั้นตอนที่ 6: กำหนดโครงสร้างพาธผลลัพธ์ (Project Paths)
- **ประสานงานสกิล:** `project-paths`
- วางมาตรฐานโฟลเดอร์สำหรับผลลัพธ์ (Output files) โดยให้สร้างโฟลเดอร์ผลลัพธ์ตามชื่อไฟล์อินพุตภายในโฟลเดอร์ของสคริปต์รันเนอร์ (`.bat` / `.command`)

---

## ขั้นตอนที่ 7: ลงทะเบียนระบบติดตามสถานะโครงการ (Project Beacon)
- **ประสานงานสกิล:** `project-beacon`
- ทำการบันทึก telemetry event และลงทะเบียนโปรเจกต์เข้าสู่ระบบ Project Status Tracking กลาง

---

## สรุปผลการเริ่มต้นโครงการ
เมื่อดำเนินการครบทุกขั้นตอน ให้สรุปสถานะสั้นกระชับ:
- โครงสร้างโฟลเดอร์และสถาปัตยกรรมที่จัดเตรียมไว้
- สถานะ Git Dual-Push
- คำแนะนำขั้นตอนถัดไป (เช่น เรียกใช้ `/athena` เพื่อวางแผนและทำ Spec ฟีเจอร์)
