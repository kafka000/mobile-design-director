# Data Visualization Art — Turning Numbers into Sensory Experiences

First-principles data visualization for mobile apps. Transform cold charts from "Excel dread" to "visual pleasure" by removing clinical scaffolding and injecting Dribbble-grade aesthetics.

> **Formula:** `[Axis-less] + [Smooth Fat Splines] + [Glowing Nodes & Gradient Fills] = Emotional Data Charts`

> For gamified data visualization (dopamine layer), see `ux-psychology-playbook.md` §2.2.
> For color allocation in data charts, see `bento-color-playbook.md` Decision 1.

---

## Principle 1: Strip the Scaffolding (去坐标轴化)

**Theorem:** `Data Aesthetics = Signal / Chrome`

The "chrome" (axes, gridlines, tick marks, legends) of traditional charts is designed for precision reading (scientific papers, Excel). In mobile UI, precision is secondary to **emotional impression** — the user needs to feel "I'm doing great" or "I need to catch up," not "my value is exactly 2,347."

### What to Remove

| Element | Traditional | Premium Mobile |
|---------|------------|----------------|
| X-axis line | Thick black line | ❌ Remove entirely |
| Y-axis line | Thick black line | ❌ Remove entirely |
| Grid lines | Full grid overlay | Remove, or use 1–2 ultra-faint horizontal reference lines (opacity 0.03) |
| Tick marks | Every data point | ❌ Remove — let the curve speak |
| Dense labels | Every X tick labeled | Show only first/last, or key milestones |
| Legend box | Separate box with color keys | Inline color labels directly on data |

### What to Keep

| Element | Purpose | Treatment |
|---------|---------|-----------|
| Start/End values | Context anchoring | Whisper-style labels (10pt, medium, muted) |
| Current value | Hero "anchor" | Display large and bold at chart top or tooltip |
| Trend direction | Emotional signal | The curve shape itself communicates this |
| Time range | Context | Subtle label below chart |

### Example Transformation

```
BEFORE (Clinical):
│ 2400 ┤
│ 2000 ┤──────╱──╮
│ 1600 ┤────╱────╰────
│ 1200 ┤──╱
│  800 ┤╱
│      └──┴──┴──┴──┴──
         M   T   W   T   F

AFTER (Emotional):
          2,340 kcal ← Hero number (28pt, bold)
         ╱‾‾‾‾╲
    ∕‾‾‾╱      ╲‾‾‾‾‾  ← Fat smooth curve with glow
  ╱                        
Mon              Today     ← Whisper labels only at edges
```

### Diagnostic Checklist

```
□ Are X and Y axis lines removed or invisible?
□ Are grid lines removed or ultra-faint (opacity ≤ 0.05)?
□ Is the data shape immediately readable without any labels?
□ Are only essential reference points labeled (start, end, current)?
□ Does the chart feel "artistic" rather than "clinical"?
```

---

## Principle 2: Fat Smooth Splines (极粗平滑曲线)

**Theorem:** `Data Lines = Neon Light Tubes, Not Pencil Marks`

Transform data lines from thin, angular traces into thick, smooth, glowing curves that feel like luminous neon tubes.

### Specification

| Property | Traditional | Premium |
|----------|------------|---------|
| **Line width** | 1–2pt | **3–4pt** (fat enough to have presence) |
| **Interpolation** | Linear (angular) | **Bezier/Catmull-Rom** (smooth curves) |
| **Line cap** | Butt/square | **Round** (smooth endpoints) |
| **Shadow** | None | **Glow shadow** in line's own color |
| **Gradient** | None | Optional luminosity gradient along the line |

### Glow Effect

The curve should cast a colored glow — like a neon sign tube:

```css
/* The neon glow effect */
.data-line {
    stroke-width: 3.5;
    stroke-linecap: round;
    stroke-linejoin: round;
    filter: drop-shadow(0 0 6px rgba(186, 253, 80, 0.35))
            drop-shadow(0 0 12px rgba(186, 253, 80, 0.15));
}
```

### Multi-Stack Implementation

**React Native (react-native-svg)**
```typescript
<Path
    d={smoothPathData}
    stroke="#BAFD50"
    strokeWidth={3.5}
    strokeLinecap="round"
    fill="none"
/>
{/* Glow layer (duplicate path with blur) */}
<Path
    d={smoothPathData}
    stroke="#BAFD50"
    strokeWidth={8}
    strokeLinecap="round"
    fill="none"
    opacity={0.15}
/>
```

**SwiftUI (Charts)**
```swift
Chart(data) {
    LineMark(x: .value("Day", $0.day), y: .value("Value", $0.value))
        .interpolationMethod(.catmullRom)
        .foregroundStyle(.green)
        .lineStyle(StrokeStyle(lineWidth: 3.5, lineCap: .round))
}
.chartYAxis(.hidden)
.chartXAxis(.hidden)
```

