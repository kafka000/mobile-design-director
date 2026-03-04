# Visual Architecture & Surface Quality

Engineering-grade standards for app visual refinement. This document covers **systems-level** design architecture — color token pipelines, information hierarchy through typography tension, and sub-pixel surface craftsmanship. For raw values (spacing tables, shadow layers, font scales), see `aesthetic-formulas.md`.

---

## 1. Color Token Architecture (Design Tokens)

> `aesthetic-formulas.md` defines the palette. This section defines the **pipeline** that governs how color flows from design to code.

### Three-Layer Token Pipeline

Never use raw hex values in UI code. Route every color through a three-layer system:

```
Primitive (raw values, platform-agnostic)
  └─ gray-900, green-500, red-500 …
       ↓
Semantic (intent-based aliases)
  └─ bg-primary, text-secondary, accent-cta, border-subtle …
       ↓
Component (scoped to specific UI elements)
  └─ button-cta-bg, card-surface, input-border-focus …
```

**Why three layers?** Changing a brand color updates one Primitive. All Semantic and Component tokens cascade automatically — no search-and-replace across 200 files.

### The 90/10 Allocation Rule

| Allocation | Role | Examples |
|-----------|------|----------|
| **90% Neutrals** | Structure — backgrounds, containers, text, dividers | `bg-neutral-50`, `text-neutral-900`, `border-neutral-200` |
| **10% Intent** | Directing attention and conveying state | CTA buttons, progress rings, error badges |

High-saturation accent colors are **surgical instruments**, not decoration. Restrict them to:
- Primary CTA buttons ("Start Workout")
- Abnormal state indicators (heart rate warning)
- Progress completion visuals (activity rings)

### Closed-Loop State Management

Every interactive color token must define its full state matrix at definition time:

| State | Background | Text | Border/Ring |
|-------|-----------|------|-------------|
| Default | `accent-cta` | `white` | none |
| Pressed | `accent-cta` at 80% opacity | `white` | none |
| Disabled | `neutral-200` | `neutral-400` | none |
| Focused | `accent-cta` | `white` | `ring-2 accent-cta/50` |

Defining states ad-hoc in individual components leads to inconsistency. Define once in the token layer, consume everywhere.

### Dark Mode Elevation Mapping

In dark mode, use **luminance progression** (not hue) to express Z-axis depth:

```
Z0 (Base):       #0A0A0A    — deepest background
Z1 (Surface):    #141414    — card / container
Z2 (Elevated):   #1E1E1E    — floating element
Z3 (Overlay):    #282828    — modal / popover
```

Additionally, accent colors in dark mode must:
- **Reduce saturation** slightly to prevent eye strain
- **Increase lightness** to maintain WCAG AA contrast (4.5:1 minimum)

---

## 2. Information Hierarchy Through Typography Tension

> `aesthetic-formulas.md` covers the type scale and tracking rules. This section defines the **compositional strategy** — how to use extreme contrast to create premium information hierarchy.

### The Polarity Principle

Premium data displays use **two extremes** — never the middle of the scale:

| Role | Size | Weight | Color | Tracking | Case |
|------|------|--------|-------|----------|------|
| Hero metric | 36–48pt | Black (900) | `text-primary` | Default or negative | Numeric |
| Supporting label | 10–11pt | Medium (500) | `text-tertiary` | +10% to +15% | ALL CAPS |

The dramatic size/weight gap between hero and label **is** the design. It replaces the need for decorative elements, color accents, or visual clutter.

### Anchor + Whisper Pattern

```
┌──────────────────────────┐
│                          │
│         540              │  ← Anchor: 48pt Black
│      KCAL BURNED         │  ← Whisper: 10pt Medium, wide tracking, uppercase
│                          │
└──────────────────────────┘
```

Rules:
- **One anchor per card.** If everything is big, nothing is big.
- **Whisper labels never compete.** They exist only to contextualize the anchor.
- **Vertical gap between anchor and whisper:** Tight (4–8px) to maintain visual coupling.

---

## 3. Space as a Design Material

