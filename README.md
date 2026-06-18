
วนิจชรากร เลื่อมใส

# 1LIFE System - AI CXR Screening

โปรเจกต์นี้เป็นหน้าเว็บ static สำหรับจำลองระบบ `1LIFE System` ตามภาพตัวอย่าง ประกอบด้วย 3 หน้าหลัก คือหน้าเข้าสู่ระบบ, หน้ารายการ X-ray และหน้า Dashboard โดยทำงานผ่าน HTML, CSS และ JavaScript ในไฟล์เดียว ไม่ต้องติดตั้ง dependency เพิ่ม

## การอัพเดทล่าสุด

- **ตาราง X-ray — คอลัมน์วันที่**: เพิ่มความกว้างคอลัมน์ "วันที่ X-ray" เป็น 210px เพื่อแสดงข้อความ `04/03/2567 10.00 น.` ได้ครบโดยไม่ถูกตัด
- **ตาราง X-ray — ปุ่มจัดการ**: รีดีไซน์ให้ตรงตาม Figma — ปุ่มไอคอนตา (28×28px, ขอบมน 8px, พื้นขาว, เงา) + ลิงก์ "รายละเอียด" สีน้ำเงิน underline แยกจากกัน
- **Dashboard — header**: เปลี่ยนไอคอนเป็นนาฬิกา SVG และข้อความ "ข้อมูลอัพเดท" พร้อมวันที่
- **Dashboard — tabs**: เพิ่ม border-bottom และสีแท็บ active เป็น `#1f43a5`
- **Dashboard — Donut chart**: เปลี่ยนจาก CSS conic-gradient เป็น SVG arc path พร้อม hover tooltip (เหมือน bar chart) และ floating label 80%/20%
- **Dashboard — Layout**: ใช้ absolute positioning สำหรับ sidebar/workspace พร้อม `overflow: visible` เพื่อรองรับ vertical scroll
- **ไอคอน icon-normal.svg**: รีดีไซน์เป็นกล่องพยาบาลลายแถบสีเขียวให้ตรงกับ icon-urgent.svg

## ไฟล์ในโปรเจกต์

```text
test_inet/
├── assets/
│   ├── logo.png              # โลโก้ 1LIFE
│   ├── login-panel.png       # ภาพประกอบหน้า Login
│   ├── icon-brain.png        # ไอคอนสมอง
│   ├── icon-waiting.png      # ไอคอนเอกสารรอยืนยันผล
│   ├── icon-confirmed.png    # ไอคอนเวชระเบียน
│   ├── icon-monthly-cases.png # ไอคอนจำนวนเคสประจำเดือนใน Dashboard
│   ├── icon-normal.svg       # ไอคอนเคสปกติ (กล่องพยาบาลลายแถบเขียว)
│   ├── icon-urgent.svg       # ไอคอนเคสเร่งด่วน
│   ├── avatar-staff-reference.png # รูปเจ้าหน้าที่จากภาพดีไซน์อ้างอิง
│   └── *.svg                 # โลโก้และไอคอน UI แบบคมชัด
├── index.html   # โครงสร้างหน้าเว็บและ JavaScript สำหรับ interaction
├── styles.css   # สไตล์ทั้งหมดของทั้ง 3 หน้า
└── README.md    # คู่มือการรันและรายละเอียดโปรเจกต์
```

## วิธีรันบน localhost

เปิด Terminal / PowerShell ในโฟลเดอร์โปรเจกต์ แล้วรัน:

```powershell
python -m http.server 8000
```

จากนั้นเปิด Browser ไปที่:

```text
http://localhost:8000
```

หรือถ้า `localhost` ไม่ขึ้น ให้ลอง:

```text
http://127.0.0.1:8000
```

ถ้าเครื่องใช้ Python launcher แทนคำสั่ง `python` สามารถรันแบบนี้ได้:

```powershell
py -m http.server 8000
```

## วิธีเปิดแบบไม่ใช้ server

สามารถดับเบิลคลิกไฟล์ `index.html` เพื่อเปิดใน Browser ได้เช่นกัน แต่แนะนำให้รันผ่าน localhost เพราะใกล้เคียงการใช้งานเว็บจริงกว่า

## หน้าที่มีในระบบ

### 1. หน้า Login

- แสดงการ์ดเข้าสู่ระบบตามภาพตัวอย่าง
- ปุ่ม `ลงชื่อเข้าใช้งาน` ไปยังหน้ารายการ X-ray
- ปุ่ม `ลงทะเบียน` เปิด popup จำลองการลงทะเบียน
- ปุ่ม `เข้าสู่ระบบด้วย ONE ID` ไปยังหน้ารายการ X-ray

### 2. หน้ารายการ X-ray ที่นำเข้า

