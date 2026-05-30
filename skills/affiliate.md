---
name: affiliate
description: "TikTok affiliate / ปักตะกร้า product video prompt generator (UGC handheld). Use when user says '/affiliate [product]', '/affiliate vo', 'ปักตะกร้า', 'นายหน้า', 'รีวิวสินค้า', 'product video', 'UGC' — model โชว์สินค้าไม่พูด (VO ทีหลัง) + แนบ ref สินค้า + Product Consistency Lock + Hook→Demo→CTA + gen บท VO sync timing. Seedance 中文 + Higgsfield EN, vertical 9:16."
user_invocable: true
---

# affiliate — TikTok Affiliate / ปักตะกร้า Product Video Prompt Generator

> UGC handheld โชว์สินค้า **ไม่พูด** (เน้นถ่าย VO ใส่ทีหลัง) → Product Consistency Lock + Hook→Demo→CTA + บท VO พร้อม timing

## Usage

```
/affiliate [product desc]              # Full — visual prompts + VO script (Hook→Demo→CTA)
/affiliate scene [shot desc]           # Gen ฉาก/ช็อตเดียว (visual prompt)
/affiliate vo [product/script]         # Gen บท VO + timing อย่างเดียว
/affiliate product [desc]              # Gen product ref prompt (hero + macro)
/affiliate model [desc]                # Gen presenter/model ref prompt
/affiliate preset [unbox|before-after|lifestyle]  # โครงอื่นนอกจาก Hook-Demo-CTA
/affiliate fix [prompt]                # แก้ prompt ติด filter (สินค้า/หน้า)
```

## What It Does

```
สินค้า (desc + รูป ref) + กลุ่มเป้าหมาย
  ↓
1. วิเคราะห์ — ประเภทสินค้า, จุดขาย, กลุ่มเป้าหมาย, problem ที่แก้
2. เลือก Structure — Hook → Demo → CTA (default) หรือ preset อื่น
3. Gen Product Ref + Model Ref (Consistency Lock)
4. Gen Visual Prompt (Seedance 中文 + Higgsfield EN) — SILENT, ไม่มีบทพูด
5. Gen VO Script + Timing — sync กับ beat (พากย์ทีหลัง)
6. Output — copy ได้เลย / batch → export doc
```

---

## Golden Rules (กฎทอง)

1. **🔴 ตัวละครไม่พูด** — no lipsync, no dialogue ใน prompt — VO ใส่ทีหลัง → visual = **silent showcase**
2. **🔴 Product Consistency Lock (永远)** — สินค้าห้ามเพี้ยน: **สี / โลโก้ / ฉลาก / รูปทรง / สัดส่วน** ย้ำทุก beat — สำคัญที่สุด (model เปลี่ยนได้ สินค้าเปลี่ยนไม่ได้)
3. **แนบ product ref ทุก clip** — `@[UUID_PRODUCT]` ต้องอยู่ในเฟรมที่เห็นชัด อย่างน้อย Demo + CTA
4. **UGC handheld authentic** — กล้องสั่นเล็กน้อย, แสงธรรมชาติ/หน้าต่าง, ไม่เป๊ะแบบโฆษณา TV — "เหมือนเพื่อนถ่ายให้ดู"
5. **Hook 0-3 วิ ต้อง stop-scroll** — wow / problem / curiosity ภายใน 3 วิแรก ไม่งั้นเลื่อนผ่าน
6. **CTA ปักตะกร้า** — จบด้วย gesture **ชี้มุมล่างซ้าย** (ที่ตะกร้าส้มอยู่) — ⚠️ ถ่ายแค่ท่าชี้ **ห้าม render ไอคอนตะกร้า** (เป็น UI ของ TikTok เอง ใส่ตอน edit)
7. **Lens ทุก prompt** — `[X]mm` เสมอ
8. **Per-beat anchor** — ทุก beat ย้ำแสง/ฉาก + **ย้ำว่า product visible**
9. **Guard Wall** — `no subtitles / no on-screen text / no BGM` — VO + caption + ราคา ใส่ตอน edit ทีหลัง
10. **VO sync to beat** — บท VO timing ต้องตรงกับ visual beat (Hook line = beat hook, CTA line = beat CTA)

---

## Shoot Focus Mode — Product-Forward vs Talent-Forward

> ถาม/เดาก่อน gen ว่าจะเน้นอะไร — เปลี่ยน declaration + 主体 + 演技 block

