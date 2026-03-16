# Gestalt Cognition — The Psychology of Visual Parsing

First-principles perceptual psychology for interface design. "Beauty" largely means "extremely low cognitive load" — when the brain doesn't need to struggle to parse a layout, it produces a fluent, comfortable aesthetic experience.

> **Formula:** `[Proximity] + [Similarity] + [Closure] = Logical Beauty`

> For spacing values, see `aesthetic-formulas.md`. For typography tension, see `visual-architecture.md`.

---

## Principle 1: Proximity — Distance Speaks

**Theorem:** `Semantic Distance = Physical Distance`

Elements that are logically related must be physically close. The brain groups items by proximity in under 100ms — making spacing the most silent yet most powerful layout language.

### The Proximity Scale

| Relationship | Gap | Effect |
|-------------|-----|--------|
| **Coupled** (label + its value) | 4–8pt | "These belong together as one unit" |
| **Grouped** (items in same section) | 8–12pt | "These are siblings" |
| **Sectioned** (between groups) | 24–32pt | "New topic begins here" |
| **Segmented** (major page divisions) | 48–64pt | "Separate world" |

### The 3:1 Ratio Rule

Inter-group spacing must be **at least 3× larger** than intra-group spacing. This is the minimum ratio for the brain to automatically parse group boundaries:

```
┌────────────────────────────────────┐
│  Section A                         │
│  ┌──────────────────────────────┐  │
│  │ Item 1          ← 8pt gap   │  │   Intra-group: 8pt
│  │ Item 2          ← 8pt gap   │  │   
│  │ Item 3                      │  │
│  └──────────────────────────────┘  │
│                    ← 32pt gap      │   Inter-group: 32pt (8 × 4 = 4:1 ✅)
│  ┌──────────────────────────────┐  │
│  │ Item 4          ← 8pt gap   │  │
│  │ Item 5                      │  │
│  └──────────────────────────────┘  │
└────────────────────────────────────┘
```

### Proximity Failure Symptoms

```
❌ All gaps identical → brain can't find groups → "Where does X end and Y begin?"
❌ Intra-gap close to inter-gap → ambiguous grouping → "Does this label belong to above or below?"
❌ Label far from its value → coupling broken → "What does this number refer to?"
```

### Diagnostic Checklist

```
□ Can you identify groups by spacing alone (without reading content)?
□ Is the inter-group : intra-group ratio ≥ 3:1?
□ Are labels tightly coupled (4-8pt) to their corresponding values?
□ Do section breaks use noticeably larger gaps than item gaps?
□ Is spacing consistent within the same grouping level?
```

---

## Principle 2: Similarity — Restrained Variables

**Theorem:** `Visual Noise = Number of Unique Visual Variables`

Elements with similar shapes, colors, or typographic treatment are automatically grouped by the brain. In complex information flows, extreme restraint in the number of colors, fonts, and shapes dramatically reduces visual noise and produces a "clean" feel.

### The Restraint Budget

| Variable | Maximum Unique Values | Why |
|----------|----------------------|-----|
| Font families | **2** (1 display + 1 body) | More = typographic chaos |
| Font weights | **3** (400, 600, 900) | More = unclear hierarchy |
| Font sizes | **5–7** (from the type scale) | More = random, no system |
| Colors | **4–5 accent + neutrals** | More = carnival (see `bento-color-playbook.md`) |
| Corner radii | **3** (small, medium, large) | More = inconsistent shapes |
| Shadow depths | **3** (none, sm, lg) | More = random elevation |

### High-Reuse Component Pattern

The fewer unique component variants, the lower the visual noise:

```
✅ Premium feel: 3 card types × consistent styling = clean
   [Stat Card] [Action Card] [Data Card] — all share same radius, padding, shadow

❌ Chaotic feel: 8 card types × inconsistent styling = noisy
   [Card A: round, green] [Card B: square, blue] [Card C: shadow, red] ...
```

### Diagnostic Checklist

```
□ How many unique font sizes are visible on this screen? (Target: ≤ 5)
□ How many unique colors are visible? (Target: ≤ 5 accent + neutrals)
□ How many unique corner radii are used? (Target: ≤ 3)
□ Do similar elements (cards, buttons, labels) look identical across the screen?
□ Can you identify the "template" that repeats?
```

---

## Principle 3: Closure — Whitespace Creates Boundaries

**Theorem:** `Fewer Lines + More Whitespace = Higher Perceived Quality`

The brain automatically "closes" incomplete shapes — it fills in boundaries that aren't drawn. By leveraging generous whitespace instead of explicit border lines, the interface appears cleaner and more sophisticated.

### Closure vs Explicit Boundaries

| Approach | Implementation | Quality Feel |
|----------|---------------|-------------|
| **Hard closure** (lines) | `border-bottom: 1px solid gray` between every item | ❌ Dense, "spreadsheet" feel |
| **Soft closure** (spacing) | 24pt gap between groups, no divider lines | ✅ Premium, "boutique" feel |
| **Material closure** (elevation) | Cards float on background via shadow | ✅✅ Premium, "3D" feel |

### The Line Reduction Checklist

When reviewing a design, count explicit lines/borders. For each one, ask:

```
Can this line be REPLACED by:
  1. More whitespace between elements? (Proximity principle)
  2. A card/container boundary? (Bento grid)
  3. A shadow/elevation change? (Z-axis separation)
  4. A background tint change? (Surface differentiation)

If YES to any → remove the line.
```

### Implicit Grouping Examples

```
EXPLICIT (Low quality):
┌─────────────────────────┐
│ Name: John             │
├─────────────────────────┤    ← Explicit divider lines
│ Age: 28                │
├─────────────────────────┤    ← Explicit divider lines
│ Weight: 75kg           │
└─────────────────────────┘

IMPLICIT (High quality):
┌─────────────────────────┐
│                         │
│  John                   │  ← Name prominent, no labels needed
│                         │
│  28y  ·  75kg  ·  183cm │  ← Data inline, dot separators
│                         │
└─────────────────────────┘    ← Single card = closure
```

### Diagnostic Checklist

```
□ How many explicit divider lines are visible? (Target: 0–2 per viewport)
□ Can you remove any line by increasing spacing instead?
□ Are content groups defined by cards/surfaces rather than lines?
□ Is the layout readable if ALL lines were removed?
□ Do shadows/elevation changes handle Z-axis separation instead of lines?
```

---

## Forensic Application

When reverse-engineering a design from a screenshot:

### Step 1: Proximity Map
Draw invisible boxes around perceived groups. Measure intra-group and inter-group spacing. Calculate the ratio.

### Step 2: Similarity Inventory
Count unique visual variables: font sizes, weights, colors, radii, shadow depths. Flag excess beyond the restraint budget.

### Step 3: Closure Audit
Count explicit lines/borders. For each, determine if whitespace or elevation could replace it.

### Step 4: Diagnose
```
If groups are ambiguous → "Proximity failure — insufficient spacing differentiation"
If > 7 font sizes      → "Similarity violation — too many typographic variables"  
If > 3 divider lines   → "Closure failure — replace lines with whitespace/elevation"

Combined diagnosis:
  Low noise + clear groups + few lines = "Excellent Gestalt compliance"
  High noise + ambiguous groups + many lines = "Cognitive overload — needs simplification"
```
