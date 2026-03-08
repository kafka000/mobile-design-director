# UX Psychology Playbook — The "Michelin Chef" Framework

A product's core logic is "raw meat" — nutritious but inedible without preparation. This document codifies the three-stage culinary process that transforms functional code into addictive experiences.

---

## Stage 1: 去腥 — Remove Friction (UX Interaction Layer)

> **Goal:** Eliminate everything that makes users feel stupid, anxious, or overwhelmed.

### 1.1 Slice-and-Feed (Progressive Disclosure)

**The problem:** A 15-field form or a data-heavy dashboard dumped on a single screen.

**The fix:** Slice the steak into bite-sized pieces. One question per card. Auto-detect what you can. Show a chunky progress bar that constantly flatters: "Amazing! Just one more step!"

| Anti-Pattern | Pro Pattern |
|-------------|------------|
| All 15 fields on one scrollable page | 3–5 step wizard, 1–3 fields each |
| Raw data table with 20 columns | Layered: summary card → tap for details |
| "Fill in your address" (manual input) | Auto-detect location → "Is this right?" (1-tap confirm) |
| No progress indicator | Animated progress bar + encouraging micro-copy |

**Business impact:** Dramatically lowers cognitive resistance. Users unknowingly complete complex conversion funnels. **Registration/completion rates can double.**

### 1.2 The Undo Safety Net (Fear Elimination)

**The problem:** User taps delete. System shows a terrifying modal: "⚠️ WARNING: This action is irreversible!"

**The fix:** Let them delete freely. After deletion, a gentle toast slides in from top: "Deleted. ↩️ Undo (5s)". No scary warnings, no anxiety.

| Anti-Pattern | Pro Pattern |
|-------------|------------|
| "Are you sure? This cannot be undone!" modal | Toast: "Done. ↩️ Undo" with countdown |
| Red warning icon + aggressive text | Neutral icon + calm, conversational text |
| Blocking confirmation dialog | Non-blocking, auto-dismissing snackbar |
| Preventing the action | Allowing the action with easy reversal |

**Business impact:** Safety nets make users brave. They explore deeper features they'd otherwise avoid. **Feature discovery rate increases significantly.**

### 1.3 Smart Defaults (Reduce Decision Fatigue)

**The problem:** Every setting requires the user to make a choice from scratch.

**The fix:** Pre-fill the most common/optimal choice. Present it as "recommended". Make changing it easy but optional.

```
❌ "Select your goal:" [Empty dropdown]
✅ "Your goal: Lose Weight (recommended)" [Change →]
```

**Business impact:** Users who don't have to think, convert faster. **Setup completion time drops 40-60%.**

---

## Stage 2: 增香 — Inject Dopamine (UX Dynamic Layer)

> **Goal:** Transform "task completed" into "I NEED to do that again."

### 2.1 Sensory Micro-Feedback (Touch → Dopamine)

**The problem:** User taps "like". Database: `likes += 1`. Screen: icon color changes. Flat, dead, forgettable.

**The fix:** Every finger touch must feel like popping bubble wrap:

```
Touch event sequence (< 200ms total):
1. Icon: scale(1.3) → spring-back to scale(1.0)     [40ms]
2. Color: burst-fill with particle confetti           [60ms]
3. Haptic: single crisp tap (UIImpactFeedbackGenerator.medium)  [instant]
4. Optional: tiny counter animates up (+1)            [100ms]
```

| Interaction | Minimum Feedback |
|-------------|-----------------|
| Like / Favorite | Scale bounce + color burst + haptic tap |
| Complete task | Confetti shower + progress ring fill + haptic success |
| Pull to refresh | Rubber-band stretch + spinner morph + haptic light |
| Swipe to delete | Elastic drag + red reveal + haptic warning |
| Toggle switch | Thumb slide + color transition + haptic toggle |

**Business impact:** Visual + tactile dual stimulation triggers physiological dopamine release. Users return tomorrow to feel that micro-pleasure again. **DAU retention increases measurably.**

### 2.2 Gamified Data Visualization (Numbers → Story)

**The problem:** "You studied 41 minutes today. 5-day streak."

**The fix:** Transform cold metrics into emotional narrative:

| Raw Data | Gamified Version |
|----------|-----------------|
| "41 minutes studied" | Liquid tube slowly filling with color, 82% full |
| "5-day streak" | 🔥 Burning 3D flame icon + GIANT "5" + "DAY STREAK!" |
| "2,340 calories" | Animated ring gauge with gradient glow |
| "Level 12" | XP bar with sparkle animation at current progress |
| "3 tasks left" | RPG-style quest checklist with checkmark animations |

