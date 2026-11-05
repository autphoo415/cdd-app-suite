# CDD APP SUITE

เว็บแอปแบบ Static HTML สำหรับเผยแพร่ผ่าน GitHub และ Vercel

## โครงสร้างไฟล์

- `index.html` — หน้าเว็บหลัก CDD APP SUITE (อิงจาก v2.7)
- `vercel.json` — ตั้งค่า Vercel สำหรับ Static Site

## วิธี Deploy ผ่าน GitHub + Vercel

1. แตกไฟล์ ZIP นี้บนคอมพิวเตอร์
2. เข้า GitHub แล้วสร้าง Repository ใหม่ เช่น `cdd-app-suite`
3. อัปโหลด `index.html`, `vercel.json` และ `README.md` ไปไว้ที่ Root ของ Repository (ไม่ต้องใส่ไว้ในโฟลเดอร์ย่อย)
4. เข้า Vercel แล้วเลือก **Add New → Project**
5. เลือก **Import Git Repository** และเชื่อมต่อ GitHub หากยังไม่ได้เชื่อม
6. เลือก Repository `cdd-app-suite`
7. ในหน้า Configure Project:
   - Framework Preset: **Other**
   - Root Directory: `./`
   - Build Command: เว้นว่าง
   - Output Directory: เว้นว่าง หรือใช้ `.` หากระบบบังคับให้กรอก
   - Install Command: เว้นว่าง
8. กด **Deploy** แล้วเปิด URL ที่ Vercel ให้มา

## การอัปเดตเว็บไซต์

แก้ไข `index.html` ใน GitHub แล้ว Commit changes — Vercel จะ Deploy เวอร์ชันใหม่ให้อัตโนมัติ

## หมายเหตุเรื่องข้อมูลและการเชื่อมต่อ

- Vercel ทำหน้าที่ Hosting หน้าเว็บเท่านั้น
- รายการแอปและข้อมูล Cloud Sync ยังคงอ่าน/เขียนผ่าน Google Apps Script และ Google Sheets ตามการตั้งค่าในหน้าเว็บ ไม่ได้ถูกย้ายไปเก็บบน Vercel
- URL ของ Google Apps Script ที่ฝังอยู่ใน `index.html` เป็น URL ฝั่ง Client ผู้ที่เปิดดูซอร์สหน้าเว็บสามารถเห็นได้ จึงไม่ควรใช้ endpoint นี้เก็บข้อมูลลับหรือข้อมูลส่วนบุคคลอ่อนไหว
- หากเปลี่ยน Google Apps Script deployment URL ให้แก้ค่า `DEFAULT_GOOGLE_SCRIPT_URL` ใน `index.html` แล้ว Commit ใหม่
- ควรทดสอบเพิ่ม/แก้ไขรายการและกดรีเฟรชหน้าเว็บหลัง Deploy เพื่อยืนยันการ Sync กับ Google Sheets
