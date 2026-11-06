# web-studio (plugin)

Workflow สร้างเว็บ (landing page, parallax, web app) แบบมีขั้นตอนและจุดอนุมัติ

```
/web-start → Brief → Direction ✋ → Structure + Stack ✋ → Scaffold → Build → Motion → QA ✋ → Deploy
                 └──────────── STATUS.md จดทุกขั้น ────────────┘
```

## โครงสร้าง
| ส่วน | ไฟล์ |
|---|---|
| คำสั่งเริ่ม | `commands/web-start.md` |
| หัวหน้า (orchestrator) | `skills/web-director/` |
| ขั้นตอน | `skills/web-brief`, `web-direction`, `web-build`, `web-motion`, `web-qa`, `web-deploy` |
| คู่มือ stack | `skills/web-director/references/stacks/*.md` |

## หลัก 6 ข้อ
1. ตัดสินสไตล์ก่อนเขียนโค้ด (`docs/design.md`)
2. ใช้ design token ทุกที่ ห้าม hard-code สี
3. AI ต้องดูงานจริง — screenshot ทุก section
4. Motion เป็นชั้นสุดท้าย
5. Parallax ห้ามหน่วง — transform/opacity, reduced-motion, มือถือเบาลง
6. QA วัดได้ — Lighthouse ≥ 90, a11y, 3 ขนาดจอ

## ติดตั้ง
ใน Claude Code:
```
/plugin marketplace add nattawai/web-studio
/plugin install web-studio@web-studio
```
จากนั้นพิมพ์ `/web-start` เพื่อเริ่มโปรเจกต์ใหม่

ทดลองจากโฟลเดอร์ในเครื่อง:
```bash
claude --plugin-dir ./web-studio
```

## ตัวอย่างงานจริง
[portfolio.waivern.org](https://portfolio.waivern.org) ([source](https://github.com/nattawai/portfolio)) — สร้างครบทุกขั้นด้วย plugin นี้: Lighthouse mobile 98/100/100/100, desktop 100 ทุกหมวด, axe 0 violation
บทเรียนจากงานนี้ถูกเขียนกลับเข้า `SKILL.md` แต่ละขั้น (หัวข้อ "บทเรียนจากงานจริง")

## สถานะ
v0.1.0 — ใช้งานจริงแล้ว 1 โปรเจกต์

## License
[MIT](LICENSE)
