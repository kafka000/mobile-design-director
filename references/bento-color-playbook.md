# Bento UI + Multi-Color Playbook

The definitive guide for achieving "rich, colorful, yet clean" interfaces. This document codifies the layout philosophy and multi-color decision framework that separates premium from garish.

---

## Part 1: Layout — The 5 Bento Rules (Skeleton)

### Rule 1: Everything Goes in a Box (Bento Grid)

Every data point, chart, metric, and action gets its own rounded container. No content floats freely on the raw background. Think Japanese bento: rice, fish, vegetables each in their own compartment.

**Why it works:** The brain hates disorder. Boxes provide instant visual parsing — users read content boundaries in milliseconds instead of seconds.

**Implementation:**
```
✅ Each data group → rounded card container
✅ Cards arranged in grid/stack layouts
❌ Text/metrics floating on raw background
❌ Mixing card and non-card elements at the same hierarchy level
```

### Rule 2: Kill All Sharp Corners (Aggressive Rounding)

Every interactive surface uses generous corner radii. Buttons reach full-pill shape. Even chart bars and progress indicators are rounded.

| Element | Minimum Radius |
|---------|---------------|
| Cards / Containers | 20–24pt |
| Buttons | 12pt or full pill (height/2) |
| Input fields | 10–12pt |
| Chart bars | 4–8pt |
| Progress bars | full pill |

**Why it works:** Sharp corners feel like spreadsheets. Round corners feel like candy — safe, approachable, toy-like. This dramatically reduces cognitive load when viewing dense data.

### Rule 3: Extreme Typographic Contrast (Shouting vs Whispering)

Core metrics **scream** (48pt+ bold). Supporting labels **whisper** (10–11pt medium, grayed out, often uppercase with wide tracking).

```
┌─────────────────────┐
│                     │
│        1,840        │  ← 36-48pt, Black weight, primary color
│      KCAL LEFT      │  ← 10pt, Medium, text-secondary, +10% tracking, CAPS
│                     │
└─────────────────────┘
```

**Rule:** One anchor per card. If everything is big, nothing is big. The dramatic gap IS the design.

### Rule 4: Lavish Whitespace (Space = Luxury)

Card-to-card gaps and content-to-edge padding are aggressively generous. Never pack content tightly.

```
Crowded = street flyer          ❌
Spacious = luxury boutique      ✅
```

**Minimum ratios:**
- Inter-module spacing ≥ 3× intra-item spacing
- Card internal padding ≥ 16pt (hero cards ≥ 24pt)
- Screen edge margins ≥ 20pt

### Rule 5: Toyify the Data (Kill Boring Charts)

Replace line charts with chunky colored bars, dot matrices, wave curves, or ring gauges. Sprinkle 3D micro-illustrations or emoji-tier icons for emotional punch.

**Why it works:** Transforms cold data into visual decoration — users *enjoy* looking at metrics instead of dreading them.

---

## Part 2: Color — The 5 Multi-Color Decisions (Skin)

### Decision 1: "Does This Color Have a Job?" (Color = Label)

**The newbie mistake:** "This area looks empty, let me pick a pretty color to fill it." → **Chaos.**

**The rule:** Every new color must represent a **distinct data category or state**. No color exists purely for decoration.

```
✅ Purple = Development, Yellow = Writing, Green = Science, Pink = Math
✅ Red = Calories burned, Blue = Protein intake, Green = Active minutes
❌ "This card needs color because it looks plain"
❌ Adding color because of personal preference
```

**Litmus test:** If you can't name what data category the color maps to, **do not add it.**

### Decision 2: "Same Filter, Different Hue" (Unified Saturation)

**The newbie mistake:** Mixing pastel pink with neon green with deep navy in one interface.

**The rule:** Colors are like a girl group — faces differ, but the "makeup style" must be identical.

| Mode | Filter | Result |
|------|--------|--------|
| Light mode | All colors "add milk" | Low saturation, high brightness = Macaron/Ice cream palette |
| Dark mode | All colors "electrify" | High saturation = Cyberpunk neon palette |

```
❌ Macaron pink + Neon green on same screen
✅ Macaron pink + Macaron mint + Macaron lavender (all same "milky" filter)
✅ Neon green + Neon purple + Neon yellow (all same "electric" filter)
```

### Decision 3: "80/20 Neutral Dominance" (The Stingy Rule)

**The newbie mistake:** Letting colorful elements claim large surface areas, or spreading colors evenly.

**The rule:** 80% of screen area is reserved for emotionless neutrals (black, white, gray, off-white). Colors are compressed into the remaining 20% — chart bars, icons, progress rings, small tags.

```
          80% screen area → Neutral backgrounds & containers
          20% screen area → Intentional color (charts, tags, CTAs, rings)
```

**Analogy:** A minimalist white art gallery with a few vivid paintings. The more "blank" the canvas, the more colors it can absorb without looking chaotic.

