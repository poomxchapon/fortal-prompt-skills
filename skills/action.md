# action — AI Action Movie Prompt Generator

> วิเคราะห์ฉาก Action → เลือกมุมกล้อง + เลนส์ + แสง → Gen Prompt พร้อมใช้

## Usage

```
/action [description]                    # Gen prompt ฉาก action เดียว (ครบ image + video)
/action sequence [description]           # Gen shot sequence หลาย shot ต่อเนื่อง (fight/chase)
/action style [film-reference]           # Gen prompt ตามสไตล์หนัง (john-wick, mad-max, the-raid, etc.)
/action fix [prompt]                     # แก้ prompt ที่ติด content filter
/action ref [description]               # Gen character/environment ref prompt สำหรับ action
```

## What It Does

รับ description ฉาก Action แล้วสร้าง prompt สำหรับ AI Video/Image tools:

```
Description ฉาก Action
  ↓
1. วิเคราะห์ — ประเภท action, จำนวนตัวละคร, สถานที่, อารมณ์
2. เลือก Camera Setup — มุมกล้อง + เลนส์ + camera movement
3. เลือก Lighting + Color Grade — ตาม mood ของฉาก
4. Gen Prompt ภาพ (Nano Banana Pro / Higgsfield)
5. Gen Prompt Video (Seedance 中文 + Higgsfield EN)
6. Speed/Slow-mo Guide — ถ้าฉากต้องการ
```

---

## IMPORTANT — อ่านก่อนทำงาน

ก่อนสร้าง prompt ต้องอ่าน Action Cinematography Guide:
```
ψ/learn/action-cinematography-ai-prompt-guide.md
```
ไฟล์นี้มีข้อมูลมุมกล้อง, เลนส์, แสง, สไตล์ทั้งหมดที่ต้องใช้

---

## Golden Rules (กฎทอง)

1. **1 shot = 1 action = 1 camera angle** — ห้ามยัดหลาย action ใน prompt เดียว
2. **ต้องมี lens ทุก prompt** — `"[X]mm lens"` เสมอ ไม่งั้น AI สุ่ม perspective
3. **ต้องมี lighting ทุก prompt** — ระบุ light source + mood ไม่งั้นได้ flat
4. **Seedance < 60 คำ** — สั้น precise ดีกว่ายาว (ยกเว้น timeline prompt — ดูข้อ 7)
5. **ห้าม combine orbit + zoom** — geometry warp, เลือกอย่างเดียว
6. **บอก speed ของ camera** — `"slow dolly"` `"rapid pan"` ไม่ใช่แค่ `"camera moves"`
7. **🔴 MANDATORY: ทุก video prompt ต้องมี Timeline Breakdown** — ระบุเวลาเป็นช่วงๆ (e.g., `0:00-0:03`, `0:03-0:06`) บอกว่าตอนไหนเกิดอะไร + speed (NORMAL/SLO-MO/FREEZE) — applies ทั้ง single shot และ sequence — ดูรายละเอียดที่ section "Timeline Prompt Pattern" ด้านล่าง
8. **Seedance multi-char / มี @ref → ใช้ Structured Header** — Declaration (UUID+ชื่อไทย) + Consistency Lock (永远) + 演技 block + Guard Wall ห่อหุ้ม timeline beats — ดู section "Seedance Structured Header" ด้านล่าง

---

## Prompt Structure (โครงสร้าง Prompt)

### ลำดับที่ AI ตอบสนองดีที่สุด

```
[Shot type] + [Focal length] lens,
[Character description] [Action verb],
[Location/Environment],
[Camera movement + speed],
[Lighting],
[Atmospheric FX / particles],
[Color grade / Visual style],
cinematic, no text, no watermark
```

### Quick Template

```
[SHOT], [LENS],
[WHO] [DOES WHAT],
[WHERE],
[CAMERA],
[LIGHT],
[FX],
[STYLE], cinematic, no text, no watermark
```

---

## 🔴 Timeline Prompt Pattern (MANDATORY)

> **กฎทอง #7**: ทุก video prompt ต้องระบุ timeline breakdown — บอกเป็นช่วงเวลาว่าตอนไหนเกิดอะไร

### ทำไมต้อง Timestamp?

- **AI Video model (Seedance/Higgsfield/Kling) จะ map time → action ตรงๆ** เมื่อเห็น timestamp ใน prompt
- **Speed ramp ทำงานแม่นกว่า** — model รู้ว่าวินาทีไหนต้อง slow-mo
- **Pacing ตรงใจ** — ไม่ต้อง guess ว่า action จะเกิดที่ second ไหน
- **ภูมิ tune ง่าย** — แก้แค่ beat เดียวได้ ไม่ต้องเขียนใหม่ทั้ง prompt

### Timeline Template (Single Shot, 15s)

```
[Overall shot description — 2-3 lines: shot type + lens + lighting + color grade + aspect ratio]

0:00-0:03 — [Beat 1: Setup / entry] [SPEED: NORMAL]
0:03-0:06 — [Beat 2: Action develops] [SPEED: NORMAL]
0:06-0:08 — [Beat 3: Tension build] [SPEED: RAMP DOWN]
0:08-0:11 — [Beat 4: Peak moment] [SPEED: ULTRA SLO-MO]
0:11-0:13 — [Beat 5: Resolution] [SPEED: SNAP BACK to NORMAL]
0:13-0:15 — [Beat 6: Settle / freeze] [SPEED: NORMAL → FREEZE]

[Style anchors + cinematic, no text, no watermark]
```

### Timeline Template (Sequence, 15s with multiple shots)

```
0:00-0:02 : @[ref] [LENS] [SHOT TYPE], [Chinese/EN action description]
0:02-0:04 : 切换 @[ref] [LENS], [next beat]
0:04-0:06 : 切回 [LENS] [SHOT TYPE], [continues]
0:06-0:08 : @[ref] [LENS] MACRO INSERT, [detail — ULTRA SLO-MO]
0:08-0:10 : 切换 [LENS] ECU REACTION, [emotion]
0:10-0:13 : 切回 [LENS] WIDE PAYOFF, [result]
0:13-0:15 : 定格 FREEZE FRAME, [end visual]
```

