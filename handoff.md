# Handoff: Greek God Master Skills Suite (`agent-skills`)

## 1. ภาพรวมงาน (Task Overview)
- สร้างและติดตั้งชุด **9 Master Skills สไตล์เทพเจ้ากรีก** (`gaia`, `athena`, `apollo`, `proteus`, `hades`, `hercules`, `hermes`, `atlas`, `aegis`) เพื่อเป็น One-Loop Pipeline รองรับวงจรการพัฒนาซอฟต์แวร์ครบวงจร
- รวมศูนย์ความปลอดภัย: SAP SQL Server Read-Only 100%, ป้องกันการรัน Git ที่โฟลเดอร์ Root, และระบบล็อกขอบเขตโฟลเดอร์โครงการย่อย
- กำหนดนโยบายสถาปัตยกรรมข้อมูล: เลือกใช้ **Supabase (PostgreSQL)** เป็นหลักสำหรับ Database และแคช (ใช้ประโยชน์จาก Cached Egress และ Storage ในตัว) แทนการพึ่งพา Cloudflare KV ที่ตรวจสอบโควตายาก
- **อัปเกรดมาตรฐาน UI/UX ใน `apollo`:** ปลดระวาง `hallmark` และนำมาตรฐาน **Tremor Blocks** (`blocks.tremor.so`) มาเป็นหัวใจหลักในการสร้าง Dashboard, Metric Cards, Status Banners, และ Dark/Light Mode โทน Zinc สะอาดตา
- จัดทำเป็นแพ็กเกจ Repository `supachaippu/agent-skills` (Public) และ `ocrsparepart/agent-skills` (Private Backup) เพื่อให้ติดตั้งบนเครื่องอื่นได้ทันทีผ่าน `npx skills add supachaippu/agent-skills -g`

---

## 2. ไฟล์ที่มีการเปลี่ยนแปลง / สร้างขึ้น (Modified & Created Files)
- `apollo/SKILL.md` — ยึดมาตรฐานการออกแบบสไตล์ **Tremor Blocks** สำหรับการสร้างฟีเจอร์และ Dashboard
- `gaia/SKILL.md` — เริ่มต้นโปรเจกต์ใหม่ตั้งแต่ศูนย์ วางสถาปัตยกรรม Deep Modules, Pre-commit hooks, และ Git Dual-Push
- `athena/SKILL.md` — วิจัย วางแผน สัมภาษณ์เจาะลึก (Grilling) และแตกตั๋วงาน
- `proteus/SKILL.md` — ปรับปรุง/แก้ไขโค้ดเดิมอย่างปลอดภัย ล็อกพฤติกรรมเดิมด้วย Test และสงวนรักษาโค้ดเดิม
- `hades/SKILL.md` — ออกแบบและจัดการฐานข้อมูล Supabase, RLS Policy, และเกราะ SAP Read-Only พร้อมนโยบาย Cached Egress
- `hercules/SKILL.md` — สืบสวนและปราบปรามบัคแบบเป็นระบบตามคาถา 4 ข้อ (Debug Mantra)
- `hermes/SKILL.md` — ปิดกะ สแกนหา Secret หลุด และ Dual-Push ขึ้น GitHub 2 บัญชีคู่ขนาน
- `atlas/SKILL.md` — รับช่วงงานต่อ อ่าน Handoff เข้าโหมด Caveman และหยุดรอคำสั่ง
- `aegis/SKILL.md` — เกราะป้องกันความปลอดภัยระดับสากล
- `auto-ship/SKILL.md`, `ship/SKILL.md`, `atlas-resume/SKILL.md`, `sap-guardrails/SKILL.md` — สกิลทางลัดเพิ่มเติม
- `README.md` — คู่มือการติดตั้งและคำอธิบายชุดสกิล
- `.gitignore` — ป้องกันการอัปโหลดไฟล์ลับและแคช

---

## 3. สถานะปัจจุบัน (Current Status)
- ✅ ลบ `hallmark` ออกจากระบบเรียบร้อยแล้ว
- ✅ อัปเกรด `apollo` สู่มาตรฐาน Tremor Blocks UI/UX เรียบร้อยทุกที่ (`.agents/skills/`, `~/.agents/skills/`, `agent-skills/`)
- ✅ Dual-Push ขึ้น GitHub ทั้ง 2 บัญชีเรียบร้อย:
  - `https://github.com/supachaippu/agent-skills` (Public)
  - `https://github.com/ocrsparepart/agent-skills` (Private Backup)

---

## 4. สิ่งที่ต้องทำต่อในรอบหน้า (Next Steps)
- เมื่อสั่ง `/apollo` ในการทำหน้าเว็บหรือ Dashboard ระบบจะยึดรูปแบบ Tremor Blocks ทันที
- สามารถติดตั้งบนเครื่องอื่นผ่านคำสั่ง `npx skills add supachaippu/agent-skills -g`