- Sidebar เมนู Dashboard และรายการ X-ray
- เลือกหน่วยบริการจาก dropdown
- Tab รายการ X-ray สมอง / ทรวงอก / ดวงตา
- Card สรุปรายการทั้งหมด, รอยืนยันผล, ยืนยันผลวินิจฉัย
- ค้นหารายการ X-ray
- กรองตามความเร่งด่วน / สถานะ
- ปุ่มตัวกรองขั้นสูง
- ตารางรายการ X-ray พร้อมปุ่มจัดการ (ไอคอนตา + รายละเอียด) ตรงตาม Figma
- คอลัมน์ "วันที่ X-ray" แสดงข้อความเต็ม เช่น `04/03/2567 10.00 น.`
- Pagination
- ปุ่มอัปโหลดฟิล์ม X-ray จำลองการเพิ่มแถวข้อมูล
- ปุ่ม Export ดาวน์โหลดไฟล์ CSV

### 3. หน้า Dashboard

- Long Scroll Layout, Card Based Layout, Vertical Scroll
- Sidebar แบบ absolute positioning (กว้าง 228px, สูง 1459px) พร้อมย่อขยายได้
- Header แสดง Dashboard title + ไอคอนนาฬิกา + "ข้อมูลอัพเดท" + วันที่
- Tab active สี `#1f43a5` พร้อม border-bottom
- สรุปจำนวนเคสประจำเดือน
- Card เคสด่วน / เคสปกติ (ไอคอนลายแถบเขียว)
- การ์ดรายวันพร้อมปุ่มเลื่อน
- **Donut chart SVG** รูปแบบ Consult พร้อม hover tooltip + floating label 80%/20%
- Bar chart สถิติพร้อม hover tooltip
- สรุปการนัด Consult
- ปุ่ม Export ดาวน์โหลดไฟล์ CSV

## ฟังก์ชันที่ใช้งานได้

- เปลี่ยนหน้าโดยไม่ reload ผ่าน hash route เช่น `#login`, `#xray`, `#dashboard`
- เปิด/ปิด modal
- แสดง toast notification
- ค้นหาและกรองข้อมูลในตาราง
- เปลี่ยนจำนวนรายการต่อหน้า
- อัปโหลดไฟล์จำลองและเพิ่มข้อมูลเข้า table
- Export CSV
- ย่อ/ขยาย sidebar
- เปลี่ยน tab และ card filter
- Hover tooltip บน Donut chart และ Bar chart

## โครงสร้าง Layout

| หน้า | เทคนิค Layout |
|------|--------------|
| Login | Flexbox จัดกลาง |
| X-ray | CSS Grid (sidebar + content) + sticky table header |
| Dashboard | Absolute positioning (1440px frame) + vertical scroll |

แนวทาง Auto Layout:
- `Horizontal`: Top bar, Tabs, Summary cards, Toolbar, Pagination, Metric cards, Day cards และกลุ่ม Consult
- `Vertical`: Sidebar, กลุ่มเมนู, Content panel, Dashboard sections, Filter controls และข้อมูลภายในแต่ละ Consult card

## โทนสีหลัก

| การใช้งาน | สี |
|-----------|-----|
| Primary (ปุ่ม, active) | `#20409C` |
| Dashboard title | `#1f43a5` |
| เคสปกติ (icon) | `#0FAD78` |
| พื้นหลัง Dashboard | `radial-gradient` + `linear-gradient` |
| Panel | `rgba(255,255,255,0.95)` |

## หมายเหตุเรื่องรูปภาพและความตรงกับต้นแบบ

ภาพประกอบฝั่งซ้ายของหน้า Login ใช้ไฟล์ `assets/login-panel.png` ซึ่งเตรียมจาก PNG ดีไซน์ต้นฉบับ ส่วนไอคอนและกราฟประกอบอื่นสร้างด้วย PNG, CSS และ SVG โดยไม่ต้องพึ่งไลบรารีภายนอก

ไอคอนทางการแพทย์หลักถูกสร้างเป็น PNG พื้นหลังโปร่งใส และไอคอน UI เช่น Filter, Export, การแจ้งเตือน และโลโก้ใช้ SVG เพื่อให้คมชัดทุกขนาด

## Browser ที่แนะนำ

- Google Chrome
- Microsoft Edge
- Firefox รุ่นใหม่

## การแก้ไขเพิ่มเติม

- แก้ layout และสีหลักที่ `styles.css`
- แก้ข้อมูลตัวอย่าง ตาราง และ logic ปุ่มต่าง ๆ ที่ส่วน `<script>` ด้านล่างของ `index.html`
- ถ้าต้องการแยก JavaScript ออกเป็นไฟล์ใหม่ สามารถย้าย script ไปไว้ใน `script.js` แล้วเพิ่ม `<script src="script.js"></script>` ก่อนปิด `</body>`
