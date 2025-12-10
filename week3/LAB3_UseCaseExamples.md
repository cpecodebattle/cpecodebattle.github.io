## UC-XX: <ชื่อ Use Case>

**Primary Actor:** <Student / Instructor / TA>  
**Goal:** <เป้าหมายหลักที่ Actor ต้องการทำให้สำเร็จ>

### Preconditions
- เงื่อนไขที่ต้องเป็นจริงก่อนเริ่ม Use Case

### Postconditions
- เงื่อนไขที่ต้องเป็นจริงหลัง Use Case สำเร็จ

### Main Flow (Happy Path)
1. ...
2. ...
3. ...
4. ...

### Alternative Flows / Exceptions
- **AF-1 – <ชื่อกรณีย่อย>**
  1. ...
  2. ...
- **AF-2 – <ชื่อ error หรือกรณีพิเศษ>**
  1. ...
  2. ...

---

## UC-01: View Lab List

**Primary Actor:** Student  
**Goal:** ดูรายการ LAB ทั้งหมดของวิชา ENGCE301

### Preconditions
- นักศึกษาเข้าหน้า Home ของ Portal ได้
- มี LAB อย่างน้อย 1 รายการในระบบ

### Postconditions
- นักศึกษาเห็นรายการ LAB ทุกตัว พร้อมข้อมูลสำคัญ

### Main Flow (Happy Path)
1. นักศึกษาเปิดหน้า Home หรือหน้า Lab List
2. ระบบโหลดรายการ LAB ของวิชา ENGCE301
3. ระบบแสดง list/card ของ LAB แต่ละตัว
4. แต่ละ LAB แสดงชื่อ, คำอธิบายสั้น ๆ, deadline, สถานะ (Open/Closed)
5. นักศึกษาตรวจดู LAB ที่ต้องทำ และเลือก LAB ที่สนใจ

### Alternative Flows / Exceptions
- **AF-1 – ไม่มี LAB ในระบบ**
  1. ที่ขั้นตอน 2 ระบบไม่พบ LAB
  2. ระบบแสดงข้อความ “ยังไม่มี LAB สำหรับรายวิชานี้”
  3. Use Case จบลง

---

## UC-02: View Lab Details

**Primary Actor:** Student  
**Goal:** ดูรายละเอียดทั้งหมดของ LAB แต่ละตัวก่อนเริ่มทำ

### Preconditions
- นักศึกษาเข้าถึงหน้ารายการ LAB (Lab List) ได้
- LAB ที่เลือกต้องถูกเผยแพร่แล้วและมีรายละเอียดพร้อมแสดง

### Postconditions
- นักศึกษาเห็นรายละเอียดโจทย์ LAB ครบถ้วน รวมถึงไฟล์แนบและ deadline

### Main Flow (Happy Path)
1. นักศึกษาคลิกที่ชื่อ LAB หรือปุ่ม "Details" จากหน้า Lab List (UC-01)
2. ระบบดึงข้อมูลรายละเอียดทั้งหมดของ LAB นั้นจากฐานข้อมูล
3. ระบบแสดงหน้า Lab Details ซึ่งประกอบด้วย: ชื่อ LAB, จุดประสงค์, รายละเอียดโจทย์, deadline, ไฟล์แนบ
4. ระบบแสดงสถานะการส่งงานของนักศึกษาคนนั้น (Not Submitted / Submitted / Graded)
5. นักศึกษาดูรายละเอียดและจบ Use Case

### Alternative Flows / Exceptions
- **AF-1 – Lab ไม่พร้อมใช้งาน**
  1. นักศึกษาพยายามเข้าถึงรายละเอียด LAB ที่ผู้สอนยังไม่ได้เผยแพร่
  2. ระบบแสดงข้อความปฏิเสธการเข้าถึง: “รายละเอียด LAB นี้ยังไม่พร้อมใช้งาน”
  3. Use Case จบลง

---

## UC-03: Submit Lab

**Primary Actor:** Student  
**Goal:** ส่งไฟล์งาน LAB ผ่านระบบ

### Preconditions
- นักศึกษาเข้าถึงหน้ารายละเอียด LAB นั้นได้
- LAB ยังเปิดรับส่ง (ไม่ว่าจะเป็นตรงเวลาหรือ Late Submission ตาม Policy)

### Postconditions
- ระบบบันทึกไฟล์และเวลาส่งงานของนักศึกษา
- สถานะ LAB ของนักศึกษาคนนี้อัปเดต (Submitted หรือ Late)

### Main Flow (ส่งตรงเวลา)
1. นักศึกษาเปิดหน้า Lab Details (UC-02)
2. ระบบแสดงส่วน “Submit Your Lab”
3. นักศึกษากดเลือกไฟล์ (.pdf/.docx/.zip)
4. ระบบตรวจสอบชนิดและขนาดไฟล์เบื้องต้น
5. นักศึกษากดปุ่ม “Submit”
6. ระบบบันทึกไฟล์และเวลาส่ง (timestamp)
7. ระบบตรวจสอบว่า **ไม่เกิน deadline**
8. ระบบอัปเดตสถานะเป็น **“Submitted”**
9. ระบบแสดงข้อความ “ส่งงานเรียบร้อยแล้ว”

