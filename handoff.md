# Handoff: Greek God Master Skills Suite (`agent-skills`)

## 1. ภาพรวมงาน (Task Overview)
- สร้างและติดตั้งชุด **9 Master Skills สไตล์เทพเจ้ากรีก** (`gaia`, `athena`, `apollo`, `proteus`, `hades`, `hercules`, `hermes`, `atlas`, `aegis`) เพื่อเป็น One-Loop Pipeline รองรับวงจรการพัฒนาซอฟต์แวร์ครบวงจร
- **ฝังจุดเบรกบังคับหยุด (Hard Blocking Gates) ในทุกสกิล:** ป้องกันไม่ให้ AI แอบรวบรัดตัดตอนคิดเองเออเอง โดยบังคับให้ต้องสัมภาษณ์ป๋าจริง, ท่องคาถาดีบักจริง, แสดง Wireframe จริง, และขออนุมัติก่อนแตะต้องโค้ดหรือฐานข้อมูล 100%
- **ฝัง `wayfinder` สถาปัตยกรรมม่านหมอกลงใน `athena` แบบเจาะลึก:** ถ้าเป็นงานใหญ่ AI ต้องกาง Wayfinder Map (Destination, Decisions so far, Fog of War, Out of scope) ออกมาทันที แล้วดึงหัวข้อในหมอกไป Grilling ซักไซ้ป๋าทีละรอบ
- รวมศูนย์ความปลอดภัย: SAP SQL Server Read-Only 100%, ป้องกันการรัน Git ที่โฟลเดอร์ Root, และระบบล็อกขอบเขตโฟลเดอร์โครงการย่อย
- กำหนดนโยบายสถาปัตยกรรมข้อมูล: เลือกใช้ **Supabase (PostgreSQL)** เป็นหลักสำหรับ Database และแคช (ใช้ประโยชน์จาก Cached Egress และ Storage ในตัว) แทนการพึ่งพา Cloudflare KV ที่ตรวจสอบโควตายาก
- อัปเกรดมาตรฐาน UI/UX ใน `apollo` สู่มาตรฐาน **Tremor Blocks** (`blocks.tremor.so`)
- จัดทำเป็นแพ็กเกจ Repository `supachaippu/agent-skills` (Public) และ `ocrsparepart/agent-skills` (Private Backup) เพื่อให้ติดตั้งบนเครื่องอื่นได้ทันทีผ่าน `npx skills add supachaippu/agent-skills -g`

---

## 2. รายละเอียดจุดเบรก (Hard Blocking Gates) ที่ฝังในแต่ละสกิล
1. **`athena`:** กางแผนที่ **Wayfinder Map** เจาะม่านหมอก (Fog of War) ➡️ หยุดรันทันทีเพื่อยิงคำถาม Grilling (❓ Q1, ❓ Q2...) ซักไซ้ป๋าเป็นรอบๆ **ห้ามเขียน Spec จนกว่าป๋าจะตอบเสร็จ**
2. **`hercules`:** ท่องบทสวดดีบัก 4 ข้อในบรรทัดแรก และ **หยุดทันทีหากยังจำลองบัคไม่ได้ (Cannot Repro)** ห้ามเดาสาเหตุแก้ไขโค้ดลอยๆ
3. **`apollo`:** หยุดเพื่อแสดง **Tremor Blocks Wireframe Layout** ให้ป๋าตรวจและอนุมัติก่อนเขียนโค้ดหน้าเว็บจริง
4. **`proteus`:** หยุดเพื่อแสดง **Implementation Plan & Blast Radius** (รายชื่อไฟล์ที่จะแก้และผลกระทบ) ให้ป๋าอนุมัติก่อนแตะต้องโค้ด
5. **`gaia`:** หยุดเพื่อถาม **เป้าหมายโครงการและ Tech Stack** จากป๋าก่อนเริ่มสร้างโครงสร้างและ `CONTEXT.md`
6. **`hades`:** หยุดเพื่อแสดง **SQL DDL Migration Script** ให้ป๋าตรวจสอบและยืนยันก่อนรันเข้าฐานข้อมูลจริง

---

## 3. สถานะปัจจุบัน (Current Status)
- ✅ ผสาน `wayfinder` และจุดเบรก (Hard Blocking Gates) ครบถ้วนทุกสกิลแล้ว
- ✅ ซิงค์เข้าสู่ `~/.agents/skills/`, `.agents/skills/`, และ `agent-skills/`
- ✅ ผ่านการทดสอบ syntax/frontmatter ทุกตัว 100%
