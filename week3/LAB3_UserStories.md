# User Stories – EventHub: แพลตฟอร์มจัดการและลงทะเบียนกิจกรรมภายในมหาวิทยาลัย

> **อ้างอิงจาก SRS.pdf**
> - **วัตถุประสงค์:** ใช้สำหรับสร้าง Use Case Diagram / Use Case Scenario และเป็นฐานในการออกแบบหน้า HTML/CSS (Week 3 LAB)
> - **เป้าหมาย:** ระบบนี้ถูกออกแบบมาเพื่อแก้ไข Pain Point P1, P2, P3, P4, และ P5

---

## กลุ่ม Student (นักศึกษา)

### US-01 – Browse Approved Event List (P1: ขาดศูนย์กลางข้อมูล)
**As a** student  
**I want** to view a central list of all approved activities/events  
**So that** I don't miss any important events and can easily find activities to register for

**Acceptance Criteria (Checklist)**
- [ ] เมื่อเปิดหน้าหลัก จะเห็นรายการกิจกรรมที่ถูกอนุมัติแล้วทั้งหมด  
- [ ] แต่ละกิจกรรมแสดง ชื่อกิจกรรม, คำอธิบายสั้น ๆ, วันที่/เวลาจัด, และสถานะการรับสมัคร (เปิด/ปิด)  
- [ ] สามารถกรอง/ค้นหากิจกรรมตามหมวดหมู่ได้

*(ใน LAB HTML, ส่วนนี้ map → Section “Upcoming Events” ใน index.html)*

---

### US-02 – View Full Event Details
**As a** student  
**I want** to view the full details of a specific event  
**So that** I understand the objective, criteria, and location before deciding to register

**Acceptance Criteria (ตัวอย่าง Given–When–Then)**
- **Given** ฉันอยู่ในหน้า Event List  
- **When** ฉันคลิกกิจกรรมที่สนใจ  
- **Then** ระบบแสดงหน้า Event Details ที่มี  
    - ชื่อ, จุดประสงค์, รายละเอียดเต็ม, แผนที่/สถานที่, กำหนดการ, และโควตาที่เหลือ  

---

### US-03 – Register for an Event (UC-03)
**As a** student  
**I want** to submit my registration form online  
**So that** I secure my seat and receive a verifiable digital ticket/QR code (P4)

**Acceptance Criteria (ย่อ)**
- มีปุ่ม/ส่วนติดต่อให้กรอกข้อมูลและกดยืนยันการลงทะเบียน  
- เมื่อลงทะเบียนสำเร็จ ระบบยืนยันการลงทะเบียน (Registered) และสร้าง **QR Code** ให้ทันที  
- หากโควตาเต็ม ระบบต้องแจ้งเตือนว่า “เต็ม” และไม่ให้ลงทะเบียนต่อ

*(ใน LAB HTML, ส่วนนี้ใช้สำหรับทำ Mock UI ของฟอร์มลงทะเบียน)*

---

### US-04 – View My Registration Status & QR Code (P4, P5)
**As a** student  
**I want** to see the status of all events I registered for, and access my QR Code
**So that** I know which events I need to attend and have the necessary proof of registration ready for check-in

**Acceptance Criteria**
- หน้า “My Events” แสดงรายการกิจกรรมที่ลงทะเบียนทั้งหมดของฉัน  
- แต่ละกิจกรรมมีสถานะอย่างน้อย:  
    - “Registered”, “Attended”, “Rejected”, “Pending Approval”  
- ถ้าสถานะเป็น “Registered” ต้องมีปุ่ม/ลิงก์เพื่อแสดง **QR Code** สำหรับ Check-in

*(ใน LAB HTML, ใช้ตารางแสดงสถานะ → my-events.html)*

---

## กลุ่ม Organizer / Admin (ผู้จัดกิจกรรม / ผู้ดูแลระบบ)

### US-05 – Create New Event Request (P3: ขั้นตอน Manual)
**As an** organizer  
**I want** to create a new activity/event and submit it for approval  
**So that** the event details are centralized and the manual approval process is replaced with a digital workflow

**Acceptance Criteria (ย่อ)**
- ผู้จัดสามารถกรอก: ชื่อกิจกรรม, รายละเอียด, วันที่/เวลา, สถานที่, โควตานักศึกษา  
- เมื่อส่ง ระบบเปลี่ยนสถานะกิจกรรมเป็น **“Pending Approval”** (รอการอนุมัติ)

---

### US-06 – Approve/Reject Event (UC-08)
**As an** Admin/Faculty Advisor  
**I want** to review submitted event requests and approve or reject them  
**So that** all events displayed to students are official and verified

**Acceptance Criteria**
- ผู้ดูแลระบบเข้าดูรายการกิจกรรมที่ “Pending Approval”  
- มีปุ่ม/ฟังก์ชันให้ “Approve” (กิจกรรมแสดงให้นักศึกษาเห็น) หรือ “Reject” (กิจกรรมถูกซ่อน)

---

### US-07 – Check-in Attendee via QR Code (UC-07 / P2: Check-in ล่าช้า)
**As an** organizer  
**I want** to use a scanner/app to scan the student’s QR code  
**So that** attendance is recorded instantly, accurately, and minimizes the check-in queue

**Acceptance Criteria**
- เมื่อสแกน QR Code สำเร็จ ระบบจะแสดงชื่อนักศึกษา และเปลี่ยนสถานะการเข้าร่วมเป็น **“Attended”** ทันที  
- หาก QR Code ซ้ำ/หมดอายุ ระบบแจ้งเตือนว่า “Invalid Code”

---

### US-08 – View/Export Attendance Report (P5: หลักฐานไม่ชัดเจน)
**As an** organizer  
**I want** to view a summary and detailed list of students who attended the event  
**So that** I can easily generate an official attendance report for evidence and future planning

**Acceptance Criteria**
- ในหน้า Event Management แสดงสรุปจำนวนผู้ลงทะเบียน (Registered) และผู้เข้าร่วมจริง (Attended)  
- สามารถดาวน์โหลดไฟล์ (เช่น CSV) ที่มีรายชื่อและเวลา Check-in ได้

---

## 3) วิธีใช้ชุด SRS + User Stories นี้ใน LAB

1.  **ทำ Use Case Diagram**
    * ระบุ Actors: **Student**, **Organizer**, **Admin/Faculty** และ Use Cases ที่สอดคล้องกับ US-01 ถึง US-08
    * วาด Diagram (Student, Organizer/Admin + System Boundary) 

2.  **เขียน Use Case Scenario** (อย่างน้อย 2–3 ตัว)
    * แนะนำ: **US-03 Register for an Event**, **US-04 View My Registration Status & QR Code**, และ **US-07 Check-in Attendee via QR Code**

3.  **เชื่อมกับ LAB HTML/CSS (Week 3)**
    * **US-01 + US-02:** Section “Upcoming Events” บน `index.html`
    * **US-03:** ปุ่ม “ลงทะเบียน” และหน้ายืนยันการลงทะเบียน
    * **US-04:** หน้า `my-events.html` แสดงตารางสถานะการลงทะเบียนและช่อง **QR Code**
    * ใช้ NFR (Usability / Layout) เป็น guideline ในการออกแบบ