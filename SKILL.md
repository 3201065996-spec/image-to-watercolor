---
name: image-to-watercolor
description: >-
  Converts photos or illustrations into Japanese-style fresh watercolor hand-drawn
  artworks on white watercolor paper, with English title, subtitle, circular swatches
  with hex codes, prop icon, season stamp, detail inset, and pigment accident marks.
  Use when the user asks to 转手绘图, 水彩插画, photo to watercolor, hand-drawn
  illustration, 图片转水彩, or wants an image rendered as native painting on white
  watercolor paper.
---

# Image to Watercolor Hand Drawing

Turn a reference image into one finished piece: native watercolor + light ink/pencil line work painted directly on white watercolor paper, with English title, subtitle, four circular swatches with hex codes, a tiny prop icon, a season/moment stamp, a pencil-framed detail inset, and a few pigment accident marks — all on the same sheet.

## When to use

- User provides an image (or path) and asks for 手绘图 / 水彩 / watercolor conversion
- User wants portfolio-style illustration output with title + color palette

## Workflow

Copy and track:

```
Progress:
- [ ] 1. Read reference image + measure width/height
- [ ] 2. Extract subject, mood, palette, signature props
- [ ] 3. Draft title + subtitle + 4 hex + prop icon + stamp + detail inset
- [ ] 4. Generate with GenerateImage (same aspect as upload)
- [ ] 5. Self-check against style rules; regenerate if needed
```

### 1. Read the reference

- Use the image path the user provides (or the attached image file path).
- Note: main subject, setting, lighting, dominant colors, mood.
- **Measure size**: read pixel `width` × `height` of the upload (via reading the image or a quick size probe). Output must follow this size — see **Match input size**.

### 2. Derive copy and palette

From the image, invent **original** English copy (do not copy watermarks or brand text from the photo):

| Element | Rules |
|---------|--------|
| Title | 2–6 words, evocative, portfolio-like |
| Subtitle | One short phrase (about 4–12 words) |
| 4 colors | Representative, harmonious, **light pastel bias**. Under each circle print its **hex 色号** only (e.g. `#E8A4B0`) — no English color names; avoid deep/muddy hex |
| Prop icon | One minimal pencil line icon echoing a signature prop (glasses, beanie, collar, etc.) |
| Stamp | One faint round watercolor stamp in a **corner of the paper**; 1–3 uppercase words, e.g. WINTER LIGHT / DAY RIDE — never as in-scene signage |
| Detail inset | One small close-up (eyes+glasses, hands on collar, etc.) with pencil line frame only |

**People-first English (required when a person is the main subject):**

- Title and subtitle must center on the **person** — presence, expression, pose, outfit, or intimate mood — not the place, weather, or props alone.
- Scene/setting may appear only as a light supporting hint in the subtitle; never let the environment own the title.
- Prefer person-led phrasing (who / how they feel / what they wear) over place-led phrasing (window, street, park, room as the hero noun).
- No people / non-portrait scene → title may focus on place, object, or atmosphere as usual.

Examples when a person is present:

| Avoid (place-led) | Prefer (person-led) |
|-------------------|---------------------|
| Soft Window Light | Soft Pink Companion |
| Parking Lot Afternoon | Quiet Smile in Pink |
| subtitle: sunlight through the glass | subtitle: she holds her collar, eyes soft |

**Creative extras (always include unless user opts out):**

1. **Prop icon** — One tiny minimal line-art symbol beside the title or near the swatches (glasses outline, beanie silhouette, collar/button, etc.). Same pencil weight as the drawing; no fill plate, no sticker shadow.
2. **Circular swatches + hex 色号** — Four filled round dots; under each circle a tiny **hex code only** (e.g. `#E85A4F`). No English color names (no blush/mint/etc.). Placement: see **Sheet layout (canonical)**.
3. **Season / moment stamp（季节/时刻小印章）** — Press one soft **circular** watercolor stamp in a **paper corner** (prefer upper-left or upper-right margin on the bare paper / near vignette edge — not the bottom title/swatch band).
   - Look: semi-transparent wash, bloomed/soft edges, like a journal/planner stamp fused into the paper (手账感) — pigment in the paper fiber, not a hard UI badge, not a floating sticker with drop shadow.
   - Text: 1–3 short uppercase words, e.g. `WINTER LIGHT`, `DAY RIDE`, `SWEET HOUR`, `LANTERN EVE`.
   - **Forbidden:** putting the phrase on cake toppers, bottles, ribbons, street signs, or any object inside the illustration; square seals that look like logos; opaque hard-edged stickers.
