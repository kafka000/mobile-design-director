# Color Physics — The Three Chromatic Laws

First-principles color theory for mobile interfaces. These formulas explain *why* certain color combinations feel right — rooted in optics, physics, and human perception.

> For token pipeline, 80/20 allocation, and dark mode elevation, see `visual-architecture.md`.
> For multi-color decisions and Bento grid integration, see `bento-color-playbook.md`.

---

## Law 1: The 60-30-10 Spatial Allocation

**Theorem:** `Visual Harmony = Dominant(60%) + Secondary(30%) + Accent(10%)`

Color in interfaces must have a strict hierarchy. Even distribution (33/33/33) is the #1 cause of visual chaos.

### The Three Layers

| Layer | Budget | Role | Typical Values |
|-------|--------|------|----------------|
| **60% — Base Tone** | Background / Surface | Sets the page "temperature" and serves as the canvas for whitespace. Must be extremely restrained. | Light: `#F5F5F0` (warm off-white) · Dark: `#12121A` (deep charcoal) |
| **30% — Secondary** | Cards / Secondary Elements | Differentiates information hierarchy. Card backgrounds, deselected states, secondary buttons. Must maintain extremely low contrast against the base tone — same color family, slight adjustment. | Light: `#FFFFFF` (pure white cards on off-white) · Dark: `#1C1C22` (elevated surface) |
| **10% — Accent Focus** | CTA / Key Data / Progress | The "eye-catcher." Primary buttons, core metric highlights, active progress bars. Must have extreme saturation or brightness to capture attention instantly. | `#BAFD50` (neon green) · `#F65555` (fire red) · `#FFD556` (energy yellow) |

### Diagnostic Checklist

When analyzing a screenshot, measure the approximate area percentage:

```
□ Does the background/base tone occupy ~60% of the viewport?
□ Are card surfaces and secondary elements confined to ~30%?
□ Are high-saturation accents compressed to ≤10% surface area?
□ If accents exceed 10%, does the interface feel "noisy" or "garish"?
□ Is there a clear visual hierarchy: floor → furniture → flowers?
```

### Common Violations

| Violation | Symptom | Fix |
|-----------|---------|-----|
| Accent overuse (>15%) | Interface feels like a carnival | Reduce accent to data elements only (icons, rings, bars) |
| No 60% base | Everything is equally important | Establish a dominant neutral background |
| 30% too different from 60% | Jarring card-to-background transition | Reduce contrast between card and base (same hue family) |

---

## Law 2: HSB Shadow/Highlight Physics

**Theorem:** `Realistic Variants = Same Hue (H) + Physical S/B Adjustment`

When generating dark mode variants, hover states, or pressed states, **never change the hue**. Instead, follow real-world light physics to adjust Saturation (S) and Brightness (B).

### The Two Rules

| Effect | Saturation (S) | Brightness (B) | Physical Analogy |
|--------|---------------|----------------|------------------|
| **Shadow / Dark state** | ↑ Increase S (+10-20%) | ↓ Decrease B (-15-30%) | Object in shadow: colors darken and become richer/more saturated |
| **Highlight / Light state** | ↓ Decrease S (-15-25%) | ↑ Increase B (+15-25%) | Object in strong light: colors wash out and become paler |

### Interactive State Matrix (Example: Brand Green #BAFD50)

```
                    H       S       B
Default:           81°     69%     99%
Hover (highlight): 81°     54%     100%    ← S↓15%, B↑1%
Pressed (shadow):  81°     82%     82%     ← S↑13%, B↓17%
Disabled:          81°     15%     60%     ← S↓↓, B↓↓ (desaturated gray)
```

### Multi-Stack Implementation

**React Native (NativeWind)**
```typescript
// Generate shadow variant
const shadow = adjustHSB(baseColor, { s: +15, b: -20 });
// Generate highlight variant  
const highlight = adjustHSB(baseColor, { s: -15, b: +15 });
```

**SwiftUI**
```swift
let shadow = Color(hue: 0.225, saturation: 0.84, brightness: 0.80)
let highlight = Color(hue: 0.225, saturation: 0.54, brightness: 1.0)
```

### Diagnostic Checklist

```
□ Do pressed/hover states maintain the same hue as the default?
□ Do dark variants increase saturation while decreasing brightness?
□ Do light variants decrease saturation while increasing brightness?
□ Are disabled states achieved by extreme S↓ + B↓ (grayish)?
□ Is the transition between states smooth and physically plausible?
```

---

## Law 3: WCAG Contrast — Information Clarity

**Theorem:** `Beautiful + Unreadable = Failed Design`

Dribbble-style aesthetics sometimes sacrifice readability. True beauty must be built on utility.

### Minimum Contrast Ratios

| Element Type | Minimum Ratio | Standard | Notes |
|-------------|---------------|----------|-------|
| **Body text** (< 18pt) | **4.5:1** | WCAG AA | Non-negotiable for all readable text |
| **Large text** (≥ 18pt bold / 24pt regular) | **3:1** | WCAG AA | Hero numbers, display headings |
| **Interactive controls** | **3:1** | WCAG 2.1 | Button borders, input outlines, focus rings |
| **Decorative elements** | **No minimum** | — | Intentionally low contrast to recede (e.g., subtle halos, background gradients) |

### The Decorative Contrast Strategy

Maximize information clarity by using contrast contrast:
- **Content elements**: high contrast (4.5:1+) to dominate attention
- **Decorative elements**: intentionally low contrast (1.5:1 or less) to recede into background

```
┌───────────────────────────────────────────┐
│                                           │
│   ░░░ soft glow ░░░    ← 1.2:1 ratio     │  Decorative: barely visible
│                                           │
│         540                ← 12:1 ratio   │  Content: maximum clarity
│     KCAL BURNED            ← 4.8:1 ratio  │  Label: clearly readable
│                                           │
│   ░░░ subtle halo ░░░  ← 1.3:1 ratio     │  Decorative: mood only
│                                           │
└───────────────────────────────────────────┘
```

### Diagnostic Checklist

```
□ Does all body text achieve ≥ 4.5:1 against its direct background?
□ Do hero numbers achieve ≥ 3:1 (large text exemption)?
□ Are decorative elements intentionally below 2:1 to avoid competing?
□ Do buttons/inputs have ≥ 3:1 border contrast in all states?
□ In dark mode: are text colors bright enough against #1C1C22?
□ In light mode: are text colors dark enough against #F5F5F0?
```

### Tools

| Tool | Use |
|------|-----|
| [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) | Quick pair check |
| [Stark Plugin](https://www.getstark.co/) | Design file integration |
| `color-contrast-calc` (npm) | Programmatic checking |
| Xcode Accessibility Inspector | Live app audit |

---

## Forensic Application

When reverse-engineering a design from a screenshot:

### Step 1: Measure the 60-30-10 Split
Use eyedropper to sample dominant areas. Calculate approximate percentage of viewport occupied by each layer.

### Step 2: Extract HSB Values
For each accent color, extract its H/S/B. Check if hover/pressed states follow the physical S/B rules.

### Step 3: Run Contrast Audit
Sample text-on-background pairs. Calculate contrast ratios. Flag any below WCAG thresholds.

### Step 4: Diagnose
```
If 60/30/10 is off → "Spatial allocation imbalance"
If HSB rules violated → "Non-physical state transitions"
If contrast fails → "WCAG violation at [specific location]"
```