| Mode | เน้น | คนปรากฏ | ใช้ตอน |
|------|------|---------|--------|
| **Talent-Forward** (default) | รีวิวเวอร์ + สินค้า | เห็นหน้า/ครึ่งตัว | สร้าง trust, รีวิวบุคลิก, lifestyle |
| **Product-Forward** ⭐ | **สินค้าเป็นพระเอก** | **เห็นแค่มือ ไม่เห็นหน้า** | เน้นตัวสินค้า/texture/swatch, ASMR, B-roll, สินค้าพูดเอง |

**Product-Forward — ปรับ 3 จุด:**
1. **Declaration** เปลี่ยน `@[UUID_MODEL]` (ตัวเต็ม) → `@[UUID_HAND] 这是手部参考——[ผิว/มือ] 仅出现手部不露脸`
2. **เพิ่ม block** `【画面主体要求 - 突出产品】产品为绝对主体，人物仅出现手部不露脸，镜头聚焦产品本身、质地、标签、使用瞬间`
3. **演技 block** เหลือแค่ `仅手部动作自然真实，稳定拿取、挤压、涂抹、推开`
4. Shot เน้น **product hero (50mm) + macro texture/swatch (100mm)** — สินค้าอยู่กลางเฟรมตลอด
5. **Swatch บนผิว** = proof shot ที่ดีสุด (โดยเฉพาะ before/after texture, สี, การซึม)

> สั่งสั้น: `/affiliate [product] product-forward` หรือ `เน้นสินค้า เห็นคนน้อย`

---

## Intercut Sequence Mode (ตัดสลับ — รีวิวจริง) ⭐

> default ของ affiliate ที่ดู pro = **ตัดสลับหลายมุม** ไม่ใช่ long shot ช็อตเดียว
> สูตร: **INSERT สินค้า → ลองใช้ → INSERT (proof) → ถ่ายคู่กัน (คน+สินค้า) + CTA**

```
0:00-0:03 〔INSERT 产品〕100mm微距 — สินค้า hero บนโต๊ะ label ชัด (มีแต่สินค้า)
0:03-0:06 切换 〔ลองใช้〕50mm — model ใช้จริง/ทา/สาธิต (เห็นหน้า+สินค้า)
0:06-0:09 切换 〔INSERT proof〕100mm微距 — swatch/texture/ผลลัพธ์ (เกลี่ยไม่ขาว ฯลฯ)
0:09-0:12 切回 〔ถ่ายคู่กัน 人与产品同框〕35mm — คน+สินค้าในเฟรม + CTA ชี้มุมล่างซ้าย
```

**กฎ Intercut:**
- ใช้ `切换` (cut to) / `切回` (cut back) ตัดในคลิปเดียว
- **เปลี่ยนเลนส์ทุก cut ไม่ซ้ำติดกัน** (100→50→100→35)
- **มาร์คชนิดช็อตทุก beat** `〔INSERT〕`/`〔ลองใช้〕`/`〔ถ่ายคู่กัน〕`
- ใส่ `【剪辑】多角度切换，每个镜头不同景别` ใน header
- `@ref` เฉพาะตัวที่อยู่ใน beat นั้น (insert สินค้าล้วน = แนบแค่ `@[UUID_PRODUCT]`)
- **proof shot (เกลี่ยไม่ขาว/before-after) วางเป็น INSERT** — แก้ปัญหา loop เพราะมันเป็น one-way action
- **คุณภาพสูงสุด** = gen แยก 4 คลิป (1 มุม 1 action) แล้วตัดต่อ > ยัด 切换 คลิปเดียว

> สั่งสั้น: `/affiliate [product] intercut` หรือ "ตัดสลับ insert + ลองใช้ + ถ่ายคู่"

---

## Loopable Clip Mode (seamless loop — วนซ้ำเนียน)

> ใช้เมื่ออยากได้คลิปสั้น (8-12s) ที่ **เปิดวนซ้ำหลายรอบได้เนียน** — VO ทับยาวกว่าได้ (ปล่อยภาพวน 1.5-2 รอบ)

**กฎ Loopable:**
1. **เฟรมแรก = เฟรมสุดท้าย** — ท่า/composition/ตำแหน่งสินค้า/สีหน้า ต้องเหมือนกันเป๊ะ (จุดต่อ loop)
2. **ใช้ action แบบ cyclical** (วนกลับที่เดิม) — ห้ามใช้ action ทางเดียว (ทา/เกลี่ย/แกะกล่อง = จบแล้ว loop กระตุก)
   - ✅ ถือ+หมุนสินค้า / ขยับเข้า-ออก / nod+blink+ยิ้ม / sway เบาๆ
   - ❌ ทาครีมแล้วเกลี่ย / เทออก / กดปั๊ม (one-way → แยกเป็น insert clip)
