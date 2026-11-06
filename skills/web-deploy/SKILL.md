---
name: web-deploy
description: Deploy เว็บขึ้นจริง (default Cloudflare Pages) แล้วตรวจลิงก์จริงอีกครั้ง. ใช้ในขั้นสุดท้ายของ web-director หรือเมื่อผู้ใช้สั่งขึ้นเว็บ/ขอลิงก์.
---

# Web Deploy

1. ยืนยันกับผู้ใช้ก่อน (เป็นการเผยแพร่สาธารณะ) ✋
2. `npm run build`
3. Cloudflare Pages:
   ```bash
   npx wrangler pages deploy dist --project-name <name>
   ```
   (ครั้งแรกผู้ใช้ต้อง `npx wrangler login` เอง)
4. เปิดลิงก์จริง: เช็ก console, OG tags, สลับภาษา
5. อัปเดต STATUS.md: ลิงก์ + วันที่

## บทเรียนจากงานจริง (portfolio, 2026-11)
- ก่อน deploy รัน `npx wrangler whoami` + `npx wrangler pages project list` — ถ้ามีโปรเจกต์/โดเมนเดิมอยู่ ถามผู้ใช้ก่อนว่าจะทับหรือแยก (อย่าเดาจากชื่อ)
- โปรเจกต์ใหม่: `wrangler pages project create <name> --production-branch main` แล้ว `pages deploy dist --project-name <name> --branch main --commit-dirty=true`
- ผูก custom domain: wrangler ไม่มีคำสั่ง และห้ามดึง OAuth token ของ wrangler ไปยิง API เอง → ให้ผู้ใช้ login dashboard ใน browser pane แล้วทำผ่าน UI: `dash.cloudflare.com/<account>/pages/view/<project>/domains` → Set up a custom domain → ใส่โดเมน → Continue → Activate domain (โซนอยู่บัญชีเดียวกัน CNAME สร้างให้เอง, สถานะ Initializing ไม่กี่นาที)
- ก่อน deploy เตรียม: og-image 1200×630 (render ด้วย puppeteer จาก token สีของเว็บ), canonical, og:url, twitter:card, sitemap.xml, robots.txt ชี้ sitemap, `public/_headers` cache `/assets/*` immutable
- curl บน Windows (schannel) อาจล้มด้วย CRYPT_E_REVOCATION_OFFLINE กับ *.pages.dev ใหม่ — ตรวจด้วย puppeteer/Chrome แทน: status ไฟล์ static, header cache, title/og, console, สลับภาษา
