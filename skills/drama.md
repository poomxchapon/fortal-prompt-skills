# drama — AI Vertical Drama Prompt Generator

> อ่านบท → แบ่ง Shot → Gen Prompt ทั้ง Pipeline อัตโนมัติ

## Usage

```
/drama [path-to-script.pdf]              # Full pipeline — อ่านบท gen prompt ทั้งหมด
/drama scene [description]               # Gen prompt ฉากเดียว
/drama character [name] [description]    # Gen character ref prompt
/drama poster [title]                    # Gen movie poster prompt
/drama fix [prompt]                      # แก้ prompt ที่ติด filter
```

## What It Does

อ่านบทละคร (PDF/text) แล้วสร้าง prompt สำหรับ AI tools ทั้ง pipeline:

```
บท (PDF/text)
  ↓
1. วิเคราะห์บท — ตัวละคร, ฉาก, อารมณ์
2. แบ่ง Story (30 วิ/story) + Shot List + Lens
3. Gen Prompt ภาพฉาก (Nano Banana Pro / Higgsfield)
4. Gen Prompt Video (Seedance 中文 + Higgsfield EN)
5. Gen Prompt เสียง (ElevenLabs Voice Design)
6. Export Production Doc
```

---

## IMPORTANT — อ่านก่อนทำงาน

ก่อนสร้าง prompt ต้องอ่าน README Guide:
```
ψ/active/vivah-klone/README_AI_PROMPT_GUIDE.md
```
ไฟล์นี้มีกฎและเทคนิคทั้งหมดที่ต้องทำตาม

---

## Step 1: วิเคราะห์บท

เมื่อได้รับบท (PDF หรือ text):

1. **ระบุตัวละคร** — ชื่อ, อายุ, ลักษณะ, บทบาท, ความสัมพันธ์
2. **ระบุฉาก** — สถานที่, ช่วงเวลา (กลางวัน/กลางคืน), สภาพอากาศ
3. **แบ่ง Story** — แต่ละ Story ไม่เกิน 30 วินาที
4. **แบ่ง Shot ใน Story** — ตามจังหวะอารมณ์ที่เปลี่ยน
5. **เลือก Lens** — ตามอารมณ์แต่ละ Shot

> 📷 **ภาษากล้องเต็ม** (shot size · angle · movement · lens · composition · 9:16): `.claude/skills/_shared/master-camera-reference.md`

### Lens Guide (เลนส์ = ภาษาอารมณ์)

| Lens | ฟีล | ใช้ตอน |
|------|------|--------|
| 16mm | กว้าง scale อำนาจ | Establishing, ห้องใหญ่ คนตัวเล็ก |
| 24mm | กว้าง+distortion | Low angle ให้ดูยิ่งใหญ่, action |
| 33mm | CU + context | เปิดฉาก, บทสนทนาที่ต้องเห็นห้อง |
| 50mm | ตาคนจริง | OTS, POV, tracking |
| 85mm | isolate อารมณ์ | Reaction, emotional, CU ตัวละคร |
| 100mm macro | detail จัด | Insert — มือ, วัตถุ, เค้กในโคลน |
| 135mm | เบลอหมด | Extreme isolation — ตา, น้ำตา |

---

## Step 2: Gen Character Ref Prompt

### โครงสร้าง

```
character reference sheet, front view and side view,
[เชื้อชาติ/เพศ], age [อายุ],
[ลักษณะเด่นของใบหน้า],
[ทรงผม],
[เสื้อผ้า],
[อารมณ์/สีหน้า],
white background, ID photo style, clean lighting,
full face visible, photorealistic,
Thai Asian face, consistent features
```

### ข้อควรระวัง
- ตัวละครที่แตกต่างกัน ต้อง describe ให้ชัดเจนว่าต่างกันตรงไหน
- ใส่ keyword ที่ทำให้แยกแยะได้ เช่น `sharp jawline` vs `soft feminine features`
- Uniform/ชุดพิเศษ ให้ describe ละเอียด รวม logo, สี, material

---

## Step 3: Gen Scene Ref Prompt (ภาพฉาก ไม่มีคน)

### โครงสร้าง

```
Cinematic [มุมกล้อง], [เลนส์],
[รายละเอียดสถานที่],
[ช่วงเวลา — กลางวัน/กลางคืน],
[แสง],
[อารมณ์/บรรยากาศ],
no people,
photorealistic, vertical 9:16
```

### ข้อควรระวัง
- ช่วงเวลาต้อง sync กับฉากก่อนหน้า/หลัง
- ถ้าเป็น interior หลายมุม ใช้ `multiple angles, 4 panels layout`
- ภาพฉากนี้จะเอาไปเป็น ref ใน Seedance (เพราะ Seedance ไม่รับ face ref)