3. **กล้องเกือบนิ่ง** — extreme subtle handheld, สินค้า+หน้า อยู่ในเฟรมตลอดไม่ออกนอกจอ
4. **มี 【循环要求】block** — `首帧与尾帧完全一致，平滑循环可无限重复，无明显起止点`
5. **มาร์ค anchor pose** ใน beat แรกและสุดท้าย — `【起始锚点姿势】` ... `【回到起始锚点姿势完全一致】`
6. **Proof shot (one-way) → แยก insert clip** — เช่น swatch/เกลี่ยไม่ขาว gen เป็น macro clip ต่างหาก แทรกตอน VO พูดถึง

> สั่งสั้น: `/affiliate [product] loop 10s` หรือ "ทำให้ loop ได้ 10 วิ"

---

## UGC Structured Prompt (โครงสร้าง 3 ชั้น — product-locked, no dialogue)

> โครงคล้าย Seedance Structured ของ /drama แต่ **เพิ่มชั้นสินค้า + ตัด 台词 ออก**

### ชั้น 1 — Reference Declaration (头部声明)

```
@[UUID_SCENE]   这是场景参考——[ฉาก: ห้อง/โต๊ะ/หน้าต่าง + แสงธรรมชาติ + mood UGC]
@[UUID_MODEL]   这是[ROLE]（[ชื่อไทย/รีวิวเวอร์]）——[เสื้อผ้า casual + 泰国男性/女性 + อายุ岁 + ทรงผม]
@[UUID_PRODUCT] 这是产品参考——[ชื่อสินค้า + สี + ฉลาก/โลโก้ + รูปทรง + วัสดุ + ขนาด]
```
- **product ref = ชั้นหนึ่ง** — describe ละเอียดกว่าทุกตัว (สี ฉลาก โลโก้ รูปทรง)
- ชื่อไทยในวงเล็บช่วย map model

### ชั้น 1.5 — Directive Blocks + Consistency Lock (【】+ 永远)

```
【产品要求 - Consistency Lock】(สำคัญสุด)
产品永远是[สี/ฉลาก/โลโก้]，logo朝向镜头清晰可见，
产品不变形、不换色、不换包装，比例真实，
手持时不遮挡logo和主要卖点

【演技要求 - 不说话】(model ไม่พูด)
角色全程不说话、闭口或自然微笑，绝对不开口说台词，
自然展示产品、手持稳定、眼神看镜头，
自然的微表情、点头、呼吸起伏、轻微重心移动，真实不僵硬

【运镜要求 - UGC手持】
手持轻微晃动、自然真实、生活感，
自然光/窗光为主，不要影棚打光，像朋友帮忙拍

【时间与光线要求】
[lock แสง/เวลา — เช่น 明亮自然光，温暖居家氛围]

重要 (Lock ซ้ำ):
- 产品永远[สี/ฉลาก/โลโก้คงที่]
- [model]永远穿[เสื้อผ้าคงที่]
- 场景永远是[environment คงที่]
```

### ชั้น 2 — Timeline Beats (per-beat: product visible + ไม่มีบทพูด)

```
0:00-0:03 : @[UUID_MODEL] @[UUID_PRODUCT]
[X]mm[shot]，[ย้ำแสง/ฉาก]，
[HOOK action — หยิบสินค้าขึ้นมา/ทำหน้า wow/ชี้ปัญหา]，
产品清晰可见logo朝镜头，角色不说话只做表情和动作

0:03-0:10 : @[UUID_MODEL] @[UUID_PRODUCT]
[X]mm[shot]，[ย้ำแสง/ฉาก]，
[DEMO action — ใช้จริง/โชว์เนื้อ/สาธิตผล]，
产品保持一致，手不遮logo，角色专注展示不说话

0:10-0:15 : @[UUID_MODEL] @[UUID_PRODUCT]
[X]mm[shot]，[ย้ำแสง/ฉาก]，
[CTA action — ยกสินค้าใกล้กล้อง + 手指向画面左下方]，
角色微笑看镜头，手指轻点画面左下角方向（不渲染任何图标），产品logo清晰
```

### ชั้น 3 — Guard Wall (尾部 bilingual)