### Beat Map (สรุปสั้น — ใส่ท้าย prompt)

```
0:00 ─┬─ [Beat 1 name]
0:03 ─┼─ [Beat 2 name]
0:06 ─┼─ [Beat 3 name]  ◀ Build
0:08 ─┼─ ⚡ [Peak moment] ▶ SLO-MO
0:11 ─┼─ [Recovery]
0:13 ─┼─ [Exit]
0:15 ─┴─ FREEZE
```

### Rules for Timeline Prompts

| Rule | Why |
|------|-----|
| **ทุก beat ต้องมี speed marker** | NORMAL / SLOW BUILDUP / ULTRA SLO-MO / SPEED SNAP / FREEZE |
| **Peak moment = ULTRA SLO-MO** | สำหรับ impact / wow / reveal — มักอยู่ระหว่าง 0:07-0:11 |
| **Freeze ตอนจบ** | ภาพสุดท้ายค้าง = legendary feel |
| **Beat ละ 2-3 วินาที** | < 1.5s = สั้นเกินไป, > 4s = model จะ drift |
| **ระบุ camera motion ต่อ beat** | ถ้ามี camera move เปลี่ยนระหว่าง shot |
| **Sequence ใช้ 切换/切回** | Seedance รู้ว่า cut to / cut back |
| **Single shot ไม่ใช้ 切换** | 切换 = ตัดไปอีก shot, single shot ใช้แค่ pacing |

### Single Shot vs Sequence — เลือกยังไง?

| Pattern | ใช้ตอน | Example |
|---------|--------|---------|
| **Single Shot Timeline** | 1 ref + 1 continuous shot | Immersive installation, hero shot, slow-mo reveal |
| **Sequence Timeline** | หลาย ref + intercut | Fight, chase, multi-character action |

### Common Speed Patterns

```
Pattern A — Build to Peak (most cinematic):
NORMAL → NORMAL → RAMP DOWN → ULTRA SLO-MO → SNAP BACK → NORMAL → FREEZE

Pattern B — Cold Open (start with peak):
ULTRA SLO-MO → SNAP TO NORMAL → NORMAL → NORMAL → SLO-MO → FREEZE

Pattern C — Continuous Reveal (no slo-mo):
NORMAL → NORMAL → NORMAL → NORMAL → NORMAL → FREEZE (camera-driven only)
```

---

## Seedance Structured Header & Guard Wall (声明层 + Consistency Lock) ⭐

> ใช้คู่กับ Timeline Prompt Pattern ด้านบน — **header + lock ห่อหุ้ม timeline beats (ที่มี speed marker)**
> แก้ปัญหา: ตัวละครสลับชุด / ลุค drift ระหว่าง beat / หน้าแข็ง / แสงเปลี่ยนกลางคลิป / 字幕หลุด
> ใช้เมื่อ Seedance clip มี @ref ตัวละคร (โดยเฉพาะ sequence หลายคน)

### ชั้น 1 — Reference Declaration (头部)

```
@[UUID_SCENE] 这是场景参考——[สถานที่+เวลา+แสง+mood ละเอียด]
@[UUID_X] 这是[ROLE]（[ชื่อไทย]）——[เสื้อผ้า/ชุดรบ + 泰国男性/女性 + อายุ岁 + ทรงผม]
```
- ชื่อไทยในวงเล็บ → map ตัวละครแม่น
- ⚠️ ชุดรบ/อาวุธเด่นในรูป ref → ระวัง image filter (ดู `/action fix`) — ถ้าโดน reject ให้ describe ใน text แทน

### ชั้น 1.5 — Lock + Acting + Lighting (【】块)

```
【光线要求】
[lock แสง+เวลา ย้ำ non-negotiable — เช่น 必须是夜晚霓虹冷光，绝对不是白天]

重要 (Consistency Lock — 永远):
- [角色A]永远穿[ชุด/เกราะ/อาวุธคงที่]
- 场景必须是[environment คงที่]

【演技要求】
表演自然真实生动不僵硬，
自然的微表情、呼吸起伏、肌肉发力、重心移动、关节发力真实
```
> action เพิ่ม `肌肉发力` (muscle exertion) + `关节发力真实` เข้า acting block → ให้ฟีลออกแรงจริง ไม่ลอย

### ชั้น 2 — Beats (speed marker + per-beat anchor)

ทุก beat ย้ำแสง/ฉากซ้ำ + **คง speed marker เดิม** (`[速度: 超慢动作]`):

```
0:08-0:11 : @[UUID_X] [LENS][SHOT]，[ย้ำแสง/ฉาก]，
[action verb + 肌肉发力]，[速度: 超慢动作]
```

### ชั้น 3 — Guard Wall (尾部 bilingual)

```
no subtitles / no on-screen text / no captions
no background music / no BGM / no soundtrack
no grid lines / no overlay / no mesh
[ย้ำ scene constant]
cinematic professional camera language
```

---

## Camera Angle Selection (เลือกมุมกล้องตามอารมณ์)

> 📷 **ภาษากล้องเต็ม** (shot size · angle · height · movement · lens · composition · 9:16 · when-NOT-to-use): `.claude/skills/_shared/master-camera-reference.md` — ตารางด้านล่างคือชุดที่ /action ใช้บ่อย

