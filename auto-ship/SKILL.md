---
name: auto-ship
description: One-shot end-of-session pipeline that automatically updates handoff.md, scans for secrets, commits changes, and dual-pushes to both GitHub accounts (supachaippu and ocrsparepart). Trigger on /ship, /auto-ship, "handoff+commit+push", "จบงาน", or "ส่งงานขึ้น git".
---

# Auto-Ship Pipeline (Handoff + Secret Scan + Commit + Dual-Push)

เมื่อผู้ใช้พิมพ์ `/ship`, `/auto-ship`, `handoff+commit+push` หรือบอกว่า "จบงาน / ส่งงานขึ้น git":
ให้ปฏิบัติตามลำดับขั้นตอนอัตโนมัตินี้แบบต่อเนื่อง (Closed-Loop) ทันที:

---

## Step 1: ตรวจสอบขอบเขตโฟลเดอร์ (Subproject Identification)
1. ระบุโฟลเดอร์ของโครงการย่อยปัจจุบันที่กำลังทำงานอยู่ (เช่น `/Users/bart/ไฟล์ดิบ/<subproject>`)
2. **กฎเหล็ก:** ห้ามรันคำสั่ง Git ในโฟลเดอร์ Root (`/Users/bart/ไฟล์ดิบ`) เด็ดขาด ต้องทำงานอยู่ภายในโฟลเดอร์ของโปรเจกต์ย่อยนั้นๆ เสมอ

---

## Step 2: เขียนและอัปเดต `handoff.md` อัตโนมัติ (Handoff Generation)
สร้างหรืออัปเดตไฟล์ `handoff.md` ภายในโฟลเดอร์ย่อยนั้น โดยต้องมีหัวข้อสำคัญครบถ้วน:
- **ภาพรวมงาน (Task Overview):** สรุปเป้าหมายของงานในรอบนี้
- **ไฟล์ที่มีการเปลี่ยนแปลง (Modified Files):** รายชื่อไฟล์ที่สร้างใหม่หรือแก้ไข
- **สถานะปัจจุบัน (Current Status):** ฟังก์ชันอะไรใช้งานได้แล้ว ผลการทดสอบเป็นอย่างไร
- **งานที่ต้องทำต่อในเซสชันถัดไป (Next Steps):** ระบุสิ่งที่ต้องทำต่อเป็นข้อๆ เพื่อให้ `atlas-resume` มาอ่านต่อแล้วเข้าใจทันที

---

## Step 3: ตรวจสอบความปลอดภัย ป้องกันข้อมูลลับรั่วไหล (Strict Leak Prevention)
ก่อนทำ Git commit ต้องสแกนไฟล์ที่ถูกแก้ไขและ `handoff.md` ทันที:
1. ตรวจสอบว่าไม่มี Passwords, API Keys, Tokens (เช่น GitHub Token, Cloudflare Token) แบบ Plaintext อยู่ในไฟล์ใดๆ
2. ตรวจสอบว่ามีไฟล์ `.gitignore` และมีการละเว้นไฟล์ `.env`, `.DS_Store`, และ cache folders แล้ว
3. หากพบความเสี่ยง ให้หยุดแจ้งเตือนผู้ใช้ทันที ห้าม Push ขึ้น GitHub เด็ดขาด

---

## Step 4: ตั้งค่า Git Dual-Push & เตรียม Commit (Git Setup)
1. ตรวจสอบว่าโฟลเดอร์ย่อยมี `.git` หรือยัง หากยังไม่มีให้รัน `git init`
2. ตั้งชื่อ Repo เป็นภาษาอังกฤษตัวพิมพ์เล็กสะอาดตา (Clean repo name)
3. ตรวจสอบและตั้งค่า Remote `origin` ให้ Push ไปยัง 2 บัญชีคู่ขนาน:
   - Primary: `https://<GITHUB_TOKEN>@github.com/supachaippu/<repo_name>.git`
   - Secondary: `https://<SECONDARY_GITHUB_TOKEN>@github.com/ocrsparepart/<repo_name>.git`
4. รัน `git add .` และ `git status` เพื่อแสดงรายการไฟล์ที่พร้อมขึ้น

---

## Step 5: ขอยืนยันและทำการ Commit & Push (Commit & Dual-Push)
1. แสดงสรุปรายชื่อไฟล์ให้ผู้ใช้ทราบในแชท และขอคำยืนยันสั้นๆ (หากผู้ใช้สั่ง "ทำเลย", "ลุยเลย", "yes" หรือยืนยันแล้ว ให้ดำเนินการทันที)
2. ทำการ Commit ด้วยข้อความอธิบายที่ชัดเจน (Semantic Commit Message เช่น `feat: ...` หรือ `fix: ...`)
3. ทำการ Push ขึ้นทั้ง 2 บัญชีคู่ขนาน:
   ```bash
   git push -u origin main || git push -u origin master
   ```

---

## Step 6: สรุปรายงานจบกะ (Executive Summary)
เขียนข้อความสรุปผลงานสั้นๆ 3-4 บรรทัดในสไตล์ `management-talk` เพื่อให้ผู้ใช้สามารถคัดลอกไปแปะใน Line หรือรายงานผู้บริหารได้ทันที
