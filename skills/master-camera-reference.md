# Master Camera Reference — ภาษากล้องกลาง (ใช้ร่วม /action /drama /horror /affiliate)

> reference เดียวที่ครอบคลุม taxonomy กล้องทั้งหมด — มุม · ขนาดภาพ · ความสูง · การเคลื่อน · เลนส์ · composition
> **กฎทอง: เลือกกล้องเพื่อ "อารมณ์" ไม่ใช่ "ภาพสวย"** — ทุก prompt ต้องระบุ `[X]mm lens` + angle + movement เสมอ
> สกิลแต่ละตัวมี signature ของตัวเอง (ดูท้ายไฟล์) แต่ vocabulary พื้นฐานมาจากที่นี่

---

## 1. Shot Size (ขนาดภาพ — ระยะใกล้-ไกล)

ระยะตัดสินว่า "เห็นอะไร" และ "อยู่ใกล้อารมณ์แค่ไหน"

| Shot | ย่อ | เห็นอะไร | อารมณ์ | Prompt keyword | จีน |
|------|-----|---------|--------|----------------|-----|
| **Extreme Wide / Establishing** | EWS | สถานที่ทั้งหมด คนจิ๋ว | scale, isolation, เปิดเรื่อง | `extreme wide establishing shot` | 大远景 |
| **Wide / Long** | WS | เต็มตัว + สภาพแวดล้อม | context, 2 ฝ่ายเผชิญหน้า | `wide shot` | 远景 |
| **Full Shot** | FS | เต็มตัวพอดี | body language, ท่าทาง | `full body shot` | 全景 |
| **Medium Wide / Cowboy** | MWS | เข่าขึ้นไป | action + พื้นที่ | `cowboy shot, knee up` | 中全景 |
| **Medium** | MS | เอวขึ้นไป | บทสนทนา, neutral | `medium shot, waist up` | 中景 |
| **Medium Close-Up** | MCU | อกขึ้นไป | reaction, talking head | `medium close-up, chest up` | 中近景 |
| **Close-Up** | CU | หน้าเต็มเฟรม | emotion | `close-up` | 近景/特写 |
| **Extreme Close-Up** | ECU | ตา/ปาก/นิ้ว/detail | intensity, detail สูงสุด | `extreme close-up` | 大特写 |
| **Insert / Macro** | — | object/มือ/texture | object weight, proof | `100mm macro insert` | 微距特写 |

> **Vertical 9:16 note**: CU / MCU / Insert เวิร์กสุด เพราะใช้พื้นที่แนวตั้งเต็ม. EWS แนวนอนเสียพื้นที่บน-ล่าง — ใช้เฉพาะ establishing สั้นๆ

---

## 2. Camera Angle (มุมกล้อง — สูง-ต่ำ-เอียง)

มุม = "ใครมีอำนาจในเฟรม"

| มุม | อารมณ์ | ใช้ตอน | Prompt | จีน |
|-----|--------|--------|--------|-----|
| **Eye-level** | neutral, สมจริง | บทสนทนา, default | `eye-level shot` | 平视 |
| **Low angle** | ยิ่งใหญ่ ทรงพลัง | hero, ตัวร้ายปรากฏ | `low angle shot` | 仰拍 |
| **Extreme low / Worm's eye** | crush, towering | ผู้ชนะยืนเหนือ | `worm's eye view` | 极低角度 |
| **High angle** | อ่อนแอ vulnerable | ถูกล้อม, แพ้, เด็ก | `high angle shot` | 俯拍 |
| **Bird's Eye / Top-down** | god-view, tactical | choreography, flat-lay | `top-down bird's eye` | 顶视/俯视 |
| **Dutch / Canted** | สับสน บ้าคลั่ง ผิดปกติ | chaos, ผี, เมา | `dutch angle, tilted horizon` | 倾斜构图 |
| **Over-the-Shoulder** | เผชิญหน้า, ความสัมพันธ์ | stare-down, บทคู่ | `over-the-shoulder shot` | 过肩镜头 |
| **POV / First-person** | immersive, เป็นตัวละคร | ถูกไล่, รีวิวส่อง, ผีมอง | `first-person POV` | 第一人称视角 |
| **Profile / Side** | สังเกตการณ์, แบ่งแยก | เดิน, เผชิญหน้าด้านข้าง | `profile side shot` | 侧面 |
| **Back / Following** | ลึกลับ, ตามติด | เดินเข้าฉาก, suspense | `from behind, following` | 背面跟拍 |