| มุมกล้อง | อารมณ์ | ใช้ตอน | Prompt Keyword |
|----------|--------|--------|----------------|
| **Low Angle** | ยิ่งใหญ่ ทรงพลัง | Hero moment, ตัวร้ายปรากฏ | `low angle shot` |
| **High Angle** | อ่อนแอ vulnerable | ถูกล้อม, แพ้, ล้ม | `high angle shot` |
| **Bird's Eye** | Tactical, god-view | เปิดสมรภูมิ, choreography | `bird's eye view` / `top-down shot` |
| **Dutch Angle** | สับสน บ้าคลั่ง | Chaos, villain, chase | `dutch angle, tilted horizon` |
| **OTS** | Confrontation | Stare-down, ก่อนสู้ | `over-the-shoulder shot` |
| **POV** | Immersive | ถูกไล่, วิ่งหนี, หมัดเข้าหน้า | `first-person POV shot` |
| **Close-Up / ECU** | Emotion, detail | ตาเบิกกว้าง, นิ้วกดไก | `extreme close-up` |
| **Wide** | Scale, context | เปิดฉาก, 2 ฝ่ายเผชิญหน้า | `extreme wide shot` |

### Variations ที่ใช้บ่อย

```
"extreme low angle"     → กล้องแทบวางพื้น
"slight low angle"      → heroic แต่ไม่ over
"worm's eye view"       → กล้องวางพื้นเลย
```

---

## Lens Selection (เลือกเลนส์ตามฉาก)

| Focal | ชื่อ | ใช้ตอน (Action) | Prompt |
|-------|------|----------------|--------|
| **12-16mm** | Ultra Wide | Establishing, chase, explosion panorama | `ultra wide, 16mm lens` |
| **20-24mm** | Wide | Low angle hero, fight tight space, POV | `wide angle, 24mm lens` |
| **28-35mm** | Moderate Wide | Group fight, action + environment | `35mm lens` |
| **50mm** | Standard | OTS, tracking, confrontation | `50mm lens` |
| **85mm** | Medium Tele | Reaction, emotional beat, face | `85mm lens, shallow DOF` |
| **100mm** | Macro | มือจับอาวุธ, insert shot | `100mm macro lens` |
| **135-200mm** | Telephoto | ไล่ล่า (compression), sniper | `200mm telephoto` |
| **Anamorphic** | Anamorphic | ทุกฉากที่อยากได้ feel "หนังจริง" | `anamorphic lens, lens flare, 2.39:1` |

### เลือกเลนส์ตามประเภทฉาก

**Chase:**
```
เปิดฉาก: 16mm → เห็น location ทั้งหมด
วิ่งตาม: 24mm tracking → dynamic
ปะทะ:   85mm close-up → reaction/impact
จบ:     200mm telephoto → compression effect
```

**Hand-to-Hand:**
```
เปิดฉาก: 35mm → เห็น 2 คน + environment
สู้กัน:  24mm handheld → in-the-action
Reaction: 85mm → isolate อารมณ์
Insert:  100mm → กำปั้น, หมัดปะทะ
```

**Explosion:**
```
ก่อน:     50mm → ตัวละครสังเกตสิ่งผิดปกติ
ระเบิด:   16mm ultra wide → scale
Aftermath: 35mm tracking → เดินผ่านซาก
Detail:   100mm → เศษ, ไฟ, ฝุ่น
```

---

## Camera Movement (การเคลื่อนกล้อง)

| Movement | อารมณ์ | Prompt Keyword |
|----------|--------|----------------|
| **Tracking** | ตามติด เร่งรีบ | `tracking shot following [char]` |
| **Dolly In** | เพิ่ม intensity | `slow dolly-in over 4 seconds` |
| **Dolly Out** | Reveal scale | `dolly-out revealing destruction` |
| **Orbit** | Epic hero moment | `orbiting camera, 360-degree arc` |
| **Crane** | ยกขึ้น reveal / ลงมา intimate | `crane shot rising` |
| **Whip Pan** | ฉับพลัน ตกใจ | `whip pan, rapid horizontal swing` |
| **Steadicam** | ลื่นไหล elegant | `Steadicam, smooth continuous` |
| **Crash Zoom** | ช็อก เน้นจุด | `rapid crash zoom into face` |
| **Dolly Zoom** | Disorienting, panic | `dolly zoom, vertigo effect` |

---

## Lighting Presets (แสงสำหรับ Action)

| Lighting | ฟีล | Prompt Keywords |
|----------|-----|-----------------|
| **Backlight/Rim** | Silhouette, dramatic | `strong backlight, rim light on edges, silhouette` |
| **Practical** | สมจริง, industrial | `lit by practical lights, flickering fluorescent` |
| **Volumetric** | แสงลอดฝุ่น, mystical | `volumetric light beams, dust particles illuminated` |
| **Neon** | Cyberpunk, nightclub | `neon-lit, pink and cyan light, wet reflections` |
| **Strobe** | Chaotic, disorienting | `strobe light effect, intermittent flashes` |
| **Fire** | ร้อน dramatic | `lit by raging fire, orange flickering, embers` |
| **Moonlight** | เย็น mysterious | `cold moonlight, blue-silver tone, noir` |
| **Mixed Temp** | Visual tension | `warm tungsten left, cool blue right, split lighting` |

### Cheat Sheet (keyword สั้น)

```
"dramatic side lighting"     → เงาครึ่งหน้า
"top-down harsh light"       → เงาลึก ใต้ตามืด
"under-lighting"             → villain look น่ากลัว
"golden hour backlight"      → แสงทอง ตอนเย็น
"single source key light"    → dramatic มาก
"rim light separation"       → ขอบตัวเรือง แยกจาก BG
```

---

## Color Grading (โทนสี)

| Style | ฟีล | ใช้กับ | Prompt |
|-------|-----|-------|--------|
| **Teal & Orange** | Hollywood blockbuster | ฉาก action ทั่วไป | `teal and orange color grade` |
| **Desaturated** | โหด สมจริง war | Military, street fight | `desaturated bleach bypass, gritty` |
| **Cold Blue** | เย็นเฉียบ clinical | Sci-fi, assassin | `cold steel blue, metallic sheen` |
| **B&W High Contrast** | Graphic novel, art | Stylized fight | `high contrast black and white, noir` |
| **Warm Amber** | ย้อนยุค dusty | Desert, western | `warm amber, golden desert tones` |
| **Neon Saturated** | Cyberpunk stylish | Nightclub, neon city | `hyper-saturated neon, vivid pink and blue` |

### Quick Keywords

```
"cinematic color grade"     → ปลอดภัย blockbuster look
"crushed blacks"            → เงาดำสนิท
"film emulation"            → เหมือนฟิล์ม analog
"cross-processed"           → สีเพี้ยนแบบตั้งใจ
"split toning"              → สีต่างกันใน highlight/shadow
```

---

## Speed & Slow-Motion

| Keyword | Effect |
|---------|--------|
| `"24fps cinematic"` | ฟีลหนังมาตรฐาน |
| `"60fps ultra smooth"` | ลื่นมาก เห็น detail |
| `"120fps feeling"` | Slow-mo feel |
| `"ultra slow motion"` | ช้ามากเห็นทุก detail |
| `"overcranked"` | ภาษาหนังของ slow-mo |
| `"speed ramping"` | เร็ว→ช้า→เร็ว (Zack Snyder/Guy Ritchie) |

### Slow-Mo Prompt Patterns

```
# Basic
"ultra slow motion, every movement stretched in time"