---

## Step 4: Gen Image Prompt (ตัวละครในฉาก)

### โครงสร้าง — Nano Banana Pro

```
Cinematic [มุมกล้อง], [เลนส์] lens,
[คำอธิบายตัวละคร — อายุ, เสื้อผ้า, ทรงผม],
[action/ท่าทาง],
[อารมณ์/สีหน้า],
[สถานที่],
[แสง],
photorealistic, vertical 9:16
```

### ข้อควรระวัง
- ใส่ ref ตัวละคร เป็น input image เสมอ
- ระบุเลนส์ทุกครั้ง
- ระบุแสง + ช่วงเวลาให้ชัดเจน
- `vertical 9:16` ทุกครั้ง

---

## Step 5: Gen Video Prompt

### แบบ A — Seedance Structured Prompt (新版结构化 — Declaration + Lock + Guards) ⭐

> โครงสร้าง 3 ชั้น: **หัว (声明 + Lock)** → **timeline beats (per-beat anchor)** → **ท้าย (guard wall)**
> ใช้แทนแบบเก่า "นี่คือ [ชื่อ]" — แก้ปัญหาตัวละครสลับชุด / ฉากเปลี่ยนแสง / หน้าแข็ง / 字幕หลุด

#### ชั้น 1 — Reference Declaration (头部声明)

ประกาศ ref ทุกตัวบนสุด: `@[UUID] 这是[ROLE]（[ชื่อไทย]）——[คำอธิบาย persistent]`

```
@[UUID_SCENE] 这是场景参考——[สถานที่+เวลา+แสง+mood ละเอียด]
@[UUID_X] 这是[ROLE]（[ชื่อไทย]）——[เสื้อผ้า + 泰国男性/女性 + อายุ岁 + ทรงผม]
@[UUID_Y] 这是[ROLE]（[ชื่อไทย]）——[...]
```
- ใส่ **ชื่อไทยในวงเล็บ** `（ท่านรองประธาน）` → model map ตัวละครแม่นขึ้น
- คำอธิบาย = **persistent** (จะถูก lock ซ้ำทุก beat) — ใส่เสื้อผ้า/ผม/อายุ ให้ครบ

#### ชั้น 1.5 — Directive Bracket Blocks (【】指令块 + Consistency Lock)

```
【时间与光线要求】
[lock เวลา+แสง ย้ำ non-negotiable — เช่น 必须是夜晚黑夜深黑色夜空，金色灯光照明，绝对不是白天]

重要 (Consistency Lock — ใช้ 永远):
- [角色A]永远穿[เสื้อผ้า/ลุคคงที่]
- [角色B]永远[ลักษณะคงที่]
- 场景必须是[environment คงที่]

【演技要求】(กันหน้าแข็ง)
所有角色表演要自然真实生动，不要僵硬呆板，
要有自然的微表情、眨眼、呼吸起伏、重心轻微移动

【台词与字幕要求】(ถ้ามีบทพูด)
角色对口型准确说出泰语台词嘴型同步，画面绝对不出现任何字幕文字 NO subtitles
```

#### ชั้น 2 — Timeline Beats (per-beat environment anchor)

ทุก beat: `@[ref]` + เลนส์ + **ย้ำแสง/ฉากซ้ำ** + action+表情+micro-acting + บทพูด

```
0:00-0:04 : @[UUID_X]
[X]mm[近景/中景/远景]，[ย้ำแสง/ฉาก เช่น 夜晚酒店金色灯光背景]，
[action + 表情(emotion) + micro-acting]，
对口型准确说出泰语台词不显示字幕 "[บทไทย]" NO subtitles

0:04-0:08 : @[UUID_X] @[UUID_Y]
[X]mm[shot]，[ย้ำแสง/ฉาก]，
[action ละเอียด + emotion]，
对口型准确说出泰语台词不显示字幕 "[บทไทย]" NO subtitles

...ต่อจนครบ 15 วิ — beat ที่ไม่มีบทพูดให้ตัด dialogue line ออก เหลือแค่ action+emotion...
```

#### ชั้น 3 — Output Guard Wall (尾部 — bilingual redundant)

ย้ำ guard หลายภาษา หลาย phrasing (กัน 字幕/BGM หลุด):

```
【画面输出严格要求 - 绝对禁止任何字幕】
画面绝对不显示任何字幕 NO subtitles
不要任何屏幕文字 NO on-screen text
不要对白字幕 NO captions
画面中绝对没有任何文字 NO text on screen

【声音要求】
不要背景音乐 no background music
不要配乐 no BGM / no soundtrack
只保留角色对白和环境音 dialogue and ambient sound only

no grid lines / no overlay / no mesh
[ย้ำ scene constant — เช่น 必须是夜晚黑夜场景不是白天 nighttime night scene dark sky]
cinematic professional camera language
```

