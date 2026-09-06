---
name: hermes
description: Master skill for safe end-of-session shipping, handoff documentation, secret leak scanning, dual-push to GitHub, and executive reporting. Orchestrates handoff, git-rules, auto-ship, and management-talk. Triggers on /hermes, /ship, "handoff+commit+push", "ส่งงาน", "จบงาน", "ship".
---

# Hermes: Safe End-of-Session Shipping & Dual-Push Pipeline

เมื่อผู้ใช้สั่งจบงาน, ส่งงาน, หรือพิมพ์ `/hermes`, `/ship`, `handoff+commit+push`, "จบงาน", "ส่งงานขึ้น git":
AI **ต้องแสดงกล่องติดตามสถานะ (Pipeline Tracker) ในคำตอบแรกเสมอ** และปฏิบัติตามลำดับขั้นตอนดังนี้:

---

## 📊 กฎเหล็ก: แสดงกล่อง Pipeline Tracker ทุกครั้ง
ในทุกๆ ข้อความตอบกลับ AI **ต้องพิมพ์กล่องสถานะนี้ไว้บนสุดของคำตอบเสมอ**:

```text
══════════════════════════════════════════════════════
🏛️ [Hermes Shipping & Dual-Push Pipeline Tracker]
[1/4] Subproject Identification: [✅ ล็อกขอบเขตโฟลเดอร์ & ป้องกัน Root Workspace]
[2/4] Handoff Generation: [✅ เขียน/อัปเดต handoff.md เรียบร้อย]
[3/4] Secret Leak Scan: [✅ สแกนรหัสผ่านและ Token รั่วไหล 100%]
[4/4] Commit & Dual-Push: [🛑 แสดงรายการไฟล์ รอคำยืนยันก่อน Push]
══════════════════════════════════════════════════════
```

---

## ขั้นตอนที่ 1: ตรวจสอบขอบเขตโฟลเดอร์ (Subproject Identification)
1. ระบุโฟลเดอร์ของโครงการย่อยปัจจุบันที่กำลังทำงานอยู่
2. **กฎเหล็กสูงสุด:** **ห้ามรันคำสั่ง Git ใน Root (`/Users/bart/ไฟล์ดิบ`) เด็ดขาด** ต้องทำงานอยู่ภายในโฟลเดอร์ของโปรเจกต์ย่อยนั้นๆ เสมอ
3. อัปเดตข้อ [1/4] เป็น ✅

---

## ขั้นตอนที่ 2: เขียนและอัปเดตเอกสารส่งต่องาน (Handoff Generation)
- **ประสานงานสกิล:** `handoff`
- สร้างหรืออัปเดตไฟล์ `handoff.md` ภายในโฟลเดอร์โครงการย่อย (Overview, Modified Files, Current Status, Next Steps)
- อัปเดตข้อ [2/4] เป็น ✅

---

## ขั้นตอนที่ 3: สแกนความปลอดภัยป้องกันข้อมูลลับรั่วไหล (Strict Leak Prevention)
- สแกนไฟล์ที่ถูกแก้ไขและ `handoff.md` ทันที ตรวจสอบ Passwords, API Keys, Tokens แบบ Plaintext
- ตรวจสอบว่า `.gitignore` ละเว้นไฟล์ `.env` และ build cache แล้ว
- **หากพบความเสี่ยง ให้หยุดแจ้งเตือนทันที ห้าม Push เด็ดขาด**
- เมื่อปลอดภัย 100% อัปเดตข้อ [3/4] เป็น ✅

---

## ขั้นตอนที่ 4: จุดเบรก — ขอยืนยันและทำการ Commit & Push (Commit & Dual-Push)
- **ประสานงานสกิล:** `git-rules`
- ตรวจสอบว่าโฟลเดอร์ย่อยมี `.git` หรือยัง และตั้งค่า Remote `origin` ให้ Push ไปยัง 2 บัญชีคู่ขนาน:
  - Primary: `https://<GITHUB_TOKEN>@github.com/supachaippu/<repo_name>.git`
  - Secondary: `https://<SECONDARY_GITHUB_TOKEN>@github.com/ocrsparepart/<repo_name>.git`
- 🛑 **คำสั่งเบรกแตก:**
  1. อัปเดตข้อ [4/4] เป็น `🛑 แสดงรายการไฟล์ รอคำยืนยันก่อน Push`
  2. แสดงสรุปรายชื่อไฟล์ที่พร้อม Commit ให้ผู้ใช้ตรวจสอบ
  3. **หยุดรอคำยืนยันจากผู้ใช้ (หากสั่ง "ยืนยัน", "ทำเลย", "yes" จึงลงมือ Push ได้ทันที)**
- เมื่อได้รับยืนยัน ทำการ Commit และ Push ไปยังทั้ง 2 บัญชีคู่ขนาน แล้วอัปเดตข้อ [4/4] เป็น ✅

---

## ขั้นตอนที่ 5: สรุปรายงานสำหรับผู้บริหาร (Executive Summary)
- **ประสานงานสกิล:** `management-talk`
- เขียนข้อความสรุปผลงานสั้นๆ 3-4 บรรทัดในภาษาที่กระชับ ชัดเจน พร้อมนำไปส่งต่อได้ทันที