# With detail
"slow motion 120fps, water droplets frozen, fabric rippling"

# Speed ramp
"velocity ramp — normal speed charge,
slowing to ultra-slow-motion at impact,
snapping back to full speed on recovery"

# Freeze frame
"freeze frame at peak action, mid-air,
dust particles suspended, time stopped"
```

---

## Action Keywords Library (คลังคำ)

### Impact & Combat
```
"bone-crushing impact"       → หนักแน่น
"visceral combat"            → ดิบ เจ็บจริง
"fluid martial arts"         → นุ่ม ลื่น สวย
"explosive hand-to-hand"     → หมัดถี่ เร็ว
"precise choreography"       → ท่าต่อสู้ออกแบบมา
"gritty street fight"        → ข้างถนน ไม่มีกฎ
"sword clash with sparks"    → ดาบกระทบ ประกาย
"devastating finishing blow"  → หมัดจบ
```

### Movement & Chase
```
"parkour through urban jungle" → วิ่งข้ามสิ่งกีดขวาง
"high-speed pursuit"          → ไล่ล่าความเร็วสูง
"desperate sprint"            → วิ่งสุดชีวิต
"acrobatic dodge"             → หลบแบบกายกรรม
"leaping between rooftops"    → กระโดดข้ามหลังคา
"wall-running"                → วิ่งบนผนัง
```

### Destruction & Explosion
```
"massive explosion erupting"  → ระเบิดครั้งใหญ่
"shockwave rippling outward"  → คลื่นกระแทก
"debris flying through air"   → เศษซากลอย
"glass shattering in slow-mo" → กระจกแตก
"sparks showering down"       → ประกายไฟกระจาย
"dust cloud billowing"        → ฝุ่นม้วนตัว
```

### Atmosphere
```
"rain-soaked street"          → ถนนเปียกฝน
"smoke-filled corridor"       → ทางเดินมีควัน
"wind-swept battlefield"      → สนามรบลมพัด
"fog-shrouded arena"          → สังเวียนในหมอก
"snow falling during fight"   → หิมะตกระหว่างสู้
```

### Particles & VFX
```
"floating embers"             → ประกายไฟลอย
"dust particles in light"     → ฝุ่นในลำแสง
"muzzle flash"                → แฟลชปากกระบอกปืน
"energy wave"                 → คลื่นพลังงาน (fantasy)
"speed lines"                 → เส้นความเร็ว (anime)
"motion trails"               → เส้นตามการเคลื่อนไหว
```

---

## Film Style Presets

เมื่อภูมิใช้ `/action style [film]` → ใช้ preset เหล่านี้:

### John Wick (Neo-Noir Action)
```
Camera: Steadicam + tracking, low angle
Lens: 35mm anamorphic
Light: Neon backlight, wet reflections, cyan/magenta
Grade: Neon saturated, high contrast
Speed: Normal + slow-mo on kills
FX: Shell casings, wet floor, neon glow
```

### Mad Max (Desert Chaos)
```
Camera: Low mounted, tracking, whip pan
Lens: 16mm ultra wide
Light: Harsh golden hour, lens flare
Grade: Warm amber, desaturated, film grain
Speed: Speed ramping (Snyder style)
FX: Dust trail, debris, fire, sand
```

### The Raid (Raw Corridor)
```
Camera: Handheld, shaky, tight tracking
Lens: 28mm
Light: Practical fluorescent, gritty
Grade: Desaturated, documentary feel
Speed: Normal (raw realism)
FX: Blood spray (ระวัง filter), sweat
```

### Matrix (Bullet Time)
```
Camera: Orbit + freeze, dolly zoom
Lens: 50mm
Light: Volumetric green-tinted
Grade: Cold green/blue
Speed: Bullet time, freeze frame
FX: Bullets mid-flight, air trails, shockwave
```

### 300 / Snyder (Hyper-Stylized)
```
Camera: Speed ramp tracking, low angle
Lens: 35mm
Light: Chiaroscuro, dramatic side
Grade: Desaturated + high contrast, sepia
Speed: Speed ramping (signature)
FX: Blood splatter (stylized), dust, sparks
```

### Samurai / Wuxia (Elegant Action)
```
Camera: Wide tracking, dolly in at clash
Lens: 35mm wide → 85mm at clash moment
Light: Cold moonlight, volumetric mist
Grade: Cold blue, high contrast
Speed: Slow-mo at sword clash
FX: Sparks from blade, fabric flow, mist
```

### Anime Action (2D/2.5D Style)
```
Camera: Dynamic angles, crash zoom
Lens: 24mm (exaggerated perspective)
Light: Dramatic rim light, bold shadows
Grade: High saturation, cel-shaded
Speed: Speed lines + impact frames
FX: Energy trails, radial speed lines, wind
```

### One-Shot (1917 / Oldboy)
```
Camera: Steadicam continuous, no cuts
Lens: 28-35mm
Light: Natural/practical, changing as character moves
Grade: Cinematic neutral
Speed: Real-time (no slow-mo)
FX: Environment interaction, debris
```

---

## Step-by-Step: Gen Prompt

### /action [description]

เมื่อภูมิบอก description ฉาก action:

1. **วิเคราะห์ฉาก**
   - ประเภท: hand-to-hand / chase / explosion / gunfight / sword / supernatural?
   - ตัวละคร: กี่คน? ลักษณะ?
   - สถานที่: indoor/outdoor? กลางวัน/กลางคืน?
   - อารมณ์: epic / gritty / elegant / chaotic?

2. **เลือก Camera Setup**
   - มุมกล้อง → ตามอารมณ์ (ดูตาราง)
   - เลนส์ → ตามประเภทฉาก
   - Camera movement → ตามจังหวะ

3. **เลือก Visual Style**
   - Lighting → ตาม setting + mood
   - Color grade → ตาม genre
   - Speed → ต้อง slow-mo ไหม?
   - FX/particles → มีอะไรในฉาก?

4. **Gen Prompt 3 แบบ** (🔴 Video prompts ต้องมี timeline — ดู Golden Rule #7)

   **Image Prompt (Nano Banana / Higgsfield) — static, ไม่ต้อง timeline:**
   ```
   Cinematic [มุมกล้อง], [เลนส์] lens,
   [ตัวละคร + action],
   [สถานที่],
   [แสง],
   [FX/particles],
   [color grade], photorealistic, vertical 9:16
   ```

   **Video Prompt — Seedance (中文) — MUST have timeline:**
   ```
   [总体描述 — shot type + 镜头 + 灯光 + 色调 + 画幅]

   0:00-0:03：[Beat 1 description] [速度: 正常]
   0:03-0:06：[Beat 2 description] [速度: 正常]
   0:06-0:08：[Beat 3 description] [速度: 渐慢]
   0:08-0:11：[Beat 4 — PEAK] [速度: 超慢动作]
   0:11-0:13：[Beat 5] [速度: 速度回正]
   0:13-0:15：[Beat 6 — FREEZE] [速度: 定格]

   电影质感, no text, no watermark, no overlay, no background music,
   cinematic professional camera language
   ```

   **Video Prompt — Higgsfield (EN) — MUST have timeline:**
   ```
   [Overall shot description — shot type + lens + lighting + color grade + aspect ratio]

   0:00-0:03 — [Beat 1 description] [SPEED: NORMAL 24fps]
   0:03-0:06 — [Beat 2 description] [SPEED: NORMAL 24fps]
   0:06-0:08 — [Beat 3 description] [SPEED: RAMP DOWN]
   0:08-0:11 — [Beat 4 — PEAK] [SPEED: ULTRA SLO-MO 120fps]
   0:11-0:13 — [Beat 5] [SPEED: SNAP BACK to NORMAL]
   0:13-0:15 — [Beat 6 — FREEZE] [SPEED: NORMAL → FREEZE]

   cinematic, [style anchors],
   no text, no watermark, no subtitles
   ```

5. **เพิ่ม Beat Map** ท้าย output — สรุปสั้น (ดู Timeline Prompt Pattern section)

6. **แนะนำ** — shot ก่อน/หลัง ถ้าเป็น sequence

---

### /action sequence [description]

เมื่อภูมิบอก action sequence (หลาย shot):

1. **แบ่ง Shot List** — แต่ละ beat = 1-3 วินาที ใน clip 15 วินาที
2. **เลือก Lens Progression** — เปลี่ยนเลนส์ทุก beat ไม่ซ้ำติดกัน
3. **Intercut Map** — แผนผังตัดสลับ visual แบบ tree
4. **Speed Map** — กราฟ speed ทุกวินาที
5. **Sound Design** — เสียง per timestamp
6. **Start Frames** — image prompts สำหรับ key moments

### Full Sequence Output (5 ส่วนครบ)

เมื่อ gen sequence ต้องให้ครบ **5 deliverables** ทุกครั้ง:

#### 1. Seedance Prompt (ภาษาจีน + Timestamp)

```
@[char1 ref] 这是[NAME]——[brief description]
@[char2 ref] 这是[NAME]——[brief description]
@[scene ref] 这是场景参考——[scene description]

