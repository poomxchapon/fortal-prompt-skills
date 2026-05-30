---
name: horror
description: "Horror/Thai-psychological vertical drama prompt generator. Use when user says '/horror [script.pdf]' or '/horror scene [desc]' to convert horror scripts into image/video/sound prompts for Seedance + Higgsfield + Nano Banana. Specialized for ผีไทย + J-horror grammar + 9:16 vertical format. Outputs Production Doc .docx."
user_invocable: true
---

# horror — AI Horror Vertical Drama Prompt Generator

> อ่านบทผี → เลือก Director Tradition → Gen Prompt ทั้ง Pipeline พร้อม Sound Design + Production Doc

## Usage

```
/horror [path-to-script.pdf]             # Full pipeline — อ่านบทผี gen prompt ครบ
/horror scene [description]              # Gen prompt ฉากผีฉากเดียว
/horror beat [scene] [tradition] [archetype]  # Gen 1 beat ตาม director + archetype (compression/stretching/default/insert-heavy/surveillance/ticking)
/horror character [name] [description]   # Gen character ref (รวม "ผี" character)
/horror reveal [type]                    # Gen ghost reveal shot (mirror/edge/tilt/withhold)
/horror sound [scene]                    # Gen sound design timeline สำหรับฉากนั้น
/horror poster [title]                   # Gen horror poster
/horror fix [prompt]                     # แก้ prompt ติด filter
```

---

## IMPORTANT — อ่านก่อนทำงาน

ก่อน gen prompt ต้องอ่าน research base:

```
ψ/active/research/2026-05-05_horror-directing-thai-jhorror-vertical.md
```

ไฟล์นี้มี:
- Director techniques: Banjong, Sopon, Nakata, Shimizu, Kurosawa
- Vertical 9:16 adaptation rules
- Pacing structure (4-beat)
- Sound design principles (mid-frequency)

นอกจากนี้ตรวจ:
```
ψ/active/research/                       — ไฟล์ horror research อื่นๆ
ψ/learn/action-cinematography-ai-prompt-guide.md  — base camera/lens reference
```

---

## Golden Rules (กฎทอง)

1. **เลิก jump scare** — Banjong, Sopon, Nakata ปี 2010+ เลิกหมด ใช้ duration + silence-then-mid-freq-hit
2. **Y-axis blocking** — vertical 9:16 ใช้ top-bottom ไม่ใช่ left-right (ผีโผล่จากบน, มือคืบจากล่าง)
3. **Withhold the ghost** — Sopon "moment before the ghost" — บางฉากไม่เผยผีเลย
4. **Hold longer than feels safe** — Shimizu rule — ค้างหลัง reveal นานกว่าสัญชาตญาณ 1-2 วิ
5. **Sound mid-frequency 200Hz-4kHz** — phone speaker reality, sub-bass หาย
6. **Cut on question, not answer** — แต่ละตอนจบด้วย cliffhanger
7. **Karma engine (reframed)** — ผี ≠ ตัวลงโทษ — **Karma flows THROUGH ghost as conduit, victim's own karma kills victim**. ผีคือ trapped being ที่ติด attachment (upādāna) — environment ฆ่า victim (ของตก/รถเหวี่ยง/น้ำท่วม) ไม่ใช่ผีตี
8. **Object-as-conduit + Apparatus hierarchy** — phone (highest, daily attachment) > mirror (self-attachment) > photo (memory) > inherited > random. **Apparatus** (camera/phone/CCTV/baby monitor) > passive object เพราะมัน record/transmit ได้
9. **Lens ทุก prompt** — `[X]mm lens` เสมอ
10. **No on-screen subtitle** — ห้ามมี caption บนหน้าจอใน video output (บท dialogue ยังคงไว้สำหรับ lipsync ได้)
11. **Structured Header + Consistency Lock** — ทุก Seedance clip ใส่ Declaration (UUID+ชื่อไทย) + 永远 lock + 演技 block บนหัวก่อน timeline ของ archetype — **คนเป็น = natural micro-acting / ผี = invert (ไม่กระพริบตา ไม่หายใจ ขยับ delay)** — ดู section "Structured Header & Consistency Lock"

---

## Master Reference Layer (จาก Murch / Hitchcock / Block / Brown / Tarkovsky / Alton)

> ก่อน gen prompt ทุกครั้ง — ทุก beat ต้องมี answer ใน 5 axis นี้

### Axis 1: Murch's Rule of Six (cut weighting)

ทุก cut ต้องมี justification ใน 6 มิติ — Emotion มาก่อน:

| # | Criterion | Weight | Apply to /horror |
|---|-----------|--------|------------------|
| 1 | **Emotion** | **51%** | beat ต้อง declare `emotional_intent`: dread / dawning / recognition / paralysis / release |
| 2 | Story | 23% | what does this beat advance? |
| 3 | Rhythm | 10% | cut on accent, off-beat |
| 4 | Eye-trace | 7% | shot N+1 ghost-entry zone = shot N final eye-rest zone (vertical-critical) |
| 5 | 2D Planarity | 5% | break 180° rule if emotion > continuity |
| 6 | 3D Spatial | 4% | spatial coherence ต่ำสุด — Shimizu can violate |

**Murch's blink rule**: cut **บน blink ของตัวละคร** หลัง dread-onset, ไม่ใช่ก่อน. Image prompt vocabulary: `subject mid-blink, eyelid 30% closed`

### Axis 2: Hitchcock's Suspense Doctrine

| Concept | Rule |
|---------|------|
| **Suspense ≠ Surprise** | Suspense = audience รู้ ตัวละครยังไม่รู้ = 60× tension. Surprise = ทั้งคู่ไม่รู้ = cheap |
| **The Bomb Under Table** | ก่อนระเบิดต้อง show audience ว่ามีระเบิด — ผีเหมือนกัน |
| **Visible time-anchor** | TICKING archetype ต้องมี clock/timer **ใน frame** (analog clock at 12:47, second hand moving) |
| **MacGuffin** | Object lore ไม่ต้อง logical — ตัวละครเชื่อก็พอ |
| **Helplessness trigger** | Audience can't warn character = engagement. Subject pauses, head turns 15°, dismisses, resumes |

### Axis 3: Block's Contrast & Affinity (intensity dial)

ทุก beat ต้อง declare:
- **CONTRAST 2 components** (intensity ↑ — สร้าง dread spike)
- **AFFINITY 4-5 components** (intensity ↓ — dread floor)

Block's 7 components: **space / line / shape / tone / color / movement / rhythm**

| Component | Contrast (↑) | Affinity (↓) |
|-----------|-------------|--------------|
| Space | Deep + ambiguous | Flat, frontal |
| Line | Diagonal + curved/straight mix | Pure horizontal/vertical |
| Shape | Mixed types | Repeated |
| Tone | Wide gray range, non-coincidence | Narrow range |
| Color | Complementary saturated | Analogous desaturated |
| Movement | Mixed direction/speed | Uniform |
| Rhythm | Irregular, broken | Regular |

**Horror sweet spot**: ~2 components contrast against affinity floor. Pure-contrast = chaos (ไม่กลัว). Pure-affinity = น่าเบื่อ.

### Axis 4: Brown's Motivated Lighting + Ratio

- **Motivation token**: ทุก light source ต้องมี `because:` clause (e.g., `phone_glow because: character checking message at 3am`)
- **Source motivation**: `visible | implied | unmotivated` — reject `unmotivated` for /horror
- **Lighting ratio**: horror default = **8:1 minimum** (low-key chiaroscuro). Drop fill light entirely for chiaroscuro beats.
- **Practical-only rule** — single hard source motivated by visible practical (lamp/TV/phone/candle)

### Axis 5: Tarkovsky's "Leaves No Air"

> "It leaves no air" — Tarkovsky on overstuffed editing

**System rule**: ทุก scene ต้องมีอย่างน้อย 1 beat ที่ **hold without event** (8-15s lock-off, ผีไม่ปรากฏ, ambient only). ถ้าทุก beat มี event = นานๆ ดูแล้วชาไม่กลัว

**Time-pressure (Tarkovsky) ≠ Clock-pressure (Hitchcock)**:
- Clock-pressure = external deadline (TICKING archetype)
- Time-pressure = time itself is substance — single long take, **nothing happens**, audience scans frame for threat themselves → STRETCHING-TARKOVSKY variant

---

## Director Tradition Selector

ก่อน gen ต้องเลือก grammar — **ผสมได้ 2-3 ตัว, ห้าม Kurosawa เพราะ vertical ไม่ work**

### 1. Banjong (Object-Conduit + Karma + Guilty Hero)
**ใช้เมื่อ**: เรื่องมี object เด่น (มือถือ, กระจก, ภาพถ่าย, ของใช้แม่) + ตัวละครมี guilt/moral debt

**🔥 Core Rule (Banjong-confirmed)**: Protagonist **ต้อง morally compromised ก่อน scene 1** — ผีรู้
- Shutter = ตุน gang-rape Natre แล้วทิ้ง
- Alone = พรากแฝด
- Pee Mak = โกหกเรื่อง Nak ตาย
- ผีไทยแบบ Banjong ≠ random monster — มันคือ **karmic mirror** ของ guilt

**70/30 Rule**: 70% atmospheric build + 30% reveal/scare. Max 1 jump per 90 วินาที. Banjong: "Today, there's more focus on creating atmospheric horror... [horror lets us explore] sin, guilt, and human nature"

**Signature moves:**
- Object-as-conduit — ผีเข้ามาผ่าน object ที่เห็นใน reel แรก
- **Apparatus-as-conduit** (stronger): camera/phone/screen/baby monitor — devices ที่ record/transmit > passive object
- Unconscious tell — plant twist ใน body language ตั้งแต่ต้น (เก่งนวดคอ = Natre นั่งบนไหล่)
- **WEIGHT-ON-SHOULDER shot recipe** — slight character slouch + shadow asymmetry + neck strain (ผีนั่งไหล่)
- Two-act shift — ครึ่งแรก controlled / ครึ่งหลัง chaotic
- Wide bright frame + ผีอยู่ deep background soft focus (Pee Mak technique)

