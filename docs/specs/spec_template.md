# 📋 Specification: [Feature Name] (`spec_[feature].md`)

- **Feature / Module**: `src/modules/[feature_name]/`
- **Author / Agent**: [AI Agent Name / Author]
- **Created Date**: YYYY-MM-DD
- **Last Updated**: YYYY-MM-DD
- **Status**: [ ] Draft / [ ] In Progress / [ ] Completed / [ ] Verified

---

## 1. 🎯 วัตถุประสงค์และขอบเขต (Objective & Scope)
- **Objective**: อธิบายว่าฟีเจอร์นี้สร้างขึ้นเพื่อแก้ปัญหาอะไร และทำอะไรได้บ้าง
- **In-Scope**: สิ่งที่ต้องทำในรอบนี้
- **Out-of-Scope**: สิ่งที่ยังไม่ทำ หรือยกยอดไปเฟสถัดไป

---

## 2. ⚙️ Single Source of Truth & Configurations (`src/config/`)
ระบุค่าคงที่ เมนู หรือสิทธิ์ที่จะเพิ่มลงใน Config กลาง:
- [ ] **Routes**: กำหนด Path ใน `src/config/routes.ts`
- [ ] **Permissions**: กำหนด Role & Permission ใน `src/config/permissions.ts`
- [ ] **Navigation**: เพิ่มเมนูใน `src/config/navigation.ts` (ถ้ามี UI Menu)
- [ ] **Feature Flags**: เพิ่ม Flag ใน `src/config/features.ts` (ถ้ามี)

---

## 3. 🧩 Architecture & File Mapping

| Layer | File Path | หน้าที่ความรับผิดชอบ |
| :--- | :--- | :--- |
| **Page / Action** | `src/app/(dashboard)/[feature]/page.tsx`<br>`src/app/(dashboard)/[feature]/actions.ts` | Routing, Server Actions, Error boundaries |
| **UI Components** | `src/modules/[feature]/components/...` | Presentation, User Interactions, States |
| **Service Layer** | `src/modules/[feature]/services/[feature].service.ts` | Pure Business Rules, Calculations |
| **Repository** | `src/modules/[feature]/repositories/[feature].repository.ts` | Database Queries (Prisma/Drizzle/SQL) |
| **Schema & Validation** | `src/modules/[feature]/schemas/[feature].schema.ts` | Zod Validation Schemas |
| **Types & Interfaces** | `src/modules/[feature]/types/[feature].types.ts` | TypeScript Definitions |
| **Module Config** | `src/modules/[feature]/config/[feature].config.ts` | Module-specific settings |

---

## 4. ✅ Implementation & Verification Checklist (ตารางตรวจงาน)

### Phase 1: Specifications & Configurations
- [ ] 1.1 สร้าง/อัปเดตไฟล์ `docs/specs/spec_[feature].md` นี้ให้ครบถ้วน
- [ ] 1.2 ประกาศ Routes, Permissions, และ Config ที่เกี่ยวข้องใน `src/config/`

### Phase 2: Domain, Schema & Service Layer
- [ ] 2.1 กำหนด TypeScript Interfaces ใน `types/[feature].types.ts`
- [ ] 2.2 สร้าง Zod Validation Schema ใน `schemas/[feature].schema.ts`
- [ ] 2.3 สร้าง Database Repository ใน `repositories/[feature].repository.ts`
- [ ] 2.4 เขียน Business Logic ใน `services/[feature].service.ts`
- [ ] 2.5 ตรวจสอบ Server-side Authorization & Data Sanitization

### Phase 3: UI & Interaction Layer
- [ ] 3.1 สร้าง UI Components ใน `modules/[feature]/components/`
- [ ] 3.2 เชื่อมต่อ Server Actions ใน `app/.../actions.ts`
- [ ] 3.3 จัดการ State: Loading, Error, Empty, และ Success Feedback

### Phase 4: Constitution & Architecture Review
- [ ] 4.1 ตรวจสอบว่าไม่มี Hardcode (ใช้ Config ครบถ้วน)
- [ ] 4.2 ตรวจสอบว่า UI ไม่มี Business Logic หรือ DB Access ปะปน
- [ ] 4.3 ตรวจสอบ DRY และไม่มีโค้ด Duplicate
- [ ] 4.4 ตรวจสอบว่า Error Handling ไม่หลุดข้อมูลความลับ

---

## 5. 🔍 Acceptance Criteria & Test Scenarios (เกณฑ์การตรวจรับงาน)

- [ ] **Scenario 1 (Happy Path)**:
  - *Given*: ผู้ใช้ที่มีสิทธิ์กรอกข้อมูลครบถ้วน
  - *When*: กดบันทึกข้อมูล
  - *Then*: ระบบบันทึกสำเร็จ แสดงข้อความแจ้งเตือน และข้อมูลแสดงในตารางทันที

- [ ] **Scenario 2 (Validation Error)**:
  - *Given*: ผู้ใช้กรอกข้อมูลไม่ถูกต้องตาม Schema
  - *When*: ส่งฟอร์ม
  - *Then*: Server ปฏิเสธและส่ง Error message ชัดเจนกลับมาแสดงที่ฟอร์ม

- [ ] **Scenario 3 (Unauthorized Access)**:
  - *Given*: ผู้ใช้ที่ไม่มี Permission เข้าถึงหรือพยายามยิง Action
  - *When*: เรียกใช้ API / Server Action
  - *Then*: ระบบปฏิเสธด้วย `403 Forbidden` และไม่รัน Business Logic