4. **Detail inset** — Small watercolor close-up with pencil line frame only, placed in a side/upper margin of the **painted** area (not in the bottom 留白 band with title/swatches). Never a card, white mat, drop shadow, or hard rectangular panel.
5. **Pigment accidents（颜料偶然感）** — Intentionally leave **1–2** soft pale-pink and/or gray-blue water stains, splatters, or slightly unclean brush marks on the paper (near painting edges or in the blank margin). Subtle “just finished painting” realism — not messy, not covering title/swatches.

### Sheet layout (canonical — match this structure)

Reference look: main illustration is **smaller** — about **60–65%** of sheet height, centered in the upper area with visible paper margins on the sides; a larger bottom paper band (~35–40%) holds centered title, subtitle, then four round swatches.

```
┌─────────────────────────────────────┐
│         watercolor paper            │
│     ┌─ paint bleeds ─┐              │
│     │ MAIN ILLUSTRATION│            │  ← ~60–65% height (smaller)
│     │ (feather edges)  │            │     + side paper margins
│     └──────────────────┘            │
│         (bare paper 留白)            │  ← ~35–40% height
│            Title (centered)         │
│          subtitle (centered)        │
│        ●  ●  ●  ●  (centered)       │  ← swatches + hex under each
│       #hex #hex #hex #hex           │
└─────────────────────────────────────┘
```

Rules:
- Entire canvas = one continuous white/warm-white watercolor paper (texture everywhere).
- Main painting is **compact**: upper-center, not filling the sheet; leave clear paper on left/right and a **generous** bottom 留白.
- Do **not** let the illustration run edge-to-edge or dominate ~75%+ of the height.
- Paint edges irregularly dissolve into paper (no hard rectangle crop of the scene).
- In the bottom 留白, top-to-bottom order: **title → subtitle → four circular swatches → hex under each** (all horizontally centered).
- Swatches sit only on bare paper white — never on pigment; each circle has its **hex 色号** underneath; no English color names; even breathing space between painting edge, text, and swatches.
- Prop icon beside title; stamp + inset stay out of the bottom centered text/swatch stack.
- Include 1–2 subtle pigment accident marks (pale pink / gray-blue).

Present briefly to the user: title, subtitle, four hex, prop icon, stamp text, inset subject — then generate (unless they already specified these).

### 3. Generate the image

Call `GenerateImage` with:

- `reference_image_paths`: `[user's image path]`
- `description`: build from the **Master prompt** below (fill placeholders)
- `filename`: optional, e.g. `watercolor-<short-slug>.png` (filename only; tool may temp-save elsewhere)
- `aspect_ratio`: **must match the uploaded image** (see below) — never default to `3:4` / `4:3` by habit

Do **not** invent a separate background plate behind the artwork. The output IS the paper.

### Output save path

Do **not** hardcode a machine-specific drive (e.g. `E:\图片`). Paths must work for any user after open-source install.

**Resolve output directory in this order:**

1. Path the user explicitly gives this turn (highest priority)
2. Else if the workspace has `.cursor/skills/image-to-watercolor/` or the skill lives in the repo → save under workspace `output/watercolor/` (create if missing)
3. Else → save under the current workspace root `output/watercolor/`
4. If the user asks to keep the tool’s default location, leave the file where `GenerateImage` saved it

**After generate:**

1. `GenerateImage` may temp-save under Cursor `assets/` — that is fine as a temporary path
2. Copy/move the final file into the resolved `output/watercolor/` (or user path), creating folders as needed
3. Prefer telling the user the **final** path under `output/watercolor/` (or their custom path)
4. Optional cleanup: remove duplicate temp copies in Cursor `assets/` only when you successfully saved to the output folder and the user did not ask to keep temps

### Match input size

**Rule: 上传图多大比例，生成手绘图就用多大比例。** Do not force portrait-sheet or landscape defaults.

1. Compute `ratio = width / height` from the reference.
2. Pick the closest allowed `aspect_ratio` for `GenerateImage`:

| Target | Ratio (w/h) | Use when |
|--------|-------------|----------|
| `1:1` | 1.00 | Square or nearly square |
| `4:3` | 1.333 | Landscape, wider than tall |
| `3:4` | 0.75 | Portrait, taller than wide |
| `16:9` | 1.778 | Wide landscape / banner |
| `9:16` | 0.5625 | Tall phone / story |

3. Choose by smallest absolute difference between `width/height` and each target ratio. Examples:
   - 1080×1080 → `1:1`
   - 4032×3024 → `4:3`
   - 3024×4032 → `3:4`
   - 1920×1080 → `16:9`
   - 1080×1920 → `9:16`
4. If the user explicitly requests a different ratio, honor that override.
5. Mention briefly in the reply: input `W×H` → chosen `aspect_ratio`.
6. Tool limit: generation APIs expose aspect ratios, not arbitrary pixel counts. Matching **aspect** is required; exact pixel equality is not always available — do not invent a wrong ratio to “look more like a portfolio sheet.”

### 4. Quality gate (must pass)

Before finishing, verify the result against every rule in **画纸与绘制方式**, especially **纸画融合**. Fail and regenerate once if any of these appear:

- Illustration looks like a sticker / cutout / opaque photo-filter block sitting on blank paper
- Hard rectangular paint boundary, sharp vignette box, or clear “picture area vs margin” split
- Background fills are dense/opaque so paper tooth cannot be seen through the wash
- Scene edges do not dissolve into the sheet; paper grain missing inside painted areas
- Card backdrop, frame, drop shadow, beige filter, torn edges, text on a colored panel, or square/rectangular color chips (must be circular)
- Missing any of: prop icon, season/moment stamp, detail inset, pigment accidents (unless user opted out)
- Missing hex 色号 under any of the four color circles, or English color names under swatches instead of/in addition to hex
- Layout not matching canonical sheet: painting too large (over ~65–70% height or edge-to-edge), missing generous bottom 留白 (~35%+), or title/swatches not a centered stack under the art
- Color swatches overlapping painted washes, in a corner, or not on bare paper under the centered title/subtitle
- Stamp missing from corner, OR stamp is in-scene (cake stick, sign, bottle label), OR stamp looks like a hard sticker / UI badge / opaque logo with sharp edge or drop shadow
- Inset looks like a hard sticker, photo frame, or opaque card on the paper
- Overly clean digital look with zero water stains / accidental marks when accidents were not opted out
- Color style too deep / heavy / muddy / over-saturated (fails light airy wash look) — regenerate with lighter, softer, higher-key washes only; keep layout/stamp/inset/hex/extras the same

Corrective regen must explicitly say: dissolve edges into paper, transparent washes, paper grain visible through pigment, no floating rectangle; redraw **corner circular watercolor stamp** (not in-scene text); redraw inset as pencil + watercolor on the same sheet; if only color is wrong: **lighten palette, keep all other elements**.

---

## Master prompt

Compose `description` in English (models follow English art direction reliably). Keep the Chinese style block’s meaning intact. Fill `{title}`, `{subtitle}`, `{c1}`–`{c4}`, `{prop_icon}`, `{stamp}`, `{inset}`, and a one-line `{subject_summary}` from the reference.