#### ทำไมเทคนิคนี้เวิร์ก

| ชั้น | แก้ปัญหาเดิม |
|------|-------------|
| Declaration + ชื่อไทยวงเล็บ | ตัวละครหน้าเปลี่ยน / map ผิดตัว |
| 永远 Consistency Lock | เสื้อผ้า/ลุค drift ระหว่าง beat |
| Per-beat environment anchor | ฉาก/แสงเปลี่ยนกลางคลิป (คืน→วัน) |
| 演技 block | หน้าแข็ง หุ่นยนต์ ไม่มี micro-expression |
| Guard wall (bilingual ×หลาย phrasing) | 字幕/subtitle หลุดบนจอ, BGM โผล่ |

### แบบ B — Timeline 15 วินาที (legacy quick draft)

> ใช้ได้สำหรับ draft เร็ว แต่ของจริงให้ใช้ **แบบ A (Structured)** ด้านบน

```
@[ref ฉาก] 这是角色位置、场景和接下来将要发生的事件的参考

0:00-0:XX : @[ref ตัวละคร](NAME – action description)
[เลนส์] [มุมกล้อง], [action ละเอียด],
"[บทพูด]"

0:XX-0:XX : @[ref ตัวละคร](NAME – action description)
[เลนส์] [มุมกล้อง], [action ละเอียด]

...ต่อจนครบ 15 วิ...

no background music
no grid lines
no overlay
no mesh
cinematic professional camera language
```

### แบบ C — Higgsfield (ภาษาอังกฤษ)

```
Cinematic [มุมกล้อง], [เลนส์] lens,
[ตัวละคร + action],
[อารมณ์],
[สถานที่],
[แสง],
[camera movement],
photorealistic, Netflix cinematography, vertical 9:16
```

### กฎสำคัญ
1. **Default = idle** — ทุก shot ที่มีบทพูด gen เป็น idle (ไม่ขยับปาก) เพราะ lipsync ทำแยก
2. **ตั้งชื่อตัวละครไทย** — `นี่คือ สิงหา` ไม่ใช่ "young Thai man"
3. **ย้ำ object consistency** — `同一把伞` `继续撑着` ทุก timestamp
4. **บทพูดรุนแรง → เอาออก** — เก็บไว้ใส่ TTS + lipsync
5. **Seedance 5 วิ = 1 มุม 1 action** — ไม่ intercut ในคลิปเดียว gen แยกแล้วตัดต่อ
6. **Reference Declaration บนหัวเสมอ** — `@[UUID] 这是[ROLE]（ชื่อไทย）——persistent desc` ก่อนเข้า timeline
7. **Consistency Lock ด้วย 永远** — ย้ำเสื้อผ้า/ลุค/ฉากใน 重要 block กัน drift ระหว่าง beat
8. **Per-beat environment anchor** — ทุก beat ย้ำแสง/ฉากซ้ำ (เช่น 夜晚金色灯光背景)
9. **演技 block ทุกครั้ง** — กันหน้าแข็ง: `自然的微表情、眨眼、呼吸起伏、重心轻微移动`
10. **Guard Wall ท้าย (bilingual)** — NO subtitles ×หลาย phrasing + no BGM ทั้งจีน+อังกฤษ

### Idle Keywords
```
idle状态，自然呼吸，轻微眨眼，极轻微晃动
```

### คำที่ Seedance Block (ห้ามใส่ใน prompt)
```
แจ้งตำรวจ, จับ, คุก, ตาย, ฆ่า, ทำร้าย
凶狠, 威胁, 最后通牒, 强硬, 暴力
```
ใช้คำแทน: `严肃` `认真` `坚定` `不满` `不屑`

---

## Step 6: Gen Voice Design Prompt (ElevenLabs)

### โครงสร้าง

```
A [เพศ] [เชื้อชาติ] [อายุ].
[ลักษณะเสียง — ทุ้ม/แหลม/นุ่ม/คม].
[วิธีพูด — เร็ว/ช้า/หนักแน่น/อ่อนโยน].
[อารมณ์เสียง].
[ลักษณะพิเศษ].
```

---

## Step 7: Export Production Doc

สร้างไฟล์ production doc ที่รวม prompt ทั้งหมด:

```markdown
# [ชื่อเรื่อง] — ตอนที่ X Production Doc

## ตัวละคร
[ตาราง ชื่อ + ลุค + เสื้อผ้า]

## Story 1 — [ชื่อฉาก]
### Shot 1.1
- มุมกล้อง / Lens
- Action
- บทพูด
- Nano Banana Prompt
- Seedance Prompt (中文)
- Higgsfield Prompt (EN)

### Shot 1.2
...
```

---