---

## 3. Camera Height & Distance Nuance (รายละเอียดที่คนลืม)

| ตัวแปร | ตัวเลือก | ผลต่ออารมณ์ |
|--------|---------|-------------|
| **ความสูงกล้อง** | ground / hip / chest / eye / above | ต่ำ = ใหญ่/ข่มขู่, สูง = เล็ก/ถูกมอง |
| **ระยะห่าง (จิต)** | intimate (<0.5m) / personal / social / public | ใกล้ = อึดอัด/สนิท, ไกล = เย็นชา/สังเกต |
| **Subject ในเฟรม** | centered / rule-of-thirds / edge / negative space | edge+negative = unease (horror), centered = สมมาตร/นิ่ง |

---

## 4. Camera Movement (การเคลื่อนกล้อง — ต้องบอก "ความเร็ว")

> ห้ามเขียนแค่ `camera moves` — ต้องบอกชนิด + speed: `slow dolly-in over 4s`

| Movement | อารมณ์ | Prompt | จีน |
|----------|--------|--------|-----|
| **Static / Lock-off** | นิ่ง, dread, observe | `static locked-off` | 固定镜头 |
| **Pan** (ซ้าย-ขวา) | สำรวจ, เผย | `slow pan left` | 横摇 |
| **Tilt** (บน-ล่าง) | reveal สูง-ต่ำ (9:16 native) | `slow tilt up` | 纵摇/上下摇 |
| **Tracking / Follow** | ตามติด เร่งรีบ | `tracking shot following` | 跟拍 |
| **Dolly in** | เพิ่ม intensity | `slow dolly-in over 4s` | 推镜 |
| **Dolly out** | reveal scale, จากไป | `dolly-out revealing` | 拉镜 |
| **Orbit / Arc** | epic hero (⚠️ ไม่ดีกับ 9:16) | `orbiting 360° arc` | 环绕 |
| **Crane / Jib** | ยกขึ้น reveal / ลงมา intimate | `crane shot rising` | 升降镜 |
| **Handheld** | ดิบ สมจริง doc | `subtle handheld shake` | 手持晃动 |
| **Steadicam** | ลื่นไหล elegant | `Steadicam smooth continuous` | 斯坦尼康 |
| **Whip pan** | ฉับพลัน ตกใจ (action) | `whip pan rapid swing` | 急速横摇 |
| **Crash zoom** | ช็อก เน้นจุด (action/comedy) | `rapid crash zoom` | 急速变焦 |
| **Dolly zoom (Vertigo)** | disorient, panic | `dolly zoom vertigo effect` | 滑动变焦 |
| **Push-in macro** | object reveal (insert) | `slow macro push-in` | 微距推进 |

⚠️ **ห้าม combine**: orbit + zoom พร้อมกัน = geometry warp. เลือกอย่างเดียว

---

## 5. Lens (เลนส์ = ภาษาอารมณ์ + พื้นที่)

| Focal | ชื่อ | spatial | psychological | ใช้ตอน |
|-------|------|---------|---------------|--------|
| **12-16mm** | Ultra wide | ขยายสุด, edge distort | reality-warp, vast | establishing, POV คับแคบ, chase |
| **20-24mm** | Wide | ขยาย, deep space | isolation in space | low-angle hero, ห้องว่าง |
| **28-35mm** | Moderate | near-natural | grounded, human | group, establishing, character |
| **50mm** | Standard | ตาคนจริง | neutral observer | OTS, dialogue, two-shot |
| **85mm** | Medium tele | mild compress | subject isolated | reaction, emotion, cornered |
| **100mm** | Macro | detail สุด, no context | object = universe | insert มือ/object/texture |
| **135-200mm** | Telephoto | compress หนัก | threat collapsed | ไล่ล่า, sniper, stalker |
| **Anamorphic** | — | 2.39:1 + flare | "หนังจริง" | ฉากที่อยากได้ cinematic feel |

---

## 6. Composition Rules (จัดองค์ประกอบ)

| หลัก | ใช้ตอน | Prompt |
|------|--------|--------|
| Rule of thirds | default สมดุล | `rule of thirds composition` |
| Centered / symmetry | นิ่ง, อำนาจ, Kubrick | `centered symmetrical` |
| Leading lines | ดึงตาไปจุดสำคัญ | `leading lines toward subject` |
| Frame-in-frame | กรอบในกรอบ (กระจก/ประตู) | `framed through doorway` |
| Negative space | เหงา, unease, ผี | `negative space, subject at edge` |
| Foreground/Background depth | layering, mismatch (horror) | `deep focus, foreground + background` |
| Shallow DOF | isolate subject, bokeh | `shallow depth of field, bokeh` |