**Camera/Lens preset:**
```
Lens: 35mm + 85mm (alternating)
Light: Practical + cool fluorescent
Frame: Photo-as-frame (กรอบในกรอบ — กระจก, มือถือ, ภาพ)
Sound: Room tone heavy, no score sting
```

### 2. Sopon (Withhold + Architecture)
**ใช้เมื่อ**: ฉากใน domestic space (บ้าน, ออฟฟิศ, หมู่บ้าน) + ต้องการความค้างคา

**🔥 Doctrine Correction (Hitchcock-confirmed)**: Sopon withhold = **withhold จาก CHARACTER แต่ TELEGRAPH ให้ AUDIENCE** (ไม่ใช่หลบทั้งคู่)
- Suspense ≠ Surprise — Suspense = audience รู้ว่ามีผี ตัวละครยังไม่รู้ — audience screams "หันไปสิ!"
- Surprise = ทั้งคู่ไม่รู้แล้วผีโผล่ = cheap, 15 วินาที shock
- Sopon: "I wanted to change the focus from encountering ghosts to that moment you can sense there might be a ghost, yet you can't see it"

**Signature moves:**
- "Moment before the ghost" — character sense แต่ไม่เห็น (audience เห็น)
- **Architecture-first rule** — wide architectural shot ของตึก/ห้อง ก่อน character interior — building's trauma > character's
- **Negative-space mandatory** — ทุก scene ต้องมี 1 shot ที่ผี implied โดย absence (เก้าอี้ยุบ, ประตูเปิดเอง, ไอเย็นไม่มีร่าง)
- **Theme-park doctrine** — ทุกห้อง = 1 beat — Sopon: "creating a ghost house in a theme park where you need to design how the audience would feel when they arrive at certain points"
- **Expectation-inversion** — ถ้าฉากก่อนใช้ reveal-behind, ฉากต่อไปใช้ reveal-already-there (ผีอยู่ในเฟรมตั้งแต่แรก)
- Fake-jump-scare specialist — sting หลอก (ringtone/ของตก) → relief → real scare ในความเงียบ
- Aborted reveal — เริ่ม reveal แล้วตัดก่อน (Ladda Land fridge)

**Camera/Lens preset:**
```
Lens: 35mm wide + 50mm
Light: Two-mode — high-key magazine glossy (day) vs underexposed lamp pool (night)
Frame: Static long take, locked-off
Sound: Fake sting → silence → real scare (no sting)
```

### 3. Shimizu (Spatial Transgression — 6 Canonical Vectors)
**ใช้เมื่อ**: ผีปรากฏในที่ปลอดภัย (เตียง, อ่างอาบน้ำ, ใต้โต๊ะ) + ต้องการ rattle/sound signature

