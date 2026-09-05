---
name: hermes
description: Master skill for safe end-of-session shipping, handoff documentation, secret leak scanning, dual-push to GitHub, and executive reporting. Orchestrates handoff, git-rules, auto-ship, and management-talk. Triggers on /hermes, /ship, "handoff+commit+push", "ส่งงาน", "จบงาน", "ship".
---

# Hermes: Safe End-of-Session Shipping & Dual-Push Pipeline

เมื่อผู้ใช้สั่งจบงาน, ส่งงาน, หรือพิมพ์ `/hermes`, `/ship`, `handoff+commit+push`, "จบงาน", "ส่งงานขึ้น git":
ให้ปฏิบัติตามลำดับขั้นตอนอัตโนมัตินี้แบบต่อเนื่อง (Closed-Loop) ทันที:

---

## ขั้นตอนที่ 1: ตรวจสอบขอบเขตโฟลเดอร์ (Subproject Identification)
1. ระบุโฟลเดอร์ของโครงการย่อยปัจจุบันที่กำลังทำงานอยู่ (เช่น `/Users/bart/ไฟล์ดิบ/<subproject>`)
2. **กฎเหล็กสูงสุด:** **ห้ามรันคำสั่ง Git ในโฟลเดอร์ Root (`/Users/bart/ไฟล์ดิบ`) เด็ดขาด** ต้องทำงานอยู่ภายในโฟลเดอร์ของโปรเจกต์ย่อยนั้นๆ เสมอ

---

## ขั้นตอนที่ 2: เขียนและอัปเดตเอกสารส่งต่องาน (Handoff Generation)
- **ประสานงานสกิล:** `handoff`
- สร้างหรืออัปเดตไฟล์ `handoff.md` ภายในโฟลเดอร์โครงการย่อย โดยมีหัวข้อครบถ้วน:
  - **ภาพรวมงาน (Task Overview):** วัตถุประสงค์และสรุปสิ่งสำคัญในรอบนี้
  - **ไฟล์ที่มีการเปลี่ยนแปลง (Modified Files):** รายชื่อไฟล์ที่สร้างใหม่หรือแก้ไข
  - **สถานะปัจจุบัน (Current Status):** สิ่งที่เสร็จสมบูรณ์ และผลการทดสอบ
  - **สิ่งที่ต้องทำต่อในรอบหน้า (Next Steps):** รายการงานถัดไปแบบชัดเจน เพื่อให้ `atlas` มาอ่านต่อแล้วทำงานได้ทันที

---

## ขั้นตอนที่ 3: สแกนความปลอดภัยป้องกันข้อมูลลับรั่วไหล (Strict Leak Prevention)
ก่อนทำ Git commit ต้องสแกนไฟล์ที่ถูกแก้ไขและ `handoff.md` ทันที:
1. ตรวจสอบว่าไม่มี Passwords, API Keys, Tokens (เช่น GitHub Token, Cloudflare Token) แบบ Plaintext อยู่ในไฟล์ใดๆ
2. ตรวจสอบว่ามีไฟล์ `.gitignore` และมีการละเว้นไฟล์ `.env`, `node_modules`, `.DS_Store`, และ build cache แล้ว
3. **หากพบความเสี่ยง ให้หยุดและแจ้งเตือนผู้ใช้ทันที ห้าม Push ขึ้น GitHub เด็ดขาด**

---

## ขั้นตอนที่ 4: ตั้งค่า Git Dual-Push & เตรียม Commit (Git Setup)
- **ประสานงานสกิล:** `git-rules`
1. ตรวจสอบว่าโฟลเดอร์ย่อยมี `.git` หรือยัง หากยังไม่มีให้รัน `git init` ในโฟลเดอร์นั้น
2. ตั้งชื่อ Repository เป็นภาษาอังกฤษตัวพิมพ์เล็ก สะอาดตา (Clean repo name)
3. ตรวจสอบและตั้งค่า Remote `origin` ให้ Push ไปยัง 2 บัญชีคู่ขนาน:
   - Primary: `https://<GITHUB_TOKEN>@github.com/supachaippu/<repo_name>.git`
   - Secondary: `https://<SECONDARY_GITHUB_TOKEN>@github.com/ocrsparepart/<repo_name>.git`
4. รัน `git add .` และ `git status` เพื่อเตรียมรายการไฟล์

---

## ขั้นตอนที่ 5: ขอยืนยันและทำการ Commit & Push (Commit & Dual-Push)
1. แสดงสรุปรายชื่อไฟล์ให้ผู้ใช้ทราบในแชท และขอคำยืนยันสั้นๆ (หากผู้ใช้สั่ง "ทำเลย", "ลุยเลย", "yes" หรือยืนยันแล้ว ให้ดำเนินการทันที)
2. ทำการ Commit ด้วย Semantic Commit Message ที่ชัดเจน (เช่น `feat: ...`, `fix: ...`)
3. ทำการ Push ขึ้นทั้ง 2 บัญชีคู่ขนาน:
   ```bash
   git push -u origin main || git push -u origin master
   ```

---

## ขั้นตอนที่ 6: สรุปรายงานสำหรับผู้บริหาร (Executive Summary)
- **ประสานงานสกิล:** `management-talk`
- เขียนข้อความสรุปผลงานสั้นๆ 3-4 บรรทัดในภาษาที่กระชับ ชัดเจน พร้อมให้นำไปคัดลอกส่งใน Line หรือรายงานต่อผู้บริหารได้ทันที