```
Transform the reference image into a finished hand-painted illustration.

SUBJECT (preserve composition and likeness from reference):
{subject_summary}

SURFACE — white watercolor paper as the entire artwork (not a drawing placed on a background):
- Natural white or slightly warm-white watercolor paper as the base of the whole piece
- Fine, realistic, low-contrast watercolor paper fiber and grain texture visible everywhere, including inside washes
- The same continuous paper extends through the illustration, English title, subtitle, and circular color swatches — one flat sheet, no layered planes
- No separate background board, card base, photo frame, drop shadow, or extra rectangular mat

PAPER–PAINT FUSION (critical — avoid “picture glued on paper”):
- Pigment soaks into the paper; washes are translucent so fiber/grain shows through sky, walls, skin midtones, and soft backgrounds
- Outer edges of the scene feather, bloom, or dry-brush away into bare paper — never a hard rectangular crop or filled illustration box
- Background and secondary areas stay light and open; do not paint a solid opaque backdrop behind the subject
- Subject and setting share the same wet-into-wet paper surface; no cutout silhouette with uniform white halo
- Margins around the painting are the same paper continuing outward, not a different white layer

COLOR STYLE (critical — light & airy like Soft Blush Nails v1; layout/extras stay like v2):
- Target the **lighter, fresher** color feel of a first successful light pass: pale peach, soft blush pink, cream, misty blue-gray — NOT a deeper, denser, more shadowed second pass
- Keep overall value high-key; leave plenty of paper white in midtones; avoid muddy, heavy, over-saturated, or darkened fills
- Skin, fabric, nails, and soft backgrounds stay translucent and bright; do not push shadows into deep brown/gray/violet slabs
- Accent colors may be a touch clearer, but still soft pastel — never neon, never ink-dense
- Hex swatches must also bias lighter pastels to match this airy look
- If regenerating only for color: lighten washes only — keep stamp, inset, hex placement, layout, and pigment accidents unchanged

PAINTING — painted directly on the paper:
- People, environment, sky, plants, and other elements in watercolor with light ink/pencil line work
- Natural pigment bloom, diffusion, layering, slight pooling, uneven transparency
- Edges may softly fade, show dry-brush, or irregular watercolor boundaries
- Leave unpainted paper white for highlights, clouds, negative space — paper white is part of the image, not a mat around it
- Pigment accidents: 1–2 soft pale-pink and/or gray-blue water stains, splatters, or slightly unclean brush marks near edges or on blank paper — “just finished” feel, subtle
- No uniform beige/sepia filter over the whole piece; no fake torn-paper border

SHEET LAYOUT (canonical — follow exactly):
- Whole canvas is continuous watercolor paper
- Main illustration SMALLER: upper-center ~60–65% height with side paper margins; edges feather into paper; bottom ~35–40% is bare paper 留白
- In bottom 留白, centered stack top-to-bottom: title → subtitle → four round swatches → hex code under each circle
- Do not put title/swatches on the painted area; do not put swatches in corners

LAYOUT — typography and swatches:
- English title (centered in bottom 留白): {title}
- English subtitle (centered under title): {subtitle}
- If the reference has a main person: title/subtitle MUST emphasize that person; do not lead with setting or props
- Tiny prop icon (minimal pencil line art) beside the title: {prop_icon}
- Four circular color swatches on bare paper only, colors: {c1}, {c2}, {c3}, {c4}
- Under each circle print its hex 色号 in tiny type: {c1}, {c2}, {c3}, {c4} — hex only, no English color names
- Season/moment stamp REQUIRED in a paper CORNER: soft circular watercolor wash stamp, semi-transparent, bloomed edges, journal-stamp feel fused into paper; text: {stamp} (e.g. WINTER LIGHT / DAY RIDE). NOT inside the scene on props; NOT bottom title/swatch band; NOT hard sticker/UI badge
- Detail inset in side/upper painted margin: {inset}; pencil frame only; no card/mat/shadow
- No colored text panels or boxes

FINAL LOOK:
Portfolio sheet like Soft Pink Companion layout with **light airy pastel color** (not deep/muddy): upper watercolor scene dissolving into paper with subtle pigment accidents; a soft circular corner stamp; bottom blank band with centered title, subtitle, and four round swatches each labeled with hex; plus prop icon and pencil inset — all on one paper.
```

---

## 画纸与绘制方式：白色水彩纸原生绘画

最终作品必须呈现为直接绘制在白色水彩纸上的完整手绘插画，而不是将插画放置在某种背景上。

**纸张要求**
- 使用自然白或微暖白的水彩纸作为整张作品的基础。
- 纸张具有细腻、真实、低对比度的水彩纸纤维与颗粒纹理。
- 纸张从插画区域连续延伸至英文标题、副标题和配色卡区域。
- 禁止添加独立的背景板、卡片底板、相框、投影或额外的矩形衬底。

**纸画融合（重点）**
- 颜料渗入纸纤维，淡彩层保持透明，纸纹须透过天空、背景、皮肤中间调等大面积色块可见。
- 画面外缘须自然晕开、干笔收束或溶入纸白，禁止出现生硬矩形画框、实心底图块或「上图画、下留白」的分层感。
- 背景与次要区域保持轻薄留白，勿把场景画成不透纸的厚涂底板。
- 主体与环境处于同一纸面湿画关系中，禁止抠图描边式剪影或均匀白边贴图感。
- 插画四周的空白就是同一张水彩纸的延续，不是另外叠上去的白底。

