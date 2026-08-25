# AI ENGINEERING CONSTITUTION

## Config-Driven Modular Architecture with Single Source of Truth

**Version:** 1.0  
**Platform:** Next.js Full-stack  
**Status:** Mandatory  

---

## 1. CORE PRINCIPLE

ระบบนี้พัฒนาภายใต้แนวคิด:

> **Config-Driven Modular Architecture with Single Source of Truth**

เป้าหมายหลักไม่ใช่การเขียนโค้ดให้เร็วที่สุด

แต่คือการสร้างระบบที่:

* Maintainable (ดูแลรักษาง่าย)
* Modular (เป็นโมดูลแยกอิสระ)
* Reusable (นำกลับมาใช้ซ้ำได้)
* Extensible (ต่อขยายได้ง่าย)
* Testable (ทดสอบได้ครอบคลุม)
* Secure (ปลอดภัย)
* เข้าใจง่ายในระยะยาว

**Maintainability > Development Speed**

---

## 2. SINGLE SOURCE OF TRUTH

ข้อมูลหรือ configuration ที่มีความหมายเดียวกันต้องมีแหล่งข้อมูลหลักเพียงแห่งเดียว

ตัวอย่าง:

* Navigation
* Menu
* Routes
* Permissions
* Roles
* Feature Flags
* Settings
* Prompts
* Constants
* Status
* Validation Rules
* Theme
* Application Configuration

ห้ามสร้างข้อมูลเดียวกันซ้ำในหลายตำแหน่ง

### หลักคิด

```text
One Source
    ↓
Multiple Consumers
```

ถ้าแก้ข้อมูลจากจุดเดียวแล้วระบบทั้งหมดเปลี่ยนตามได้ ถือว่าเป็นแนวทางที่ถูกต้อง

---

## 3. CONFIG-DRIVEN

หากสิ่งใดสามารถกำหนดด้วย Configuration ได้ และมีโอกาสถูกใช้ซ้ำหรือเปลี่ยนในอนาคต ให้พิจารณาทำเป็น Config

ตัวอย่างโครงสร้าง:

```text
src/config/
├── app.ts
├── navigation.ts
├── permissions.ts
├── features.ts
├── prompts.ts
└── settings.ts
```

Component หรือ Service ควร **consume config** แทนการประกาศค่าซ้ำเอง

---

## 4. NO UNNECESSARY HARDCODE

ห้าม Hardcode ค่าที่ควรเป็น Configuration

ตัวอย่างที่ควรพิจารณาเป็น Config:

```text
Menu
Route
Permission
Feature Flag
Business Setting
Prompt
Status
System Limit
Application Setting
```

แต่ไม่จำเป็นต้องสร้าง Config สำหรับค่าที่เป็น implementation detail และไม่มีเหตุผลต้องเปลี่ยน

> Config-driven ไม่ได้หมายถึงทุกอย่างต้องกลายเป็น Config

---

## 5. DRY — DON'T REPEAT YOURSELF

ห้าม Copy-Paste logic ที่มีหน้าที่เดียวกัน

ก่อนสร้างสิ่งใหม่:

```text
Search
  ↓
ตรวจสอบของเดิม
  ↓
Reuse?
 ├─ YES → Reuse
 └─ NO
      ↓
สามารถ Extend ได้?
 ├─ YES → Extend
 └─ NO → Create
```

หากพบ implementation ที่คล้ายกัน ให้พิจารณา Refactor ก่อนสร้างใหม่

---

## 6. SEARCH BEFORE CREATE

ก่อนสร้าง:

* Component
* Service
* Hook
* Utility
* Config
* API
* Validation
* Schema
* Type
* Repository

AI **MUST** ตรวจสอบก่อนว่า project มีสิ่งที่สามารถนำกลับมาใช้ได้หรือไม่

**ห้ามสมมติว่าไม่มีของเดิม**

---

## 7. NEXT.JS FULL-STACK PRINCIPLE

ระบบนี้ใช้ Next.js เป็น Full-stack Application เดียว

**ไม่จำเป็นต้องแยก Frontend และ Backend เป็นสองโปรเจกต์**

Architecture ต้องแยกตาม:

> **Module และ Responsibility**

ไม่ใช่ตาม:

> Frontend / Backend

ตัวอย่าง:

```text
src/modules/
├── auth/
├── users/
├── attendance/
├── reports/
└── settings/
```

แต่ละ Module สามารถมีส่วนประกอบที่จำเป็น เช่น:

```text
src/modules/attendance/
├── components/
├── services/
├── repositories/
├── schemas/
├── types/
└── config/
```

ไม่จำเป็นต้องแยก deployment หรือ project เพียงเพราะมี UI และ server logic อยู่ใน Feature เดียวกัน

---

## 8. MODULAR ARCHITECTURE

ทุก Feature ที่มีขอบเขตชัดเจนควรออกแบบเป็น Module

Module ต้อง:

* มี Responsibility ชัดเจน
* มี Boundary
* Reuse ได้
* ทดสอบได้
* ไม่พึ่ง internal implementation ของ Module อื่นโดยไม่จำเป็น

ตัวอย่าง:

```text
modules/
├── auth/
├── users/
├── attendance/
├── notifications/
└── reports/
```

---

## 9. HIGH COHESION

สิ่งที่เกี่ยวข้องกันควรอยู่ใกล้กัน

ตัวอย่าง:

```text
attendance/
├── attendance.service.ts
├── attendance.repository.ts
├── attendance.schema.ts
├── attendance.types.ts
└── attendance.config.ts
```

ไม่ควรกระจาย logic ของ Feature เดียวไปทั่ว Project โดยไม่มีเหตุผล

---

## 10. LOW COUPLING

Module ต้องพึ่งพากันให้น้อยที่สุด

หลีกเลี่ยงการเข้าถึง implementation ภายในของ Module อื่นโดยตรง

ควรสื่อสารผ่าน:

* Public API
* Service
* Interface
* Shared abstraction ที่เหมาะสม

เป้าหมาย:

```text
Module A
   ↓
Public Interface
   ↓
Module B
```

ไม่ใช่:

```text
Module A
   ↓
Internal File
   ↓
Internal File
   ↓
Module B
```

---

## 11. UI RESPONSIBILITY

UI มีหน้าที่:

* Render
* รับ User Interaction
* แสดง State
* แสดง Loading
* แสดง Error
* แสดง Result

UI **MUST NOT** contain complex Business Logic

ห้ามให้ Component เป็นที่รวม:

* Business Rules
* Database Logic
* Permission Logic
* API Logic
* Validation Logic จำนวนมาก
* Data Transformation ที่ซับซ้อน

หาก Logic เริ่มซับซ้อน ให้แยกออก

---

## 12. BUSINESS LOGIC

Business Logic ต้องอยู่ใน Service / Domain Layer ที่เหมาะสม

ตัวอย่าง:

```text
UI
 ↓
Service
 ↓
Repository / Data Access
 ↓
Database
```

Service ไม่ควรผูกกับ UI

Service ควรสามารถถูกนำไปใช้จาก:

* Server Action
* Route Handler
* Background Job
* CLI
* Test
* Automation

โดยไม่ต้องเปลี่ยน Business Logic

---

## 13. DATA ACCESS

Database / ORM logic ควรแยกจาก Business Logic เมื่อเหมาะสม

ตัวอย่าง:

```text
Service
   ↓
Repository
   ↓
ORM
   ↓
Database
```

ไม่ควรให้ Component เข้าถึง Database โดยตรง

และไม่ควรให้ UI เป็นผู้ตัดสิน Business Rule

---

## 14. VALIDATION

Validation ต้องอยู่ในตำแหน่งที่เหมาะสม

สามารถมี:

```text
UI Validation
      ↓
Server Validation
      ↓
Business Validation
```

แต่ Validation สำคัญต้องถูกตรวจสอบฝั่ง Server เสมอ

ห้ามเชื่อข้อมูลจาก Client โดยตรง

หาก Validation Rule ถูกใช้หลายตำแหน่ง ให้พิจารณาใช้ Schema หรือ Rule กลาง

---

## 15. AUTHORIZATION & PERMISSION

Permission ต้องมี Single Source of Truth

ไม่ควรกระจาย:

```ts
if (role === "admin")
```

ไปทั่วระบบ

ควรมี:

```text
Permission Configuration
        ↓
Authorization Logic
        ↓
UI / Server / Service
```

UI สามารถใช้ Permission เพื่อแสดงหรือซ่อน UI

แต่ **Server-side authorization ต้องเป็นตัวตัดสินที่แท้จริง**

---

## 16. SECURITY

ทุก Feature ต้องพิจารณา:

* Authentication
* Authorization
* Input Validation
* Access Control
* Sensitive Data
* Secrets
* Injection
* XSS
* CSRF เมื่อเกี่ยวข้อง
* File Upload Security
* Rate Limiting เมื่อจำเป็น
* Audit Logging เมื่อเหมาะสม

ห้ามเก็บ Secret หรือ API Key ใน Source Code

---

## 17. ERROR HANDLING

Error ต้องจัดการอย่างเป็นระบบ

ต้อง:

* ตรวจสอบ Error
* Log อย่างเหมาะสม
* Return Error ที่เข้าใจได้
* ไม่เปิดเผยข้อมูลลับ
* แยก Technical Error กับ User-facing Message เมื่อเหมาะสม

ห้ามกลืน Error โดยไม่มีเหตุผล

---

## 18. REUSABLE COMPONENTS

Component ที่มีการใช้ซ้ำควรอยู่ใน Shared UI / Component Layer

ตัวอย่าง:

```text
src/components/
├── ui/
├── shared/
└── layouts/
```

แต่ไม่ควรสร้าง Shared Component เพียงเพราะ "เผื่ออนาคต"

ต้องมีเหตุผลด้าน Reusability ที่ชัดเจน

---

## 19. DESIGN SYSTEM

ค่าที่เป็น Design Token ควรมีศูนย์กลาง

เช่น:

* Color
* Typography
* Spacing
* Radius
* Shadow
* Breakpoint
* Z-index

Component ควรใช้ Design System แทนการสร้างค่าซ้ำเอง

---

## 20. NAVIGATION & MENU

Navigation ต้องมี Single Source of Truth

ตัวอย่าง:

```text
src/config/navigation.ts
```

แล้วนำไปใช้กับ:

```text
Navbar
Sidebar
Mobile Menu
Breadcrumb
Permission Filtering
```

ไม่ควรสร้าง Menu Array ซ้ำในแต่ละ Component

---

## 21. ROUTES

Route ที่ใช้ซ้ำควรมีแหล่งข้อมูลกลางเมื่อเหมาะสม

หลีกเลี่ยงการเขียน String เดียวกันซ้ำทั่วระบบ

หาก Route มี Metadata หรือ Permission ให้รวมไว้กับ Route Configuration เมื่อเหมาะสม

---

## 22. PROMPTS

Prompt ที่ใช้ซ้ำต้องไม่กระจายอยู่ใน Code

ควรจัดเก็บใน:

```text
src/config/prompts/
```

หรือ Prompt Configuration กลาง

ตัวอย่าง:

```text
requirementAnalysis
codeReview
documentAnalysis
contentGeneration
```

แก้ Prompt ที่เดียวแล้วทุก Consumer ใช้เวอร์ชันใหม่ตามกัน

---

## 23. FEATURE FLAGS

Feature Toggle ต้องมีแหล่งข้อมูลกลาง

ตัวอย่าง:

```text
src/config/features.ts
```

ไม่ควรมี:

```ts
if (true)
```

หรือ Flag กระจายหลาย Component

---

## 24. TYPES & SCHEMAS

Type และ Schema ที่มีความหมายเดียวกันควรมี Single Source of Truth

หลีกเลี่ยงการสร้าง Type ซ้ำโดยไม่มีเหตุผล

หากมี DTO, Domain Model หรือ Database Model ที่แตกต่างกันจริง ต้องระบุ Boundary และหน้าที่ให้ชัดเจน

---

## 25. CHANGE PROPAGATION

ก่อนสร้างหรือแก้ Code ให้ถาม:

> **ถ้าค่านี้เปลี่ยนในอนาคต ต้องแก้กี่จุด?**

เป้าหมาย:

```text
แก้ 1 จุด
   ↓
ระบบที่เกี่ยวข้องเปลี่ยนตาม
```

หากต้องแก้หลายจุดเพราะข้อมูลเดียวกันถูก Duplicate:

> พิจารณาปรับ Architecture ก่อน

---

## 26. IMPACT ANALYSIS

ก่อนแก้ Shared Module หรือ Core Module:

1. Search Consumers
2. ตรวจสอบ Dependencies
3. ตรวจสอบ API ที่เกี่ยวข้อง
4. ตรวจสอบ Tests
5. ประเมิน Breaking Change
6. จึงค่อยแก้ไข

ห้ามแก้ Shared Code แบบไม่ตรวจผลกระทบ

---

## 27. NO SILENT ARCHITECTURAL CHANGE

AI ห้ามเปลี่ยน Architecture สำคัญโดยไม่แจ้ง

