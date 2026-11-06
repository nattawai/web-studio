# Stack: React + Vite + TypeScript

## Scaffold (Windows/Git Bash ทดสอบแล้ว)
```bash
npm create vite@latest <name> -- --template react-ts --no-interactive < /dev/null
cd <name>
npm install
npm install -D tailwindcss @tailwindcss/vite
npm install gsap @gsap/react lenis i18next react-i18next
```
> `--no-interactive` + `< /dev/null` จำเป็น ไม่งั้น create-vite ค้างรอคำถาม

## vite.config.ts
```ts
import tailwindcss from '@tailwindcss/vite'
plugins: [react(), tailwindcss()]
```

## โครงไฟล์
```
src/
  styles/tokens.css     CSS variables + @theme ของ Tailwind v4
  styles/global.css     @import "tailwindcss"; @import "./tokens.css";
  i18n/index.ts         i18next init + จำภาษาใน localStorage (try/catch)
  i18n/th.json, en.json
  sections/Hero.tsx, About.tsx, Projects.tsx, Experience.tsx, Contact.tsx
  components/           ปุ่ม, การ์ด, LangSwitch
  motion/useLenis.ts    smooth scroll + ปิดเมื่อ reduced-motion
```

## SEO / แชร์ลิงก์ (SPA)
ใส่ `<title>`, `meta description`, `og:*` ใน `index.html` และ `lang` ให้ตรง

## Deploy
Cloudflare Pages: build `npm run build`, output `dist`