**🔥 6 Canonical Entry Vectors** (use one per shot, never mix):
1. **Ceiling/top-edge descent** — ผีลงจากเพดาน/บนเฟรม (vertical 9:16 native — Vector #1)
2. **Under-blanket reveal** — มือ/ผมโผล่จากใต้ผ้าห่ม
3. **Behind-curtain intrusion** — เงาขยับด้านหลังม่านอาบน้ำ/ม่านหน้าต่าง
4. **Stairwell descent** — ผีคืบลงบันได (Ju-on signature)
5. **Mirror reflection** — เงาในกระจกไม่ตรงกับตัวจริง
6. **Peripheral vision** — ตัวละครอื่นในเฟรมเห็นก่อน, ตัวเอกยังไม่รู้

**Suggestion Ratio (McRoy)**: 70% implied + 30% on-screen (Shimizu prefers ส่อมากกว่าเผย)

**Signature moves:**
- Curse = location, not arc — ใครเข้าฉากนี้ตายหมด
- Wrong place exact — ผีอยู่ตรงที่ไม่ควรอยู่
- Slow pan toward frame edge → off-screen sound or foreground intrusion
- Domestic zone-based ghost behavior (ใต้ฟูก/ในตู้/บนบันได/หลังม่าน)
- Death Rattle audio signature

**Camera/Lens preset:**
```
Lens: 28mm + 35mm
Light: Available + practical (no movie light)
Frame: Handheld + security-cam static
Sound: Mid-freq death rattle / ambient creaks / silence
```

### 4. Nakata (Amplified Mundane)
**ใช้เมื่อ**: เรื่องเกี่ยวกับเทคโนโลยี (โทรศัพท์, TV, video, internet) + slow burn

**Signature moves:**
- Foreground/background mismatch — normality หน้า, abnormality หลัง
- Withhold the face — เห็นแค่ตาผ่านผม
- Dolly-in claustrophobic — frame ตัดทุกอย่างทิ้ง เหลือ subject + threat
- Washed palette + chromatic accent (เสื้อกันฝนเหลือง = wrong)

**Camera/Lens preset:**
```
Lens: 50mm + 85mm
Light: Cold grey/green washed
Frame: Dolly-in + foreground/background depth
Sound: 50 SFX tracks layered, single dissonant note score, mid-freq scrape
```

### ❌ Kurosawa (Wide-Shot Ontological)
**ห้ามใช้กับ vertical 9:16** — ต้องการ horizontal width สำหรับ background scanning

---

## Thai Female Ghost Archetypes (ผี ≠ J-horror long-black-hair default)

**กฎสำคัญ**: ผีไทย = **recognizable woman, just wrong** — ไม่ใช่ผมยาวคลุมหน้าแบบญี่ปุ่น default. แต่ละ archetype มี visual + behavioral signature เฉพาะ + karmic trigger เฉพาะ:

| Archetype | Visual Signature | Behavioral Grammar | Karmic Trigger |
|-----------|-----------------|--------------------|-----------------|
| **Mae Nak** (phii tai tang glom) | ท้อง/อุ้มเด็ก, แขนยาวผิดปกติ, ทำงานบ้านได้ปกติ | เอื้อมหยิบของ — แขนยืดออก / ทำกับข้าวให้สามี / **เห็นผิดปกติเมื่อมองจากด้านหลัง/บน** | ตายตอนคลอด, สามีไม่อยู่, love-attachment |
| **Krasue** | หัวสวย + ไส้ห้อยเรืองแสง, body ซ่อนในตู้/cellar กลางวัน | ลอยที่ระดับหน้าต่าง, ล่าเนื้อดิบ/รก/เด็กเกิดใหม่, ตัดออกจาก body ตอนเย็น | แม่มด/หญิงนอกใจ, curse bifurcation |
| **Pee Pob** (Phi Pop) | ไม่มีรูปร่างตายตัว, host ดูปกติ แต่ตาแก้ว, เดินกลางคืนชนบท | possess, กินไส้ victim **จากภายใน**, ย้าย host เมื่อ host ตาย | hereditary curse, ทำลาย taboo, กินของต้องห้าม |
| **Nang Tani** | สาวสวยชุดเขียว, ปากแดง, **เท้าไม่แตะพื้น**, ผิวออกเขียว | อยู่ในต้นกล้วยตานี, **ลวงผู้ชายคืนพระจันทร์เต็ม**, passive ถ้าไม่ถูกแหย่ | ตายเด็ก/ไม่แต่งงานใกล้ดงกล้วย, sexual betrayal |
| **Phii Tai Hong** (generic) | **ผมเปียก, ชุดสีขาว funeral, แผลเหตุตายมองเห็น** | กลับที่ตายเวลาที่ตาย, ออกจาก radius ไม่ได้จนกว่า karma จะคลี่คลาย | ตายฉับพลันรุนแรง, ไม่มีงานศพ |

### Body-Grammar Tells (Thai-specific reveal mechanism)

แทนที่จะใช้ผมยาวคลุมหน้าแบบ J-horror — ใช้:
- **No shadow** — ผี recognizable แต่**ไม่มีเงา**ในแสงเดียวกับคนรอบข้าง
- **Wet in dry room** — ผมเปียก/ชุดเปียกในห้องแห้ง
- **Feet not touching floor** — ลอย 1-2 ซม. (Nang Tani signature)
- **Reflection mismatch** — เงาในกระจกขยับช้ากว่า/แตกต่างจากตัวจริง
- **Arm extension** — เอื้อมไกลกว่าที่ควรเอื้อม (Mae Nak signature)
- **Breath not visible in cold** — คนอื่นหายใจเป็นไอ ผีไม่เป็น

### Suggestion Ratio (per ghost archetype)

| Archetype | Suggest : Show |
|-----------|---------------|
| Mae Nak | 50:50 — เห็นบ่อย เพราะปลอม living |
| Krasue | 30:70 — visual ชัด, head + viscera trail |
| Pee Pob | 90:10 — ส่วนมากผ่าน host body, แทบไม่เห็น "ผี" จริง |
| Nang Tani | 40:60 — เห็นชัดในชุดเขียว |
| Phii Tai Hong | 70:30 — Sopon withhold default |

---

## Buddhist Karma Framework (Thai Horror ≠ Western Horror)

| Western Horror | Thai Buddhist Horror |
|---------------|---------------------|
| Good vs Evil binary | Karma as causation — ไม่มีดี/ชั่ว, มีแค่ debt + merit |
| Demon = external invader | Ghost = trapped being, owes/is owed |
| Exorcism by faith/ritual | **Merit-transfer** (offering food, robes, building) |
| Salvation through righteousness | Liberation through **cessation of attachment** (upādāna) |
| Object cursed by demon | Object = anchor of clinging |
| Ghost wants destruction | Ghost wants completion of unfinished karmic duty |

**Prompt-level rule**: ห้ามเขียน "ghost attacks." เขียน "karma resolves through ghost's proximity." Victim death = karmic balance, ไม่ใช่ malice.

### Buddhist Boundary Objects (4th conduit category)

Sacred objects ที่ defeat horror — แตก/desecrate = inciting incident:
- **Sai sin** (สายสิญจน์) — สายสีขาวจากพระ, แตกแล้วเชิญผีเข้า
- **Yantra cloth** (ผ้ายันต์) — ขีดข่วน = lose protection
- **Buddha image** (พระพุทธรูป) — ล้ม/แตก = ผีเข้า
- **Monk-blessed amulet** (ตะกรุด/พระเครื่อง) — สูญหาย = vulnerable
- **Pali chant forward** = protective. **Reversed/slowed Pali** = demonic inversion (Thai equivalent ของ "demonic Latin")

### Faith-Context (8th Context Variable)

แต่ละ context มี protective object + danger object ต่างกัน:

| Faith Context | Protective | Danger | Visual Cue |
|---------------|-----------|--------|-----------|
| **Animist village** | Spirit house (ศาลพระภูมิ), tree wraps | Banana grove, banyan tree | Saffron cloth, incense |
| **Theravada urban** | Monk amulet, sai sin | Phone/screen, mirror | Buddha shelf in condo |
| **Muslim south** | Quran verses, prayer rug | Forbidden food, broken wudu | Thobe, rosary |
| **Chinese-Thai shrine** | Joss paper, ancestor altar | Empty altar, broken urn | Red lanterns, incense coils |
| **Secular condo** | None — vulnerable | Modern apparatus all-conduit | Glass towers, white walls |

---

## Pipeline (7 ขั้น)

### Step 1: วิเคราะห์บท
1. **ระบุ tradition** — เลือก 1-2 director grammar ที่ fit
2. **ระบุตัวละคร** — ชื่อ, อายุ, บทบาท, **karmic debt** (ผีไทยต้องมี)
3. **ระบุ object-conduit** — object หลักที่จะเป็นช่องทางผี
4. **ระบุฉาก** — สถานที่, ช่วงเวลา, ระดับ darkness
5. **อ่าน 7 Context Variable ของแต่ละฉาก** — Madiew doctrine — scale/mobility/time/subjects/light/objects/sound (ดู Context Engine section)
6. **เลือก Beat Archetype ของแต่ละฉาก** — COMPRESSION / STRETCHING / DEFAULT / INSERT-HEAVY / SURVEILLANCE / TICKING (อาจ mix 2 ตัว)
7. **ระบุ ghost reveal strategy** — withhold / mirror / edge / tilt / aborted
8. **แบ่ง Story** — ไม่เกิน 30 วินาที/story
9. **แบ่ง Beat ใน Story** — ตาม archetype ที่เลือก × tradition grammar (ไม่ใช่ paste 5-beat template)

### Step 2: Character Ref (รวม "ผี")

**Living character:**
```
character reference sheet, front view and side view,
[เชื้อชาติ/เพศ], age [อายุ],
[ลักษณะใบหน้า — sharp jawline / soft features],
[ทรงผม],
[เสื้อผ้า — ปกติ ไม่ใส่ blood/horror props],
[อารมณ์: tired/anxious/exhausted — NOT scared (gen ทีหลัง)],
white background, clean lighting, ID photo style,
full face visible, photorealistic, Thai Asian face
```

**Ghost character (ใช้เพื่อ ref ภายในทีม — Seedance อาจ block):**
```
character reference sheet, front and side view,
[เชื้อชาติ/เพศ], age [อายุตอนตาย],
[ลักษณะ — long black hair covering face partially / pale skin / sunken eyes],
[เสื้อผ้า — ตอนตาย, soaked/torn but NOT bloody],
calm dead expression (NOT scary, NOT screaming),
white background, soft lighting,
photorealistic, Thai Asian face
```

**กฎสำคัญ:**
- Ghost ref **อย่าใส่ blood, screaming, aggressive pose** — Seedance block แน่
- Ghost ref ใช้เฉพาะใน Higgsfield/Nano Banana — Seedance พยายามไม่แนบ
- Ghost ใน Seedance ใช้ "text describe" แทน character ref เป็นหลัก

### Step 3: Scene Ref (ฉากไม่มีคน)

มี 3 mode ให้เลือก ตาม use case:

#### Mode A — Single Scene Shot (single panel)

ใช้ตอน: ต้องการ ref ภาพเดียวสำหรับ Seedance feed

```
Cinematic [angle], [lens] lens,
[location detail with horror atmosphere — not gore],
[time — late night / 3am],
[lighting — single source / cool fluorescent / window moonlight],
[atmosphere — empty office / quiet / fog / dust particles in light],
no people, photorealistic, vertical 9:16
```

#### Mode B — Multi-Panel Location Sheet with Title & Captions (ภูมิ approved version)

ใช้ตอน: ต้องการเห็นฉากหลายมุม + close-up details + พร้อมส่งทีม โดยตรง

**ต้องมี uploaded reference image เป็น input** (gen base image 16:9 ก่อนถ้าไม่มี)

```
Create a professional location reference sheet based strictly on the uploaded reference image.
Match the exact realistic visual style, lighting quality, color treatment, and texture of the reference.

Add a title bar at the top reading: "LOCATION REFERENCE SHEET: [SCENE NAME] ([TIME OF DAY])"

Arrange into two horizontal rows on a dark charcoal grey background frame.

Top row (four panels with captions below each):
- FRONTAL ([describe subject — e.g. "DESK", "DOOR", "RIGHT WALL"])
- LEFT ANGLED
- RIGHT ANGLED
- REVERSE WIDE

Bottom row (three detailed close-ups with captions below each, format "DETAIL: [items]"):
- DETAIL: [first key prop or zone]
- DETAIL: [second key prop or zone]
- DETAIL: [third key prop or zone]

All captions in light grey sans-serif uppercase text below each panel.
Maintain architectural consistency, accurate proportions, and consistent lighting across all panels.
No people in any panel.
Output a crisp, ultra-realistic, print-ready location sheet.
```

**ก่อน gen ทุกครั้ง — กรอก 4 ช่อง:**
1. `[SCENE NAME]` — e.g. "OFFICE INTERIOR — KENG'S WORKSTATION"
2. `[TIME OF DAY]` — e.g. "2AM", "NIGHT", "DAWN"
3. `FRONTAL ([xxx])` — ระบุ subject หลักของ frontal view
4. `DETAIL: xxx` × 3 — เลือก object-conduit หรือ key props จากบท

**สำหรับ horror specifically — เลือก DETAIL panels จาก plant ที่ต้องใช้ใน beat ต่อไป:**
- ฉาก office → `AC VENT & DUST` / `KEYBOARD & MUG` / `GLASS DOOR HARDWARE`
- ฉากบ้าน → `MIRROR & SINK` / `BED & FLOOR EDGE` / `WINDOW LATCH`
- ฉากบันได → `HANDRAIL` / `FIRST STEP` / `SHADOW POOL AT BOTTOM`

#### Mode C — Aerial View Landscape

ใช้ตอน: ต้องการมุมสูง bird's eye / drone establishing

**ต้องมี uploaded reference image เป็น input**

```
Create a professional location reference of Aerial view landscape on the uploaded reference image.
Match the exact realistic visual style, lighting quality, color treatment, and texture of the reference.
Output a crisp, ultra-realistic, ultra-details, 8K
```

**ตัดสินใจ Mode**

| ใช้ตอน | Mode |
|--------|------|
| Beat แรก (Hook) — ต้องการ scene-setting ไว | A |
| Scene สำคัญที่จะใช้ทุก beat ในตอน | **B** (multi-panel — ใช้คุ้ม) |
| Establishing wide shot / outdoor / urban | **C** (aerial) |
| ภายในห้องเดียว | A หรือ B |

**Horror scene keywords (safe):**
```
"empty corridor at night"
"abandoned office bathed in cold fluorescent"
"single desk lamp casting long shadows"
"glass door reflecting empty hallway"
"narrow stairwell descending into darkness"
"bedroom with window moonlight as only source"
```

**ห้ามใช้:**
```
❌ "blood-stained" / "haunted" / "demonic" / "cursed"
✅ "abandoned" / "empty" / "isolated" / "dimly-lit"
```

### Step 4: Image Prompt (ตัวละครในฉาก)

**Living character in horror scene:**
```
Cinematic [angle], [lens] lens,
[character description — exhausted, late-night work],
[action/pose — tired posture, looking at phone/screen],
[emotion — anxious/disturbed, NOT screaming],
[location with cold lighting],
[atmosphere — solitude, empty space],
photorealistic, vertical 9:16
```

**Ghost reveal frame (Sopon withhold):**
```
Cinematic [angle], [lens],
[empty corner of frame / negative space],
[hint of presence — wet handprint on glass / shadow at edge / mist],
[no visible figure — IMPLIED only],
[cold lighting + single source],
photorealistic, vertical 9:16
```

**Ghost reveal frame (Edge — top of frame):**
```
Cinematic low-angle [lens],
[character in lower third looking down/forward],
[pale figure descending from top edge of frame — only legs/lower body visible],
[long black hair partially obscuring frame top],
[cold backlight from above creating silhouette],
[character UNAWARE of figure],
photorealistic, vertical 9:16
```

### Step 5: Video Prompt — 3 Formats

#### Format A: Seedance Single Beat (5-6 วิ, จีน)

```
@[char ref] 这是[NAME] —— [brief ภาพรวม],
@[scene ref] 这是场景参考,
cinematic live-action，电影级画质，
[lens]镜头[shot type]，
[action ภาษาจีน — idle หรือ subtle motion]，
[camera movement — slow / static / tilt],
[lighting]，[atmosphere],
no background music, no grid lines, no overlay, no mesh,
no subtitles, no on-screen text,
cinematic professional camera language，竖屏9:16
```

#### Format B: Seedance Timeline (15 วิ — เลือก archetype ตาม context)

> **อ่าน Context Engine ก่อน** — เลือก archetype จาก 6 ตัว ตาม trigger context

##### B-1: DEFAULT (ออฟฟิศ/บ้านปกติ — 5 beat × 3s)

```
@[char ref] 这是[NAME] —— [brief]
@[scene ref] 这是场景参考

0:00-0:03 : @[ref](NAME – action) [LENS] [SHOT]，
[setup — character doing mundane activity]，
[camera static / slow tilt]

0:03-0:06 : 切换 [LENS] [SHOT]，
[detail insert — object-conduit close-up]，
[hint of wrongness — sound / shadow / drip]

0:06-0:09 : 切回 @[ref](NAME – reaction) [LENS] [SHOT]，
[character notices something — subtle]，
[hold longer than feels safe]

0:09-0:12 : [LENS] [SHOT]，
[escalation — object behaves wrong / silence / temperature drop visualized]

0:12-0:15 : [LENS] [SHOT]，
[ghost presence implied — handprint / shadow / breath visible],
[STATIC FRAME hold to end]

no background music, no grid lines, no overlay, no mesh,
no subtitles, no on-screen text,
cinematic professional camera language，竖屏9:16
```

**Beat Pattern**: SETUP(3s) → INSERT(3s) → NOTICE(3s) → ESCALATE(3s) → WITHHOLD(3s)

##### B-2: COMPRESSION (ในรถ/ลิฟท์/ห้องน้ำล็อก — 4 beat × 2-3s, breath-tight)

```
0:00-0:03 : @[ref](NAME) [TIGHT LENS 50-85mm] [CU]，
[character ใน confined space — hand on door/wheel/lock]，
[subtle breath, no music]，[static]

0:03-0:06 : 切换 [LENS] [Y-AXIS DETAIL]，
[wrongness ที่ขอบเฟรม — handprint บนกระจกข้าง / lock click / window fog]，
[silence drop]

0:06-0:10 : 切回 @[ref](NAME – reaction) [85mm CU]，
[breath caught, eyes shift]，
[hold 4 seconds — Madiew "trapped beat"]

0:10-0:15 : [LENS] [Y-AXIS REVEAL]，
[ghost intrusion จากขอบบน/ล่าง — feet/hair descend / hand on shoulder]，
[static, no escape, hold to end]

no background music, no grid lines, no overlay, no mesh,
no subtitles, no on-screen text,
cinematic professional camera language，竖屏9:16
```

**Beat Pattern**: TIGHT(3s) → EDGE-WRONG(3s) → REACTION(4s) → INTRUSION(5s)

##### B-3: STRETCHING (ห้องโล่งมืด/บันได/ทุ่ง — 3 beat × 5-7s, hold dominant)

```
0:00-0:07 : @[ref](NAME) [WIDE 24-35mm] [FULL FIGURE]，
[character เล็กในเฟรม empty space]，
[slow tilt up OR static long take]，
[ambient drone enters at -24dB]

0:07-0:12 : 切换 [LENS] [SLOW PUSH-IN OR STATIC]，
[architecture-as-ghost — corridor end / staircase bottom / corner darkness]，
[character ไม่เคลื่อน, dread breathes]

0:12-0:15 : [LENS] [STATIC LOCKED-OFF]，
[withhold — ghost ENTRY ZONE empty, sound carries presence],
[no reveal, cut on question]

no background music, no grid lines, no overlay, no mesh,
no subtitles, no on-screen text,
cinematic professional camera language，竖屏9:16
```

**Beat Pattern**: WIDE-PRESENCE(7s) → ARCHITECTURE-DREAD(5s) → WITHHOLD-CUT(3s)

##### B-4: INSERT-HEAVY (ครัว/แล็บ/ห้องรก — 6 beat × 1.5-2.5s, macro ถี่)

```
0:00-0:02 : @[ref](NAME) [35mm WIDE]，[character entering cluttered space]
0:02-0:04 : 切换 [100mm MACRO]，[object 1 — มีดบนเขียง / ขวดยา]
0:04-0:06 : 切换 [85mm CU NAME]，[reaching for something, slight unease]
0:06-0:08 : 切换 [100mm MACRO]，[object 2 wrongness — drip / hair in jar / wet mark]
0:08-0:11 : 切回 [85mm reaction]，[notice, frozen, hold 3s]
0:11-0:15 : [50mm WIDE]，[reveal — wrong object position changed / something missing]，[static]

no background music, no grid lines, no overlay, no mesh,
no subtitles, no on-screen text,
cinematic professional camera language，竖屏9:16
```

**Beat Pattern**: ENTER → MACRO-1 → CU-ACTION → MACRO-2-WRONG → REACTION-HOLD → WIDE-REVEAL

##### B-5: SURVEILLANCE (CCTV/baby cam/Zoom — 1-2 beat × 15s, single locked frame)

```
0:00-0:15 : [SURVEILLANCE STATIC ANGLE / CCTV HIGH CORNER / WEBCAM POV]，
[no cut, single locked frame for full 15s]，
[character does mundane action ใน foreground]，
[wrongness develops ใน background depth — ผีโผล่ deep BG / door opens by itself / lamp flicker]，
[character ไม่หันไป — audience sees first]，
[NO camera move, NO zoom, NO cut]，
[ambient hum + occasional digital glitch sound]

no background music, no grid lines, no overlay, no mesh,
no subtitles, no on-screen text,
cinematic professional camera language，竖屏9:16
```

**Beat Pattern**: SINGLE-FRAME-15s (Madiew "watch and wait")

##### B-6: TICKING (นาฬิกาเดิน/เคาท์ดาวน์ — beat sync กับ time signal)

```
0:00-0:02 : [50mm CU clock/timer — TICK]，[number/hand visible]
0:02-0:05 : 切换 [85mm CU NAME]，[reaction synced to tick rhythm]，[breath matches]
0:05-0:07 : 切换 [100mm MACRO]，[clock TICK 2 — closer to threshold]
0:07-0:10 : 切回 [WIDE 35mm]，[character moves with urgency, room feels tighter]
0:10-0:12 : [50mm CU clock — FINAL TICK approaching]
0:12-0:15 : [STATIC LOCKED]，[time hits — wrongness arrives — door / phone / ghost intrusion]

no background music, no grid lines, no overlay, no mesh,
no subtitles, no on-screen text,
cinematic professional camera language，竖屏9:16
```

**Beat Pattern**: TICK-CU → REACT → TICK-CU → URGENCY → TICK-CU → ARRIVAL

---

**กฎ archetype mixing**:
- Hybrid scene → ผสม 2 archetype ได้ (เช่น confined + clutter = COMPRESSION beat count + INSERT-HEAVY macro density)
- ห้าม assume archetype จากชื่อสถานที่อย่างเดียว — **ต้องอ่าน 7 context variable**
- ถ้าไม่แน่ใจ → ถามภูมิก่อน gen หรือเสนอ 2 archetype + reason

---

#### Structured Header & Consistency Lock (声明层 — ห่อทุก archetype) ⭐

> ใส่ header นี้บนหัว **ก่อน timeline ของ archetype ใดก็ได้ (B-1 ถึง B-6)** — แก้ปัญหาตัวละคร/ผี drift, แสงเปลี่ยน, หน้าแข็ง, 字幕หลุด

```
@[UUID_SCENE] 这是场景参考——[สถานที่+เวลา(深夜/3am)+แสง+atmosphere]
@[UUID_X] 这是[ROLE]（[ชื่อไทย]）——[เสื้อผ้าปกติ + 泰国男性/女性 + อายุ岁 + ทรงผม]

【时间与光线要求】
[lock เวลา+แสง — 必须是夜晚深夜，单一光源，低调冷光，绝对不是白天] (ratio 8:1+)

重要 (Consistency Lock — 永远):
- [角色]永远穿[เสื้อผ้าคงที่]
- 场景必须是[environment คงที่ — เช่น 深夜冷光走廊]

【演技要求】
所有真人角色表演自然真实不僵硬，自然的微表情、眨眼、呼吸起伏、极轻微重心移动

【台词与字幕要求】(ถ้ามีบทพูด)
对口型准确说出泰语台词嘴型同步，画面绝对不出现任何字幕 NO subtitles
```

> **🔥 Horror twist — 演技 block ใช้ได้ 2 ทาง:**
> - **คนเป็น (living)** = natural micro-acting (`自然的微表情、眨眼、呼吸起伏`) — เหมือน /drama
> - **ผี / ถูกสิง (ghost/possessed)** = **invert** → `不眨眼、不呼吸、动作僵硬延迟、重心不自然` = **body-grammar tell** (ดู Body-Grammar Tells section) — ความ "ผิดธรรมชาติ" คือตัว scare เอง
> - ใน clip เดียวที่มีทั้งคน+ผี → แยก acting note ต่อ @ref: คน natural / ผี invert

> Guard wall ของ horror อยู่ท้ายทุก Format แล้ว (`no subtitles, no on-screen text...`) — ถ้าอยากเข้ม เพิ่ม 字幕 variant จีน: `画面绝对不显示任何字幕 / 不要对白字幕 / 画面中绝对没有任何文字`

#### Format C: Higgsfield (EN, สำหรับ start frame หรือ stylized)

```
Cinematic [shot type], [lens] lens,
[character + action],
[horror atmosphere — withhold ghost or edge-of-frame reveal],
[location],
[cold lighting + single source],
[camera: static or slow tilt],
no jump scare, slow burn dread,
photorealistic, vertical 9:16
```

### Step 6: Sound Design (per beat — adapted from /action)

```
0:00 — [ambient: empty office hum / refrigerator buzz / late-night traffic distant]
0:02 — [diegetic: keyboard typing / breath / chair creak]
0:05 — [WRONGNESS layer: low-mid drone enters at -18dB]
0:07 — [STOP — silence 0.5s — ambient kills]
0:08 — [diegetic foreground only: character's breath becomes audible]
0:10 — [mid-freq scrape OR drip OR whisper at edge of audibility]
0:12 — [silence 0.3s — anticipation]
0:13 — [reveal sound: NOT a sting — a wet sound / fabric brush / mid-freq hit]
0:14 — [hold sound — keep wrongness layer running]
0:15 — [cut to next clip with sound carry-over]
```

**กฎ Horror Sound:**
- **Mid-frequency dominant (200Hz-4kHz)** — phone speaker reality
- **Silence-before-reveal 0.3-0.5s** — Hitchcock principle, amplified on mobile
- **No score sting** — late Banjong rule
- **Diegetic carries** — breath, swallow, footsteps, phone vibrate
- **Wrongness drone** — low-mid, -18 to -24dB, builds slowly
- **Death Rattle equivalent** — เลือก signature sound 1 อันต่อ "ผี" — เสียงเล็บขูด, drip, breath wet
- **Headphone bonus only** — binaural whisper เป็น layer เสริม ไม่ load-bearing
- **จบด้วย silence หรือ carry-over** ไม่จบด้วย sting

### Step 7: Production Doc Export (.docx)

ใช้ python-docx สร้าง:

```
[Title] — ตอน X Production Doc

Section 1: Director Tradition
  - ตารางสรุป grammar ที่ใช้ (Banjong/Sopon/Shimizu/Nakata mix)
  - Justification — ทำไมเลือก tradition นี้

Section 2: Karma & Object-Conduit
  - Karmic debt ของตัวละครหลัก
  - Object-conduit หลัก
  - Ghost reveal strategy

Section 3: Characters
  - ตาราง: ชื่อ | role | karmic relation | character ref prompt
  - Ghost character (separate row, marked GHOST)

Section 4: Scenes
  - ตาราง: scene | location | scene ref prompt

Section 5+: Stories (Story 1, 2, 3...)
  แต่ละ Story:
    - Director tradition for this story
    - **Context reading**: 7 context variable values (scale/mobility/time/subjects/light/objects/sound)
    - **Beat archetype chosen**: COMPRESSION / STRETCHING / DEFAULT / INSERT-HEAVY / SURVEILLANCE / TICKING (พร้อม reasoning จาก context)
    - Beat breakdown (จำนวน + ความยาว beat ตาม archetype — ไม่ตายตัว)
    - For each shot:
      - Lens / angle / movement
      - Action (Thai)
      - Sound design timeline
      - Image prompt (Nano Banana / Higgsfield) — boxed
      - Seedance prompt 中文 — boxed
      - Higgsfield prompt EN — boxed

Section X: Sound Design Master Timeline
  - ตาราง: timestamp | sound layer | dB | freq range

Section Y: Editing Notes
  - Where to hold-longer-than-safe
  - Cut-on-question button
  - Sound carry-overs between clips
```

ชื่อไฟล์: `[ชื่อเรื่อง]_ตอน[N]_Horror_Production_Doc.docx`

บันทึกที่: working dir ของบทต้นฉบับ หรือ `ψ/active/horror/`

---

> 📷 **ภาษากล้องเต็ม** (shot size · angle · movement · lens · composition · 9:16 · when-NOT-to-use): `.claude/skills/_shared/master-camera-reference.md` — ตารางด้านล่างคือ psychology-first lens ของ horror

## Lens Guide — Psychology-First (Brown-aligned)

ห้ามเลือกเลนส์เพื่อ "ภาพสวย" — เลือกเพื่อ **emotional intent**

| Lens | Spatial Effect | Psychological Effect | Horror Use Case | Tradition Match |
|------|---------------|---------------------|-----------------|-----------------|
| **14-16mm** | Extreme expansion, edge distortion | Reality-warp, dream-state, faceted dread | POV under bed, mirror reflection, claustrophobic-but-warped | Shimizu spatial transgression |
| **24mm** | Wide expansion, deep space | **Isolation in vast empty space** | Empty apartment, long hallway, tiny figure | Nakata amplified-mundane / Sopon withhold |
| **28mm** | Mild expansion, doc-realism | CCTV truth, found-footage feel | Surveillance archetype | SURVEILLANCE / OMNISCIENT-FRAME |
| **35mm** | Near-natural, slight environment | Grounded, human eye | DEFAULT establishing, character beats | DEFAULT |
| **50mm** | Normal | Neutral observer | Dialogue, reaction, POV | DEFAULT / STRETCHING |
| **85mm** | Mild compression | **Subject alone IN FRONT OF threat** | Victim cornered, stalker behind | Sopon withhold / COMPRESSION |
| **100mm macro** | Extreme detail, no context | Object becomes universe — **fetish/karma weight** | Hair, skin, drip, handprint | Banjong object-conduit / INSERT-HEAVY / HAIR-INSERT |
| **135mm** | Heavy compression, BG stack | **Threat collapsed onto victim** | Stalker pull-focus, two-figures-fused | TICKING |

### Hitchcock Triplet (mandatory pattern for Nakata tradition)

ทุก Nakata beat ต้องใช้ 3 shots:
1. **35mm** — character looks (shoulder cam OTS)
2. **50mm** — POV (subject's eye-line)
3. **85mm** — character reacts (tight CU)

Lock audience into character emotional state.

**Horror lens rules:**
- ห้ามใช้เลนส์เดียวกัน 2 beat ติดกัน
- Macro insert (100mm) **ทุกครั้งที่มี object-conduit** ปรากฏ
- 135mm ใช้สำหรับ "ตาเห็นผี" reflection shot
- **ทุก lens choice ต้องมี `because:` clause** — ถ้าเลือกไม่ได้ว่าทำไม = AI slop, restart

---

## Y-Axis Composition (Vertical 9:16)

### Eye Zones
```
Top 10%      → UI safe (avoid critical horror beats)
10-40%       → EYES of character / GHOST FACE / handprint
40-60%       → BODY / midground action
60-90%       → HANDS / objects / ground-level threat
90-100%      → UI safe
```

### Ghost Entry Patterns

**Top-edge descent** (Shimizu Stairs Crawl):
```
Character lower third (looking forward)
Ghost figure descends from above frame line
Only feet/legs/hair visible from top edge initially
Tilt-up reveal slowly OR stay static and let ghost descend
```

**Bottom-edge crawl** (Ju-on under-bed):
```
Character upper-mid frame (sitting/standing)
Hand or hair crawls up from bottom edge
Lower third becomes "wrong zone"
```

**Mirror frame-in-frame** (Banjong Polaroid):
```
Vertical frame = mirror/screen edge
Character reflection in central column
Ghost appears in reflection BUT NOT in surrounding "real" space
0.5s lag between character motion and reflection motion
```

**Stack-in-depth** (Nakata foreground/background mismatch):
```
Foreground: character (in focus, lower-mid)
Midground: empty space
Background: ghost figure (soft focus, upper third)
Character UNAWARE — audience sees first
```

**Withhold** (Sopon "moment before"):
```
Frame composed with ghost ENTRY ZONE clearly defined
Ghost NEVER enters
Sound + temperature cue + character reaction carries the scare
```

---

## Context Engine — Madiew Doctrine

> "หนังผีมี Beat ที่เปลี่ยนไปตามบริบทของฉาก"
>   — มะเดี่ยว ชูเกียรติ ศักดิ์วีระกุล

**Beat ไม่ใช่ template — มันคือ output ของ context × tradition.**
ห้าม paste 5-beat เดียวลงทุกฉาก ฉากในรถ ≠ ฉากในห้องน้ำ ≠ ฉากในซอยมืด

### 10 Context Variables (expanded from 7 — Block-aligned)

ก่อน split beat **ต้องอ่าน context ของฉาก** 10 ตัวก่อน:

| # | Variable | Values | ผลต่อ Beat |
|---|----------|--------|------------|
| 1 | **Scale of space** | confined / intimate / medium / expansive | confined = beat ถี่+สั้น / expansive = beat น้อย+ยาว |
| 2 | **Space mode** ⭐NEW | deep / flat / ambiguous | ambiguous (น้ำ/หมอก/มุ้ง) = disorient — ผีไทย default / deep = J-horror corridor / flat = Shimizu-with-intrusion |
| 3 | **Mobility** | trapped / limited / free | trapped = compression / free = wandering |
| 4 | **Time pressure** | none / implicit / explicit-clock | clock = ticking beat 2-3s / none = stretching |
| 5 | **Subject count** | solo / dyad / group | solo = internal beat / dyad = 切换 reaction / group = whose-turn |
| 6 | **Light state** | high-key / lamp-pool / near-darkness | + lighting ratio ต้อง 8:1+ for horror |
| 7 | **Object density** | clutter / medium / sparse | clutter = macro insert ถี่ / sparse = static hold ยาว |
| 8 | **Sound floor** | loud-ambient / medium / silent | loud = wrongness ต้องดัง / silent = silence-dominant |
| 9 | **Dominant line** ⭐NEW | horizontal (calm) / vertical (rigid threat) / diagonal (tension) / curved (organic) / mixed (unsettled) | Banjong = curved (hair/smoke) on straight architecture |
| 10 | **Faith context** ⭐NEW | animist-village / Theravada-urban / Muslim-south / Chinese-Thai-shrine / secular-condo | each = different protective + danger objects (ดู Buddhist Karma Framework) |

### Beat Archetypes (8 ตัว — เลือกตาม context)

| Archetype | Trigger Context | Beat Pattern (15s) |
|-----------|----------------|--------------------|
| **COMPRESSION** | trapped + confined (รถ/ลิฟท์/ห้องน้ำล็อก/ตู้) | 4-5 beat × 2-3s, Y-axis intrusion fast, breath-tight |
| **STRETCHING** | sparse + near-darkness + free (ห้องโล่งมืด/ทุ่ง/บันได/โถงโรงแรม) | 2-3 beat × 5-7s, hold-longer dominant, single tilt |
| **STRETCHING-TARKOVSKY** ⭐NEW | sparse + observational, "leaves no air" rule | **1 beat × 8-15s, lock-off no-cut, NO event in frame, audience scans for threat themselves**, room tone only — never confirms reveal |
| **DEFAULT** | medium + lamp-pool + standard (ออฟฟิศ/ห้องนอน/บ้านปกติ) | 5 beat × 3s — SETUP/INSERT/NOTICE/ESCALATE/WITHHOLD |
| **INSERT-HEAVY** | clutter + medium-light (ครัว/แล็บ/ห้องเก็บของ/โต๊ะทำงานรก) | 6-7 beat × 1.5-2s, macro insert ทุก 2nd beat — subtype **HAIR-INSERT** (kuroi kami precedes ghost) |
| **SURVEILLANCE / OMNISCIENT-FRAME** | static-cam diegetic OR audience-knows-character-doesn't (CCTV/Zoom/ghost-in-mirror-behind-subject) | 1-2 beat × 7-15s, no cut, single locked frame, ghost visible to camera NOT character |
| **TICKING** | explicit-clock (นาฬิกา/เคาท์ดาวน์/นัดเจอ/ลิฟท์ปิด) | beat sync กับ time signal — **MANDATORY: visible clock in frame** (Hitchcock rule) |
| **DELAYED-RECOGNITION** ⭐NEW | Thai animist context — ghost normalized | character treats ghost as living for 2-3 shots → body-grammar break (no shadow, feet not on floor, wet in dry room) = real scare |
| **MERIT-TRANSFER** ⭐NEW | ritual interrupt scene | monk + sai sin + amulet stops haunt — Pali chant **forward**, orange robe, white thread, smoke. Karmic accounting transaction |

### Decision Matrix — เลือก Archetype ยังไง

```
Step 1: อ่าน 7 context variable ของฉาก
Step 2: หา trigger ที่ match table ข้างบน — ปกติได้ 1-2 archetype
Step 3: ถ้าได้ 2 — choose dominant (เช่น trapped > clutter = COMPRESSION ชนะ INSERT-HEAVY)
Step 4: Apply archetype × director tradition
       (Banjong COMPRESSION ≠ Shimizu COMPRESSION — grammar คนละแบบ)
Step 5: ถ้าฉาก hybrid (เช่น ครัวมืด trapped) → mix archetype: 4 beat 2s แบบ COMPRESSION + macro insert จาก INSERT-HEAVY
```

---

## Pacing Structure (1-2 minute horror)

### 4-Beat Macro (Default Scaffold — ไม่ใช่ตายตัว)

```
HOOK (0-15s)        Frame 1 = wrong-thing already visible
                    Beat archetype = ตาม context ฉากเปิด

FRICTION (15-60s)   Physical/emotional constraint introduced
                    Beat archetype = adjust ตาม mobility + time pressure

SPIKE (60-90s)      Threshold crossed, no jump scare
                    Beat archetype = ปกติเปลี่ยนเป็น COMPRESSION/TICKING

BUTTON (last 5-10s) Cut on question
                    Beat archetype = STRETCHING หรือ SURVEILLANCE
```

**Macro structure ก็ไม่ตายตัวเช่นกัน**:
- ฉากเดียว 30s sustained dread → ใช้แค่ FRICTION + BUTTON ก็ได้
- ฉาก slow burn 3 ตอน → HOOK ของตอน 1 = FRICTION ของ macro
- Madiew rule: **ปรับ beat ตามฉาก ไม่ใช่บีบฉากให้เข้า template**

### Pacing Map (Default — ปรับได้)
```
0:00 ████████░░ HOOK     — wrong-thing on screen
0:15 ██████░░░░ FRICTION — character vs constraint
0:45 ████░░░░░░ DREAD    — sustained, mid-freq drone
1:00 ██████████ SPIKE    — escalation, fast cuts
1:20 ░░░░░░░░░░ HOLD     — STATIC withhold
1:30 ░░░░░░░░░░ BUTTON   — cut to black + sound
```

---

## Camera Movement — Horror

| Movement | ฟีล | Prompt |
|----------|-----|--------|
| **Static long take** | Sopon dread | `static locked-off` |
| **Slow dolly-in** | Nakata claustrophobic | `slow dolly-in over 4 seconds` |
| **Slow tilt up** | Reveal ghost from above | `slow tilt up from feet to head` |
| **Slow tilt down** | Reveal hand/object below | `slow tilt down to floor` |
| **Slow pan to edge** | Shimizu — pan toward where nothing happens | `slow pan to frame edge` |
| **Handheld subtle** | Shimizu doc feel | `subtle handheld breathing` |
| **Security-cam static** | Faux-doc surveillance | `surveillance static angle` |
| **POV phone-as-camera** | Vertical native | `first-person phone POV vertical` |
| **Mirror reflection static** | Frame-in-frame | `static facing mirror reflection` |

**ห้าม:**
- ❌ Whip pan (action vocab)
- ❌ Crash zoom (jump-scare vocab)
- ❌ Orbit (Kurosawa — ไม่ work vertical)
- ❌ Steadicam continuous (drama vocab — ใช้สำหรับ chase)

---

## Lighting Presets — Horror (12 presets, motivation-required)

ทุก preset ต้องมี **`because:` clause** (motivation token) — ห้าม unmotivated lighting

### Modern Sources (สำหรับฉาก contemporary)

| Lighting | ฟีล | Prompt | Default Motivation |
|----------|-----|--------|---------------------|
| **Cool fluorescent flicker** | Hospital, office, late-night | `cool fluorescent overhead flickering` | because: working overtime, building lights buggy |
| **Single desk lamp** | Solitude, focused dread | `single warm desk lamp casting long shadows` | because: only character awake at 3am |
| **Window moonlight** | Bedroom, intimate threat | `cold window moonlight as only source` | because: light failed / chose not to turn on |
| **Phone screen glow** | Modern horror, mobile-native | `pale blue phone screen lighting face from below` | because: checking message at 3am — **HIGHEST conduit** |
| **Refrigerator door open** | Sopon kitchen, food-decay | `cold refrigerator light from offscreen` | because: midnight snack, door left ajar |
| **TV static glow** | Nakata Ringu | `TV static blue glow, intermittent` | because: signal lost, victim alone |
| **Hallway sensor light** | Outside-in transgression | `motion-sensor white light from corridor` | because: SOMETHING triggered it (implied = scarier) |
| **No light, edge sodium** | Withholding, almost-darkness | `near-darkness, single sodium streetlight outside window` | because: power out / chose dark |

### Alton's Noir Setups (สำหรับ stylized/period/ritual)

| Lighting | ฟีล | Prompt | Use Case |
|----------|-----|--------|----------|
| **Slatted keylight** ⭐NEW | Bars of shadow across face | `hard side key through venetian blinds / shoji / bamboo screen` | Apartment hallway, victim "imprisoned by light" |
| **Criminal under-light** ⭐NEW | Bare hard source low+side, deep shadow opposite | `hard bare source from below-side, no fill, deep shadow opposite cheek` | Ghost POV, possessed character CU — innocent face → sinister |
| **Backlit fog** ⭐NEW | Hard back + smoke = silhouette | `hard backlight through smoke/fog, full silhouette` | Hallway emergence, ghost appearing from corridor |
| **Single-dot practical** ⭐NEW | One small motivated source in pitch black | `one small practical visible (phone/altar candle/fridge crack) in 95% black frame` | Ritual, possession, animist village shrine |

### Horror Lighting Rules (Brown + Alton + practical)

- **Lighting ratio 8:1 minimum** — low-key chiaroscuro default. Drop fill light entirely for chiaroscuro beats
- **Source motivation: visible | implied | unmotivated** — reject `unmotivated` — ส่ง back ไป edit
- **One source dominant** — ไม่ใช่ Hollywood three-point
- **Cool dominant + warm accent** — fluorescent (cool) + desk lamp (warm) = visual tension
- **Underexpose 1-2 stops** — let blacks crush, hide ghost in shadow
- **Practical lights only** — ไม่มี movie light visible — Shimizu doc feel
- **Below-eye underlight ONLY ผี**, ไม่ใช้กับ living character
- **Tonal coincidence flag** — `coincidence` (range reveals subject) vs `non-coincidence` (range hides) — declare per shot
- **Shadow as positive space** — Alton: "I used light for mood" — design shadow first, light second

---

## Sound Design Library — Horror

### Diegetic Foundation (mid-freq, phone-speaker safe)
```
"empty office HVAC hum"           — 200-400Hz drone
"refrigerator compressor buzz"    — 80-200Hz (low layer)
"single fluorescent ballast hum"  — 100Hz
"keyboard typing"                 — broadband
"chair creak"                     — 800Hz-2kHz
"breath / swallow"                — 100Hz-1kHz
"phone vibrate on wood"           — 60-150Hz + clack
"footsteps on tile"               — 200-1kHz
```

### Wrongness Layer (mid-freq, builds at -24 to -18dB)
```
"low-mid drone tone"              — 200-400Hz sine
"distant whisper unintelligible"  — 1-3kHz (phone-safe!)
"wet drip on hard surface"        — broadband but mid-peak
"fabric brush slow"               — 400-800Hz
"fingernail scrape on glass"      — 2-4kHz (HORROR ICONIC)
"hair against fabric"             — 1-2kHz
"breath wet / glottal click"      — Shimizu rattle reference, 200-1kHz
"reversed Pali chant slowed"      — Thai demonic inversion (≠ Western Latin) ⭐NEW
"water dripping in dry room"      — un-mourned dead signature ⭐NEW
```

### Reveal Sounds (NOT a sting — design carefully)
```
"single wet handprint on glass"   — broadband short
"door handle turning slowly"      — 200-800Hz
"phone notification — wrong tone" — mid-freq beep
"voice — barely audible"          — 1-2kHz, processed
"name whispered as exhale"        — 100-1kHz
```

### ห้ามใช้
- ❌ Sub-bass BRAAM (Inception) — phone speaker คายไม่ออก
- ❌ Loud violin sting — late masters เลิกหมด
- ❌ Orchestral score — ใช้ ambient only
- ❌ Reverse sound effect (action vocab)

---

## Filter Cheatsheet — Horror Specific

### Text Filter (Seedance)

| ❌ Block | ✅ ใช้แทน |
|---------|----------|
| `鬼` (ghost) | `身影` (figure) / `存在` (presence) / `影子` (shadow) |
| `死` (death/dead) | `静止` (still) / `不动` (motionless) |
| `血` (blood) | `深色液体` (dark liquid) / `痕迹` (mark) |
| `恐怖` (horror) | `氛围紧张` (tense atmosphere) / `不安` (unease) |
| `恶魔` (demon) | `身影` (figure) |
| `灵异` (supernatural) | `异常` (abnormal) / `奇怪` (strange) |
| `尖叫` (scream) | `屏息` (hold breath) / `怔住` (frozen) |
| `阴森` (eerie/sinister) | `寂静` (quiet) / `空旷` (empty) |
| `诅咒` (curse) | (avoid entirely) |
| `颤抖恐惧` (shake in fear) | `轻微颤抖` (slight tremble) |
| `扭曲的脸` (distorted face) | (avoid — ไม่ระบุหน้า) |
| `黑色头发遮住脸` (black hair covering face) | `头发垂下` (hair falling down) |

### Image Filter

| ❌ Reject | ✅ แก้ |
|-----------|--------|
| Ghost ref ที่ pale + dead expression | Crop เฉพาะ silhouette / hand / hair only |
| รูปเลือด/บาดแผล | ลบออก ใช้ "wet liquid" abstract |
| ผีท่ากรี๊ด/aggressive | ใช้ท่า static standing only |
| Dark/threatening atmosphere ref | Brighten 30% + slight desaturate ก่อนอัพ |

### Safe Wording Patterns
```
Instead of: "ghost appears behind character"
Use: "pale figure stands in background depth, soft focus"

Instead of: "scary handprint with blood"
Use: "wet handprint mark on glass surface, dark liquid drip"

Instead of: "demonic voice whispers"
Use: "faint voice carries through silence, source unclear"

Instead of: "character screams in horror"
Use: "character holds breath, eyes wide, mouth slightly open"

Instead of: "haunted office at night"
Use: "empty office bathed in cool fluorescent, late hour"
```

---

## Ghost Reveal Strategies (Catalog)

ใช้ `/horror reveal [type]` เพื่อ gen specific reveal shot

### Type 1: WITHHOLD (Sopon)
**ผีไม่ปรากฏเลย** — สื่อผ่านสิ่งแวดล้อม

```
Visual: empty corner of frame, locked-off static, hold 8-15s
Audio: silence → mid-freq drip OR breath sound from offscreen
Beat: character looks at empty space, slowly turns away, NEVER sees
End: cut to black or next scene
```

### Type 2: EDGE-OF-FRAME (Vertical native)
**ผีโผล่จากขอบบน/ล่าง**

```
Top-edge: low-angle, character lower third, ghost feet/legs descend from above
Bottom-edge: high-angle, character upper third, hand/hair crawls up
Lens: 24mm-35mm
Movement: STATIC — let ghost enter the frame, don't move camera
Sound: silence → fabric/footstep at moment of entry
```

### Type 3: MIRROR LAG (Banjong)
**Reflection ขยับช้ากว่าตัวจริง**

```
Setup: character looks in mirror (gen as frame-in-frame)
Beat 1: character moves → reflection moves with normal sync
Beat 2: character moves → reflection delayed 0.3-0.5s
Beat 3: character stops → reflection continues alone
Lens: 50mm facing mirror
Sound: diegetic only, no music
```

### Type 4: BACKGROUND APPARITION (Nakata)
**ผีอยู่ deep background, soft focus, character ไม่เห็น**

```
Foreground: character in focus, doing mundane action
Background: pale figure in soft focus, far depth
Character: NEVER turns around, never notices
Audience: sees first
Lens: 35mm-50mm with deep depth-of-field
Sound: ambient only — no cue at appearance
```

### Type 5: TILT REVEAL (Vertical native)
**Slow tilt up หรือ down เผยผี**

```
Tilt-up: start at object/floor → tilt to ceiling/door → ghost in upper frame
Tilt-down: start at face/eyes → tilt to hands/floor → wrong shadow/handprint
Speed: 4-6 second tilt (slow, dread-building)
Lens: 24mm-35mm
Sound: ambient drone builds during tilt
```

### Type 6: ABORTED REVEAL (Sopon Ladda Land)
**เริ่ม reveal แล้วตัดก่อน — never see**

```
Setup: character approaches container/door/closet
Build: hand reaches for handle, music/sound builds
Cut: phone rings / interruption / cut to next scene
Result: audience never knows what was inside
```

### Type 7: OBJECT-AS-CONDUIT (Banjong)
**ผีปรากฏผ่าน object — Polaroid, phone screen, mirror, photo**

```
Object: prominent in scene from frame 1 (plant)
Beat 1: character interacts with object normally
Beat 2: object behaves wrongly (Polaroid develops with figure / phone shows wrong message)
Beat 3: zoom into object, ghost manifestation IN object only
Reveal: ghost is INSIDE the object, not around character
Lens: 100mm macro for object detail
```

---

## Common Mistakes (ที่ Friday เคยพลาด — ห้ามทำซ้ำ)

| ❌ ผิด | ✅ ถูก |
|--------|--------|
| ใส่ score sting ตอน reveal | Silence → mid-freq diegetic only |
| ใช้ jump scare แบบ 90s | Hold static + duration |
| Crop horizontal ภาพยนตร์เป็น 9:16 | Compose native vertical (Y-axis) |
| Reveal ผีเต็มตัวตั้งแต่ตอน 1 | Withhold — partial reveal only, cut on question |
| ใช้ Kurosawa wide-shot grammar | ❌ ใน vertical — ใช้ Shimizu/Nakata/Banjong/Sopon |
| ใส่ blood/scream ใน image ref | ใช้ neutral pose + "anxious" emotion |
| Sub-bass BRAAM | Mid-freq 200Hz-4kHz only (phone reality) |
| Ghost random ไม่มี karma | ผีไทยต้องมี moral debt — explicit ใน Section 2 |
| ใช้เลนส์เดียวกัน 2 beat ติด | Alternate ทุก beat |
| ใส่ subtitle/caption บนหน้าจอ | NO on-screen text — dialogue ทำผ่าน lipsync แยก |
| Reveal หน้าผีเต็ม | Hair-over-face, partial silhouette, edge-only |
| Paste 5-beat × 3s template ทุกฉาก (ไม่ดู context) | Madiew doctrine — อ่าน 7 context variable แล้วเลือก archetype |
| ฉากในรถ/ลิฟท์ ใช้ DEFAULT 5-beat | ใช้ COMPRESSION 4-beat × 2-3s, Y-axis intrusion |
| ฉากห้องโล่งมืด split เป็น 5 beat ถี่ | ใช้ STRETCHING 2-3 beat × 5-7s, hold-longer dominant |
| ฉาก CCTV/Zoom call ตัด beat หลายช็อต | ใช้ SURVEILLANCE single-frame 15s no cut |
| `按下喷雾罐` (press spray) ไม่ระบุทิศ | `向上喷洒` / `向天花板方向` / `对着空气喷洒` — ระบุ **direction** target |
| Character ถือ prop ที่ระดับใบหน้า ไม่ระบุ direction | Default = ใช้กับใบหน้าตัวเอง — ต้องบอก `向外` (outward) / `远离自己` (away from self) |
| Action เปลี่ยน position ไม่ระบุ transition | บอก explicit: `站起身` (stand up) / `坐下` (sit down) / `走两步` (walk 2 steps) / `转身` (turn body) |
| Beat ต่อมา assume position เดิม | Re-anchor pose ทุก beat ที่เปลี่ยน position: `站立着` / `坐在椅子上` / `蹲下` |
| **Story-First Cut** (Murch) — cut ตามพล็อตก่อน emotion จบ | Hold beat ให้ครบ 1 inhale-exhale (~4s) ก่อน cut |
| **Withhold from BOTH** (audience + character) | Sopon = withhold จาก character, telegraph audience (Hitchcock) |
| Ghost punishes victim directly | Karma flows THROUGH ghost, victim's own karma kills (objects fall, vehicles swerve) |
| Default to J-horror long-black-hair-over-face | Thai ghost = recognizable woman just wrong (no shadow / wet in dry room / arm extension) |
| TICKING ใส่ tick sound แต่ไม่มี clock ใน frame | Hitchcock rule — clock visible in décor, second hand moving |
| Banjong protagonist = pure innocent victim | Banjong protagonist = morally compromised before scene 1 |
| Sopon ฉาก start จาก character | Architecture-first — wide architectural shot ก่อน character interior |
| Ghost = external invader (Western frame) | Ghost = trapped being (Buddhist) — wants completion of unfinished karmic duty |
| Every beat loaded with event | Tarkovsky "leaves no air" — ≥1 beat per scene must hold without event |
| Shimizu mix entry vector ภายใน shot | One vector per shot — 6 canonical (ceiling/under-blanket/curtain/stairs/mirror/peripheral) |
| Lens choice ไม่มี emotional reasoning | Brown — ทุก lens ต้องมี `because:` clause |
| Lighting ratio ไม่ระบุ | Horror default 8:1 minimum |

---

## Action Verb Direction Rules (สำหรับ prop interactions)

ทุก action ที่มี **prop in hand** ต้องระบุ 3 อย่าง:

1. **Pose state** — `站着` / `坐着` / `蹲着` (standing / sitting / crouching)
2. **Prop direction** — `向[direction]` (toward direction)
3. **Target** — `对着[target]` (at target — air / ceiling / wall / not self)

### Common Prop Directions

| Prop | ❌ Vague | ✅ Explicit |
|------|---------|-------------|
| Spray bottle | `按下喷雾罐` | `站立着,向上对着空气喷洒` |
| Lighter | `点燃打火机` | `蹲在桌下,将打火机举到面前点燃` |
| Phone | `拿起手机` | `从桌上拿起手机,举到耳边` |
| Flashlight | `打开手电筒` | `握住手电筒,光束指向前方走廊` |
| Knife/scissors | `拿起刀` | `从桌上拿起刀,刀尖朝下` (ระบุ blade direction!) |
| Cup/mug | `举起杯子` | `举起杯子凑近眼前查看` |
| Book/paper | `翻看` | `坐着翻看,书本放在膝盖上` |
| Mirror/compact | `看镜子` | `举起小镜子对着自己的脸查看` (clear self-target = OK) |

### Position Transition Verbs (ห้ามขาด)

| Transition | จีน |
|------------|-----|
| Stand up from chair | `从椅子上站起身` |
| Sit down on chair | `坐到椅子上` |
| Walk forward N steps | `向前走N步` |
| Turn around | `转身` / `转过身来` |
| Crouch / kneel | `蹲下` / `跪下` |
| Lean forward | `身体前倾` |
| Step back | `向后退一步` |
| Lie down | `躺下` |

---

## Output Rules

1. **ทุก prompt** → ต้องมี lens + lighting + composition zone (vertical 9:16)
2. **Seedance** → ภาษาจีน + filter-safe wording เสมอ
3. **Higgsfield/Nano Banana** → ภาษาอังกฤษ
4. **Timeline format** → 0:00-0:XX ทุก beat
5. **Sound design** → per-beat timeline, mid-freq dominant
6. **Director tradition** → declare ก่อน gen ทุกครั้ง
7. **Karma + object-conduit** → identify ก่อน gen ทุก script
8. **Cut on question** → ทุก clip จบด้วย withhold + cliffhanger
9. **Hold-longer-than-safe** → mark explicitly ใน production doc
10. **No on-screen subtitle** — guard wording: `no subtitles, no on-screen text` ใน Seedance prompt
11. **Beat = Context × Tradition, ไม่ใช่ template** — Madiew doctrine, ทุกฉากต้องอ่าน **10 context variables** แล้วเลือก archetype ก่อน split beat
12. **Declare archetype ก่อน gen** — ระบุชัดใน production doc ว่าฉากนี้ใช้ archetype ไหนใน 8 ตัว พร้อม context reasoning
13. **Beat schema mandatory fields** (Murch+Hitchcock) — ทุก beat ต้อง declare: `emotional_intent` + `information_asymmetry` (ใครรู้/ไม่รู้) + `motivation` (lighting because:)
14. **Contrast/Affinity declaration** (Block) — ทุก beat declare 2 components ใน contrast / 4-5 ใน affinity
15. **"Leaves no air" rule** (Tarkovsky) — ทุก scene ≥1 beat hold-without-event
16. **Suggestion ratio 70/30** (Shimizu) — implied : on-screen ghost — adjust ตาม Thai archetype (ดู table)
17. **Karma-as-conduit** — ห้ามเขียน "ghost attacks" — เขียน "karma resolves through ghost's proximity"

---

## Sub-Commands Reference

### /horror [script.pdf] — Full Pipeline
1. อ่านบท → ระบุ tradition + karma + object-conduit
2. **อ่าน 7 context variable ของแต่ละฉาก** → เสนอ archetype + tradition mix ให้ภูมิ confirm ก่อน gen
3. แบ่ง story + beat (จำนวน beat ตาม archetype, ไม่ตายตัว)
4. Gen character refs (incl. ghost)
5. Gen scene refs
6. Gen image prompts ทุก beat
7. Gen video prompts (Seedance Timeline + Single + Higgsfield)
8. Gen sound design per beat
9. Export Production Doc .docx
10. สรุปในแชท + ถาม noti

### /horror scene [description] — Single Scene
1. ถาม tradition + karma + object
2. Gen scene ref + image + video + sound (3-4 prompts)
3. แสดงในแชท (ไม่ต้อง .docx)

### /horror beat [scene] [tradition] [archetype]
1. ถ้าไม่ระบุ archetype → ถาม 7 context variable ก่อน
2. Gen beat ตาม tradition × archetype ที่ระบุ
3. Show context reasoning + beat breakdown

### /horror character [name] [desc]
Gen character ref (ถ้าระบุ "ghost" หรือ "ผี" → ใช้ ghost ref pattern)

### /horror reveal [type]
- `withhold` / `edge-top` / `edge-bottom` / `mirror-lag` / `background` / `tilt-up` / `tilt-down` / `aborted` / `object-conduit`
- Gen prompt ตาม type ที่ระบุ

### /horror sound [scene]
Gen sound design timeline (per beat) — text + dB + freq range

### /horror poster [title]
1. ถาม direction: minimal/busy, withhold/show
2. เสนอ 2-3 concept
3. Gen prompt — vertical 9:16, no logo

### /horror fix [prompt]
1. Identify block layer (text/image/face)
2. Apply filter cheatsheet swap
3. Show before/after diff

---

## When to Export Word .docx

| Command | Export? |
|---------|---------|
| `/horror [script.pdf]` | **Yes — full pipeline** |
| `/horror scene [desc]` | No — chat output |
| `/horror beat ...` | No |
| `/horror character ...` | No |
| `/horror reveal ...` | No |
| `/horror sound ...` | No |
| `/horror poster ...` | No |
| `/horror fix ...` | No |

ชื่อไฟล์: `[ชื่อเรื่อง]_ตอน[N]_Horror_Production_Doc.docx`
บันทึกที่: working dir ของ script ต้นฉบับ หรือ `ψ/active/horror/[project]/`

---

## Reference Files

### Research Base
```
ψ/active/research/2026-05-05_horror-directing-thai-jhorror-vertical.md
  └─ Director techniques + vertical adaptation (research base)

ψ/learn/action-cinematography-ai-prompt-guide.md
  └─ Base camera/lens reference (shared with /action)
```

### Knowledge Library — `ψ/learn/horror/` (book deep dives)
```
fundamentals/
  ├─ murch-rule-of-six.md            ← Cut hierarchy (Emotion 51%) + Blink-Cut Doctrine
  ├─ hitchcock-suspense.md            ← Suspense vs Surprise + Bomb Under Table + MacGuffin
  ├─ block-contrast-affinity.md       ← 7 visual components + intensity dial
  ├─ brown-lens-emotion.md            ← Lens psychology + motivated lighting + 8:1 ratio
  ├─ tarkovsky-time-pressure.md       ← Sculpting in Time + "leaves no air"
  └─ alton-noir-lighting.md           ← Mystery/Sinister/Slatted/Criminal lighting setups

directors/
  ├─ banjong-deep.md                  ← 70/30 + guilty hero + apparatus conduit
  ├─ sopon-deep.md                    ← Theme-park + architecture-first + expectation-inversion
  ├─ shimizu-vectors.md               ← 6 canonical entry vectors (J-horror)
  ├─ nakata-mundane.md                ← Hitchcock Triplet + amplified mundane
  └─ madiew.md                        ← Context Engine doctrine

genre/
  ├─ thai-female-ghosts.md            ← Mae Nak / Krasue / Pee Pob / Nang Tani / Phii Tai Hong
  ├─ buddhist-karma-engine.md         ← Karma-as-conduit + Buddhist Boundary Objects
  └─ jhorror-grammar.md               ← Hair / water / domestic uncanny / haunted display

recipes/
  ├─ kenworthy-master-shots.md        ← 20 named shot recipes mapped to horror
  └─ alton-lighting-recipes.md        ← Specific setup walkthroughs

interviews/
  └─ [director]-[YYYY-MM-DD].md       ← First-hand director conversations
```

### Skill Cross-references
```
.claude/skills/action/SKILL.md
  └─ Sound design + speed map patterns (reused)

.claude/skills/drama/SKILL.md
  └─ Pipeline structure + Production Doc format (reused)
```

---

## Philosophy

> "The horror is not what you see — it's what you *almost* see, then don't."
>   — Sopon Sukdapisit doctrine

> "I wanted to change the focus from encountering ghosts to that moment you can sense there might be a ghost, yet you can't see it."
>   — Sopon Sukdapisit

> "Today, there's more focus on creating atmospheric horror... [horror lets us explore] sin, guilt, and human nature."
>   — Banjong Pisanthanakun

> "หนังผีมี Beat ที่เปลี่ยนไปตามบริบทของฉาก"
>   — มะเดี่ยว ชูเกียรติ ศักดิ์วีระกุล (Context Engine doctrine)

> "It's not where you cut, it's why you cut. I want to feel that I'm cutting on the breath of the actor."
>   — Walter Murch (Rule of Six — Emotion 51%)

> "There is a distinct difference between suspense and surprise, and yet many pictures continually confuse the two."
>   — Alfred Hitchcock

> "Greater the contrast in a visual component, the more the visual intensity of the picture increases."
>   — Bruce Block (Contrast & Affinity)

> "It leaves no air."
>   — Andrei Tarkovsky (against overstuffed editing)

> "I used light for mood."
>   — John Alton (shadow as positive space)

> "Their own karma killed them after they tried to harm her family."
>   — Katarzyna Ancuta on Mae Nak (karma-as-conduit, not punishment)

> "Vertical 9:16 = native phone-as-camera = perfect Banjong object-conduit"
>   — Friday's vertical horror axiom

---

*Last updated: 2026-05-07 — Major refactor: 6 books synthesized (Murch / Hitchcock / Block / Brown / Tarkovsky / Alton / McRoy / Ainslie-Ancuta / Kenworthy). Added: Master Reference Layer, 5 Thai Female Ghost Archetypes, Buddhist Karma Framework, 10 Context Variables (was 7), 8 Beat Archetypes (was 6), Hitchcock Triplet, Alton's noir lighting, Murch's blink-cut doctrine. Critical fixes: Sopon withhold reframe, Karma-as-conduit, Banjong guilty-hero rule.*
*Researched & built by Friday | Nothing is Deleted*
