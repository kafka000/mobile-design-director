# Asset & Imagery Strategy

How to handle photography, icons, illustrations, and badges so they **enhance** — rather than undermine — the design system. This document defines the compositional rules for integrating real-world assets into a token-driven interface.

> For corner radius values, see `aesthetic-formulas.md`. For haptic presets, see `motion-physics.md`. For component state matrices, see `visual-architecture.md`.

---

## 1. Photography — Staging Real Images

Raw photos with cluttered backgrounds destroy premium UI instantly. The principle: **extract the subject, let the system provide the stage.**

### Mandatory Cutouts

All core imagery (exercise library, coach portraits, hero shots) must be delivered as **transparent-background PNGs** or masked at render time.

| Asset Type | Background Treatment | Why |
|-----------|---------------------|-----|
| Exercise demos | Alpha-transparent cutout | System controls the backdrop via tokens |
| Coach/trainer portraits | Alpha-transparent cutout | Enables dark/light mode adaptation |
| Lifestyle/motivational | Full-bleed with **heavy blur or gradient overlay** | Never raw; always processed |
| User-uploaded photos | Contained within a token-controlled frame | Prevents visual chaos |

### System-Controlled Backdrops

Place cutout subjects onto backgrounds managed by design tokens:

```
Normal state:       bg-surface with subtle gradient
Achievement (PR):   High-saturation gradient burst
Rest day:           Muted, desaturated surface
Dark mode:          bg-surface-elevated with soft radial glow
```

The background **reacts to context** without changing the asset itself. One cutout, many moods.

### Out-of-Bounds Composition

Let subjects **break the card boundary** to inject energy. A dumbbell edge or athlete's head extending past the container conveys dynamism while keeping the grid intact.

```
┌─────────────────────────┐
│                    ╱    │
│    540 kcal      ╱     │
│    BURNED       👤←── subject extends 20-30pt
│               ╱        │    beyond card top edge
│             ╱           │
└─────────────────────────┘
```

Implementation:
- Use **negative margin** or **absolute positioning** to overflow the container
- Set `overflow: visible` on the parent card
- Constrain overflow to **one edge only** — breaking more than one edge looks broken, not intentional
- Max overflow: 20–30pt beyond the card boundary

---

## 2. Dual-Track Iconography

Balance professionalism and personality by maintaining **two strictly separated icon systems**. Never mix their styles within the same context.

### Track A — Functional Icons

**Where:** Navigation bars, settings lists, data panels, form inputs.

| Property | Specification |
|----------|--------------|
| Stroke weight | 1.5–2px, consistent across the set |
| Style | Geometric, clean cuts, optically balanced |
| Reference | SF Symbols (iOS), Material Symbols (Android) |
| Color | Monochrome — inherits from `text-secondary` or `text-tertiary` token |
| Sizes | 20pt (inline), 24pt (standard), 28pt (prominent) |

These icons establish the app's **professional, high-end** baseline. They should be invisible — functional, not decorative.

### Track B — Expressive Assets & Badges

**Where:** Streak rewards, achievement badges, empty states, upgrade prompts, celebration moments.

| Property | Specification |
|----------|--------------|
| Style | 3D claymorphism, bold gradients, high-saturation illustration |
| Shape | Oversized rounded forms, playful proportions |
| Color | High-saturation accents against the neutral UI — deliberate contrast |
| Animation | Always animated on reveal (see `motion-physics.md` for spring presets) |
| Haptics | Always paired with tactile feedback on interaction (see `motion-physics.md`) |

The **visual contrast** between the minimal neutral interface and a sudden high-saturation 3D badge creates a dopamine hit — especially effective for Gen Z engagement patterns.

### Mixing Rules

```
✅  Functional icons in navigation + Expressive badge in achievement modal
✅  Functional icons in data panel + Expressive illustration in empty state
❌  Expressive badge as a navigation icon
❌  Functional line icon as an achievement reward
❌  Both styles in the same card or row
```

---

## 3. Shape Language & Exaggerated Radii

> For exact corner radius values and squircle availability per platform, see `aesthetic-formulas.md` and `platform-guidelines.md`.

### Unified Shape Tokens

All image containers, cards, and asset frames share from a single radius token set. No ad-hoc `borderRadius` values.

### Friendly Exaggeration

To balance hardcore fitness content with approachability, push corner radii **larger than industry standard**:

| Standard App | This System | Effect |
|-------------|------------|--------|
| 8–12pt cards | 16–20pt cards | Softer, more inviting |
| 8pt buttons | 12–14pt buttons | Rounded but still professional |
| 12pt image frames | 16–20pt image frames | "Bouncy" feel that softens intensity |

Combined with bold typography (see `visual-architecture.md` Anchor + Whisper), the oversized radii create a "friendly premium" personality — premium without being cold.

### Continuous Curvature

All rounded shapes must use **continuous curvature (squircle)** where platform-supported. Standard `border-radius` circles create visible kinks at large radii that undermine the smooth feel. See `aesthetic-formulas.md` for platform-specific implementation.

---

## 4. Asset Loading Engineering

> `visual-architecture.md` defines the 5-state component lifecycle. This section covers **asset-specific** loading strategies.

Premium feel is destroyed by white flashes, content jumps, or abrupt image appearances during loading.

### Aspect-Ratio Placeholders

Before any remote image loads, display a placeholder container that **exactly matches** the final image dimensions:

| Requirement | Specification |
|------------|--------------|
| Aspect ratio | Must match the loaded image (e.g. 16:9, 1:1, 3:4) |
| Fill | Theme-matched neutral tone with subtle pulse animation |
| Pulse timing | 1.5s cycle, opacity oscillating between 0.04 and 0.08 |
| Corner radius | Matches the final image container |

Never show a blank white rectangle or a mismatched-size skeleton.

### Fade-In Transition

All remote images must execute a **200–300ms opacity fade-in** on load completion. No abrupt appearance.

```
t=0ms:     Image loaded, opacity = 0
t=0-250ms: opacity 0 → 1 (ease-out curve)
t=250ms:   Fully visible
```

This must be enforced at the **component level** — wrap the standard Image component so every remote image automatically fades in. Developers should not need to remember to add this.

### Expressive Asset Reveals

Track B assets (badges, achievements, celebrations) deserve more ceremony than a simple fade:

| Asset | Reveal Pattern | Duration |
|-------|---------------|----------|
| Achievement badge | Scale 0 → 1.05 → 1.0 (spring overshoot) + fade-in | 400ms |
| Streak fire icon | Slide up + fade + bounce | 350ms |
| Empty state illustration | Fade-in + subtle float | 500ms |
| Upgrade prompt visual | Scale-in from center + glow pulse | 450ms |

Pair all Track B reveals with haptic feedback (see `motion-physics.md` for appropriate levels).

---

## Quick Checklist

| Principle | ❌ Anti-pattern | ✅ Correct |
|-----------|---------------|-----------|
| Photography | Raw photo with cluttered background | Transparent cutout on token-controlled backdrop |
| Photo composition | Subject fully contained inside card | Controlled out-of-bounds overflow on one edge |
| Functional icons | Decorative, colorful, varied stroke weights | Monochrome, 1.5–2px stroke, geometric |
| Expressive assets | Used in navigation or data panels | Reserved for achievements, celebrations, empty states |
| Icon mixing | Both styles in the same component | Strict separation — one track per context |
| Shape language | Ad-hoc border-radius per component | Shared radius tokens, continuous curvature |
| Image loading | Blank rect → abrupt image pop-in | Ratio-matched placeholder → 250ms fade-in |
| Badge reveal | Static image, no motion or haptics | Spring animation + haptic feedback |
