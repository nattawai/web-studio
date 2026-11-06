---
name: web-director
description: คุม workflow สร้างเว็บตั้งแต่ต้นจนจบ — landing page, parallax, portfolio, web application. ใช้เมื่อผู้ใช้อยากทำเว็บใหม่, ทำเว็บต่อ, ถามว่าขั้นต่อไปคืออะไร, หรืออยากเปลี่ยน framework. Triggers - ทำเว็บ, สร้างเว็บ, landing page, parallax, portfolio, web app, ทำต่อ, เปลี่ยน stack.
---

# Web Director

หัวหน้า workflow — เลือกขั้นตอน คุม gate และจด `STATUS.md` ที่ root ของโปรเจกต์

## ลำดับขั้น
| # | ขั้น | skill | ผลลัพธ์ | Gate |
|---|---|---|---|---|
| 1 | Brief | `web-brief` | `docs/brief.md` | ครบทุกหัวข้อ |
| 2 | Direction | `web-direction` | `docs/design.md` + tokens | ✋ ผู้ใช้เลือกสไตล์ |
| 3 | Structure + Stack | (ขั้นนี้เอง) | wireframe ใน `docs/design.md`, stack ใน STATUS | ✋ ผู้ใช้อนุมัติ |
| 4 | Scaffold | ตาม `references/stacks/<stack>.md` | โปรเจกต์รันได้ + tokens + i18n | `npm run build` ผ่าน |
| 5 | Build | `web-build` | ทีละ section | screenshot ทุก section |
| 6 | Motion | `web-motion` | animation/parallax | ไม่หน่วง, reduced-motion |
| 7 | QA | `web-qa` | รายงาน QA | ✋ ผ่านเกณฑ์ + ผู้ใช้ดู |
| 8 | Deploy | `web-deploy` | ลิงก์จริง | เปิดลิงก์ได้ |

ห้ามข้ามขั้นที่ gate ยังไม่ผ่าน ทุกครั้งที่จบขั้น ให้อัปเดต `STATUS.md` (ตารางสถานะ + Decisions)

## Stack Selector (ขั้น 3)
อ่าน `references/stack-selector.md` แล้ว **เสนอ** stack พร้อมเหตุผลและข้อเสีย ให้ผู้ใช้ตัดสิน ห้ามเลือกเงียบ ๆ

## เปลี่ยน stack
- ก่อน scaffold: เปลี่ยนได้ทันที
- หลัง scaffold: แจ้งงานที่ต้องย้าย (component) และสิ่งที่ใช้ต่อได้ (tokens, i18n JSON, motion recipes) แล้วขอยืนยันก่อน

## หลักที่ต้องรักษา
ดู `../../README.md` หัวข้อ "หลัก 6 ข้อ"
