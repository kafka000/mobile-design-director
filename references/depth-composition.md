# Depth Composition — Breaking the Flat Plane

First-principles techniques for creating three-dimensional depth perception and cinematic visual interlocking in mobile interfaces. Combines image-text interplay from editorial design with "presentation meta" strategies for Dribbble/portfolio-grade compositions.

> **Part 1 Formula:** `[Oversized Background Typography] + [Foreground Obscuration] + [Z-Depth Separation] = Magazine Depth`
> **Part 2 Formula:** `[Mood-Matched Canvas] + [Physical Mockup/Isometric View] + [Floating Ornaments] = Presentation Meta`

---

## Part 1: Interlocking Composition — Image-Text Depth

Traditional layout keeps image and text strictly separated. Premium editorial design deliberately interleaves them to create perceived three-dimensionality.

### Technique 1: Oversized Background Typography

**Theorem:** `Giant faded text as backdrop = instant depth layer`

Place core numbers or keywords at extreme scale (200%–400% of normal), reduce opacity to 5%–12%, and use them as a background element. Content renders on top of this typographic backdrop.

```
┌─────────────────────────────────────┐
│                                     │
│    5 4 0                            │  ← 96pt number at 8% opacity = backdrop
│                                     │
│    540                              │  ← 36pt number at 100% = foreground data
│    KCAL BURNED                      │  ← 10pt whisper label
│                                     │
│    [Start Workout →]                │
│                                     │
└─────────────────────────────────────┘
```

### Implementation

```typescript
// React Native — background number layer
<View style={{ position: 'relative' }}>
    <Text style={{
        position: 'absolute',
        fontSize: 120,
        fontWeight: '900',
        color: 'rgba(255,255,255,0.06)',
        top: -20,
        left: -10,
    }}>
        540
    </Text>
    {/* Foreground content */}
    <Text style={{ fontSize: 36, fontWeight: '900' }}>540</Text>
    <Text style={{ fontSize: 10, letterSpacing: 2 }}>KCAL BURNED</Text>
</View>
```

```swift
// SwiftUI
ZStack(alignment: .topLeading) {
    Text("540")
        .font(.system(size: 120, weight: .black))
        .foregroundColor(.white.opacity(0.06))
        .offset(x: -10, y: -20)
    
    VStack(alignment: .leading) {
        Text("540").font(.system(size: 36, weight: .black))
        Text("KCAL BURNED").font(.caption2).kerning(2)
    }
}
```

### Technique 2: Foreground Obscuration (Occlusion Depth)

**Theorem:** `Occluding object = brain auto-perceives Z-axis depth`

When a 3D illustration, human figure, or foreground card partially covers background text/content, the brain automatically infers a spatial relationship. This **occlusion cue** is the strongest depth signal in 2D composition.

```
FLAT (no depth):                    INTERLOCKED (depth):
┌──────────────┐                    ┌──────────────┐
│ [text]       │                    │ [te     ╱╲   │  ← subject partially
│              │ [image]            │         │ │   │     covers the text
│              │                    │     540 │👤│  │
│              │                    │         │ │   │
└──────────────┘                    └─────────╲╱───┘
  Perceived depth: 0                  Perceived depth: ++
```

### Technique 3: Z-Axis Layer Separation

Establish clear front/middle/back layers with distinct visual treatments:

| Layer | Z-Depth | Treatment | Example |
|-------|---------|-----------|---------|
| **Background (Z-0)** | Furthest | Blurred, low opacity, or oversized typography | Giant faded number, gradient wash |
| **Middle (Z-1)** | Card/container | Standard rendering, full opacity | Data cards, content containers |
| **Foreground (Z-2)** | Closest | Crisp, high contrast, may cast shadow on Z-1 | Hero subject breaking card bounds, floating badges |

### Rules for Depth Interlocking

```
✅ DO:
  - Let ONE foreground element break ONE card boundary
  - Use oversized type as Z-0 background layer
  - Keep Z-2 elements crisp while Z-0 elements are faded/blurred
  - Maintain logical reading order despite visual overlap

❌ DON'T:
  - Overlap so much that text becomes unreadable
  - Use more than 3 Z-layers (creates confusion)
  - Break multiple card edges simultaneously
  - Place critical information under obscured areas
```

### Diagnostic Checklist

```
□ Is there a visible background layer (oversized type, gradient, blur)?
□ Does at least one element create foreground occlusion?
□ Are Z-layers clearly distinct (different opacity, scale, blur)?
□ Is text still fully readable despite overlapping elements?
□ Does the composition feel "three-dimensional" when eye-scanned?
```

---

## Part 2: Presentation Meta — The "Dribbble Shot" Science