**绘画要求**
- 人物、环境、天空、植物和其他场景元素均以水彩与淡彩线稿的方式直接绘制在纸面上。
- 水彩颜料应呈现自然的渗透、扩散、叠色、轻微积色和不均匀的透明度。
- 画面边缘允许出现自然的颜料渐淡、干笔痕迹和不规则水彩边界。
- 局部保留未着色的白纸，让纸白直接参与画面的高光、云朵、留白和空间表现。
- 不要给整张作品统一覆盖米黄色滤镜，不要人为制造撕纸边框。

**颜色风格（只调色感，不改版式）**
- 以色感参考「美甲第一版」的浅淡清透：粉、桃、米白、雾蓝灰等**第一遍淡彩**；禁止「第二版」那种发深、发闷、阴影加重的二次压色。
- 中间调多留纸白；阴影保持轻薄，不要压成深棕/深灰/深紫实底。
- 强调色可稍清亮，但仍柔和 pastel；色卡 hex 也倾向浅淡。
- 版式、角落印章、局部特写、色号、偶然感等**一律保持第二版完整效果**；质检若只有颜色偏深：重生成时**只提亮淡化色感**，其余不变。

**版式（必须，参考 Soft Pink Companion 结构）**
- 整张画布即一张连续水彩纸；主插画**偏小**，约占上方居中 60–65%，左右留出纸边，边缘晕入纸面；底部约 35–40% 为干净留白带。禁止主画铺满或占高超过约 70%。
- 底部留白内自上而下、水平居中：**英文标题 → 副标题 → 四个圆形色点 → 各点下方色号（hex）**；插画下沿、文字、色卡之间留均匀呼吸间距。
- 色卡只落在未着色纸白上，禁止压住颜料、禁止贴角落、禁止与标题区错位成左右分栏。
- 印章与局部特写放在画面侧/上缘，不要挤进底部标题+色卡居中带。

**英文文案与配色卡**
- 英文标题、副标题和四个圆形配色点均直接排版在同一张白色水彩纸上。
- 文字区域通过留白、位置、字体与间距自然形成，不使用独立的色块背景板。
- 配色卡必须为圆形色点（filled circles），禁止方形或矩形色块。
- **每个色点下方必须标注色号（hex，如 `#E85A4F`）**；不要写英文色名（如 blush / mint）。

**创意细节（默认开启）**
- **道具符号**：标题旁或色点旁画一枚极简铅笔线稿小图标（眼镜、针织帽轮廓、衣领/扣等），呼应人物道具，无底板、无投影。
- **季节/时刻小印章**：在纸面**角落**盖一枚淡水彩**圆形**印章文案（如 WINTER LIGHT、DAY RIDE、SWEET HOUR），半透明、边缘晕开，像手账贴纸但颜料渗入纸面；禁止硬边 UI 徽章、投影贴纸；**禁止**把文案画成画面内的蛋糕插牌、路牌、瓶标等道具文字。
- **局部放大**：主画面旁加一小块淡彩特写（如眼睛+眼镜、手握衣领）；线框仅为铅笔细线，禁止卡片底板、白卡垫或投影相框。
- **颜料偶然感**：故意留 1–2 处淡粉/灰蓝水渍溅点或未洗干净的笔触，增强「刚画完」的真实感；克制、自然，勿盖住标题与色卡。

**最终视觉目标**
呈现一张真实的白色水彩纸作品：纸面有细腻肌理，颜料与纸张自然融合，带轻微颜料偶然痕迹，画面具有日系清新水彩插画和淡彩铅笔线稿质感；底部为英文标题、副标题与带色号的圆形色点，并含道具小图标、淡彩印章与铅笔框局部特写，全部画在同一张纸上。

---

## User overrides

Honor explicit user choices when given:

- Custom title / subtitle / colors / stamp / prop icon / inset
- Opt out of any creative extra (including pigment accidents)
- Crop or focus on a region of the photo
- Explicit aspect ratio override (otherwise always follow upload size)
- Custom output folder (otherwise `output/watercolor/` under the workspace)
- More / less line work, denser / lighter wash

If the user only says “转成手绘图” with an image, run the full default workflow above.

## Output to user

1. Show the generated image (tool display is enough; do not dump the full prompt unless asked).
2. Confirm the final saved path (`output/watercolor/...` or the user-specified folder).
3. List title, subtitle, four hex (also printed under swatches on the image), prop icon, stamp text, detail inset, and input size → `aspect_ratio` used.
4. Offer one short revision pass if they want different text, palette, stamp, inset, or composition emphasis.
