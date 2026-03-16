# Typographic Rhythm — The Music of Black, White & Gray

First-principles typography for mobile interfaces. Strip all color and imagery — an excellent layout in grayscale reveals a water-like flow of visual "gray tone," rhythmic and comfortable.

> **Formula:** `[x-Height Consistency] + [Line-Height/Tracking Tension] + [F/Z Pattern Gravity] = Rhythmic Beauty`

> For the type scale system and tracking rules, see `aesthetic-formulas.md`.
> For anchor+whisper pattern, see `visual-architecture.md`.

---

## Principle 1: Typographic "Breathing" — Tension & Release

**Theorem:** `Bold Large = Tight Tracking · Small Regular = Loose Line-Height`

Like music alternating between tension (forte) and release (piano), text must alternate between compressed energy and relaxed flow.

### The Tracking Rule

| Text Role | Size Range | Tracking | Line-Height | Weight | Character |
|-----------|-----------|----------|-------------|--------|-----------|
| **Hero / Display** | 36–64pt | -1% to -3% | 1.0–1.1× | Black (900) | Power, compressed energy |
| **Title** | 24–32pt | -0.5% to -1% | 1.1–1.2× | Bold (700) | Authority, control |
| **Subheading** | 18–22pt | 0% | 1.2–1.3× | Semibold (600) | Structure |
| **Body** | 14–16pt | 0% | 1.5–1.6× | Regular (400) | Readable, relaxed flow |
| **Caption / Whisper** | 10–12pt | +8% to +15% | 1.3–1.4× | Medium (500) | Airy, whispered context |

### The Music Analogy

```
HERO TEXT     ← Fortissimo: heavy weight, tight tracking, compressed
  title       ← Forte: strong but not overwhelming
    subhead   ← Mezzo-forte: structural marker
Body text flows naturally    ← Piano: light, airy, readable
across multiple lines with
generous line-height.
  CAPTION LABEL    ← Pianissimo: wide tracking, uppercase, barely there
```

### Diagnostic Checklist

```
□ Do large headings use tighter tracking than body text?
□ Does body text have generous line-height (≥ 1.5×)?
□ Do caption/overline labels use wide tracking (+8%+) and ALL CAPS?
□ Is there a perceptible "rhythm" when scanning top-to-bottom?
□ Are there at most 3 weight variations visible per viewport?
```

---

## Principle 2: Eliminating Typographic "Holes" — Uniform Gray Density

**Theorem:** `Squint Test → Even Gray = Good Typography`

Squinting at a layout (or viewing it blurred/from distance) should reveal an even, smooth "gray" distribution. Two failure modes destroy this:

### Failure Mode A: Dark Clumps (过于拥挤)

**Symptom:** Dense blocks of text or tightly packed elements create areas that appear as dark blobs.

```
❌ Dark clump:
┌─────────────────────────┐
│TITLE SUBTITLE ICON BADGE│  ← Everything crammed together
│TEXT TEXT TEXT TEXT TEXT...│     creates a dark mass
│TEXT TEXT TEXT TEXT TEXT...│
└─────────────────────────┘

✅ Even gray:
┌─────────────────────────┐
│                         │
│  Title                  │  ← Generous padding creates
│  Subtitle               │     breathing room
│                         │
│  Body text flows here   │
│  with comfortable       │
│  line height.           │
│                         │
└─────────────────────────┘
```

### Failure Mode B: White Holes (尴尬的孤立空间)

**Symptom:** Awkward empty spaces where orphaned elements sit isolated, creating unintentional visual "voids."

```
❌ White hole:
┌─────────────────────────┐
│  Title                  │
│                         │
│                         │  ← Awkward void — too much space
│                         │     with nothing meaningful
│              [tiny btn] │  ← Orphaned element
└─────────────────────────┘

✅ Even gray:
┌─────────────────────────┐
│                         │
│  Title                  │
│  Subtitle               │  ← Content fills space naturally
│                         │
│  [Button with purpose]  │  ← Anchored to content group
│                         │
└─────────────────────────┘
```

### The Squint Test Protocol

1. Blur the screenshot (Gaussian blur radius: 8-10px) or squint
2. Look at the resulting gray map
3. Mark any areas that are significantly darker or lighter than the average
4. Each anomaly represents a typographic rhythm violation

### Diagnostic Checklist

```
□ Does the layout pass the squint test (even gray distribution)?
□ Are there no "dark clumps" (overcrowded areas)?
□ Are there no "white holes" (awkward empty voids)?
□ Is every piece of whitespace intentional (creating groups, not leftover)?
□ Does the layout feel "balanced" when viewed from arm's length?
```

---

## Principle 3: Visual Gravity — F-Pattern & Z-Pattern

**Theorem:** `Core Information → On the Natural Reading Path`

Human eyes follow predictable scanning patterns. Place the most important information where the eye naturally lands.

### F-Pattern (Content-Heavy Screens)

Used for list views, settings pages, data dashboards — anywhere with multiple text blocks.

```
Eye path:
→→→→→→→→→→→→→→→→   ← First horizontal sweep (title/header)
→→→→→→→→→→             ← Second, shorter sweep (subtitle/summary)
↓                        ← Vertical scan down left edge
→→→→→→                  ← Occasional horizontal dip into content
↓
→→→→→→→→
↓
[CTA at bottom-left]     ← Decision point
```

**Rule:** Place the most important element (title, hero metric) at the **top-left** where the first sweep begins.

### Z-Pattern (Single-Focus Screens)

Used for landing pages, login screens, splash pages — single-action screens.

```
Eye path:
→→→→→→→→→→→→→→→→   ← Top sweep: logo / brand mark
                  ↘     ← Diagonal scan
              ↘          
→→→→→→→→→→→→→→→→   ← Bottom sweep: CTA / action button
```

**Rule:** Place brand identity at **top-left**, primary CTA at **bottom-right** — connected by the natural diagonal.

### Mobile-Specific Adaptation: Thumb Zone

On mobile, the thumb's comfortable reach zone overrides pure visual patterns:

```
┌──────────────────┐
│  ░░ HARD ░░░░░░  │  ← Stretch zone — info display only
│  ░░ STRETCH ░░░  │
│                  │
│   COMFORTABLE    │  ← Primary interaction zone
│     ZONE         │  ← Core tappable elements here
│                  │
│  [PRIMARY CTA]   │  ← Bottom = easiest thumb reach
└──────────────────┘
```

### Diagnostic Checklist

```
□ Is the most important info in the F-pattern's first sweep area (top)?
□ Does the CTA sit in the Z-pattern's terminal position (bottom)?
□ Are primary interactive elements in the thumb's comfortable zone?
□ Does the eye flow naturally from top-left to bottom-right?
□ Is there a clear "visual entry point" that captures attention first?
```

---

## Forensic Application

When analyzing a screenshot for typographic rhythm:

### Step 1: Grayscale Conversion
Convert the screenshot to grayscale. Remove all color information to isolate pure typographic rhythm.

### Step 2: Squint Test
Blur/squint at the grayscale version. Mark dark clumps and white holes.

### Step 3: Tracking Analysis
Extract visible text elements. Verify that large text uses tight tracking and small text uses wide tracking.

### Step 4: Reading Path Overlay
Draw F or Z pattern lines over the layout. Check if core content falls on the natural reading path.

### Step 5: Diagnose
```
If dark clumps present → "Overcrowded zone at [location] — add breathing room"
If white holes present → "Dead space at [location] — redistribute content or reduce container"
If tracking uniform   → "No typographic tension — tighten hero text, widen captions"
If core info off-path → "Key content at [location] is off the F/Z reading path"
```