```
画面绝对不显示任何字幕 NO subtitles
不要任何屏幕文字 NO on-screen text / NO captions / NO price text
画面中绝对没有任何文字、没有购物车图标 NO cart icon, NO text on screen

不要背景音乐 no background music / no BGM / no soundtrack
保留环境音 ambient sound only（VO后期配音）

no grid lines / no overlay / no mesh
[ย้ำ product + scene constant]
cinematic UGC handheld, vertical 9:16，竖屏9:16
```

> **ทำไมต่างจาก drama**: ไม่มี 【台词与字幕】 block (ไม่พูด) — แทนด้วย 【产品要求 Lock】 + `角色不说话`. Guard wall เพิ่ม `NO cart icon` + `NO price text`

---

## Shot Library — UGC Commerce (เลือกตาม beat)

> 📷 **ภาษากล้องเต็ม** (shot size · angle · movement · lens · composition · 9:16): `.claude/skills/_shared/master-camera-reference.md` — ตารางด้านล่างคือชุดที่ affiliate ใช้บ่อย

| Shot | เลนส์ | ใช้ใน beat | จีน keyword |
|------|------|-----------|-------------|
| **Talking-head หยิบสินค้า** | 35mm | Hook | `中景手持，拿起产品对镜头` |
| **Product hero ใกล้กล้อง** | 50mm | Hook/CTA | `产品举近镜头，logo朝前` |
| **Macro เนื้อ/texture** | 100mm macro | Demo | `100mm微距，产品质地特写` |
| **In-use lifestyle** | 35mm | Demo | `自然使用产品，生活场景` |
| **Before/After split** | 50mm | Demo | `使用前后对比` |
| **Hand demo สาธิต** | 50mm | Demo | `手部演示产品效果` |
| **CTA ชี้ตะกร้า** | 35mm | CTA | `手指向画面左下方，微笑看镜头` |
| **POV ส่องสินค้า** | 28mm | Hook | `第一人称视角看产品` |

**Hand-product grammar (ไม่พูด เน้นมือ):**
```
拿起 (หยิบ) / 展示 (โชว์) / 打开 (เปิด/แกะ) / 涂抹 (ทา) / 喷洒 (ฉีด)
按压 (กด) / 倒出 (เท) / 演示效果 (สาธิตผล) / 举近镜头 (ยกใกล้กล้อง)
```

---

## Structure: Hook → Demo → CTA (default — 15-30s)

```
HOOK (0-3s)     หยุดนิ้ว — wow / ปัญหา / "อันนี้ดีจริง"
                Shot: หยิบสินค้า + ทำหน้า / product hero close

DEMO (3-Xs)     โชว์จุดขาย — ใช้จริง / texture macro / before-after
                Shot: macro + in-use + hand demo (สลับ 2-3 ช็อต)

CTA (last 3-5s) ปักตะกร้า — ยกสินค้า + ชี้มุมล่างซ้าย + ยิ้ม
                Shot: hero + point gesture
```

**Beat Map (15s):**
```
0:00 ─┬─ HOOK    หยิบ+wow         ◀ stop scroll
0:03 ─┼─ DEMO 1  macro texture
0:07 ─┼─ DEMO 2  ใช้จริง/ผลลัพธ์
0:11 ─┼─ CTA      ยกใกล้+ชี้ตะกร้า
0:15 ─┴─ END      ยิ้มค้าง logo ชัด
```

### Preset อื่น (`/affiliate preset [name]`)

| Preset | โครง | เหมาะกับ |
|--------|------|---------|
| **unbox** | แกะกล่อง → เผยสินค้า → first impression → CTA | สินค้าแพ็กเกจสวย, gadget |
| **before-after** | ปัญหา/ก่อน → ใช้สินค้า → หลัง/ผล → CTA | สกินแคร์, ทำความสะอาด, สุขภาพ |
| **lifestyle** | สินค้าในชีวิตจริง (ไม่ขายตรง) → soft CTA | แฟชั่น, ของแต่งบ้าน, ไลฟ์สไตล์ |

---

## VO Script (Google Gemini TTS Composer Format — default output)

> ตัวละครไม่พูดในคลิป → gen บท VO แยก ภูมิเอาไปเข้า **Google Gemini TTS** แล้ว overlay
> 🔴 **Output VO เป็น Composer format เสมอ** — Scene + Sample Context + Speaker + บทที่มี `[emotion]` tag

### Composer Format (3 ช่อง + tagged speech)

