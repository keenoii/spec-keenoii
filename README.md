# 🏛️ AI Engineering Constitution & Starter Template

> **Config-Driven Modular Architecture with Single Source of Truth**  
> ออกแบบมาเพื่อกำหนดมาตรฐานการทำงานร่วมกับ AI (Claude, Antigravity, Cursor, Copilot) ในการพัฒนา Next.js Full-Stack Application อย่างมีระบบและยั่งยืน

---

## 🚀 เอกสารสำคัญสำหรับเริ่มต้น

1. **[`START_HERE.md`](./START_HERE.md)** — จุดเริ่มต้นสำหรับ AI Agents และ Developers (Workflow, Directory structure, Pre-code checklist)
2. **[`CONSTITUTION.md`](./CONSTITUTION.md)** — รัฐธรรมนูญวิศวกรรมซอฟต์แวร์ AI ฉบับเต็ม 42 ข้อบังคับ
3. **[`AGENTS.md`](./AGENTS.md)** / **[`GEMINI.md`](./GEMINI.md)** — กฎสำหรับ AI Agent ในการโหลดเข้า Context อัตโนมัติ

---

## 📁 โครงสร้างเอกสารในโปรเจกต์ (`docs/`)

* **`docs/requirements/`**: เก็บผลการวิเคราะห์ Requirement จาก `/grill-with-docs`
* **`docs/specs/`**: เก็บ Technical Specifications จาก `/to-spec`
* **`docs/tickets/`**: เก็บ Implementation Tickets และ Acceptance Criteria จาก `/to-tickets`
* **`docs/decisions/`**: เก็บบันทึกการตัดสินใจสถาปัตยกรรม (ADR)
* **`docs/handovers/`**: เก็บบันทึกส่งต่องานระหว่าง AI Session หรือข้ามโมเดล

---

## 🌟 กฎทอง (The Golden Rules)

* 🔍 **Search Before Create** — ค้นหาของเดิมก่อนสร้างใหม่เสมอ
* ♻️ **Reuse Before Duplicate** — นำกลับมาใช้ซ้ำก่อนสร้างซ้ำ
* ⚙️ **Config Before Hardcode** — แยกค่าคงที่และการตั้งค่าไปที่ `src/config/`
* 🏢 **Service Before Business Logic in UI** — UI ทำหน้าที่แสดงผลเท่านั้น Business logic ต้องอยู่ใน Service
* 🎯 **Single Source Before Multiple Sources** — แหล่งข้อมูลและกฎต้องมีจุดเดียว
* 📦 **Module Before Monolith** — แยกโค้ดตามความรับผิดชอบของแต่ละ Feature (`src/modules/`)
* ❓ **Ask Before Assume** — แยกข้อเท็จจริงออกจากข้อสันนิษฐาน ถ้าไม่แน่ใจให้ถามก่อน
* 🎯 **Targeted Diagnostics Before Full-File Reading** — รัน `tsc --noEmit` / lint ก่อนอ่านไฟล์เพื่อประหยัด Token
* ✍️ **Direct Native Edits Before Script Generation** — แก้ไขไฟล์ตรงๆ ห้ามสร้าง Python script มาเขียนทับโค้ด
* 📊 **Impact Analysis Before Shared Code Changes** — วิเคราะห์ผลกระทบก่อนแก้ Shared Code เสมอ
* 🏗️ **Architecture Before Speed** — สถาปัตยกรรมและความยั่งยืนสำคัญกว่าความเร็ว