### Diagnostic Checklist

```
□ Is the data line ≥ 3pt wide (substantial, not threadlike)?
□ Does the line use smooth interpolation (no sharp angles)?
□ Are line endpoints round-capped?
□ Does the line cast a colored glow shadow?
□ Does the curve feel like a "glowing neon tube," not a "pencil line"?
```

---

## Principle 3: Gradient Volume Fills (底部渐变填充)

**Theorem:** `Area Fill = Three-Dimensional Volume`

Below the data curve, add a gradient fill that fades from the line color to transparent. This transforms a flat 2D line into a "mountain range" with perceived volume and mass — dramatically increasing the emotional weight of the data.

### Fill Specification

```
Line color:      #BAFD50 (or accent color)
Fill top:        rgba(186, 253, 80, 0.25)     ← Right below the curve
Fill middle:     rgba(186, 253, 80, 0.08)     ← Fading
Fill bottom:     rgba(186, 253, 80, 0.00)     ← Fully transparent at X-axis

Direction: top → bottom (perpendicular to baseline)
```

### Combined Effect

```
         ╱‾‾‾‾╲
    ∕‾‾‾╱      ╲‾‾‾‾‾   ← 3.5pt smooth curve with neon glow
  ╱░░░░░░░░░░░░░░░░░░░   ← Gradient fill (25% → 0% opacity)
╱░░░░░░░░░░░░░░░░░░░░░
░░░░░░░░░░░░░░░░░░░░░░░
░░░░░░░░░░░░ (fading) ░░
░░░░░░ (barely visible) ░
                          ← Transparent at bottom
```

### Multi-Stack Implementation

**React Native (react-native-svg)**
```typescript
<Defs>
    <LinearGradient id="areaFill" x1="0" y1="0" x2="0" y2="1">
        <Stop offset="0" stopColor="#BAFD50" stopOpacity="0.25" />
        <Stop offset="0.5" stopColor="#BAFD50" stopOpacity="0.08" />
        <Stop offset="1" stopColor="#BAFD50" stopOpacity="0" />
    </LinearGradient>
</Defs>
<Path d={areaPathData} fill="url(#areaFill)" />
<Path d={linePathData} stroke="#BAFD50" strokeWidth={3.5} fill="none" />
```

**SwiftUI**
```swift
Chart(data) {
    AreaMark(x: .value("Day", $0.day), y: .value("Value", $0.value))
        .interpolationMethod(.catmullRom)
        .foregroundStyle(
            .linearGradient(
                colors: [.green.opacity(0.25), .green.opacity(0)],
                startPoint: .top, endPoint: .bottom
            )
        )
    LineMark(x: .value("Day", $0.day), y: .value("Value", $0.value))
        .interpolationMethod(.catmullRom)
        .foregroundStyle(.green)
        .lineStyle(StrokeStyle(lineWidth: 3.5, lineCap: .round))
}
```

### Advanced: Glowing Nodes at Data Points

Add small glowing dots at key data points (current value, max, min):

| Node Type | Size | Effect |
|-----------|------|--------|
| Current value | 8pt circle | Filled accent + outer glow (12pt blur) + pulse animation |
| Peak value | 6pt circle | Filled accent + subtle glow |
| Regular data points | ❌ None | Too many dots = visual noise |

### Diagnostic Checklist

```
□ Does the area below the curve have a gradient fill (not flat color)?
□ Does the gradient fade from ~25% opacity to 0% (not abrupt cutoff)?
□ Does the combined curve + fill create a sense of "volume" or "mass"?
□ Are key data points marked with glowing nodes (not all points)?
□ Does the overall chart feel like a "mountain range," not a "flat graph"?
```

---

## Forensic Application

When analyzing a data visualization from a screenshot:

### Step 1: Scaffolding Audit
Count visible chart chrome elements (axes, gridlines, tick marks, dense labels). Each one adds clinical feeling.

### Step 2: Line Quality
Measure approximate line width. Check for smooth interpolation vs angular. Look for glow/shadow effects.

### Step 3: Fill Analysis
Check if area below curves has gradient fill. Verify gradient direction and opacity range.

### Step 4: Diagnose
```
If heavy scaffolding → "Clinical chart — strip axes and gridlines"
If thin angular lines → "Pencil-mark quality — fatten to 3-4pt smooth curves"
If no glow effect → "Flat data line — add neon glow shadow"
If no area fill → "2D chart — add gradient volume fill for emotional weight"
If all present → "Dribbble-grade data visualization ✅"
```
