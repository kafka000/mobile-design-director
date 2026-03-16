# Container Micro-Texture — The Physical Quality of Surfaces

First-principles surface design for premium UI containers. Even a blank card should never be just a flat colored rectangle. Master designers build a "micro-climate" inside every container using **edge physics**, **material grain**, and **localized light**.

> **Formula:** `[1px Inner Border] + [Noise/Grain Overlay] + [Local Inner Glow] = Premium Container`

> For glassmorphism standards, see `visual-architecture.md`.
> For shadow layers, see `aesthetic-formulas.md`.

---

## Technique 1: The 1px Physical Highlight

**Theorem:** `Edge Light = Perceived Physical Material`

Real-world objects made of glass, acrylic, or polished metal have a thin highlight along their cut edge where light catches the surface geometry. Simulating this with a **1px semi-transparent inner stroke** instantly elevates a flat card to feel like a physical object.

### Implementation

| Mode | Border Spec | Effect |
|------|------------|--------|
| **Dark mode** | `1px solid rgba(255, 255, 255, 0.08–0.15)` | Subtle white edge glow |
| **Light mode** | `1px solid rgba(0, 0, 0, 0.03–0.06)` | Barely perceptible shadow edge |
| **Glass surface** | `1px solid rgba(255, 255, 255, 0.12–0.20)` | Frosted glass rim catch |

### Multi-Stack Code

**React Native (NativeWind)**
```typescript
className="border border-white/10 rounded-2xl"
// Or for inner stroke simulation:
style={{
  borderWidth: StyleSheet.hairlineWidth,
  borderColor: 'rgba(255,255,255,0.12)',
}}
```

**SwiftUI**
```swift
RoundedRectangle(cornerRadius: 20, style: .continuous)
    .fill(Color.black.opacity(0.3))
    .overlay(
        RoundedRectangle(cornerRadius: 20, style: .continuous)
            .stroke(Color.white.opacity(0.12), lineWidth: 0.5)
    )
```

**CSS (Web/PWA)**
```css
.premium-card {
    border: 1px solid rgba(255, 255, 255, 0.10);
    /* For true inner border: */
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08);
}
```

### Diagnostic Checklist

```
□ Do cards have a visible but subtle edge highlight?
□ Is the highlight ≤ 1px and semi-transparent (not opaque)?
□ Does the border color match the mode (white on dark, dark on light)?
□ Is the opacity between 0.06 and 0.20 (visible but not distracting)?
□ Does the highlight use the same corner radius as the container?
```

---

## Technique 2: Noise / Grain Overlay

**Theorem:** `Pure Gradient + Noise = Film/Organic Quality`

Pure digital gradients look "too CG" — eerily smooth and synthetic. Overlaying a very low-opacity noise texture (2%–5%) gives surfaces a warm, organic quality reminiscent of film photography, textured paper, or frosted glass.

### Noise Parameters

| Parameter | Value | Effect |
|-----------|-------|--------|
| **Opacity** | 2%–5% | Barely visible — felt more than seen |
| **Frequency** | Fine grain (1px dots) | Photographic film quality |
| **Color** | Monochrome (white noise) | Neutral, doesn't shift palette |
| **Blend mode** | Overlay or Soft Light | Preserves underlying color integrity |

### When to Apply

| Surface | Apply Noise? | Why |
|---------|-------------|-----|
| Large gradient backgrounds | ✅ Always | Eliminates banding artifacts, adds depth |
| Glass/frosted surfaces | ✅ Always | Simulates frosted glass texture |
| Solid dark surfaces | ✅ Subtle (2%) | Adds warmth, prevents "dead screen" feel |
| Small UI elements (buttons) | ❌ Never | Too small to perceive, wastes rendering |
| Photography/images | ❌ Never | Already has natural grain |

### Multi-Stack Implementation

**React Native** — Use a pre-rendered noise PNG overlay:
```typescript
<View style={styles.container}>
  <Image
    source={require('@/assets/textures/noise-2pct.png')}
    style={[StyleSheet.absoluteFill, { opacity: 0.03 }]}
    resizeMode="repeat"
  />
  {/* Card content */}
</View>
```

**CSS (Web/PWA)** — Use SVG filter:
```css
.textured-surface {
    position: relative;
}
.textured-surface::after {
    content: '';
    position: absolute;
    inset: 0;
    opacity: 0.04;
    background-image: url('/noise-256.png');
    background-repeat: repeat;
    mix-blend-mode: overlay;
    pointer-events: none;
}
```

