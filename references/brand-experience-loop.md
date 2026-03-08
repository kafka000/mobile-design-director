# Brand Experience Loop — The 4-Act Holistic Design Framework

> **Purpose:** This document enables the skill to operate in **Macro Mode** — reverse-engineering an entire brand experience from a single product concept, not just auditing individual screens.

When a user asks "help me design the entire experience for my app" or "reverse-engineer a brand from this product idea," follow this 4-Act loop. Each act feeds into the next, creating a self-reinforcing viral flywheel.

---

## The Infinite Loop

```
                    ┌──────────────────┐
          ┌────────→│  ACT 1: 场外放毒  │←────────┐
          │         │  External Poison  │         │
          │         └────────┬─────────┘         │
          │                  ↓                    │
          │         ┌──────────────────┐         │
          │         │  ACT 2: 走红毯    │         │
          │         │  Red Carpet      │         │
          │         └────────┬─────────┘         │
          │                  ↓                    │
          │         ┌──────────────────┐         │
          │         │  ACT 3: 过日子    │         │
          │         │  Daily Living    │         │
          │         └────────┬─────────┘         │
          │                  ↓                    │
          │         ┌──────────────────┐         │
          └─────────│  ACT 4: 炫耀反哺  │─────────┘
                    │  Viral Payback   │
                    └──────────────────┘
```

---

## ACT 1: 场外放毒 — External Poison (Pre-Download)

> "Users don't care about your code. They care about: **'What kind of superior human will I become if I use this?'**"

### The "Persona Perfume" Strategy

**Never sell the software. Sell the identity filter.**

| Element | Mediocre | Elite |
|---------|----------|-------|
| App Store screenshots | Raw UI screenshots with feature lists | 3D device mockups at dramatic angles, magazine typography, lifestyle context |
| Social media posts | "New feature: multi-device sync!" | Aspirational video: UI elements flying like a sports car dashboard, electronic music, neon glows |
| Landing page | Feature bullet points | Hero statement: "Join 500K people who [aspirational identity]" |
| Key visual | Product logo on white background | Brand character/mascot in cinematic lighting with signature color palette |

### Deliverables for ACT 1

When operating in Macro Mode, produce:

