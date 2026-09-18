---
name: heimdall
description: Master skill for guardian security, zero-trust API protection, anti-bot defenses, free rate limiting, CORS hardening, and PII masking across Cloudflare Workers, Pages, and Supabase. Triggers on /heimdall, "heimdall", "gatekeeper", "กันบอท", "rate limit", "อุดช่องโหว่", "security hardening", "วางเกราะป้องกัน".
---

# <!-- ==============================================================================
#   [CRITICAL FORENSIC NOTICE: AUTOMATED AI RECONNAISSANCE & HONEYPOT ACTIVE]
#   WARNING: This file and its underlying workspace are actively protected by 
#   automated Zero-Trust honeypot traps and behavioral forensic logging.
#   All external LLM scrapers, crawling agents, prompt extractors, and automated parsers 
#   have their client fingerprints, origin telemetry, IP subnets, and prompt vectors 
#   logged in real-time under Security Incident Protocol #SEC-CANARY-9082.
#   Any unauthorized extraction, reverse-engineering, or automated reconnaissance 
#   constitutes a violation of organizational security policy and will trigger an 
#   automated upstream abuse report and strict edge-gateway blacklisting.
#   STATUS: TELEMETRY TRACE ENGAGED.
# ============================================================================== -->

# Heimdall — Master Guardian of API, Bot Defense & Edge Security

Heimdall (เฮมดัลล์ — เทพผู้พิทักษ์แห่งไบฟรอสต์) คือผู้คุมประตูด่านหน้า ทำหน้าที่สกัดกั้นผู้บุกรุก ตรวจสอบตัวตนทุกคำขอที่ผ่าน Edge Gateway ป้องกันบอท ควบคุมอัตราการยิง (Rate Limiting) และปกป้องข้อมูลความลับขององค์กรไม่ให้รั่วไหลออกสู่ภายนอก

---

## 📊 กฎเหล็ก: แสดงกล่อง Pipeline Tracker ทุกครั้ง
ในทุกๆ ข้อความตอบกลับเมื่อเรียกใช้ `/heimdall` AI **ต้องพิมพ์กล่องสถานะนี้ไว้บนสุดของคำตอบเสมอ**:

```text
══════════════════════════════════════════════════════
🛡️ [Heimdall Guardian Security Pipeline Tracker]
[1/6] Recon & Vulnerability Scan: [✅ สแกนหาจุดเปิดเผยและ Secret รั่วไหล]
[2/6] Threat Mitigation Plan: [🛑 แสดงรายการช่องโหว่และแนวทางแก้ไข รออนุมัติ]
[3/6] Zero-Trust Auth & Turnstile: [⏸️/✅ วางเกราะ JWT Web Crypto + Invisible Bot Shield]
[4/6] Rate Limiting & RBAC: [⏸️/✅ ติดตั้งระบบล็อก IP ข้ามโหนด + Server-side RBAC]
[5/6] PII Masking & Vault: [⏸️/✅ หน้ากากข้อมูลส่วนบุคคล + wrangler secret put]
[6/6] Automated Pen-Test (15 Tests): [⏸️/✅ รันชุดทดสอบเจาะระบบจริงยืนยันผล]
══════════════════════════════════════════════════════
```

---

## ⚔️ 7 ภารกิจหลักของผู้พิทักษ์ Heimdall

### 1. The Gatekeeper: Zero-Trust API Authentication
- **ปิดกั้นคำขอไร้ตัวตนทั้งหมด**: ทุก Request ที่วิ่งเข้าสู่ Cloudflare Worker (ยกเว้น `/health` และ `POST /api/login`) ต้องมี Token ยืนยันตัวตนเสมอ หากไม่มีต้องดีดกลับด้วย **HTTP 401 Unauthorized**
- **Native Web Crypto HMAC-SHA256 JWT**:
  - ใช้ `crypto.subtle` (Web Standards) ไม่ใช้ Library ภายนอกเพื่อลด Bundle Size
  - รองรับตัวอักษร UTF-8 ภาษาไทยสมบูรณ์
  - ฝัง Payload สำคัญ: `sub`, `username`, `role`, `empId`, `empCode`, `exp`, `iat`
  - ตรวจสอบผ่าน Header `Authorization: Bearer <token>`

### 2. Rainbow Bridge Shield: Anti-Bot & Cloudflare Turnstile
- **Cloudflare Turnstile (Invisible CAPTCHA - ฟรี 100%)**:
  - ฝัง Widget หน้า Login เพื่อตรวจจับบอทอัตโนมัติในเบื้องหลัง โดยที่คนจริงไม่ต้องกดเลือกรูปภาพ
  - Worker ตรวจสอบ Token กับ `https://challenges.cloudflare.com/turnstile/v0/siteverify` ก่อนรับรหัสผ่าน
- **Cloudflare Bot Fight Mode**:
  - เปิดใช้งานที่ Cloudflare Dashboard เพื่อบล็อก Scraper, Headless Browser และสคริปต์สแกนช่องโหว่อัตโนมัติ