```
[ช่อง Scene]
[setting สั้นๆ — เช่น "Cozy home vanity, casual UGC review."]

[ช่อง Sample Context]
[tone + pacing เป็นอังกฤษ — เช่น "TikTok affiliate skincare review in Thai. Warm girl-next-door tone, like recommending to a close friend. Dynamic pacing—starts relatable, builds to excited proof, ends punchy and urgent. Authentic, conversational, not salesy."]

[Speaker 1 - [ชื่อ voice]]
[emotion] [HOOK ภาษาไทย] [emotion] [transition] [informative] [DEMO1] [impressed] [DEMO2 proof] [confident] [SPF/feature] [urgent] [CTA — กดตะกร้าสีส้มมุมล่างซ้ายเลย]
```

**กฎ Composer:**
- **บทพูด = ภาษาไทย / `[emotion]` tag = อังกฤษ** (Gemini อ่าน tag เป็น delivery direction)
- **วาง tag หน้าทุก beat/ทุกอารมณ์ที่เปลี่ยน** — ไม่ใช่ทุกคำ
- **Sample Context** = คุม pacing รวม (เขียนเป็นอังกฤษ ได้ผลดีกว่า)
- **Scene** = บรรยากาศห้องอัด/setting สั้นๆ
- บท 1 ย่อหน้าต่อเนื่อง (ไม่ใส่ timestamp ใน Composer — TTS อ่านรวด) แต่คุมความยาวให้ fit ~15s

### Emotion Tag Library (affiliate)

| Beat | Tags ที่ใช้ |
|------|-----------|
| **HOOK** | `[relatable]` `[frustrated]` `[curious]` `[intrigue]` `[surprised]` |
| **Transition** | `[hopeful]` `[excited]` `[realization]` |
| **DEMO/proof** | `[informative]` `[impressed]` `[reassuring]` `[confident]` |
| **CTA** | `[urgent]` `[confident]` `[friendly]` `[punchy]` |

### Timing Reference (sync กับ video beat — ไม่ต้องใส่ใน Composer)

> ใช้ตอน map บท ↔ ภาพ ว่าประโยคไหนตรง beat ไหน

```
0:00-0:03  HOOK   : [tag] "[ประโยคหยุดนิ้ว]"
0:03-0:07  DEMO1  : [tag] "[จุดขาย 1]"
0:07-0:11  DEMO2  : [tag] "[proof / ผลลัพธ์]"
0:11-0:15  CTA    : [tag] "[ปิดการขาย + ปักตะกร้า]"
```

### กฎ VO

| กฎ | รายละเอียด |
|----|-----------|
| **Thai-first ภาษาคนจริง** | พูดเหมือนเพื่อนเล่าให้เพื่อน ไม่ใช่สคริปต์ขาย |
| **Hook ≤ 2 วินาที** | ขึ้นด้วยปัญหา/ผลลัพธ์ ไม่ใช่ "สวัสดีค่ะวันนี้จะมารีวิว" |
| **3-4 คำ/วินาที** | Thai pacing — อย่ายัดยาวเกิน beat |
| **1 benefit = 1 beat** | อย่ายัดหลายจุดขายใน beat เดียว |
| **CTA ชัด** | "กดตะกร้าสีส้มมุมล่างซ้าย" / "ของมันต้องมี" / "ลิงก์อยู่ในตะกร้า" |
| **ไม่เคลม overclaim** | เลี่ยง "รักษา/หายขาด/ดีที่สุดในโลก" |

### Tone เลือกได้

```
เพื่อนแนะนำเพื่อน (default)  → เป็นกันเอง น่าเชื่อ
ปากตลาด/แม่ค้า              → เร็ว มันส์ เร่งปิด
สายเฮลตี้/พรีเมียม          → นุ่ม ข้อมูลแน่น
ตลก/ดราม่าเกินจริง          → hook แรง viral
```

> VO ตัวเต็มควร sync กับ `/แพะแดง` ได้ — ถ้าอยากได้ copy คมๆ ส่งต่อ `/แพะแดง` เขียน hook+CTA

---

## Product Ref Prompt (`/affiliate product`)

**Hero (white BG — ส่งทีม / e-com):**
```
product photography, [ชื่อสินค้า],
[สี + ฉลาก + โลโก้ + รูปทรง + วัสดุ],
front view, logo clearly visible facing camera,
clean white background, soft even studio light,
sharp focus, true color, photorealistic, no text overlay
```

**Macro (texture/detail — สำหรับ Demo insert):**
```
100mm macro product shot, [ชื่อสินค้า],
extreme close-up of [texture/ฉลาก/จุดขาย],
[สี + วัสดุ], natural soft light,
shallow depth of field, photorealistic, vertical 9:16
```

