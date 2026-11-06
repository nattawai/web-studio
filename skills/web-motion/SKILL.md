---
name: web-motion
description: ใส่ animation, parallax, scroll reveal, smooth scroll ให้เว็บที่สร้างเสร็จแล้ว โดยไม่ทำให้หน่วงและเคารพ reduced-motion. ใช้ในขั้น Motion ของ web-director หรือเมื่อผู้ใช้ขอ parallax/animation/เอฟเฟกต์ตอน scroll.
---

# Web Motion

ใส่หลังเว็บสวยแบบนิ่งแล้วเท่านั้น สูตรอยู่ที่ `references/recipes.md`

## กฎบังคับ
- ขยับเฉพาะ `transform` / `opacity` (ไม่ animate width/top/box-shadow)
- `gsap.matchMedia()` แยก: `(prefers-reduced-motion: no-preference)` และ `(pointer: fine)`
- reduced-motion → ไม่มี parallax, ไม่มี Lenis, เนื้อหาแสดงครบทันที
- ทุก animation อยู่ใน `useGSAP` (React) เพื่อ cleanup อัตโนมัติ
- เนื้อหาต้องมองเห็นได้แม้ JS ไม่ทำงาน (อย่าเริ่มด้วย `opacity:0` ใน CSS)

## ตรวจ
- เลื่อนทั้งหน้าใน browser pane ดู console ไม่มี error
- Performance: ไม่มี long task จาก scroll handler

## บทเรียนจากงานจริง (portfolio, 2026-11)
- รวม motion ไว้ hook เดียว (`useMotion`) ที่อ่าน `data-speed` / `data-reveal` / `data-line` / `data-count` / `data-tilt` จาก markup — section ไม่ต้อง import GSAP
- Reveal: `gsap.set(...{opacity:0,y:24})` ใน JS + `ScrollTrigger.batch(..., {once:true})` ดีกว่า from() ต่อ section — element ใหม่ที่ React สร้างหลังสลับภาษาจะแสดงปกติ ไม่ค้าง
- **ห้าม `overwrite: 'auto'` ใน reveal** ถ้า element เดียวกันมี tilt — มันฆ่า tween rotate ทิ้ง
- Tilt ใช้ `gsap.to(card, {rotateX, rotateY, overwrite:'auto'})` + `transformPerspective` บนการ์ด (ไม่ต้องแก้ CSS parent)
- Count-up: เก็บค่าจริงใน `el.dataset.countOriginal ??=` — StrictMode รัน effect 2 รอบ รอบสองจะอ่านได้ "0+" ที่เราเขียนทับ แล้วนับถึง 0; cleanup ให้คืนข้อความเดิม
- ใช้ `ResizeObserver(document.body)` → debounce `ScrollTrigger.refresh()` (setTimeout ไม่ใช่ rAF) ครอบคลุมสลับภาษา/ฟอนต์/รูปโหลด
- Anchor link: ดัก click `a[href^="#"]` → `lenis.scrollTo(target, {offset: -ความสูง header})`
- Import `lenis/dist/lenis.css`
- ทดสอบใน browser pane ที่ **ซ่อนอยู่**: rAF ไม่ทำงาน → animation ไม่เดิน. import gsap จาก URL `deps/gsap.js?v=` ใน `performance.getEntriesByType('resource')` (instance เดียวกับแอป) แล้วเรียก `gsap.ticker.tick()` วนเอง; `quickTo` ไม่ตอบสนองแบบนี้ — ทดสอบไม่ได้
- console ของ pane เก็บ error เก่าจาก HMR ไว้ — ดู timestamp `?t=` ก่อนสรุปว่ามี error
- reduced-motion: resize_window emulate ไม่ได้ ต้องตรวจในเบราว์เซอร์จริง (DevTools → Rendering) ช่วง QA