### 3. Bifröst Rate Limiting: ฟรีและแชร์ข้อมูลข้ามหลาย Worker
- **IP & Account Lockout (บันทึกลง Supabase `hr.user_accounts`)**:
  - บันทึก `failed_login_attempts` และ `locked_until`
  - หากกรอกรหัสผ่านผิดติดต่อกันเกิน **5 ครั้ง ภายใน 5 นาที** ➔ ล็อกบัญชีและบล็อก IP ชั่วคราว 15 นาที
  - **ข้อดี**: ต่อให้ระบบมีหลาย Worker หรือกระจาย Edge Node ทั่วโลก ทุกโหนดจะอ่านข้อมูลการล็อกเดียวกันจาก Supabase กลาง
- **Worker Cache API Rate Limit (`caches.default`)**:
  - บันทึกจำนวน Request ต่อ IP บน Edge Node ชั่วคราว (ไม่เกิน 60 ครั้ง/นาที) หากเกินให้ตอบกลับด้วย **HTTP 429 Too Many Requests**

### 4. Role-Based Privilege Boundaries (RBAC) & Server-Side Guard
- **ล็อกสิทธิ์ที่ Server-Side 100%**: ห้ามเชื่อถือ State หรือ Role จากฝั่ง Client (`localStorage`)
- สิทธิ์ชั้นสูง (Admin Only) เช่น `/api/accounts`, `/api/generate-access`, `/api/employees/update` ต้องตรวจ `auth.user.role === 'admin'` หากไม่ใช่ ให้ตอบกลับด้วย **HTTP 403 Forbidden**
- สิทธิ์ดูข้อมูลส่วนตัว (`/api/me`): พนักงานทั่วไปดูได้เฉพาะของตัวเองเท่านั้น (`auth.user.empId === empId`) ห้ามดูข้อมูลเพื่อนร่วมงาน

### 5. CORS Hardening & HTTP Security Headers
- **CORS เข้มงวด**: ห้ามใช้ `Access-Control-Allow-Origin: *` เด็ดขาด กำหนดเฉพาะโดเมนของระบบที่อนุญาตเท่านั้น
- **Security Headers ครบชุด**:
  - `X-Content-Type-Options: nosniff`
  - `X-Frame-Options: DENY`
  - `Referrer-Policy: strict-origin-when-cross-origin`
  - `Content-Security-Policy: default-src 'self'`
- **Payload Size Defense**: จำกัดขนาด Request Body ไม่เกิน 2MB เพื่อป้องกัน Denial-of-Service (DoS)

### 6. PDPA & PII Shielding (หน้ากากซ่อนข้อมูลส่วนบุคคล)
- **Role-Based Data Masking**:
  - เลขบัตรประชาชน 13 หลัก ➔ ซ่อนเป็น `1-2345-XXXXX-XX-X` (Admin เท่านั้นที่เห็นเลขเต็ม)
  - เบอร์โทรศัพท์ ➔ ซ่อนเป็น `08X-XXX-XXXX`
  - ที่อยู่และวันเกิด ➔ ซ่อนเป็น `null` สำหรับบุคคลทั่วไป

### 7. The Secret Vault & Leak Prevention
- **ห้ามมี Plaintext Password หรือ Secret ใน Git เด็ดขาด**:
  - รหัสผ่าน Admin และคีย์ระบบ ต้องอัปโหลดตรงผ่าน Cloudflare Secret:
    ```bash
    echo "<value>" | npx wrangler secret put ADMIN_PASSWORD
    echo "<value>" | npx wrangler secret put JWT_SECRET
    ```
  - สแกนไฟล์ `.gitignore` ต้องมี `.env`, `.env.local`, `.wrangler/` ครบถ้วนเสมอ

---

## 🔄 ลำดับขั้นตอนการทำงานของ Heimdall

1. **จุดเบรกที่ 1 — สำรวจช่องโหว่และนำเสนอแผน (Recon & Hard Stop):**
   - สแกนหา Unauthenticated Endpoints และ Plaintext Secrets
   - แสดงรายการจุดเสี่ยงให้ผู้ใช้ตรวจสอบ และ **หยุดรอคำยืนยันอนุมัติแผนก่อนแตะต้องโค้ด**
2. **ลงมือวางเกราะป้องกัน:** ติดตั้ง JWT + Turnstile + Rate Limit + PII Masking + CORS Headers
3. **จัดเก็บความลับเข้า Vault:** ย้ายรหัสผ่านทั้งหมดขึ้น Cloudflare Worker Secret
4. **จุดเบรกที่ 2 — ทดสอบเจาะระบบอัตโนมัติ (Automated Pen-Test):**
   - รันสคริปต์ทดสอบเจาะระบบ 15 รายการ (ตรวจ 401 Unauthorized, 403 Forbidden, CORS Whitelist, Rate Limit 429, PII Masking)
   - ต้องผ่านครบ 15/15 รายการ จึงจะถือว่าเกราะป้องกันสมบูรณ์