> **Note:** This supersedes the previous 90/10 rule. 80/20 allows richer data visualization while maintaining premium feel. The key constraint is that all 20% must be *intentional* (mapped to data categories), never *decorative*.

### Decision 4: "One Diva Per Stage" (Loud Background → Muted Content)

**The newbie mistake:** Green card with red button and blue text.

**The rule:** If a card uses a bold, vibrant background color, **all content inside must wear a monochrome uniform** — pure black or pure white only. No competing colors.

```
┌── Neon Green card (#BAFD50) ──┐
│                                │
│   ■ Black icon                 │
│   Black headline text          │  ← Everything inside is pure black
│   Black body text              │
│   [■ Dark button]              │
│                                │
└────────────────────────────────┘
```

**Formula:** `Vivid background + Monochrome content = 永远的神 (always godly)`

**Extended Diva Rule — Multi-Card Viewport:**
When multiple cards share a viewport, each card surface counts as a "stage." Giving each card a different colored tint = multiple Divas competing for attention in one viewport.

```
❌ Anti-pattern: "Temperature gradient" with different colored surfaces
┌── Amber card ──┐  ┌── Purple card ──┐
│    Calories     │  │    Nutrition     │
└────────────────┘  └────────────────┘
┌── Blue card ───┐  ┌── Green card ──┐
│    Weight       │  │    Exercise     │
└────────────────┘  └────────────────┘
→ 4 Divas = visual chaos, not richness

✅ Correct: Unified neutral surface + data elements carry color
┌── Dark glass ──┐  ┌── Dark glass ──┐
│  1,840 [▓▓▓░░] │  │  🟣25g 🟡60g   │  ← progress bar & rings carry color
└────────────────┘  └────────────────┘
┌── Dark glass ──┐  ┌── Dark glass ──┐
│  73 kg    •    │  │  💚 320 kcal   │  ← icons & accent dots carry color
└────────────────┘  └────────────────┘
→ 1 surface style + 4 data colors = rich AND clean
```

**The principle:** Surfaces are the gallery wall (neutral). Data elements are the paintings (colorful). Don't paint the walls.

### Decision 5: "Blur the Boundaries" (Diffused Gradients for Multi-Color Zones)

**The newbie mistake:** Three saturated colors placed side-by-side with sharp edges like tiles.

**The rule:** When multiple high-saturation colors must coexist in one zone, **dissolve their boundaries** using soft gradients, brush strokes, or gaussian blur.

```
❌ Sharp tiled blocks: [Purple] | [Pink] | [Yellow]
✅ Diffused blend:     Purple ~~~ Pink ~~~ Yellow (watercolor/aurora effect)
```

**Implementation approaches:**
- CSS/RN: `radial-gradient` with low opacity overlapping circles
- Noise/grain texture overlay to soften transitions
- SVG blur filters on accent background shapes
- Multiple `RadialGradient` layers in `react-native-svg`

---

## Part 3: Light Mode vs Dark Mode Color Formulas

### Light Mode: "Ice Cream / Macaron" Palette

```
Background:     Off-white with warmth (#F5F5F0, not pure #FFFFFF)
Card surface:   Pure white or very light gray
Text:           Near-black for maximum contrast (#12121A)
Accent colors:  Low saturation, high lightness (pastel/milky)
                Lavender, mint, peach, butter yellow — all "add milk"
```

### Dark Mode: "Cyberpunk Neon" Palette

```
Background:     Deep charcoal, not pure black (#12121A, not #000000)
Card surface:   Slightly lighter (#1C1C22) for Z-axis separation
Text:           Pure white for primary (#FFFFFF), gray for secondary (#A0A0A5)
Accent colors:  High saturation "acid" tones (neon green, electric purple, hot yellow)
                Small surface area only — like neon signs in a dark alley
```

### The Golden Rule for Both Modes

> **Light mode = Soft background + Hard text**
> **Dark mode = Hard background + Luminous accents**

Never use pure #FFFFFF as background (too harsh) or pure #000000 (too dead).
Always add a subtle warmth or blue-gray tint to the neutral base.

---

## Quick Decision Flowchart

```
Want to add a color?
  │
  ├── Does it represent a new data category? ── NO → Don't add it.
  │                                              YES ↓
  ├── Does it match the existing filter?
  │   (macaron OR neon, never mixed)    ── NO → Adjust saturation/lightness.
  │                                        YES ↓
  ├── Will it stay within the 20% color budget? ── NO → Remove a less important color.
  │                                                 YES ↓
  ├── Is the background already colorful?
  │   YES → Make ALL content inside monochrome (black/white only).
  │   NO  → Proceed with the accent.
  │            ↓
  └── Multiple accents touching?
      YES → Blur/diffuse their boundaries.
      NO  → Ship it. ✅
```
