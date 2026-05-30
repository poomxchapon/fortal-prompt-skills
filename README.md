# FORTAL · Prompt Skills

> วิธีเขียน AI Video/Image Prompt ระดับโปรดักชัน — กล้อง เลนส์ แสง จังหวะ และโครงสร้าง prompt
> สำหรับ **Seedance (中文)** · **Higgsfield (EN)** · **Nano Banana** — รูปแบบ **9:16 vertical**

เว็บสรุป (มีรหัสผ่าน): เปิด `index.html`

---

## สกิลทั้ง 4

| Skill | งาน | ไฟล์ |
|-------|-----|------|
| **/action** | หนัง action — timeline + speed ramp + film presets + intercut | [`skills/action.md`](skills/action.md) |
| **/drama** | ละครแนวตั้ง — บท→shot→lens, lipsync idle, voice design, export .docx | [`skills/drama.md`](skills/drama.md) |
| **/horror** | ผีไทย/จิตวิทยา — director grammar + context engine + 8 beat archetypes | [`skills/horror.md`](skills/horror.md) |
| **/affiliate** | TikTok ปักตะกร้า/UGC — product lock + ไม่พูด + Hook→Demo→CTA + VO script | [`skills/affiliate.md`](skills/affiliate.md) |

---

## โครงร่วม — Seedance Structured Prompt (3 ชั้น)

ทุกสกิลใช้ backbone เดียวกัน:

1. **Declaration (头部)** — `@[UUID] 这是ROLE（ชื่อไทย）——desc` ประกาศ ref ทุกตัวบนหัว
2. **Consistency Lock (永远)** — ย้ำเสื้อผ้า/สินค้า/ฉาก กัน drift ระหว่าง beat
3. **演技 Acting Block** — micro-expression/眨眼/呼吸 กันหน้าแข็ง
4. **Per-beat Anchor** — ทุก beat ย้ำแสง/ฉากซ้ำ กันแสงเปลี่ยนกลางคลิป
5. **Guard Wall (尾部)** — NO subtitles / no BGM / no overlay (2 ภาษา หลาย phrasing)

---

## เอาไปใช้ต่อ (สำหรับทีมอื่น / AI Agent)

ไฟล์ `.md` แต่ละอันเป็น **สกิลเต็มในตัว** — เป็นทั้งคู่มือสอนวิธีคิด และพร้อมติดตั้งเป็น skill

### วิธีที่ 1 — ให้ AI agent เรียน
วางไฟล์ `.md` ให้ AI agent ของคุณ แล้วบอกว่า:
> "เรียนวิธีเขียน prompt จากไฟล์นี้ แล้วทำเป็น skill ให้หน่อย"

AI จะเข้าใจทั้งรายละเอียดกล้อง เลนส์ แสง และโครงสร้าง prompt → ประกอบเป็นสกิลของคุณได้

### วิธีที่ 2 — ติดตั้งเป็น Claude Code skill ตรงๆ
```
.claude/skills/<name>/SKILL.md
```
แล้วเรียกด้วย `/<name>` (เช่น `/action`)

frontmatter ที่หัวไฟล์ (ใส่เฉพาะ 3 key นี้):
```yaml
---
name: action
description: "เมื่อไหร่ให้เรียกสกิลนี้ + trigger words..."
user_invocable: true
---
```

---

## โครงสร้าง

```
fortal-prompt-skills/
├── index.html          เว็บสรุป (password-gated)
├── README.md
└── skills/
    ├── action.md
    ├── drama.md
    ├── horror.md
    └── affiliate.md
```

---

*FORTAL INTERACTIVE — Prompt Engineering Playbook*
