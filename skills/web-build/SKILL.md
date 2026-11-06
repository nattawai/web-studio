---
name: web-build
description: สร้างเว็บทีละ section ตาม design.md และ tokens พร้อม screenshot ตรวจทุก section. ใช้ในขั้น Build ของ web-director หรือเมื่อผู้ใช้สั่งทำ/แก้ section ของเว็บ.
---

# Web Build

## กติกา
1. ทีละ section — ทำ → รัน dev server → screenshot (375px + 1440px) → เทียบกับ design.md → แก้ → ถัดไป
2. ใช้ token เท่านั้น (`bg-bg`, `text-ink`, `var(--clay)`) ห้าม hex ในคอมโพเนนต์
3. ข้อความทุกตัวมาจาก i18n JSON ห้ามเขียนข้อความตรงในโค้ด
4. ยังไม่ใส่ animation (เป็นหน้าที่ `web-motion`) — เตรียมแค่ `data-*` / ref ไว้
5. semantic HTML: `header`, `main`, `section[aria-labelledby]`, `footer`; รูปมี `alt`

## บทเรียนจากงานจริง
- **ใช้เนื้อหาจริงของ Hero ก่อนออกแบบ** — ความยาวชื่อ/ประโยคเปลี่ยน layout มาก (placeholder หลอกตา)
- **ชื่อยาว** (เช่น นามสกุลไทย/ทับศัพท์ 15+ ตัวอักษร): แยกชื่อ-นามสกุลคนละบรรทัด, `clamp()` ค่าต่ำสุด ~2rem แล้ววัด `scrollWidth === clientWidth` ที่ 375px
- **ตำแหน่งหลายอัน**: เลือก 1 ตำแหน่งหลัก + บรรทัด focus รอง — อย่าใส่หลาย title ใน Hero
- ยังไม่มีรูป → ใช้ monogram/gradient เว้นที่ไว้ และมี flag เปิดรูปจริงทีหลัง
- ใส่ `data-speed` บน layer ที่จะ parallax ไว้ตั้งแต่ขั้น build — ขั้น motion หยิบไปใช้ได้เลย

- **section ที่มี blob/ของตกแต่งตำแหน่ง absolute ต้องมี `overflow-hidden`** — ไม่งั้นมือถือเลื่อนซ้ายขวาได้ (เจอจริง: 472px บนจอ 375)
- **อย่าใส่ letter-spacing กับภาษาไทย** — ใช้ `[html:lang(en)_&]:tracking-*` เฉพาะอังกฤษ
- การ์ดตัวเลขที่ label ยาวไม่เท่ากัน: จัดตัวเลขชิดบนให้ตรงกัน
- ถ้าผู้ใช้มี resume/เอกสาร → อ่านก่อนถามคำถาม จะได้เนื้อหาจริงเร็วกว่า; อย่าใส่ชื่อลูกค้าโดยไม่ยืนยัน

## แตก agent
section ที่ไม่ขึ้นต่อกันแบ่งให้ subagent ทำพร้อมกันได้ แต่ละตัวแก้เฉพาะไฟล์ section ของตัวเอง และส่งกลับแค่สรุป + path screenshot

## จบขั้น
อัปเดต STATUS.md: section ไหนเสร็จ, screenshot อยู่ไหน