> This section covers presenting UI designs as portfolio shots, screenshots, or promotional materials. These techniques create the "WOW" factor in design showcases.

### Technique 4: Mood-Matched Canvas

**Theorem:** `UI mood must extend into the surrounding canvas`

The background canvas (the area outside the phone frame / card border) should resonate with the UI's emotional temperature.

| UI Mood | Canvas Treatment |
|---------|-----------------|
| **Bright / Energetic** | Soft gradient with floating light orbs, candy-colored mesh |
| **Dark / Premium** | Pure black canvas with a single focused spotlight |
| **Warm / Organic** | Earthy gradient with grain texture |
| **Neon / Cyberpunk** | Dark canvas with colored edge-glow bleeds |

### Technique 5: Breaking Orthographic View

**Theorem:** `Angled perspective = automatic premium perception`

Never present UI as flat rectangular screenshots. Apply 3D perspective or isometric views to showcase interface depth:

| View Type | When to Use | Angle |
|-----------|------------|-------|
| **Isometric** | Showcasing multiple screens simultaneously | 30° rotation on both axes |
| **Perspective tilt** | Hero showcase of single screen | 5–15° Y-axis rotation |
| **Stacked float** | Showing navigation flow | Screens overlapping with parallax offset |
| **Device mockup** | App Store screenshots, marketing | High-res 3D device model |

### Technique 6: Floating Ornaments

**Theorem:** `Contextual floating objects = thematic density`

Scatter 3D objects related to the app's domain around the UI presentation:

| App Domain | Ornament Examples |
|-----------|------------------|
| **Fitness** | Dumbbells, protein shakes, activity rings, running shoes |
| **Finance** | Coins, credit cards, calculators, gem stones |
| **Health** | Pills, molecules, heart icons, DNA helixes |
| **Education** | Pencils, lightbulbs, graduation caps, books |
| **Music** | Notes, headphones, equalizer bars, vinyl records |

### Ornament Rules

```
✅ DO:
  - Use 3D rendered objects with consistent lighting direction
  - Scatter 3–5 objects maximum around the UI element
  - Vary sizes (1 large, 2 medium, 2 small) for natural composition
  - Add slight motion blur to imply movement
  - Match object material finish to the UI's aesthetic (glossy UI = glossy objects)

❌ DON'T:
  - Use more than 5 ornaments (clutter, not enrichment)
  - Mix lighting directions across ornaments
  - Use flat 2D clip-art (destroys premium feel)
  - Place ornaments over critical UI content
  - Make ornaments larger than the UI element they support
```

### Combined Presentation Meta

```
┌─────────────────────────────────────────────────────┐
│                                                     │
│          🏋️ (3D dumbbell, floating)                  │
│                                                     │
│        ┌───────────────────────┐                    │
│        │                       │ ← Phone mockup     │
│   💊   │    App Interface      │    at 10° tilt      │
│        │    Content Here       │                    │
│        │                       │    ⚡ (small bolt)  │
│        │    [CTA Button]       │                    │
│        └───────────────────────┘                    │
│                                                     │
│    ═══════════ gradient canvas ═══════════          │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### Diagnostic Checklist (Presentation Meta)

```
□ Does the canvas color/gradient match the UI's emotional temperature?
□ Is the UI presented at an angle (not flat orthographic screenshot)?
□ Are 3-5 thematically relevant ornaments floating in the composition?
□ Do ornaments have consistent lighting and material quality?
□ Does the overall composition feel "magazine-ready"?
```

---

## Forensic Application

When analyzing a design for depth quality:

### Step 1: Layer Count
Identify distinct Z-layers. Can you see background, middleground, and foreground?

### Step 2: Occlusion Check
Is any element partially obscuring another? Does it create a depth cue?

### Step 3: Background Treatment
Is there oversized typography, gradient wash, or blurred element serving as Z-0?

### Step 4: Presentation Quality (for portfolio shots)
Is there a mood canvas? Is the view angled? Are there thematic ornaments?

### Step 5: Diagnose
```
If flat/single-layer → "No depth — add Z-0 background layer (oversized type or gradient)"
If no occlusion → "2D composition — introduce foreground element breaking card boundary"
If orthographic screenshot → "Flat presentation — add 3D perspective or device mockup"
If no ornaments → "Sterile showcase — add 3-5 thematic floating objects"

Depth Score:
  4/4 techniques = "Cinematic depth — portfolio-ready"
  3/4 = "Good depth — one technique missing: [specify]"
  2/4 = "Partial depth — composition feels somewhat flat"
  ≤1/4 = "Flat design — needs full depth treatment"
```