> ⚠️ Product ref = source of truth สำหรับ Consistency Lock — gen ให้ตรงของจริงที่สุด (สี/ฉลากต้องเป๊ะ)

---

## Model Ref Prompt (`/affiliate model`)

```
character reference sheet, front view and side view,
[เพศ] Thai Asian, age [อายุ],
[ลักษณะใบหน้า — friendly approachable],
[ทรงผม casual],
[เสื้อผ้า casual everyday — ไม่หรูเกิน, relatable],
natural friendly expression, NOT model-perfect,
white background, clean lighting, full face visible,
photorealistic, Thai Asian face, consistent features
```

> UGC = relatable > สวยเป๊ะ — เลือกหน้าที่ดู "เพื่อนข้างบ้าน" ไม่ใช่นางแบบโฆษณา

---

## Higgsfield Prompt (EN — start frame / stylized)

```
UGC handheld vertical video, [shot type], [lens] lens,
[model casual] showing [product — exact color/label],
[hook/demo/CTA action], NOT speaking, natural product handling,
[home/natural light setting],
subtle handheld shake, authentic everyday feel,
product logo clearly visible and consistent,
no subtitles, no on-screen text, no cart icon,
photorealistic, vertical 9:16
```

---

## Content Filter Cheatsheet (`/affiliate fix`)

### Product Ref Reject (รูปสินค้าไม่ผ่าน)
| ❌ ปัญหา | ✅ วิธีแก้ |
|---------|----------|
| สินค้าหมวด sensitive (อาหารเสริม/ยา/บุหรี่ไฟฟ้า) | describe เป็น text, ไม่แนบรูปฉลากชัด, เลี่ยงคำเคลม |
| ฉลากมีคำเคลมแรง (รักษา/ลดน้ำหนัก) | crop ฉลากออก หรือ blur ส่วนเคลม |
| โลโก้แบรนด์ดังโดน flag | ใช้ generic describe ไม่เอ่ยแบรนด์ใน text |

### Text Filter (คำที่ Seedance/platform มัก block)
```
รักษา/หายขาด/ลดน้ำหนัก/美白/减肥/治疗 → 帮助/呵护/改善/ช่วยดูแล
สินค้าผู้ใหญ่/แอลกอฮอล์/บุหรี่             → ไม่แนบ ref, soft describe
```

### กรณีตัวละครพูด (เผลอใส่บทพูด)
```
ลบ 台词/dialogue ออกจาก prompt ทุกจุด
ใส่ 角色不说话、闭口、只做表情 ย้ำใน 演技 block
```

---

## Output Rules

1. **Visual prompt** → code block ``` copy ได้
2. **Seedance** → 中文 เสมอ + Product Lock + `角色不说话`
3. **Higgsfield** → EN เสมอ
4. **VO script** → ภาษาไทย + timing table แยกจาก visual
5. **ทุก prompt** → product ref + lens + per-beat anchor + Guard Wall (no subtitle/no cart icon/no BGM)
6. **CTA** → ท่าชี้เท่านั้น ห้าม render ตะกร้า/ราคา
7. **Batch หลายสินค้า** → เสนอ export เป็น doc (เหมือน /drama)

---

## Common Mistakes (เลี่ยง)

| ❌ ผิด | ✅ ถูก |
|--------|--------|
| ใส่บทพูด/lipsync ในคลิป | ไม่พูด — VO ทีหลัง, prompt = silent |
| สินค้าเปลี่ยนสี/ฉลากระหว่าง beat | Product Consistency Lock (永远) ทุก beat |
| render ไอคอนตะกร้าส้มในภาพ | ถ่ายแค่ท่าชี้ — ตะกร้าเป็น UI TikTok |
| แสงโฆษณา TV เป๊ะเกิน | UGC handheld + แสงธรรมชาติ authentic |
| Hook ช้า "สวัสดีค่ะวันนี้..." | Hook ≤ 2 วิ ขึ้นปัญหา/wow ทันที |
| มือบังโลโก้ตอนโชว์ | `手不遮logo` — โลโก้หันกล้องชัดเสมอ |
| VO ยาวเกิน beat | 3-4 คำ/วิ, 1 benefit = 1 beat |
| ใส่ราคา/ข้อความบนจอ | Guard Wall — ใส่ caption ตอน edit |

---

*Related: [[feedback_seedance-structured-prompt]] · /drama (structured base) · /แพะแดง (VO copy) · /higgsfield (gen)*
*Created: 2026-05-30*