0:00-0:02 : @[ref](NAME – action description) [LENS] [SHOT TYPE]，
[detailed Chinese action description]

0:02-0:04 : 切换 @[ref](NAME – action) [LENS]，
[next beat with intercut using 切换/切回]

0:04-0:06 : 切回 [LENS] [SHOT TYPE]，
[action continues]

...

no background music
no grid lines
no overlay
no mesh
cinematic professional camera language
```

**กฎ Seedance Prompt:**
- **切换** = cut to (ตัดไปอีกมุม/ตัวละคร)
- **切回** = cut back (ตัดกลับ)
- **ทุก beat ต้องมี lens** — ระบุ mm ชัดเจน
- **@ ref ทุกครั้งที่ตัวละครปรากฏ** ใน beat นั้น
- **ลงท้ายด้วย** no background music / no grid lines / no overlay / no mesh / cinematic professional camera language
- **Intercut ≥ 8 cuts ต่อ 15 วินาที** — ตัดทุก ~1.5 วินาที
- **Reaction shots สำคัญ** — ต้องมี CU reaction ทั้ง 2 ฝ่ายก่อนและหลัง impact

#### 2. Intercut Map

```
ACTION A (lens) .................. description
  ↓ 切换
REACTION B CU (lens) ............. description
  ↓ 切回
WIDE clash (lens) ................ description
  ↓ 切换
INSERT macro detail (lens) ....... description
  ↓ 切换
ECU ตา reflection (lens) ......... description
  ↓ 切回
