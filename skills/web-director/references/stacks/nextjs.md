# Stack: Next.js (ยังไม่ทดสอบ — v0.1)

ใช้เมื่อ: ต้อง SEO จริงจัง, มี auth/DB, หรือตำแหน่งงานต้องการ Next.js

```bash
npx create-next-app@latest <name> --ts --tailwind --app --eslint --no-src-dir --use-npm
npm install gsap @gsap/react lenis
```
- คอมโพเนนต์ที่ใช้ GSAP/Lenis ต้องมี `"use client"`
- i18n: route `app/[lang]/`
- เว็บนิ่ง: `output: 'export'` ใน next.config → deploy Cloudflare Pages ได้

TODO: ทดสอบกับโปรเจกต์จริงแล้วเติมบทเรียน
