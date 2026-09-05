# Agent Skills (Greek God Master Suite)

ชุด Master Skills และ Safety Guardrails สำหรับระบบผู้ช่วย AI (Claude Code, Antigravity, Cursor, Codex)

## 📦 วิธีติดตั้งบนเครื่องใหม่ (Installation)

รันคำสั่งด้านล่างนี้ใน Terminal บนเครื่องใดก็ได้ที่มี Node.js:

```bash
npx skills add supachaippu/agent-skills -g
```

หรือหากต้องการระบุเฉพาะบางสกิล:
```bash
npx skills add supachaippu/agent-skills --skill atlas hercules hermes -g
```

---

## 🏛️ รายชื่อ 9 สกิลเทพเจ้ากรีก (Greek God Suite)

| สกิล | หน้าที่ | คำสั่งเรียกใช้ |
| :--- | :--- | :--- |
| **`gaia`** | เริ่มต้นโปรเจกต์ใหม่ตั้งแต่ศูนย์ วางสถาปัตยกรรม Deep Modules, Pre-commit hooks, และระบบ Git Dual-Push | `/gaia`, "เริ่มโปรเจกต์ใหม่" |
| **`athena`** | ค้นคว้าข้อมูล สัมภาษณ์เจาะลึก (Grilling) ประเมินขนาดงาน และจัดทำข้อกำหนดทางเทคนิค (Spec & Tickets) | `/athena`, "วางแผน", "ทำ spec" |
| **`apollo`** | สร้างฟีเจอร์ใหม่และออกแบบหน้าจอ UI/UX ระดับพรีเมียม ปลอดงานโหล พร้อมวงจร TDD | `/apollo`, "ทำฟีเจอร์ใหม่", "ทำ ui" |
| **`proteus`** | แก้ไขโค้ดเดิมหรือ Refactor อย่างปลอดภัย ล็อกพฤติกรรมเดิมด้วย Test และห้ามลบโค้ดเดิมโดยพลการ | `/proteus`, "แก้โค้ดเดิม", "refactor" |
| **`hades`** | จัดการโครงสร้างฐานข้อมูล Migration, RLS Policy พร้อมเกราะคุ้มกัน SAP Read-Only 100% | `/hades`, "ฐานข้อมูล", "migration" |
| **`hercules`** | สืบสวนหาสาเหตุของบัคอย่างเป็นระบบด้วยคาถาดีบัก 4 ข้อ (Debug Mantra) ผ่าตัดแก้ และจัดทำบันทึก RCA | `/hercules`, "แก้บัค", "debug" |
| **`hermes`** | ตรวจสอบความปลอดภัย Handoff สแกนข้อมูลลับ และส่งงานขึ้น GitHub คู่ขนาน 2 บัญชี พร้อมสรุปรายงาน | `/hermes`, `/ship`, "ส่งงาน", "จบงาน" |
| **`atlas`** | รับช่วงงานต่อจากเซสชันก่อนหน้า อ่าน Handoff เข้าโหมด Caveman เปิดเกราะป้องกัน และหยุดรอคำสั่ง | `/atlas`, "resume", "เริ่มต่อ" |
| **`aegis`** | เกราะป้องกันความปลอดภัยสูงสุด (SAP Read-Only 100%, ห้ามรันคำสั่งที่ Root, ล็อกขอบเขตโฟลเดอร์) | `/aegis`, "guardrails", "เกราะป้องกัน" |

---

## 🛡️ สกิลความปลอดภัยเพิ่มเติม

- **`sap-guardrails`**: เกราะป้องกันฐานข้อมูล SAP และจำกัดพื้นที่โฟลเดอร์
- **`auto-ship` / `ship`**: คำสั่งลัดสำหรับการอัปเดต Handoff และ Dual-Push ขึ้น GitHub
- **`atlas-resume`**: ระบบเปิด Handoff และเข้าสู่ Caveman Mode