> `aesthetic-formulas.md` defines the 8pt grid values. This section defines the **philosophy** — how to use space as an active compositional tool.

### Outer-Loose, Inner-Tight Hierarchy

Separate information groups with generous space. **Physical distance replaces divider lines.**

```
┌────────────────────────────────┐
│  Section A                     │
│  ┌──────────────────────────┐  │
│  │ Item 1          8pt gap  │  │  ← Intra-module: tight (8pt)
│  │ Item 2          8pt gap  │  │
│  └──────────────────────────┘  │
│                                │  ← Inter-module: generous (32pt)
│  ┌──────────────────────────┐  │
│  │ Item 3          8pt gap  │  │
│  └──────────────────────────┘  │
└────────────────────────────────┘
```

The ratio should be **at least 3:1** — module spacing ≥ 3× element spacing.

### Generous Container Padding

Data dashboards and stat cards need room to **breathe**:

| Card Type | Recommended Padding | Why |
|-----------|-------------------|-----|
| Hero stat card | 20–32pt | Core number needs isolation to anchor the eye |
| List/detail card | 16–20pt | Denser content tolerates less space |
| Action card (CTA) | 16–24pt | Balance between touch target and visual weight |

---

## 4. Sub-Pixel Surface Craftsmanship

> `aesthetic-formulas.md` defines shadow values and corner radii. This section covers **the micro-details** that separate polished from generic.

### Hairline Borders

Heavy borders (1px+) feel dated. Use sub-pixel borders at near-invisible opacity:

| Mode | Implementation | Effect |
|------|---------------|--------|
| Light | `0.5px solid rgba(0,0,0, 0.05)` | Ghost outline — felt more than seen |
| Dark | `0.5px solid rgba(255,255,255, 0.08)` | Subtle edge definition |

Platform note: React Native on Android rounds sub-pixel borders. Use `StyleSheet.hairlineWidth` for cross-platform consistency.

### Restrained Native Materials

Glassmorphism is powerful but easily overdone. Limit frosted glass to **structural layers only**:

| ✅ Use for | ❌ Avoid for |
|-----------|-------------|
| Navigation bars | Content cards |
| Bottom action panels | Decorative overlays |
| Status overlays | Every floating element |

The blur should be **functional** (indicating layered hierarchy), not decorative.

---

## 5. Design-to-Engineering Alignment

Design quality is zero if it cannot be precisely reproduced in code.

### Token Variable Mapping

Semantic names in design files must **exactly match** the codebase configuration (`tailwind.config.js`, `colors.ts`, `theme.xml`, etc.):

```
Design File Token          Code Token
─────────────────          ──────────
bg/primary          →      bg-primary
text/secondary      →      text-secondary
accent/cta          →      accent-cta
surface/elevated    →      surface-elevated
```

No translation layer. No "close enough." Exact 1:1 mapping.

### Component State Matrix

Every reusable component must be designed and built with its **full lifecycle**:

| State | Visual | Data Condition |
|-------|--------|---------------|
| Default | Normal data display | Data present |
| Empty | Illustration + guidance copy | No data |
| Loading | Skeleton placeholder | Fetching |
| Error | Error message + retry action | Request failed |
| Overflow | Truncation + expand affordance | Data exceeds bounds |

Designing only the "happy path" creates engineering debt. The state matrix is part of the design spec, not an afterthought.

---

## Quick Checklist

| Principle | ❌ Anti-pattern | ✅ Correct |
|-----------|---------------|-----------|
| Color tokens | Raw hex in component code | Semantic token from pipeline |
| Color allocation | Accent used for decoration | Accent restricted to intent (CTA, state) |
| Spacing | Uniform gaps everywhere | 3:1 ratio — loose between modules, tight within |
| Typography | All text at similar size/weight | Extreme polarity: hero anchor + whisper label |
| Borders | `1px solid gray-300` | `0.5px solid black/5` — hairline |
| Shadows | Single default platform shadow | Multi-layer ambient + contact |
| Component design | Only default state designed | Full 5-state lifecycle matrix |
| Dark mode depth | Color shifts for elevation | Luminance steps (Z0–Z3) |
