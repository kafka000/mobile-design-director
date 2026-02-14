# Aesthetic Formulas & The Science of "Premium"

When the user asks for "High-End," "Premium," or "Modern," apply these theorems.

---

## 1. The Law of Visual Silence

**Theorem:** `Premium = Space / Information`
Luxury is defined by what you *remove*, not what you add.

### Execution

| Element | Standard | Premium | Ultra-Premium |
|---------|----------|---------|---------------|
| Horizontal margin | 16pt | 24pt | 32pt |
| Card padding | 12pt | 16pt | 20pt |
| Section spacing | 24pt | 32pt | 48pt |
| Grid system | 8pt | 8pt strict | 8pt strict |

- **Negative Space:** Treat whitespace as an active element, not empty space.
- **Information Density:** Max 3 visual "zones" per viewport in luxury mode.
- **The Breath Rule:** Every content block needs a "breath" (min 24pt vertical gap).

### Multi-Stack Spacing

| Spacing | React Native (NativeWind) | SwiftUI | Flutter | Compose |
|---------|--------------------------|---------|---------|---------|
| 4pt | `p-1` | `.padding(4)` | `EdgeInsets.all(4)` | `Modifier.padding(4.dp)` |
| 8pt | `p-2` | `.padding(8)` | `EdgeInsets.all(8)` | `Modifier.padding(8.dp)` |
| 16pt | `p-4` | `.padding(16)` or `.padding()` | `EdgeInsets.all(16)` | `Modifier.padding(16.dp)` |
| 24pt | `p-6` | `.padding(24)` | `EdgeInsets.all(24)` | `Modifier.padding(24.dp)` |
| 32pt | `p-8` | `.padding(32)` | `EdgeInsets.all(32)` | `Modifier.padding(32.dp)` |

---

## 2. Typographic Confidence

**Theorem:** Small text + wide spacing = Sophistication. Large text + tight spacing = Power.

### Scale System (Perfect Fourth — 1.333 ratio)

```
Caption:     11pt
Body:        14pt
Subhead:     18pt → 14 × 1.333
Title:       24pt → 18 × 1.333
Display:     32pt → 24 × 1.333
Hero:        42pt → 32 × 1.333
```

### Tracking Rules

| Type | Tracking | Weight | Case |
|------|----------|--------|------|
| Display/Headlines | -1% to -3% | Black/Heavy (800-900) | Sentence case |
| Subheadings | -0.5% | Semibold (600) | Sentence case |
| Body | 0% (default) | Regular (400) | Sentence case |
| Captions/Overlines | +10% to +15% | Medium (500) | ALL CAPS |
| Buttons | +5% | Semibold (600) | ALL CAPS or Title case |

### Font Pairing Strategy

| Stack | Primary (Headlines) | Secondary (Body) | Accent |
|-------|-------------------|------------------|--------|
| iOS / SwiftUI | SF Pro Display | SF Pro Text | SF Mono |
| Android / Compose | Roboto | Roboto | Roboto Mono |
| Flutter | Google Fonts (Outfit, Inter) | System default | Mono variant |
| React Native | Poppins / Inter (custom) | System default | Mono variant |
| Cross-platform | Inter / Outfit | System default | JetBrains Mono |

---

## 3. Depth & Materiality (Glassmorphism 2.0)

**Theorem:** Objects must feel tactile.

### Micro-Borders (Dark Mode)

```
Border:       0.5pt solid rgba(255, 255, 255, 0.10)
Inner glow:   inset 0 0.5pt 0 rgba(255, 255, 255, 0.05)
```

### Multi-Stack Implementation

**React Native (NativeWind)**
```typescript
className="bg-white/5 backdrop-blur-xl rounded-2xl
           border border-white/10 shadow-lg shadow-black/10"
```

**SwiftUI**
```swift
RoundedRectangle(cornerRadius: 24, style: .continuous)
    .fill(.ultraThinMaterial)
    .overlay(
        RoundedRectangle(cornerRadius: 24, style: .continuous)
            .stroke(Color.white.opacity(0.1), lineWidth: 0.5)
    )
    .shadow(color: .black.opacity(0.12), radius: 16, y: 8)
```

**Flutter**
```dart
ClipRRect(
  borderRadius: BorderRadius.circular(24),
  child: BackdropFilter(
    filter: ImageFilter.blur(sigmaX: 20, sigmaY: 20),
    child: Container(
      decoration: BoxDecoration(
        color: Colors.white.withOpacity(0.05),
        borderRadius: BorderRadius.circular(24),
        border: Border.all(color: Colors.white.withOpacity(0.1), width: 0.5),
      ),
    ),
  ),
)
```

**Jetpack Compose**
```kotlin
Box(
    modifier = Modifier
        .clip(RoundedCornerShape(24.dp))
        .background(Color.White.copy(alpha = 0.05f))
        .border(0.5.dp, Color.White.copy(alpha = 0.1f), RoundedCornerShape(24.dp))
)
```

### Super Shadows (Layered)

Use two shadow layers for premium depth:

| Layer | Purpose | Values |
|-------|---------|--------|
| Ambient | Wide, soft | y: 16pt, blur: 48pt, opacity: 0.12 |
| Contact | Tight, dark | y: 2pt, blur: 8pt, opacity: 0.24 |

### Corner Radii

| Element | Radius | Notes |
|---------|--------|-------|
| Cards | 16-20pt | Use continuous curvature (Squircle) |
| Buttons | 12pt | Match card inner radius |
| Chips/Tags | height/2 | Full pill shape |
| Input fields | 10pt | Slightly subdued vs buttons |
| Modal/Sheet | 24pt (top) | iOS sheet pattern |

> **Squircle Rule:** Always use continuous curvature (Superellipse) on iOS. SwiftUI: `RoundedRectangle(style: .continuous)`. React Native: `borderCurve: 'continuous'` (iOS 16+). Flutter/Compose: approximate with larger radii.

---

## 4. Color Psychology for "Young Luxury"

### The Tension Palette

```
Base Layer:     Deep blacks (#0A0A0A) or pure whites (#FAFAFA)
Content Layer:  Neutral grays (#1A1A1A dark / #F5F5F5 light)
Accent:         High saturation "Acid" tones
                Electric Blue: #0066FF
                Acid Green:    #00FF88 / #BAFD50
                Warm Gold:     #FFB800
Surface Glass:  rgba(255,255,255, 0.06) on dark
                rgba(0,0,0, 0.02) on light
```

### Usage Rules
- **Max 1 accent color per screen** for impact
- **Accent only on CTAs and key metrics** — never on decorative elements
- **Gradients:** Subtle, max 2 stops, same hue family (e.g., blue → purple, not blue → green)