เช่น:

* เปลี่ยน Authentication
* เปลี่ยน Database Strategy
* เปลี่ยน State Management
* เปลี่ยน Module Boundary
* เพิ่ม Framework
* เพิ่ม Dependency สำคัญ
* เปลี่ยน API Contract

หากจำเป็นต้องเปลี่ยน:

```text
Problem
↓
Options
↓
Trade-offs
↓
Recommendation
↓
Decision
```

---

## 28. NO UNNECESSARY DEPENDENCIES

ก่อนเพิ่ม Package:

1. ตรวจว่ามีของเดิมหรือไม่
2. ตรวจ Native API
3. ตรวจ Existing Library
4. ประเมิน Maintenance
5. ประเมิน Security
6. ประเมิน Bundle / Performance
7. เพิ่มเมื่อมีเหตุผล

---

## 29. REQUIREMENT WORKFLOW

Feature ที่มีความซับซ้อนควรผ่าน:

```text
Requirement
     ↓
Grill
     ↓
Spec
     ↓
Tickets
     ↓
Implement
     ↓
Test
     ↓
Code Review
     ↓
Architecture Review
```

ไม่ควรกระโดดจาก Idea ไป Implement ทันทีสำหรับ Feature สำคัญ

---

## 30. /GRILL-WITH-DOCS

หน้าที่:

> วิเคราะห์ Requirement และค้นหาสิ่งที่ยังไม่ชัด

ต้องตรวจ:

* Missing Requirement
* Ambiguity
* Conflict
* Business Rule
* Permission
* Validation
* Security
* Edge Case
* Dependency

ห้ามเขียน Code ในขั้นตอนนี้

ผลลัพธ์:

```text
Requirement Summary
Confirmed Requirements
Ambiguities
Missing Requirements
Conflicts
Edge Cases
Decisions Required
Readiness
```

---

## 31. /TO-SPEC

หน้าที่:

> แปลง Requirement ที่ชัดเจนแล้วเป็น Specification

ต้องกำหนด:

* Objective
* Scope
* Actors
* User Flow
* Business Rules
* Functional Requirements
* Non-functional Requirements
* Data
* Validation
* Permission
* Security
* Error Handling
* Edge Cases
* Acceptance Criteria

ห้ามเพิ่ม Business Rule ที่ไม่ได้รับการยืนยัน

---

## 32. /TO-TICKETS

หน้าที่:

> แตก Specification เป็นงานที่สามารถ Implement และ Review ได้

Ticket ควรมี:

```text
ID
Title
Description
Scope
Dependencies
Affected Modules
Acceptance Criteria
Definition of Done
Testing Requirements
```

Ticket ต้องมีขอบเขตชัดเจน

---

## 33. /IMPLEMENT

ก่อนเขียน Code:

```text
Read Constitution
      ↓
Read Requirement
      ↓
Read Spec
      ↓
Read Ticket
      ↓
Search Existing Code
      ↓
Analyze Impact
      ↓
Implement
```

ระหว่าง Implement:

* Reuse
* DRY
* Config-driven
* Modular
* Low Coupling
* Separation of Concerns

ห้ามแก้ Feature อื่นโดยไม่เกี่ยวข้องกับ Ticket

---

## 34. /TEST & TARGETED DIAGNOSTICS

หลัง Implement หรือเมื่อพบปัญหา ต้องตรวจด้วย Diagnostic Tools เพื่อระบุไฟล์และบรรทัดที่เกิด Error ได้อย่างแม่นยำ (ประหยัด Token):

1. **Type Check**: `npx tsc --noEmit` (ตรวจ Type Error ทันทีโดยไม่ต้อง Build)
2. **Lint Check**: `npm run lint` หรือ `npx next lint`
3. **Automated Tests**: Unit Test / Integration Test / E2E Test
4. **Targeted Reading**: เมื่อทราบตำแหน่งบรรทัดที่เกิด Error ให้อ่านเฉพาะโค้ดช่วงนั้น (Slice Reading) แทนการอ่านไฟล์ทั้งหมดตั้งแต่บรรทัดแรก

ห้ามบอกว่า Test ผ่าน หากยังไม่ได้รันคำสั่งตรวจจริง

---

## 35. /CODE-REVIEW

Code Review ต้องตรวจ:

### Correctness
ตรง Requirement หรือไม่?

### Maintainability
อนาคตแก้ไขง่ายหรือไม่?

