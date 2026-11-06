# Stack Selector

## ปัจจัย (เรียงตามน้ำหนัก)
1. **ผู้ใช้ถนัด/อยากใช้อะไร** — น้ำหนักสูงสุด
2. **ตรงกับเป้าหมาย** — เช่น ตำแหน่งงานที่จะสมัครต้องใช้อะไร, ทีมใช้อะไร
3. **ประเภทเว็บ**
   | ประเภท | default |
   |---|---|
   | content / landing เน้นเร็ว | Astro |
   | interactive / SPA ไม่เน้น SEO | React + Vite |
   | app มี auth/DB หรือ ต้อง SEO | Next.js |
4. ความง่ายในการดูแลต่อ

## รูปแบบการเสนอ
```
แนะนำ: <stack>
เหตุผล: ...
ข้อเสีย: ...
ทางเลือก: <stack อื่น> ถ้า ...
```

## Stack ที่รองรับ (v0.1)
- `stacks/react-vite.md` ✅ ใช้จริงแล้ว (portfolio)
- `stacks/nextjs.md` ⬜ ยังไม่ทดสอบ
- `stacks/astro.md` ⬜ ยังไม่ทดสอบ

## ส่วนที่ต้อง portable เสมอ
- tokens = CSS variables (`src/styles/tokens.css`)
- เนื้อหา = JSON ต่อภาษา (`src/i18n/<lang>.json`)
- motion = GSAP recipes ไม่ผูก framework (`web-motion/references/recipes.md`)
- component แยกตาม section
