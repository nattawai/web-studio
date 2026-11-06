---
name: web-qa
description: ตรวจคุณภาพเว็บก่อน deploy ตามเกณฑ์ที่วัดได้ — screenshot 3 ขนาดจอ, Lighthouse, console error, horizontal scroll, contrast, alt text, reduced-motion. ใช้ในขั้น QA ของ web-director หรือเมื่อผู้ใช้ถามว่าเว็บพร้อมหรือยัง.
---

# Web QA

## เกณฑ์ (ค่าจริงมาจาก `docs/design.md`)
| เช็ก | วิธี | ผ่านเมื่อ |
|---|---|---|
| Build | `npm run build` | ไม่มี error |
| Layout | screenshot 375 / 768 / 1440 | ไม่มี horizontal scroll, ไม่มีอะไรล้น |
| Console | browser pane / Playwright | 0 error |
| Lighthouse | `npx lighthouse <url> --preset=desktop` + mobile | ทุกหมวด ≥ 90 |
| Contrast | เทียบตาราง token | ข้อความผ่าน AA |
| a11y | รูปมี alt, ปุ่มมีชื่อ, heading เรียงลำดับ | ครบ |
| Reduced motion | emulate `prefers-reduced-motion` | ไม่มี parallax, เนื้อหาครบ |
| i18n | สลับ TH/EN | ไม่มี key หลุด |

## ผลลัพธ์
`docs/qa-report.md` — ตารางผ่าน/ไม่ผ่าน + รายการแก้ + path screenshot
แสดงผลให้ผู้ใช้ดู ✋ ก่อนไป deploy

## บทเรียนจากงานจริง (portfolio, 2026-11)
- ตรวจบน **production build** (`vite preview`) ไม่ใช่ dev server — dev มี HMR/StrictMode ปน
- browser pane ของแอปทำ reduced-motion ไม่ได้และ rAF หยุดตอนซ่อน → ใช้ `puppeteer-core` ชี้ Chrome ที่ติดตั้งอยู่ (`executablePath`) + `page.emulateMediaFeatures([{name:'prefers-reduced-motion',value:'reduce'}])`
- สคริปต์เดียววน 3 ขนาดจอ × 2 ภาษา (ตั้งภาษาผ่าน `evaluateOnNewDocument` → localStorage): เลื่อนทั้งหน้าก่อน (ให้ reveal ทำงาน) แล้วเช็ก scrollWidth, reveal ที่ค้าง opacity 0, i18n key หลุด, console error, inject `axe-core` รัน wcag2a/wcag2aa/best-practice, screenshot fullPage
- Lighthouse: `CHROME_PATH=... npx lighthouse@<ver> <url> --chrome-flags="--headless=new" --output=json` (+ `--preset=desktop`) แล้วอ่าน JSON
- axe จับ contrast ที่ Lighthouse ปล่อยผ่าน (4.49 vs 4.5) — แก้ที่ token ไม่ใช่ที่ component; คำนวณ contrast หลายค่าก่อนเลือก
- แก้เร็วที่ได้คะแนนจริง: Google Fonts `media="print" onload="this.media='all'"` + `<noscript>` (perf +6 บนมือถือ), เพิ่ม `public/robots.txt` (SPA ไม่มีจะได้ index.html → SEO 91)
- ดู screenshot ด้วยตาทุกครั้ง — สคริปต์ไม่จับปัญหาความสวย
