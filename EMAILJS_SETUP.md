# วิธีตั้งค่า EmailJS สำหรับส่งอีเมลแจ้งเตือน

## ขั้นตอนการตั้งค่า

### 1. สมัครบัญชี EmailJS
1. ไปที่เว็บไซต์ [https://www.emailjs.com/](https://www.emailjs.com/)
2. สมัครบัญชีฟรี (Free tier ส่งได้ 200 อีเมล/เดือน)
3. ลงชื่อเข้าใช้

### 2. เพิ่ม Email Service
1. ไปที่เมนู **Email Services**
2. คลิก **Add New Service**
3. เลือกผู้ให้บริการอีเมลที่คุณใช้ (Gmail, Outlook, Yahoo, หรืออื่นๆ)
4. ทำตามขั้นตอนเชื่อมต่อบัญชีอีเมลของคุณ
5. จำ **Service ID** ที่ได้ (เช่น: `service_xxxxx`)

### 3. สร้าง Email Template
1. ไปที่เมนู **Email Templates**
2. คลิก **Create New Template**
3. ตั้งชื่อ Template เช่น "Calendar Notification"
4. ตั้งค่าดังนี้:
   - **To Email**: `{{to_email}}`
   - **Subject**: `แจ้งเตือน: {{event_title}}`
   - **Content** (HTML หรือ Text):
   ```
   สวัสดีครับ/ค่ะ

   นี่คือการแจ้งเตือนจากปฏิทิน M.5

   ชื่องาน: {{event_title}}
   วันที่/เวลา: {{event_datetime}}
   รายละเอียด: {{event_note}}

   ขอบคุณที่ใช้บริการ
   ```
5. คลิก **Save**
6. จำ **Template ID** ที่ได้ (เช่น: `template_xxxxx`)

### 4. รับ Public Key
1. ไปที่เมนู **Account** > **General**
2. ค้นหา **Public Key** (เช่น: `xxxxxxxxxxxxx`)
3. คัดลอก Public Key นี้

### 5. แก้ไขโค้ดใน index.html
เปิดไฟล์ `index.html` และค้นหาส่วนนี้:

```javascript
const EMAILJS_CONFIG = {
    serviceID: 'YOUR_SERVICE_ID',      // แก้ไขเป็น Service ID ของคุณ
    templateID: 'YOUR_TEMPLATE_ID',   // แก้ไขเป็น Template ID ของคุณ
    publicKey: 'YOUR_PUBLIC_KEY'       // แก้ไขเป็น Public Key ของคุณ
};
```

แก้ไขค่าเป็น:
- `YOUR_SERVICE_ID` → Service ID ที่ได้จากขั้นตอนที่ 2
- `YOUR_TEMPLATE_ID` → Template ID ที่ได้จากขั้นตอนที่ 3
- `YOUR_PUBLIC_KEY` → Public Key ที่ได้จากขั้นตอนที่ 4

ตัวอย่าง:
```javascript
const EMAILJS_CONFIG = {
    serviceID: 'service_abc123',
    templateID: 'template_xyz789',
    publicKey: 'abcdefghijklmnop'
};
```

## วิธีใช้งาน

1. เปิดไฟล์ `index.html` ในเบราว์เซอร์
2. กรอกอีเมลในฟอร์ม (กรอกครั้งเดียว ระบบจะจำไว้)
3. เพิ่มงานและตั้งเวลา
4. เมื่อถึงเวลาที่ตั้งไว้ ระบบจะส่งอีเมลแจ้งเตือนไปยังอีเมลที่กรอกไว้

## หมายเหตุ

- **Free tier**: ส่งได้ 200 อีเมล/เดือน
- **ความปลอดภัย**: Public Key ปลอดภัยต่อการเปิดเผย (สามารถใช้ใน frontend ได้)
- **การทดสอบ**: ทดสอบส่งอีเมลก่อนใช้งานจริง
- **ข้อจำกัด**: ต้องเปิดเบราว์เซอร์ไว้เพื่อให้ระบบส่งอีเมลได้

## ปัญหาที่พบบ่อย

### อีเมลไม่ถูกส่ง
- ตรวจสอบว่าแก้ไขค่าใน `EMAILJS_CONFIG` ครบถ้วนแล้ว
- ตรวจสอบ Console ในเบราว์เซอร์ (F12) เพื่อดู error
- ตรวจสอบว่า Service และ Template ตั้งค่าถูกต้อง

### เกินโควต้า
- Free tier ส่งได้ 200 อีเมล/เดือน
- ถ้าเกินต้องอัปเกรดเป็น Paid plan