---

## 7. Vertical 9:16 Rules (มือถือ — สำคัญสำหรับทุกสกิล)

```
✅ ใช้แกน Y (บน-ล่าง) เป็นหลัก — tilt, top-edge entry, bottom crawl
✅ Shot ที่เวิร์ก: CU, MCU, MS, Insert, POV, top-down flat-lay
✅ Subject zones: 10-40% หน้า/ตา · 40-60% ลำตัว · 60-90% มือ/object
✅ เว้น top 10% / bottom 10% เป็น UI-safe (caption, ปุ่ม)

❌ หลีกเลี่ยง: EWS แนวนอนกว้าง, orbit, bird's eye กว้างเกิน (เสียพื้นที่ข้าง)
❌ Two-shot ซ้าย-ขวา แน่นเกิน — ใช้ stack บน-ล่างแทน
```

---

## 8. Genre Signature (มุม signature ของแต่ละสกิล)

> base vocabulary ด้านบนใช้ร่วม — แต่ละสกิลเน้นชุดนี้เป็นพิเศษ

### /action
```
Hero: low angle + 24mm | Fight: handheld 24-35mm | Impact: ECU/macro 100mm
Chase: tracking 16mm→200mm compress | Reaction: 85mm | Finale: orbit/crane (ถ้าไม่ใช่ 9:16)
Signature: speed-ramp + whip pan + crash zoom
```

### /drama
```
Dialogue: OTS 50mm + MCU 85mm reaction | Establishing: 35mm | Emotion: CU/ECU 85-135mm
Two-shot: 50mm (stack แนวตั้งถ้า 9:16) | Insert: 100mm มือ/object
Signature: static + slow dolly-in, eye-level intimate
```

### /horror
```
Reveal: slow tilt (top-edge entry) | Dread: static lock-off wide 24mm | Stalker: 135mm compress
Ghost POV: 14-16mm warp | Insert conduit: 100mm macro | Surveillance: 28mm CCTV static
ห้าม: whip pan, crash zoom, orbit (= action/jump-scare vocab)
Signature: hold-longer-than-safe, negative space, Y-axis intrusion
```

### /affiliate
```
Product hero: 50mm centered | Macro texture/swatch: 100mm | Flat-lay: top-down bird's eye
Try-on/demo: 50mm MCU | Talking-head: 35mm | CTA: 35mm + point gesture | Review POV: 28mm
Signature: UGC handheld subtle shake, natural light, product always logo-to-camera
```

---

## 9. When NOT to Use (เมื่อไหร่ห้ามใช้ — กัน AI slop)

| มุม/movement | ห้ามใช้กับ | เพราะ |
|--------------|-----------|-------|
| Orbit / 360 | vertical 9:16, horror | เสียพื้นที่ + ไม่ render แม่น / ผิด genre |
| Crash zoom / whip pan | horror slow-burn | = jump-scare/action vocab ทำลาย dread |
| Dutch angle | งานขายสินค้า (affiliate) | ดูไม่น่าเชื่อถือ/ไม่มั่นคง |
| Bird's eye กว้าง | 9:16 ทุกสกิล | subject จิ๋วเกินบนจอมือถือ |
| Extreme telephoto 200mm | ห้องแคบ | compress จนไม่เห็น space |
| Steadicam continuous | static dread scene | เคลื่อนมากไปทำลายความนิ่ง |

---

## 10. Quick Decision Flow

```
1. อารมณ์อะไร? → เลือก ANGLE (อำนาจ) + SHOT SIZE (ระยะใกล้อารมณ์)
2. ใกล้อารมณ์แค่ไหน? → CU/ECU ใกล้ · WS/EWS ไกล
3. ต้องเคลื่อนไหม? → static (นิ่ง/dread) · dolly-in (intensity) · tracking (ตาม)
4. เลนส์? → ตาม spatial/psychological table
5. 9:16? → เช็ค section 7 — แกน Y, UI-safe zone
6. ตรง genre signature ไหม? → section 8
7. มี "ห้ามใช้" ไหม? → section 9
```

---

*Shared reference for: /action · /drama · /horror · /affiliate*
*ทุก video/image prompt อ้างอิงไฟล์นี้สำหรับ camera vocabulary*