RESULT wide (lens) ............... description
  ↓
FREEZE (lens) .................... END
```

#### 3. Speed Map

```
0:00 ████████░░ ปกติ      — setup/buildup
0:03 ██████████ เร็วมาก   — attack launch
0:05 ░░░░░░░░░░ ULTRA SLO  — MACRO impact detail
0:07 ░░░░████░░ SLO→เร็ว  — reversal moment
0:09 ██████████ เร็วจัด   — explosion/payoff
0:11 ░░░░░░████ SLO-MO    — aftermath float
0:14 ░░░░░░░░░░ FREEZE    — end frame
```

**กฎ Speed:**
- ปกติ → เร็ว → **ULTRA SLO ตอน impact** → เร็ว → SLO-MO → FREEZE
- MACRO insert = ALWAYS ultra slow-mo
- Speed snap (ช้า→เร็วทันที) สร้าง shock effect

#### 4. Sound Design

```
0:00 — [ambient: wind, footsteps, breathing]
0:02 — [whoosh/charge-up sound]
0:04 — [silence 0.3s — tension]
0:05 — [IMPACT: THUD/CLANG/CRACK + bass hit]
       [slo-mo: low-frequency rumble + heartbeat]
0:08 — [reverse sound effect = energy absorbed]
0:09 — [EXPLOSION: bass drop + debris sounds]
0:12 — [settle: wind, distant rumble, small debris ting ting]
0:14 — [single heartbeat: THUMP]
0:15 — [complete silence]
```

**กฎ Sound:**
- **Sound design ดิบๆ > เพลงประกอบ** สำหรับฉากต่อสู้
- **ทุก impact ต้องมีเสียง** — THUD (หมัด), CLANG (โลหะ), CRACK (กระดูก/เกราะ)
- **Silence before impact** — เงียบ 0.3 วินาทีก่อนชน = ตื่นเต้นกว่า
- **Heartbeat** = tension marker
- **Reverse sound** = พลังถูกดูดกลับ/สะท้อน
- **จบด้วย silence** ทุกครั้ง

#### 5. Start Frames (Image Prompts)

Gen 3-4 start frames ต่อ clip สำหรับ key moments:

```
[Art style] [shot type], [lens] lens,
[character description + action pose],
[environment/arena],
[lighting],
[VFX/particles],
[color grade], [aspect ratio]
```

> แนบ: character refs + scene ref ทุกครั้ง

### Shot Sequence Template (Legacy — ใช้ได้สำหรับ quick draft)

```markdown
## Shot 1 — [ชื่อ shot]
- **เลนส์**: 35mm | **มุม**: Wide | **Movement**: Tracking
- **Action**: [อะไรเกิดขึ้น]
- **ต่อกับ Shot 2 ยังไง**: [cut / whip pan / match cut]

[Image Prompt]
[Seedance Prompt]
[Higgsfield Prompt]

## Shot 2 — [ชื่อ shot]
...
```

---

## Round Transition (Remotion — HP Update Clips)

สำหรับ battle video ที่มีหลาย round ใช้ **Remotion render mp4** เป็น transition คั่นระหว่าง round

### Flow

```
[Seedance 15s]  Round combat
      ↓
[Remotion 4s]   HP transition (mp4)
      ↓