## /drama scene — Gen ฉากเดียว

เมื่อภูมิบอก scene description มา:

1. ถามว่า: กลางวัน/กลางคืน? indoor/outdoor? ตัวละครไหนบ้าง?
2. Gen prompt ภาพฉาก (ไม่มีคน)
3. Gen prompt ตัวละครในฉาก
4. Gen prompt video (Seedance + Higgsfield)
5. ถ้ามีบทพูด → สร้าง Timeline prompt 15 วิ

---

## /drama character — Gen ตัวละคร

เมื่อภูมิบอกชื่อ + description:

1. Gen character ref prompt (front + side view)
2. ถ้ามีหลายชุด → gen แต่ละชุดแยก
3. Gen voice design prompt
4. สรุปตารางเปรียบเทียบกับตัวละครอื่น (ถ้ามี)

---

## /drama poster — Gen โปสเตอร์

1. ถาม direction ก่อน: dark/bright? minimal/busy? serious/playful?
2. เสนอ 2-3 layout concept ให้เลือก
3. Gen prompt ตาม concept ที่เลือก
4. ไม่ใส่ logo/branding — ภูมิจะใส่เอง

---

## /drama fix — แก้ prompt ที่ติด filter

เมื่อภูมิส่ง prompt ที่ติด filter:

1. ระบุว่าติดชั้นไหน:
   - `识别到你上传的素材中包含人脸信息` → face detection → แก้ ref
   - `你输入的文字不符合平台规则` → text content → แก้คำ
2. แก้ prompt ให้ผ่าน
3. ระบุชัดเจนว่าเปลี่ยนตรงไหน

---

## Output Rules

1. **Prompt ภาพ** → output เป็น code block ``` copy ได้เลย
2. **Prompt video Seedance** → ภาษาจีน เสมอ
3. **Prompt video Higgsfield** → ภาษาอังกฤษ เสมอ
4. **Timeline prompt** → format 0:00-0:XX ทุกครั้ง
5. **ถ้าบทยาว** → แบ่งเป็นหลาย clip (15 วิ/clip) พร้อมบอก flow ตัดต่อ
6. **ทุก prompt** → ต้องมี lens + แสง + vertical 9:16

---

## IMPORTANT — Export เป็นไฟล์ Word (.docx) เสมอ

**เมื่อใช้ `/drama [script.pdf]` หรือ `/drama [script file]` (full pipeline)**:
ผลลัพธ์ทั้งหมดต้อง **export เป็นไฟล์ Word (.docx)** ไม่ใช่แค่แสดงเป็น text ในแชท

### วิธีทำ

1. ติดตั้ง python-docx (ถ้ายังไม่มี): `pip install python-docx`
2. สร้างไฟล์ .docx ด้วย Python script โดยใช้โครงสร้าง Production Doc
3. บันทึกไฟล์ไว้ที่เดียวกับไฟล์บทต้นฉบับ หรือ working directory
4. ชื่อไฟล์: `[ชื่อเรื่อง]_Production_Doc.docx`

### โครงสร้างไฟล์ Word

```
Title: [ชื่อเรื่อง] — ตอนที่ X Production Doc

Section 1: ตัวละคร
  - ตาราง: ชื่อ | ลุค | เสื้อผ้า | Character Ref Prompt

Section 2: Voice Design
  - ตาราง: ชื่อ | ElevenLabs Prompt

Section 3+: Story 1, 2, 3...
  แต่ละ Story มี:
    - Shot number
    - มุมกล้อง / Lens
    - Action + บทพูด
    - Nano Banana Prompt (ในกรอบ)
    - Seedance Prompt 中文 (ในกรอบ)
    - Higgsfield Prompt EN (ในกรอบ)
```

### เมื่อไหร่ต้อง export Word

| Command | Export Word? |
|---------|-------------|
| `/drama [script.pdf]` | **ต้อง** — full pipeline |
| `/drama scene [desc]` | ไม่ต้อง — แสดงในแชทได้ (prompt ไม่เยอะ) |
| `/drama character [name]` | ไม่ต้อง — แสดงในแชทได้ |
| `/drama poster [title]` | ไม่ต้อง — prompt เดียว |
| `/drama fix [prompt]` | ไม่ต้อง — แก้แล้วแสดงเลย |

### สรุปในแชท

หลัง export Word แล้ว ให้สรุปสั้นๆ ในแชท:
```
สร้าง Production Doc เสร็จแล้วครับ!

📄 ไฟล์: วิวาห์โคลน_ตอน2_Production_Doc.docx
📍 ที่: [path]

สรุป:
- ตัวละคร: 6 คน
- Stories: 4 stories
- Shots: 18 shots
- Prompt ทั้งหมด: 54 prompts (ภาพ + Seedance + Higgsfield)
```
