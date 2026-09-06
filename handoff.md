# Handoff: Greek God Master Skills Suite (`agent-skills`)

## 1. ภาพรวมงาน (Task Overview)
- สร้างและติดตั้งชุด **9 Master Skills สไตล์เทพเจ้ากรีก** (`gaia`, `athena`, `apollo`, `proteus`, `hades`, `hercules`, `hermes`, `atlas`, `aegis`) เพื่อเป็น One-Loop Pipeline รองรับวงจรการพัฒนาซอฟต์แวร์ครบวงจร
- **ระบบติดตามสถานะแบบโปร่งใส (Visual Pipeline Tracker):** ฝังกล่องแสดงสถานะ Checklist แบบ Real-time บนหัวข้อความทุกครั้ง เพื่อให้ผู้ใช้เห็นทันทีว่า AI รันขั้นตอนไหนอยู่ ขั้นตอนไหนผ่านแล้ว (`✅`) และขั้นตอนไหนกำลังหยุดรอผู้ใช้ (`🛑`) ป้องกันปัญหา Black Box และจับไต๋บัคได้ทันที 100%
- **ฝังจุดเบรกบังคับหยุด (Hard Blocking Gates) ในทุกสกิล:** บังคับให้ AI ต้องสัมภาษณ์ป๋าจริง, ท่องคาถาดีบักจริง, แสดง Wireframe จริง, และขออนุมัติก่อนแตะต้องโค้ดหรือฐานข้อมูล
- **ฝัง `wayfinder` สถาปัตยกรรมม่านหมอกลงใน `athena` แบบเจาะลึก:** ถ้าเป็นงานใหญ่ AI ต้องกาง Wayfinder Map (Destination, Decisions so far, Fog of War, Out of scope) ออกมาทันที แล้วดึงหัวข้อในหมอกไป Grilling ซักไซ้ป๋าทีละรอบ
- รวมศูนย์ความปลอดภัย: SAP SQL Server Read-Only 100%, ป้องกันการรัน Git ที่โฟลเดอร์ Root, และระบบล็อกขอบเขตโฟลเดอร์โครงการย่อย
- กำหนดนโยบายสถาปัตยกรรมข้อมูล: เลือกใช้ **Supabase (PostgreSQL)** เป็นหลักสำหรับ Database และแคช (ใช้ประโยชน์จาก Cached Egress และ Storage ในตัว) แทนการพึ่งพา Cloudflare KV ที่ตรวจสอบโควตายาก
- อัปเกรดมาตรฐาน UI/UX ใน `apollo` สู่มาตรฐาน **Tremor Blocks** (`blocks.tremor.so`)
- จัดทำเป็นแพ็กเกจ Repository `supachaippu/agent-skills` (Public) และ `ocrsparepart/agent-skills` (Private Backup) เพื่อให้ติดตั้งบนเครื่องอื่นได้ทันทีผ่าน `npx skills add supachaippu/agent-skills -g`

---

## 2. สถานะปัจจุบัน (Current Status)
- ✅ ติดตั้งระบบ **Pipeline Tracker** ครบทุกสกิลหลักแล้ว
- ✅ ซิงค์เข้าสู่ `~/.agents/skills/`, `.agents/skills/`, และ `agent-skills/`
- ✅ ผ่านการทดสอบ syntax/frontmatter ทุกตัว 100%
