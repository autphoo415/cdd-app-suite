# CDD APP SUITE – Supabase migration starter

ชุดนี้ย้ายฐานข้อมูลของ Launcher จาก Google Sheets/Apps Script ไป Supabase โดยคงหน้าตาและความสามารถเดิม ได้แก่ แสดงรายการแอป, ค้นหา, กรองหมวดหมู่, เรียงลำดับ, เพิ่ม/แก้ไข/ลบ, Export และ Import JSON

## ไฟล์ในชุด
- `index.html` – หน้าเว็บ CDD APP SUITE ที่ปรับให้ใช้ Supabase
- `supabase-config.js` – ใส่ Project URL และ anon/public key
- `supabase_schema.sql` – สร้างตาราง, RLS, ฟังก์ชันนำเข้า และข้อมูลเริ่มต้น

## ขั้นตอนติดตั้ง
1. สร้างโปรเจกต์ที่ https://supabase.com/ (Free).
2. ใน Supabase ไปที่ SQL Editor > New query เปิดไฟล์ `supabase_schema.sql` แล้ว Run.
3. ไปที่ Project Settings > API แล้วคัดลอก Project URL และ anon/public key. ห้ามใช้ `service_role` key ในหน้าเว็บ.
4. เปิด `supabase-config.js` แล้วแทนค่าตัวอย่างด้วย URL และ anon/public key จริง.
5. สร้างผู้ดูแลใน Supabase: Authentication > Users > Add user (กำหนดอีเมลและรหัสผ่านเอง). ปิดการสมัครสมาชิกสาธารณะ (Allow new users to sign up) ใน Authentication settings.
6. นำ `index.html` และ `supabase-config.js` ไปวางไว้ที่ root ของ GitHub repository (ตั้งชื่อ `index.html`). Commit แล้วให้ Vercel deploy ใหม่.
7. เปิดเว็บ Vercel กด ADMIN LOGIN แล้วเข้าสู่ระบบด้วยบัญชีที่สร้างในขั้นตอน 5. บุคคลทั่วไปอ่านรายการแอปได้ แต่เพิ่ม/แก้ไข/ลบ/นำเข้าต้องเข้าสู่ระบบ.

## ข้อควรระวัง
- อย่าเผยแพร่ `service_role` key ใน GitHub หรือไฟล์หน้าเว็บ. ใช้เฉพาะ anon/public key คู่กับ RLS ที่กำหนดไว้.
- SQL นี้อนุญาตให้ผู้ใช้ที่เข้าสู่ระบบแล้วแก้ไขข้อมูลได้ทั้งหมด ดังนั้นควรสร้างบัญชีผู้ดูแลเฉพาะผู้ได้รับอนุญาต และปิด public sign-up.
- ระบบ Launcher เก็บเฉพาะ metadata ของรายการแอปและ settings/log schema ที่เตรียมไว้. ฐานข้อมูลภายในแอปย่อย เช่น ระบบลูกหนี้/กองทุน/เอกสาร ไม่ได้ถูกย้ายโดยอัตโนมัติ ต้องนำ source code และโครงสร้างฐานข้อมูลของแต่ละแอปมาปรับแยกต่างหาก.
- ก่อนเปลี่ยนเว็บจริง ให้ Export รายการเดิมเป็น JSON เก็บไว้ก่อน. Google Sheets เดิมยังไม่ถูกลบ.

## ข้อจำกัดของเวอร์ชันนี้
ตาราง `app_settings` และ `audit_logs` ถูกเตรียมโครงสร้างไว้สำหรับการตั้งค่าและประวัติการใช้งานในระยะต่อไป; UI เดิมของ Launcher ยังไม่ได้มีหน้าจัดการผู้ใช้หรือหน้าประวัติการเปลี่ยนแปลง.
