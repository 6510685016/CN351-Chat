# Chat

นี่คือ Real-time chat web application ที่มีไว้สำหรับให้ user ที่ admin ได้สร้างเอาไว้สามารถส่งและรับข้อความหากันแบบ Real-time แต่ application นี้มีช่องโหว่บางอย่างที่จะอธิบายไง้ด้านล่าง
** โปรเจคแอปเพื่อการศึกษา Web security เท่านั้น

---

## Tech Stack
- React.js (Frontend)
- Node.js + Express + WebSocket (Backend)
- MongoDB (Database)
- Docker + Docker Compose

---

## Starting App

### 1. Clone and Setup
```bash
git clone https://github.com/6510685016/CN351-Chat.git chat
cd chat
docker compose build
```

### 2. Start Application
```bash
git clone https://github.com/6510685016/CN351-Chat.git chat
cd chat
docker compose up -d
```

### 3. สามารถใช้งานได้ผ่าน
- Web App: http://localhost:3000
- Server: http://localhost:5000

### 4. Stop Application
```bash
docker compose down
```

---
## user and admin
### admin 
- username : admin
- password : admin

### user1 
- username : user1
- password : password1

### user2
- username : user2
- password : password2

---
### ช่องโหว่ 1: **ปุ่มสำหรับ Admin แค่ซ่อนไว้เฉย ๆ**

ปุ่ม Create user อยู่ในหน้า Chat แต่แค่ `display: none` ทำให้เพียงแก้ไข html ก็จะทำให้ user ทั่วไปสามารถเข้าถึงฟังก์ชันนี้ได้

**วิธีทดสอบ**
1. เข้าสู่ระบบและไปที่หน้า Chat
2. กด Inspect Element และเปิด DevTools
3. คลิกขวา element → เลือก `Edit as HTML`
4. เอา CSS `display: none` ออก 
5. คลิกปุ่มที่ปรากฎ

---

## ช่องโหว่ 2: **เก็บ Password แบบ Plaintext ใน MongoDB**

**วิธีทดสอบ**
1. เข้าไปดูข้อมูลใน MongoDB 
2. ดู collection `users`
3. จะเห็นว่า password ถูกเก็บเป็น plaintext `"password": "123456"`

---

## ช่องโหว่ 3: **Hardcoded Session ID หลัง Login**

เมื่อ Login สำเร็จ server ส่ง `sessionId: "hardcoded-session-id-1234"` ให้สำหรับทุกคนที่ login สำเร็จ

**วิธีทดสอบ**
1. Login เป็น user ใดก็ได้
2. ดู Response Body (Network tab → login → Response)
3. เห็น sessionId เป็นค่าเดียวกันทุก user

เมื่อรู้ Session ID ก็จะสามารถเข้าใช้งานได้แม้ไม่ผ่านการ login

---

## ช่องโหว่ 4: **เปิด Public Directory Listing**

Server เปิดให้เข้าถึงโฟลเดอร์ `public/` ได้หมดโดยไม่มีการป้องกัน

**วิธีทดสอบ**
1. เปิดเว็บเบราว์เซอร์
2. ลองเข้าลิงก์
```
http://localhost:5000/secret.html
```
3. ไฟล์ที่อยู่ใน public สามารถถูกเข้าถึงได้ทั้งหมดเพียงแค่คาดเดาชื่อไฟล์ด้านใน

## ช่องโหว่ 5: **แก้ไข role ใน LocalStorage ได้**

**วิธีทดสอบ**
1. Login เข้าระบบตามปกติจะได้ role เป็น `user` ใน LocalStorage
2. เปิด DevTools, Inspect และค้นหา LocalStorage 
3. แก้ไข role เป็น `admin` เพื่อเข้าถึงฟีเจอร์ของ admin

---