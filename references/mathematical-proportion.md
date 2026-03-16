# Mathematical Proportion — The Science of Visual Order

First-principles geometry for interface design. Humans subconsciously crave order and regularity — chaos triggers anxiety, mathematical precision triggers pleasure.

> **Formula:** `[Absolute Grid] + [Mathematical Scale] + [Golden/Silver Ratio] = Order Beauty`

> For specific spacing values and type scales, see `aesthetic-formulas.md`.
> For Bento grid layout rules, see `bento-color-playbook.md`.

---

## Law 1: The Absolute Grid System

**Theorem:** `Every dimension = Base Unit × Integer`

Every element on screen — width, height, margin, padding, border-radius — must be an integer multiple of a base unit (typically **4pt** or **8pt**). Even intentional "rule-breaking" must be built on top of a rigid grid.

### The 8pt Grid

```
8pt grid positions:
0  8  16  24  32  40  48  56  64  72  80  ...

Every dimension snaps to this grid:
  Icon size:     24pt (8 × 3)
  Card padding:  16pt (8 × 2) or 24pt (8 × 3)
  Section gap:   32pt (8 × 4)
  Card radius:   16pt (8 × 2) or 24pt (8 × 3)
  Button height: 48pt (8 × 6)
```

### Sub-Grid (4pt)

Use the 4pt sub-grid for micro-adjustments that the 8pt grid is too coarse for:

| Use Case | 4pt Grid Value | Example |
|----------|---------------|---------|
| Icon-to-label gap | 4pt | Inline icon + text |
| Whisper label tracking adjust | 4pt | Fine typography control |
| Hairline border offset | 4pt | Sub-pixel precision alignment |
| Micro badge padding | 4pt | Small status dots |

### Diagnostic Checklist

```
□ Are all major dimensions (card width/height, margins) multiples of 8?
□ Are all minor dimensions (icon gaps, label offsets) multiples of 4?
□ Is the grid applied consistently across ALL elements, not just cards?
□ Do adjacent elements align on the same grid tracks?
□ Is the grid visible in a "reduce to wireframe" view?
```

### Anti-Patterns

```
❌ Card padding: 15pt (not on grid)
❌ Icon size: 22pt (not on grid)
❌ Mixed base units: some 8pt, some 10pt, some 12pt
❌ "Close enough" alignment — elements visually near but not snapped

✅ Card padding: 16pt (8×2)
✅ Icon size: 24pt (8×3)
✅ Uniform base unit throughout the entire app
✅ Pixel-perfect grid snapping verified in design tools
```

---

## Law 2: Non-Linear Visual Progression

**Theorem:** `Scale(n) = Base × Multiplier^n`

Whether it's font sizes, shadow depths, spacing steps, or opacity levels — never use linear increments. Use a fixed multiplier to create a scale with natural rhythm.

### Type Scale Multipliers

| Multiplier | Name | Character | Best For |
|-----------|------|-----------|----------|
| **1.125** | Major Second | Very compact, subtle | Dense data dashboards |
| **1.200** | Minor Third | Moderate contrast | General purpose apps |
| **1.250** | Major Third | Clear hierarchy | Content-heavy apps |
| **1.333** | Perfect Fourth | Strong contrast | Premium / luxury apps |
| **1.500** | Perfect Fifth | Dramatic contrast | Marketing / hero pages |
| **1.618** | Golden Ratio | Maximum drama | Display / editorial |

### Example: Perfect Fourth (1.333×) Scale

```
Level 0 (Base):    16pt                    (body text)
Level 1:           16 × 1.333 = 21pt      (subheading)
Level 2:           21 × 1.333 = 28pt      (section title)
Level 3:           28 × 1.333 = 38pt      (page title)
Level 4:           38 × 1.333 = 50pt      (hero display)
Level 5:           50 × 1.333 = 67pt      (mega display)
```

Round to nearest grid-friendly value: 16, 20, 28, 36, 48, 64.

### Applying to Other Properties

The same multiplier principle applies beyond font sizes:

| Property | Linear (Bad) | Scaled (Good) |
|----------|-------------|---------------|
| Shadow blur | 4, 8, 12, 16 | 4, 8, 16, 32 |
| Spacing | 8, 16, 24, 32 | 8, 12, 16, 24, 32, 48 |
| Opacity steps | 0.2, 0.4, 0.6, 0.8 | 0.05, 0.08, 0.12, 0.20, 0.40 |
| Border radius | 4, 8, 12, 16, 20 | 4, 8, 12, 20, 32 |

### Diagnostic Checklist

```
□ Does the type scale follow a consistent mathematical multiplier?
□ Are there no "orphan" sizes that don't belong to the scale?
□ Is the progression felt as a natural rhythm (not too similar, not too jarring)?
□ Do shadow depths follow a non-linear curve?
□ Does the spacing system have clear "breathing" between levels?
```

---

## Law 3: Golden & Silver Ratios

**Theorem:** `Natural Harmony = Length / Width ≈ 1:1.618 or 1:1.414`

These ratios pervade natural forms (shells, flowers, architecture) and the brain instinctively perceives them as "inherently harmonious."

### Golden Ratio (φ = 1.618)

| Application | Calculation | Example |
|------------|-------------|---------|
| Card aspect ratio | Width : Height = 1 : 1.618 | 343pt × 212pt card |
| Content : Image split | Text area 61.8% : Image area 38.2% | Hero card spatial division |
| Primary : Secondary element | Hero number : Supporting text area = 1.618:1 | Anchor-whisper typography |
| Section division | Top section : Bottom section = 1 : 1.618 | Above-fold vs below-fold |

### Silver Ratio (√2 = 1.414)

| Application | Calculation | Example |
|------------|-------------|---------|
| Card aspect ratio | Width : Height = 1 : 1.414 | A-series paper ratio |
| Column splitting | 58.6% : 41.4% | Asymmetric two-column layouts |
| Icon container | Icon : Container = 1 : 1.414 | Icon centered in square with breathing room |

### Practical Application

```
Card Design Check:
┌─────────────────────────────────────┐
│                                     │  Width: 343pt
│                                     │  Height: 212pt
│                                     │  Ratio: 343/212 = 1.618 ✅ Golden
│                                     │
│   ┌──── 61.8% ────┐┌── 38.2% ──┐   │  Content/Image split: φ ✅
│   │  Title         ││  Subject  │   │
│   │  Subtitle      ││  Image    │   │
│   │  [CTA button]  ││           │   │
│   └────────────────┘└───────────┘   │
└─────────────────────────────────────┘
```

### Diagnostic Checklist

```
□ Do primary card proportions approximate φ (1.618) or √2 (1.414)?
□ Is the content-to-image area split near a natural ratio?
□ Are section divisions on the golden/silver ratio?
□ Do the proportions feel "naturally comfortable" to the eye?
□ Is the ratio applied consistently across similar card types?
```

---

## Forensic Application

When reverse-engineering a well-designed interface:

### Step 1: Grid Extraction
Overlay an 8pt grid on the screenshot. Check if elements snap to grid tracks. Count non-compliant elements.

### Step 2: Scale Analysis
Extract all font sizes from the design. Plot them on a log scale. If they form a straight line, there's a consistent multiplier. Calculate the multiplier.

### Step 3: Proportion Measurement
Measure the width:height ratio of key cards and containers. Check proximity to φ or √2. Measure content-to-image splits.

### Step 4: Diagnose
```
If grid compliance < 80% → "Grid discipline breakdown — causes subtle visual unease"
If font sizes are arbitrary → "No type scale — hierarchy feels random"
If proportions are far from natural ratios → "Proportions feel forced — consider φ adjustment"
```