**Business impact:** Competitive drive ignites. "My tube is almost full, I MUST do 10 more minutes!" **Session duration and next-day retention increase dramatically.**

### 2.3 Celebration Moments (Emotional Peaks)

**The problem:** User completes a milestone. System: `alert("Congratulations!")`.

**The fix:** Detect the emotional peak and deploy maximum sensory reward:

```
Milestone achieved → Full-screen celebration sequence:
1. Screen dims slightly (cinematic focus)          [0ms]
2. 3D badge/trophy drops in with spring physics    [200ms]
3. Gold particle rain from top                     [400ms]
4. Large typography: achievement text               [600ms]
5. Haptic: triple success pattern                   [0-800ms]
6. Share button fades in (social currency moment)   [1200ms]
```

**Business impact:** This is the "screenshot moment." Users capture and share. **Organic viral growth via social proof.**

---

## Stage 3: 增光添彩 — Premium Packaging (UI Visual Layer)

> **Goal:** Make users trust you on sight and advertise for you for free.

### 3.1 The Halo Effect (Beauty = Trust)

**The problem:** A technically brilliant fintech/health/education app with the visual quality of a government form.

**The fix:** Deploy luxury aesthetics to hack the brain's trust circuitry:

| Signal | Implementation |
|--------|---------------|
| Lavish whitespace | 32pt+ section gaps, 24pt+ card padding |
| Perfect roundness | 20-24pt card radii, pill buttons |
| Restrained palette | 80% neutrals, accent only on CTA + data |
| Premium typography | Extreme size contrast, wide-tracked whisper labels |
| Micro-craftsmanship | Hairline borders, layered shadows, subtle glass |

**Psychology:** "If it looks THIS premium, the company behind it must be serious and trustworthy."

**Business impact:** First-impression trust. **Paid conversion rates increase significantly** because users feel safe handing over money/data.

### 3.2 Social Currency Manufacturing (The Brag Card)

**The problem:** User hits 100-day streak. System: `toast("Congratulations on 100 days!")`.

**The fix:** This is the user's emotional PEAK. Deploy maximum visual resources:

```
Achievement Poster Blueprint:
┌─────────────────────────────────────┐
│                                     │
│   [Brand logo, subtle]              │
│                                     │
│         🏆                          │
│                                     │
│        100                          │  ← 64pt, Black weight
│     DAY STREAK                      │  ← 11pt, wide tracking, gold
│                                     │
│   ── Sarah's Journey ──             │  ← Personalized
│                                     │
│   Started: Jan 1  ·  Today: Apr 10  │
│   Top 3% of all users              │  ← Social proof
│                                     │
│   [Share to Instagram]  [Save]      │
│                                     │
│   powered by YourApp               │  ← Watermark = free ad
│                                     │
└─────────────────────────────────────┘
```

**Requirements for the brag card:**
- Magazine-quality typography and layout
- Personalized with user's name and stats
- Subtle brand watermark (free advertising when shared)
- Pre-formatted for Instagram/WeChat story dimensions
- "Top X%" social proof amplifier

**Business impact:** Users share to flex, not to help you. But every share is a precision-targeted free ad. **Viral loop closes: their friends see it → download → become users → share their own cards.**

---

## The Three-Stage Checklist

Before shipping any feature, run it through this filter:

```
┌─ Stage 1: 去腥 (Friction) ─────────────────────────┐
│ □ Can the flow be split into fewer, simpler steps?  │
│ □ Are destructive actions reversible (undo toast)?   │
│ □ Are smart defaults reducing decision count?        │
│ □ Is error messaging calm, human, and helpful?       │
│ □ Are loading states engaging (skeleton, not blank)? │
└─────────────────────────────────────────────────────┘
         ↓
┌─ Stage 2: 增香 (Dopamine) ──────────────────────────┐
│ □ Does every tap have sensory feedback (visual+haptic)?│
│ □ Are metrics gamified (rings, tubes, flames, XP)?    │
│ □ Are milestones celebrated with full ceremony?       │
│ □ Is there a "share moment" at emotional peaks?       │
└──────────────────────────────────────────────────────┘
         ↓
┌─ Stage 3: 增彩 (Premium) ───────────────────────────┐
│ □ Does the visual quality trigger the halo effect?    │
│ □ Is there a shareable "brag card" for achievements?  │
│ □ Is the brag card magazine-quality with brand mark?  │
│ □ Would a user screenshot this to show friends?       │
└──────────────────────────────────────────────────────┘
```