### Alternative Flows / Exceptions
- **AF-1 – File Type ไม่ถูกต้อง**
  1. เกิดจากขั้นตอน 4 เมื่อไฟล์ไม่ใช่ชนิดที่รองรับ
  2. ระบบแจ้งเตือน “ชนิดไฟล์ไม่รองรับ”
  3. กลับไปที่ขั้นตอน 3 ให้เลือกไฟล์ใหม่

- **AF-2 – ส่งหลัง deadline (Late)**
  1. ที่ขั้นตอน 7 ระบบพบว่าเวลาส่ง **เกิน deadline**
  2. ถ้า policy อนุญาต Late:
     - ระบบบันทึกไฟล์
     - ตั้งสถานะเป็น **“Late”**
     - ระบบแสดงข้อความเตือน **"ส่งงานล่าช้า"**
  3. นักศึกษาเห็นสถานะ Late ในหน้า My Labs

- **AF-3 – ไม่อนุญาตส่งหลัง deadline**
  1. ที่ขั้นตอน 7 หาก policy ไม่รับหลัง deadline
  2. ระบบไม่บันทึก submission
  3. ระบบแสดงข้อความ **“หมดเขตส่งงานแล้ว”**

---

## UC-04: View My Lab Status

**Primary Actor:** Student  
**Goal:** ดูภาพรวมสถานะ LAB ทั้งหมดของตัวเอง

### Preconditions
- นักศึกษาเข้าหน้า My Labs ได้
- ระบบมีข้อมูล LAB ของวิชานี้สำหรับนักศึกษาคนนี้

### Postconditions
- นักศึกษาเห็นสถานะ (Not Submitted / Submitted / Graded / Late) ของทุก LAB

### Main Flow (Happy Path)
1. นักศึกษาเปิดหน้า “My Labs”
2. ระบบดึงข้อมูล LAB และสถานะการส่งงานของนักศึกษาแต่ละ LAB
3. ระบบแสดงตารางหรือ card ของ LAB ทั้งหมด
4. แต่ละแถว/การ์ดแสดงชื่อ LAB, สถานะ, คะแนน (ถ้ามี) และ Feedback สั้น ๆ (ถ้าตรวจแล้ว)
5. นักศึกษาดูว่า LAB ไหนเสร็จแล้ว และ LAB ไหนยังต้องทำ

### Alternative Flows / Exceptions
- **AF-1 – มี LAB ที่ Late / Graded**
  1. ระบบพบ LAB บางตัวที่ Late (สถานะ Late) หรือตรวจแล้ว (สถานะ Graded)
  2. แสดงสถานะ Late/Graded ด้วยสี/ป้ายชัดเจน **(ต้องใช้ CSS Class ที่แตกต่าง)**
  3. แสดงคะแนนและ Feedback ในคอลัมน์ Score

- **AF-2 – ยังไม่เคยส่งงาน**
  1. ระบบพบว่า LAB ทั้งหมดเป็นสถานะ Not Submitted
  2. ระบบแสดงข้อความเสริม เช่น “คุณยังไม่ได้ส่ง LAB ใดเลย”

---

## UC-06: Grade Submission

**Primary Actor:** Instructor / TA  
**Goal:** บันทึกคะแนนและ Feedback สำหรับงาน LAB ที่นักศึกษาส่งมา

### Preconditions
- Instructor/TA ต้องเข้าสู่ระบบ (Authenticated) 
- Student ต้องส่งงาน LAB มาแล้ว (สถานะ Submitted หรือ Late)
- Instructor/TA เข้าถึงหน้า View Submissions ของ LAB นั้นได้

### Postconditions
- ระบบบันทึกคะแนนและ Feedback เรียบร้อยแล้ว
- สถานะ LAB ของนักศึกษาคนนั้นเปลี่ยนเป็น **“Graded”**
- คะแนนและ Feedback พร้อมแสดงในหน้า My Labs ของ Student (UC-04)

### Main Flow (Happy Path)
1. Instructor/TA เปิดหน้า View Submissions (UC-06 หรือเทียบเท่า)
2. Instructor/TA เลือก Submission ของนักศึกษาที่ต้องการให้คะแนน
3. ระบบแสดงหน้าจอสำหรับกรอกคะแนน (เช่น 0-100) และช่องกรอกข้อความ Feedback
4. Instructor/TA กรอกคะแนนและข้อความ Feedback
5. Instructor/TA กดปุ่ม **“Save Score”**
6. ระบบบันทึกข้อมูลและอัปเดตสถานะเป็น **“Graded”**
7. ระบบแสดงข้อความยืนยัน “บันทึกคะแนนเรียบร้อยแล้ว”

### Alternative Flows / Exceptions
- **AF-1 – คะแนนที่กรอกไม่อยู่ในช่วง**
  1. ที่ขั้นตอน 4, Instructor/TA กรอกคะแนนที่เกินขอบเขตสูงสุด (เช่น > 100)
  2. ระบบแจ้งเตือน “คะแนนที่กรอกต้องอยู่ในช่วงที่กำหนด” 
  3. กลับไปที่ขั้นตอน 4 เพื่อแก้ไขคะแนน