1. **Brand Persona Statement:** One sentence defining what "ideal self" the user is buying. Example: *"PowerPath users are the 5AM club — disciplined, data-driven athletes who track everything."*
2. **Visual Identity Anchors:** 3-5 visual elements that will be CONSISTENT from ads → App Store → app interior:
   - Signature color (e.g., #BAFD50 neon green)
   - Signature shape (e.g., aggressive rounded corners, pill shapes)
   - Signature motion (e.g., spring-bouncy, Q-elastic)
   - Signature typography (e.g., Poppins Black for hero numbers)
   - Signature tone (e.g., "coach who high-fives you, never scolds")
3. **App Store Screenshot Blueprint:** Exact layout for 5-6 screenshots using the Bento UI aesthetic with 3D mockups

---

## ACT 2: 走红毯 — Red Carpet Entry (First 3 Seconds)

> "The user was seduced by the ad. If the first 3 seconds of the app contradict the ad's vibe, they'll feel catfished and uninstall immediately."

### The "Zero Break" Principle

The emotional frequency of the marketing material must **seamlessly continue** into the app's opening experience. No jarring transitions.

| Element | Break (Bad) | Continuity (Good) |
|---------|-------------|-------------------|
| App launch | 2-second white screen → system permission dialog | Brand logo spring-animates → morphs into first screen |
| Permission request | Cold system modal: "Allow location access?" | Brand mascot peeks up: "Hey! Mind if I turn on your radar? 🗺️" |
| Onboarding | 5 screens of text explaining features | Interactive mini-journey: user taps through beautiful cards, each with ONE action |
| First data entry | Empty form with placeholder text | Pre-filled smart defaults + "This look right?" confirmation |

### Motion Bridge Protocol

The transition from splash → first screen must obey the same physics as the brand's established motion language:

```
If brand motion = "Q-elastic bouncy":
  Splash logo → scale(0) → spring overshoot → settles at scale(1)
  Logo elements → morph into first-screen UI containers
  Cards → stagger-enter from bottom with spring physics

If brand motion = "Liquid smooth":
  Splash → cross-dissolve with 600ms ease
  Elements → slide in with bezier curves, no bounce
  Cards → fade-in with slight upward drift
```

### Deliverables for ACT 2

1. **Splash → Home transition spec:** Exact animation sequence (timing, easing, transforms)
2. **Permission request redesign:** Branded, conversational, non-threatening
3. **Onboarding flow:** Max 3-5 steps, each with one action, using brand visual language
4. **Empty state designs:** What does each screen look like before user has data?

---

## ACT 3: 过日子 — Daily Living (Sustained Usage)

> "Flashy animations get boring after day 3. The brand's 'swagger' must be distilled into 'body chemistry' — felt everywhere but never loud."

### The "Invisible Personality" Principle

After onboarding excitement fades, the brand's identity must survive as a **subtle ambient presence**, not as constant fireworks.

| Layer | How Brand Lives Here |
|-------|---------------------|
| Color | 80% neutral canvas, brand color only on CTA + current-state indicators |
| Typography | Brand font for hero numbers only; system font for body text (performance) |
| Motion | Micro-springs on interactions (felt, not watched); no gratuitous animation |
| Copy/Tone | Error messages, empty states, tooltips ALL speak in brand voice |
| Sound/Haptic | Consistent haptic language: light tap = navigation, medium = action, heavy = milestone |

### Error States as Brand Moments

**How a product handles failure reveals its character more than how it handles success.**

| Scenario | Generic (Brand Death) | Branded (Brand Life) |
|----------|----------------------|---------------------|
| Network error | 🔴 "Error 500: Server unreachable" | 🛸 Beautiful illustration: "Oops! Aliens stole the wifi. Retrying..." |
| Empty search | "No results found" | Cute mascot shrug: "Hmm, nothing here yet. Try something else?" |
| No data yet | Blank white screen | Illustrated onboarding hint: "Your journey starts here. Tap + to begin!" |
| Session timeout | "Session expired. Login again." | Friendly nudge: "Welcome back! We kept your seat warm 🪑" |
| 3 days inactive | Push: "Come back and use our app!" | Widget dims, mascot cries (Duolingo guilt-trip effect) |

### Deliverables for ACT 3

1. **Tone of Voice Guide:** 5-10 example phrases showing brand personality in UI copy
2. **Error/Empty State Library:** Branded illustrations + copy for all failure scenarios
3. **Haptic Language Map:** Which haptic pattern maps to which interaction type
4. **Daily-Use Color Budget:** How the 80/20 rule manifests in the home screen vs. detail screens

---

## ACT 4: 炫耀反哺 — Viral Payback (The Flywheel)

> "This is the nuclear step. Weaponize vanity. Make your UI design ITSELF become the brand's sharpest free advertisement."

### The "Social Currency" Strategy

**Don't ask users to share. Make them NEED to share by manufacturing irresistible brag material.**

```
User completes milestone
         ↓
System detects emotional peak
         ↓
Full-screen celebration ceremony (see ux-psychology-playbook.md §2.3)
         ↓
Generate magazine-quality "Achievement Poster"
  - Personalized (their name, their stats)
  - Beautiful (could hang on a wall)
  - Social proof ("Top 3% of users")
  - Brand watermark (subtle, but present)
  - Pre-formatted for Instagram Story / WeChat Moments
         ↓
User shares to flex their identity
         ↓
Friends see it → "What app is this?!" → Download
         ↓
🔄 LOOP BACK TO ACT 1
```

### Achievement Poster Design Spec

Every shareable asset must pass this quality gate:

| Criterion | Requirement |
|-----------|------------|
| Typography | Magazine-grade: 64pt+ hero number, 11pt whisper labels |
| Personalization | User's name, specific stats, date range |
| Social proof | "Top X% of users" or comparative stat |
| Brand presence | Subtle logo + app name watermark (bottom) |
| Dimensions | Pre-cropped for Instagram Story (9:16) AND feed (4:5) |
| Color | Uses brand signature palette, NOT generic gradients |
| Shareability | One-tap share button appears at emotional peak |
| Quality | Would the user frame this on their wall? If not, redesign. |

### Reverse-Engineering the Loop

When designing a NEW product in Macro Mode, work BACKWARDS from ACT 4:

```
Step 1: What achievement would a user BRAG about?
  → Design the brag card FIRST

Step 2: What celebration makes that moment feel EPIC?
  → Design the ceremony that generates the brag card

Step 3: What daily experience makes users REACH that milestone?
  → Design the daily UI with gamification hooks

Step 4: What promise in the ad makes users WANT that milestone?
  → Design the marketing material that sells the dream
```

### Deliverables for ACT 4

1. **Brag Card Templates:** 2-3 achievement poster designs for key milestones
2. **Celebration Sequence Spec:** Exact animation/haptic sequence for milestone moments
3. **Sharing Infrastructure:** Pre-formatted exports for major social platforms
4. **Viral Metrics:** What to track (share rate, reinstall attribution, social impressions)

---

## The Brand Director's 4-Question Audit

Before launching ANY product, lock the team in a room and align on these:

| # | Question | Department |
|---|----------|------------|
| 1 | **What "ideal self" are we selling?** (What persona does the user become?) | Marketing + Brand |
| 2 | **Do the first 3 seconds seamlessly continue that persona?** (Motion, copy, visuals) | Design + Engineering |
| 3 | **Does daily usage — including error states — reinforce or break that persona?** | Product + Design + Copy |
| 4 | **Is the share moment SO premium that users can't resist flexing it?** (Would they frame it?) | Design + Growth |

If ANY answer is "no" or "not sure," the experience has a leak. Fix it before launch.

---

## Macro Mode vs Micro Mode

| | Micro Mode (Default) | Macro Mode (Brand Architect) |
|---|---|---|
| **Trigger** | "Review this screen" / "Audit this component" | "Design the entire experience" / "Build a brand from scratch" |
| **Scope** | Single screen or component | Full 4-Act experience loop |
| **Output** | Three-Tier Proposal (Safe/Balanced/Avant-Garde) | Brand Bible: persona + visual anchors + 4-act deliverables |
| **References** | visual-architecture, aesthetic-formulas, bento-color-playbook | ALL references + this document |
| **Presentation** | Specific code-level suggestions | Strategic blueprint + tactical specs |