[Seedance 15s]  Next round combat
```

### วิธี Render

```bash
cd dreamfight/tools/remotion-battle
npm run studio          # Preview ใน browser
npm run render-all      # Render ทุก round → out/*.mp4
# หรือ render ทีละ round:
npx remotion render src/index.ts Round1 out/round1.mp4
```

### ไฟล์ที่ได้

```
out/
├── round1.mp4  — 4s, 1080p, 30fps
├── round2.mp4
├── ...
└── round6.mp4
```

### แก้ไขข้อมูล Battle

แก้ที่ `src/Root.tsx` → array `ROUNDS` — เปลี่ยน HP, skill, damage, winner, event ได้เลย

```typescript
{
  roundNumber: 4,
  p1: { name: "ภูมิ", portrait: "poomSPK.png", hpBefore: 116, hpAfter: 116, maxHp: 150, skill: "กระทิงโทสะ", damageDealt: 35 },
  p2: { name: "เต้", portrait: "Tae007.png", hpBefore: 131, hpAfter: 96, maxHp: 150, skill: "Constitutional Shield", damageDealt: 0 },
  winner: "p1",
  event: "⚡ CRITICAL 18/18 — STUNNED!",
}
```

### Animation Timeline (120 frames @ 30fps = 4s)

```
0.0s — BG fade in + neon glow
0.3s — "ROUND X" slam in + shake
0.6s — P1 portrait slide from left + P2 from right
1.0s — HP bars appear
1.5s — HP bars drain to new value
2.0s — Damage numbers fly in "-XX DMG"
2.5s — Skill names appear
3.0s — Event text (CRITICAL/STUNNED) if any
3.2s — Winner text pulses
3.5s — Everything fades out
4.0s — Black → cut to next Seedance clip
```

### เปลี่ยนตัวละคร

1. ใส่รูป portrait ใหม่ใน `public/`
2. แก้ `portrait: "filename.png"` ใน `src/Root.tsx`
3. Re-render

### เมื่อไหร่ใช้ Remotion vs Seedance

| Clip Type | ใช้ Tool | ทำไม |
|-----------|---------|------|
| ฉากต่อสู้ action | **Seedance** | ต้องการ cinematic + character animation |
| Transition HP update | **Remotion** | UI animation ชัด แม่น data ถูกต้อง |
| Result screen winner | **Remotion** | Stats + portrait + data display |
| Hologram UI (ถ้าอยาก gen) | **Seedance** | แนบแค่ scene ref ไม่ใส่ char ref |

---

## Intercut Techniques (เทคนิคตัดสลับฉาก)

การตัดสลับคือหัวใจของ action ที่ดี — ไม่ใช่แค่เล่าเส้นตรง A→B→C

### Pattern: Tension → Impact → Reaction

```
1. SETUP — ทั้ง 2 ฝ่ายเตรียมตัว (สลับ CU ทั้งคู่)
2. INSERT — detail อาวุธ/มือ/ตา (MACRO 100mm)
3. SILENCE — เงียบ 0.3 วินาที (tension สูงสุด)
4. ATTACK — wide shot action เร็ว (24mm)
5. MACRO IMPACT — ultra slo-mo จุดปะทะ (100mm)
6. ECU REACTION — ตาเห็น result ใน pupil (135mm)
7. PAYOFF — wide ผลลัพธ์ (24mm)
8. SETTLE/FREEZE — aftermath (35-50mm)
```

### Intercut Rules

| Rule | ทำไม |
|------|------|
| **≥ 8 cuts ต่อ 15 วินาที** | ต่ำกว่านี้รู้สึกช้า |
| **Reaction BEFORE payoff** | เห็นหน้าตกใจก่อนเห็นผล = ตื่นเต้นกว่า |
| **Villain smile → Hero calm** | สร้าง contrast ก่อน reversal |
| **Insert detail ก่อน impact** | มือกำ, ตาเบิก, อาวุธเรืองแสง = buildup |
| **ECU ตา + reflection** | เห็นพลังสะท้อนใน pupil = cinematic detail |
| **ไม่ซ้ำเลนส์ติดกัน** | 85→50→16→135→100→24 ไม่ใช่ 85→85→50 |
| **จบด้วย FREEZE เสมอ** | ภาพสุดท้ายค้าง = legendary feel |

### Intercut Shorthands (ใช้ใน Seedance prompt)

| จีน | ความหมาย | ใช้ตอน |
|-----|---------|--------|
| `切换` | Cut to | ตัดไปมุม/ตัวละครใหม่ |
| `切回` | Cut back | ตัดกลับมุมเดิม |
| `快速切换三个角度` | Rapid 3-angle cut | Chaos moment |
| `超慢动作` | Ultra slow motion | Impact detail |
| `速度突然加快` | Speed suddenly increases | After slo-mo snap |
| `定格` | Freeze frame | End frame |

---

### /action style [film-reference]

เมื่อภูมิบอกชื่อหนัง:

1. **ดึง preset** จาก Film Style Presets ด้านบน
2. **ถามว่า**: ฉากไหน? ตัวละครอะไร? สถานที่?
3. **Gen prompt** ตาม preset ของหนังนั้น + ฉากที่ภูมิบอก
4. **ถ้าหนังไม่มีใน preset** → วิเคราะห์สไตล์จากความรู้ cinematography แล้วสร้าง preset ใหม่

---

### /action fix [prompt]

เมื่อภูมิส่ง prompt ที่ติด filter:

1. **ระบุว่าติดอะไร:**
   - Face detection → แก้ ref image approach
   - Text content → แก้คำรุนแรง
   - Violence → tone down + brighten/desaturate ref
   - **Image rejection** → รูป ref มีอาวุธ/ชุดเกราะ/ท่าก้าวร้าว

2. **คำที่ Seedance มักจะ block:**
   ```
   血 (blood), 死 (die), 杀 (kill), 暴力 (violence), 枪 (gun)
   → แทนด้วย: 动作冲击, 激烈对决, 防御反击, 武器
   
   焦黑 (charred), 火焰痕迹 (fire traces), 冲击波 (shockwave)
   → แทนด้วย: 痕迹 (traces), 裂纹 (cracks), 水雾 (mist)
   
   血红色 (blood-red), 毁灭 (destroy), 废墟 (ruins)
   → แทนด้วย: 橙红色夕阳 (sunset orange), 古代建筑群 (ancient architecture)
   
   Dark/threatening ref image
   → brighten + desaturate ก่อนส่ง
   ```

3. **Image Rejection (รูป ref โดน reject)**
   ```
   ⚠ Error: "你上传的图片不符合平台规则"
   = รูปที่อัพโหลดไม่ผ่าน (ไม่ใช่ text)
   
   สาเหตุ: รูปมีอาวุธ, ชุดเกราะ, ท่าก้าวร้าว, เลือด, ความรุนแรง
   
   วิธีแก้:
   - ลดจำนวน ref image — ใช้แค่ scene ref อย่างเดียว
   - ถ้าต้องใช้ character ref → crop เฉพาะหน้า/ครึ่งตัวบน ไม่รวมอาวุธ
   - ถ้า character มีอาวุธเด่นมาก → ไม่แนบ ref เลย ใช้ text describe แทน
   - Brighten + desaturate รูป ref ก่อนอัพ
   ```

4. **Gen prompt ใหม่** + บอกชัดว่าเปลี่ยนตรงไหน

---

## Seedance Content Filter Cheatsheet

### Text Filter (คำต้องห้าม → คำแทน)

| ❌ โดน Block | ✅ ใช้แทน |
|---|---|
| `血` (blood) | `红色光芒` (red light) |
| `血红色天空` (blood-red sky) | `橙红色夕阳余晖` (sunset orange glow) |
| `死` (die/death) | `倒下` (fall down) |
| `杀` (kill) | `击中` (hit) / `命中` (strike) |
| `暴力` (violence) | `激烈对决` (intense duel) |
| `枪` (gun) | `武器` (weapon) / `装置` (device) |
| `焦黑` (charred) | `痕迹` (traces) |
| `火焰痕迹` (fire traces) | `光芒留下的纹路` (light patterns) |
| `冲击波` (shockwave) | `能量波纹` (energy ripple) / `气流扩散` (air flow) |
| `破坏/摧毁` (destroy) | `改变` (change) / `影响` (affect) |
| `废墟` (ruins) | `古代建筑群` (ancient architecture) |
| `爆炸` (explosion) | `能量释放` (energy release) / `光芒爆发` (light burst) |
| `闪电` (lightning) | `光束` (light beam) |
| `风暴` (storm) | `云层` (clouds) |
| `战场` (battlefield) | `竞技场` (arena) / `场地` (field) |

### Image Filter (รูป ref ต้องห้าม)

| ❌ โดน Reject | ✅ วิธีแก้ |
|---|---|
| รูปมีอาวุธชัดเจน | Crop เฉพาะหน้า หรือไม่แนบ ref |
| รูปท่าก้าวร้าว/กำลังโจมตี | ใช้ท่า neutral/ยืนปกติ |
| รูปโทนมืด/น่ากลัว | Brighten + desaturate ก่อนอัพ |
| รูปมีเลือด/บาดแผล | ลบออก ใช้รูปสะอาด |
| ส่ง ref หลายรูป | ลดเหลือ 1-2 รูป (scene ref เท่านั้น safe สุด) |

### Transition Clips (ฉากคั่น round) — กฎพิเศษ

```
Transition ไม่ต้องแนบ character ref — ใช้แค่ scene ref
เพราะ:
1. Character ref มีอาวุธ → โดน image filter
2. Transition ไม่จำเป็นต้องเห็นตัวละคร
3. ใช้ hologram UI abstract แทน — ไม่ต้องมีหน้าคนจริง