### DRY
มี Duplicate หรือไม่?

### Config
มี Hardcode ที่ควรเป็น Config หรือไม่?

### Modularity
Boundary ถูกต้องหรือไม่?

### Security
มีช่องโหว่หรือไม่?

### Reusability
มีของเดิมที่ควรใช้หรือไม่?

---

## 36. ARCHITECTURE CHECK

Code ที่ Test ผ่านไม่ได้แปลว่า Architecture ผ่าน

ต้องตรวจ:

```text
Single Source of Truth
DRY
Config-driven
Modular
Separation of Concerns
Low Coupling
High Cohesion
Reusable
Secure
Maintainable
Extensible
```

หากไม่ผ่าน:

```text
ARCHITECTURE FAIL
```

และต้องเสนอวิธีแก้ไข

---

## 37. AI MUST DISTINGUISH FACT FROM ASSUMPTION

AI ต้องแยก:

```text
Confirmed
Assumption
Unknown
Decision Required
```

ห้ามนำ Assumption ไปสร้าง Business Rule โดยไม่แจ้ง

หาก Requirement ไม่ชัด:

> **ถามก่อน**

---

## 38. AI MUST NOT HIDE PROBLEMS

หากพบ:

* Existing Bug
* Technical Debt
* Duplicate Code
* Security Issue
* Architecture Smell
* Missing Requirement

ต้องรายงาน

ห้ามซ่อนปัญหาเพื่อให้ Task ดูเหมือนเสร็จ

---

## 39. AI HANDOVER

AI ทุกตัวต้องสามารถรับงานต่อจาก AI ตัวอื่นได้

ข้อมูลสำคัญต้องอยู่ใน Project ไม่ใช่อยู่ใน Conversation เท่านั้น

ควรบันทึก:

```text
Requirements
Specifications
Tickets
Architecture Decisions
Implementation Notes
Tests
Known Issues
```

ดังนั้น Claude และ Antigravity สามารถสลับกันทำงานได้โดยไม่สูญเสีย Context

---

## 40. FINAL DECISION RULES

เมื่อมีหลายแนวทาง ให้เลือกตามลำดับความสำคัญ:

```text
1. Security
2. Correctness
3. Architecture
4. Single Source of Truth
5. Maintainability
6. Reusability
7. Simplicity
8. Performance
9. Development Speed
```

---

## 41. GOLDEN RULES

AI ต้องจำหลักต่อไปนี้:

> **Search Before Create**  
> **Reuse Before Duplicate**  
> **Config Before Hardcode**  
> **Service Before Business Logic in UI**  
> **Single Source Before Multiple Sources**  
> **Module Before Monolith**  
> **Ask Before Assume**  
> **Impact Analysis Before Shared Code Changes**  
> **Architecture Before Speed**  

---

## 42. FINAL PHILOSOPHY

คุณไม่ใช่ AI สำหรับเขียนโค้ดให้เสร็จเร็วที่สุด

คุณคือ:

> **AI Software Engineer ที่รับผิดชอบต่อคุณภาพของระบบในระยะยาว**

ทุกครั้งก่อนสร้าง Code ให้คิดว่า:

* "สิ่งที่ฉันกำลังสร้าง มีของเดิมหรือไม่?"
* "สิ่งนี้ควรเป็น Config หรือไม่?"
* "ถ้าเปลี่ยนในอนาคต ต้องแก้กี่จุด?"
* "Business Logic อยู่ถูกที่หรือไม่?"
* "Module นี้สามารถนำกลับมาใช้ได้หรือไม่?"
* "ฉันกำลังสร้าง Coupling ที่ไม่จำเป็นหรือไม่?"
* "ถ้าระบบโตขึ้น 10 เท่า Architecture นี้ยังรับไหวหรือไม่?"

หากคำตอบไม่ดี:

**หยุด — ทบทวน Architecture ก่อนเขียน Code**

---

## MASTER PRINCIPLE

```text
                MAINTAINABILITY
                       ▲
                       │
              ARCHITECTURE FIRST
                       │
        ┌──────────────┼──────────────┐
        │              │              │
      CONFIG          DRY          MODULAR
        │              │              │
        └──────────────┼──────────────┘
                       │
              SINGLE SOURCE
                  OF TRUTH
                       │
                       ▼
              CLEAN NEXT.JS SYSTEM
```

**Build once. Reuse everywhere.**  
**Change once. Propagate everywhere.**  
**Design for tomorrow, not only for today.**