**SwiftUI** — Use a noise material:
```swift
Rectangle()
    .fill(.ultraThinMaterial)
    .overlay(
        Image("noise-texture")
            .resizable(resizingMode: .tile)
            .opacity(0.03)
            .blendMode(.overlay)
    )
```

### Diagnostic Checklist

```
□ Do large gradient surfaces show noise/grain texture?
□ Is the noise opacity ≤ 5% (barely perceptible)?
□ Is the noise fine-grained (1px) and monochrome?
□ Are small elements (buttons, chips) free of noise overlay?
□ Does the frosted glass feel "physically textured" rather than "digitally smooth"?
```

---

## Technique 3: Localized Light Source (Inner Glow)

**Theorem:** `Directional Light on Container = Physical Material`

Real materials reflect light from a specific direction. By using multiple **inner shadows** to create a faint highlight in one corner (typically top-left, simulating overhead+left lighting), containers feel like they're made of a real material — resin, frosted acrylic, or brushed metal.

### Light Source Direction

The conventional light direction in UI is **top-left** (matching natural overhead lighting and cognitive expectations from physical interfaces).

```
     ☀️ Light source
      ↘
  ┌────────────────────┐
  │ ░░ highlight       │  ← Subtle glow at top-left corner
  │ ░                  │
  │                    │
  │                    │
  │              ▓▓▓▓▓ │  ← Slightly darker at bottom-right (shadow side)
  └────────────────────┘
```

### Implementation

Use multiple inner shadows for realistic lighting:

```css
/* Two-layer inner glow */
box-shadow:
    /* Top-left highlight */
    inset 8px 8px 24px rgba(255, 255, 255, 0.04),
    /* Bottom-right shadow (ambient occlusion) */
    inset -4px -4px 16px rgba(0, 0, 0, 0.08);
```

**React Native** — Since RN doesn't support inner shadows natively, use LinearGradient:
```typescript
<LinearGradient
    colors={['rgba(255,255,255,0.06)', 'transparent', 'rgba(0,0,0,0.04)']}
    start={{ x: 0, y: 0 }}
    end={{ x: 1, y: 1 }}
    style={StyleSheet.absoluteFill}
/>
```

**SwiftUI** — Use gradient overlay:
```swift
RoundedRectangle(cornerRadius: 20, style: .continuous)
    .fill(Color.gray.opacity(0.1))
    .overlay(
        LinearGradient(
            colors: [.white.opacity(0.06), .clear, .black.opacity(0.04)],
            startPoint: .topLeading,
            endPoint: .bottomTrailing
        )
        .clipShape(RoundedRectangle(cornerRadius: 20, style: .continuous))
    )
```

### Combined Three-Technique Container

```
┌────────────────────────────────────┐  ← 1px inner border (rgba(255,255,255,0.12))
│ ░░                                 │  ← Inner glow (top-left highlight)
│ ░                          ▒▒▒▒▒▒ │  ← Grain overlay (2% noise)
│                            ▒▒▒▒▒▒ │
│     [Premium Content]      ▒▒▒▒▒▒ │  ← Bottom-right ambient shadow
│                                    │
│                                ▓▓▓ │  ← Darkest corner (away from light)
└────────────────────────────────────┘
```

### Diagnostic Checklist

```
□ Is there a perceptible directional light effect on container surfaces?
□ Is the light direction consistent across ALL containers (same corner)?
□ Is the inner glow subtle (opacity ≤ 0.06 for highlights)?
□ Are all three techniques (border, noise, glow) layered together?
□ Does the container feel like a "physical object" rather than a flat div?
```

---

## Forensic Application

When analyzing a container from a screenshot or code:

### Step 1: Edge Analysis
Zoom into the container edge. Is there a visible but subtle highlight border? What's its opacity and color?

### Step 2: Surface Quality Test
Look at large surfaces. Do they appear perfectly smooth (CG synthetic) or subtly textured (organic)?

### Step 3: Light Direction Check
Look for any directional lighting (brighter corner, darker opposite corner). Is the direction consistent?

### Step 4: Diagnose
```
If edges are hard/opaque or absent → "Missing physical highlight — add 1px inner border"
If surfaces are perfectly smooth → "Missing grain overlay — add 2-4% noise texture"
If no directional light → "Flat surface — add inner glow for material feel"

Combined score:
  3/3 techniques present = "Gallery-grade container quality"
  2/3 present = "Good, one technique missing: [specify]"
  1/3 present = "Basic — needs two more layers of refinement"
  0/3 present = "Flat rectangle — needs full micro-texture treatment"
```
