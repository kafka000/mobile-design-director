<p align="center">
  <img src="https://img.shields.io/badge/Agent_Skills-compatible-6366f1?style=for-the-badge&labelColor=1e1e2e" alt="Agent Skills compatible" />
  <img src="https://img.shields.io/badge/Stacks-React_Native_%7C_SwiftUI_%7C_Flutter_%7C_Compose-22c55e?style=for-the-badge&labelColor=1e1e2e" alt="Mobile Stacks" />
  <img src="https://img.shields.io/github/license/kafka000/mobile-design-director?style=for-the-badge&labelColor=1e1e2e&color=f59e0b" alt="License" />
</p>

<h1 align="center">📱 Mobile Design Director</h1>

<p align="center">
  <strong>A senior UX/UI Design Director skill for AI coding agents.</strong><br/>
  Audit, elevate, and polish mobile interfaces — across every stack.<br/><br/>
  <a href="https://agentskills.io">Agent Skills</a> ·
  <a href="#installation">Install</a> ·
  <a href="#what-it-does">What It Does</a> ·
  <a href="#supported-stacks">Stacks</a>
</p>

---

## Installation

```bash
npx skills add kafka000/mobile-design-director
```

Works with **35+ AI coding agents** including Claude Code, Cursor, Windsurf, GitHub Copilot, Codex, Gemini CLI, Trae, and more.

> This skill follows the open [Agent Skills](https://agentskills.io/) format.

---

## What It Does

**Mobile Design Director** gives your AI agent the eye of a seasoned design director. It audits mobile UIs against Apple HIG, Material Design 3, and a curated "Young Luxury" aesthetic, then returns actionable, code-level suggestions.

Every response follows a **Three-Tier Proposal** system:

| | Option A: Safe | Option B: Balanced ⭐ | Option C: Avant-Garde |
|---|---|---|---|
| **Approach** | Platform-native components | 80% platform + 20% brand personality | Heavy motion, glassmorphism, "acid luxury" |
| **Dev Cost** | Low | Medium | High |
| **Wow Factor** | ★☆☆ | ★★☆ | ★★★ |

No vague feedback. Every suggestion includes **exact values** — spring damping, tracking percentages, WCAG contrast ratios, corner radii, and shadow layers.

---

## Activation Triggers

The skill automatically activates when you mention:

- `design audit` · `UI review` · `UX audit`
- `UI建议` · `审美讲义` · `交互建议`
- Requests for "premium" or "luxury" design feedback
- Any mobile UI polish, consistency check, or brand alignment review

---

## Supported Stacks

| Stack | Frameworks & Libraries |
|-------|----------------------|
| **React Native** | Expo, NativeWind, Reanimated, Gesture Handler |
| **SwiftUI** | UIKit interop, SF Symbols, `matchedGeometryEffect` |
| **Flutter** | Material 3, Cupertino, `flutter_staggered_animations` |
| **Jetpack Compose** | Material 3, `spring()`, `AnimatedVisibility` |
| **Kotlin Multiplatform** | Compose Multiplatform, shared resources |

---

## Reference Documents

The skill uses three reference guides, loaded on-demand for relevant audits:

### `aesthetic-formulas.md`
Visual silence, typographic scale (Perfect Fourth), glassmorphism 2.0, layered shadows, and the "Acid Luxury" color system — with implementation snippets for all four stacks.

### `motion-physics.md`
Spring presets (Snappy/Gentle/Bouncy/Heavy/Micro), haptic feedback mapping, staggered entrance choreography, and Scale-on-Press patterns — with code for Reanimated, SwiftUI `.spring()`, Flutter `SpringSimulation`, and Compose `animateFloatAsState`.

### `platform-guidelines.md`
Apple HIG touch targets & safe areas, Material 3 comparison matrix, React Native/NativeWind quick reference, KMP/CMP notes, and WCAG accessibility non-negotiables — all with multi-stack code.

---

## Skill Structure

```
mobile-design-director/
├── SKILL.md                         # Entry point with activation rules & workflow
└── references/
    ├── aesthetic-formulas.md        # Spacing, typography, depth, color
    ├── motion-physics.md            # Spring, haptics, choreography, scale
    └── platform-guidelines.md       # HIG, Material 3, a11y, cross-platform
```

---

## Example Usage

Ask your agent:

```
Review this screen for premium design quality.
```
```
Audit the motion and transitions on the home tab.
```
```
UI建议：这个卡片组件的间距和阴影合理吗？
```
```
How should I implement scale-on-press for this button in SwiftUI?
```

---

## Philosophy

1. **The 80/20 Rule** — 80% platform foundation (HIG + Material 3), 20% brand soul.
2. **Design is Physics** — Motion follows spring dynamics. Nothing moves linearly.
3. **Stack-Agnostic Thinking** — Design decisions first, framework adaptation second.
4. **Selectable Optimality** — No single "best." Always three options from safe to experimental.

---

## License

MIT © [kafka000](https://github.com/kafka000)