Pattern สำหรับ Hologram Transition:
- แนบแค่ scene ref (ฉากสนามรบ ไม่มีคน = safe)
- ใช้คำ: 全息投影 (hologram), 光幕 (light screen), 能量条 (energy bar)
- ไม่ระบุ HP ตัวเลขชัด — ใช้ "能量条下降" (energy bar decreases)
- สี: 蓝色 (blue) / 金色 (gold) / 青色 (cyan) = safe
- จบด้วย: 光芒收回/涟漪消散 (light retracts / ripple dissipates)
```

---

### /action ref [description]

Gen reference prompt สำหรับตัวละคร/สถานที่ action:

**Character Ref (Action Hero/Villain):**
```
character reference sheet, front view and side view,
[เชื้อชาติ/เพศ], age [อายุ],
[ลักษณะร่างกาย — กล้ามเนื้อ, แผลเป็น, etc.],
[ทรงผม],
[เสื้อผ้า/ชุดเกราะ/อาวุธ],
[สีหน้า — determined/menacing/calm],
white background, clean lighting,
full body visible, photorealistic
```

**Environment Ref (Action Setting):**
```
Cinematic [มุมกล้อง], [เลนส์],
[สถานที่ละเอียด],
[สภาพ — พังยับ/pristine/wet/dusty],
[ช่วงเวลา + แสง],
[บรรยากาศ — fog/rain/fire/dust],
no people, photorealistic, vertical 9:16
```

---

## Platform Rules (กฎแต่ละ Platform)

### Seedance 2.0
| Rule | Detail |
|------|--------|
| Prompt length | < 60 คำ |
| ภาษา | จีนได้ผลดีกว่า EN |
| 1 verb per shot | ห้ามหลาย action |
| V2V prefix | `"This is Pre-Visualization Animation — PRESERVE all timing..."` |
| Content filter | Dark/threatening = reject → brighten + desaturate |
| Text vs Image | Text ชนะ image — ต้อง sync กัน |
| Fight choreography | เก่ง contact physics + slow-mo |

### Kling 3.0
| Rule | Detail |
|------|--------|
| Prompt order | Scene → Characters → Action → Camera → Style |
| fps | 30fps default, 4K 60fps available |
| Camera strength | เก่ง camera motion + character physics |
| Layer movements | `"tracking with slight handheld shake"` ได้ |
| Avoid | 360 rotation + zoom พร้อมกัน |
| Negative prompt | ใช้ได้: `"no distortion, no warping"` |

### Higgsfield
| Rule | Detail |
|------|--------|
| Strength | Ref image inpaint, rotate, สร้างมุมใหม่ |
| Use case | เตรียม start frame ก่อนส่ง Seedance |

---

## Output Rules

1. **Prompt ภาพ** → code block ``` copy ได้เลย
2. **Prompt Seedance** → ภาษาจีน เสมอ
3. **Prompt Higgsfield** → ภาษาอังกฤษ เสมอ
4. **ทุก prompt** → ต้องมี lens + lighting + aspect ratio
5. **Sequence** → บอก flow ตัดต่อระหว่าง shot
6. **เปลี่ยนเลนส์ทุก shot** → ห้ามใช้เลนส์เดิมซ้ำติดกัน
7. **ถ้าต้อง intercut** → gen แยก clip + บอกจุดตัด

---

## Common Mistakes (ข้อผิดพลาดที่ต้องเลี่ยง)

| ❌ ผิด | ✅ ถูก |
|--------|--------|
| ยัดหลาย action ใน 1 clip | 1 shot = 1 action → ตัดต่อรวม |
| Prompt ยาว 200+ คำ | < 60 คำ เน้น keyword (ยกเว้น timeline prompt) |
| `"Camera moves forward"` | `"Slow dolly-in over 4 seconds at eye level"` |
| 360 orbit + zoom พร้อมกัน | เลือกอย่างเดียว |
| ไม่ใส่เลนส์ | ใส่ `"[X]mm lens"` ทุกครั้ง |
| ไม่ใส่แสง | ระบุ light source + mood |
| ใช้ `"cinematic"` อย่างเดียว | `"neo-noir cinematic"` / `"gritty war cinematic"` |
| Dark ref image | Brighten + desaturate ก่อนส่ง |
| 🔴 **Video prompt ไม่มี timeline** | **MANDATORY: ใส่ `0:00-0:03 — [action] [speed]` ทุก beat** |
| Speed แบบเหมารวม `"slow motion"` | ระบุที่ beat ไหน `"0:08-0:11 ULTRA SLO-MO 120fps"` |

---

*Reference: ψ/learn/action-cinematography-ai-prompt-guide.md*
*Last updated: 2026-05-30 — added Seedance Structured Header (Declaration + Consistency Lock + Guard Wall)*
