# Interaction & Motion Physics

A static design is a dead design. This guide defines *how it feels* — across all mobile stacks.

---

## 1. Spring System — The Only Easing You Need

Avoid `ease-in-out`. Use spring dynamics for natural motion.

### Parameter Presets

| Preset | Damping | Stiffness | Mass | Use Case |
|--------|---------|-----------|------|----------|
| **Snappy** | 15 | 400 | 0.8 | Button press, toggle, chip select |
| **Gentle** | 20 | 150 | 1.0 | Card expand, modal present |
| **Bouncy** | 10 | 300 | 0.6 | Playful reveals, celebrations |
| **Heavy** | 25 | 200 | 1.5 | Drawer slide, sheet dismiss |
| **Micro** | 18 | 500 | 0.5 | Scale feedback, press state |

### React Native (Reanimated)

```typescript
import { withSpring } from 'react-native-reanimated';

// Snappy preset
const snappy = withSpring(targetValue, {
  damping: 15, stiffness: 400, mass: 0.8,
});

// Gentle preset
const gentle = withSpring(targetValue, {
  damping: 20, stiffness: 150, mass: 1.0,
});
```

### SwiftUI

```swift
// Snappy
.animation(.spring(response: 0.3, dampingFraction: 0.7), value: isExpanded)

// Gentle
.animation(.spring(response: 0.5, dampingFraction: 0.8), value: isExpanded)

// Bouncy
.animation(.spring(response: 0.4, dampingFraction: 0.5), value: isExpanded)

// iOS 17+ interactive spring
.animation(.interactiveSpring(response: 0.3, dampingFraction: 0.7), value: isExpanded)
```

### Flutter

```dart
// Snappy — use SpringSimulation
final spring = SpringDescription(mass: 0.8, stiffness: 400, damping: 15);

// Or use Curves for simpler animations
AnimatedContainer(
  duration: Duration(milliseconds: 300),
  curve: Curves.easeOutBack, // closest to "bouncy"
  // ...
);

// spring_simulation for physics-based
final simulation = SpringSimulation(spring, 0, 1, 0);
```

### Jetpack Compose

```kotlin
// Snappy
val snappy = spring<Float>(
    dampingRatio = Spring.DampingRatioMediumBouncy,
    stiffness = Spring.StiffnessHigh
)

// Gentle
val gentle = spring<Float>(
    dampingRatio = Spring.DampingRatioNoBouncy,
    stiffness = Spring.StiffnessLow
)

// Bouncy
val bouncy = spring<Float>(
    dampingRatio = Spring.DampingRatioHighBouncy,
    stiffness = Spring.StiffnessMedium
)

// Usage
val scale by animateFloatAsState(
    targetValue = if (pressed) 0.96f else 1f,
    animationSpec = snappy
)
```

---

## 2. Haptic Feedback Mapping

| Interaction | Haptic Level | Description |
|-------------|-------------|-------------|
| Toggle/Switch | Light | Subtle confirmation |
| Button tap | Medium | Standard action feedback |
| Success | Success | Task completed |
| Error/Warning | Heavy + Error | Red flag moment |
| Long press engage | Heavy | "Locked in" moment |
| Scroll snap | Selection | Detent/tick feel |
| Delete action | Warning + Heavy | Destructive action warning |

### React Native (Expo)

```typescript
import * as Haptics from 'expo-haptics';

Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Medium);
Haptics.notificationAsync(Haptics.NotificationFeedbackType.Success);
Haptics.selectionAsync();
```

### SwiftUI / UIKit

```swift
// UIKit (works in SwiftUI too)
let generator = UIImpactFeedbackGenerator(style: .medium)
generator.impactOccurred()

let notification = UINotificationFeedbackGenerator()
notification.notificationOccurred(.success)

// SwiftUI sensory feedback (iOS 17+)
.sensoryFeedback(.impact(weight: .medium), trigger: tapped)
```

### Flutter

```dart
import 'package:flutter/services.dart';

HapticFeedback.mediumImpact();
HapticFeedback.lightImpact();
HapticFeedback.heavyImpact();
HapticFeedback.selectionClick();
```

### Jetpack Compose

```kotlin
val view = LocalView.current
view.performHapticFeedback(HapticFeedbackConstants.CONFIRM)
view.performHapticFeedback(HapticFeedbackConstants.REJECT)
view.performHapticFeedback(HapticFeedbackConstants.LONG_PRESS)
```

---

## 3. Choreography — Staggered Entrance

Elements must enter sequentially, never all at once.

### The Stagger Pattern

```
Element 1:    0ms   ████████████
Element 2:   50ms       ████████████
Element 3:  100ms           ████████████
Element 4:  150ms               ████████████
```

- **Stagger delay:** 50ms per element (max 5 elements, then batch)
- **Direction:** Top→Bottom for lists, Center→Out for grids
- **Duration:** Each element's animation = 300-400ms

### React Native (Reanimated)

```typescript
import Animated, { FadeInDown } from 'react-native-reanimated';

{items.map((item, index) => (
  <Animated.View
    key={item.id}
    entering={FadeInDown.delay(index * 50).springify().damping(15)}
  >
    <ItemCard {...item} />
  </Animated.View>
))}
```

### SwiftUI

```swift
ForEach(Array(items.enumerated()), id: \.element.id) { index, item in
    ItemCard(item: item)
        .transition(.move(edge: .bottom).combined(with: .opacity))
        .animation(
            .spring(response: 0.4, dampingFraction: 0.8)
            .delay(Double(index) * 0.05),
            value: isVisible
        )
}
```

### Flutter

```dart
AnimationController + StaggeredAnimation
// Or use flutter_staggered_animations package:
AnimationLimiter(
  child: ListView.builder(
    itemBuilder: (_, index) => AnimationConfiguration.staggeredList(
      position: index,
      duration: Duration(milliseconds: 375),
      child: SlideAnimation(
        verticalOffset: 50.0,
        child: FadeInAnimation(child: ItemCard(items[index])),
      ),
    ),
  ),
)
```

### Jetpack Compose

```kotlin
items.forEachIndexed { index, item ->
    val delay = index * 50
    AnimatedVisibility(
        visible = isVisible,
        enter = fadeIn(
            animationSpec = tween(300, delayMillis = delay)
        ) + slideInVertically(
            animationSpec = spring(stiffness = Spring.StiffnessLow),
            initialOffsetY = { it / 2 }
        ),
    ) {
        ItemCard(item)
    }
}
```

---

## 4. Scale-on-Press (The Premium Touch)

Every tappable element should respond to touch with a scale effect.

### The Formula

```
Rest state:     scale(1.0)
Pressed:        scale(0.96)  — subtle, professional
Released:       spring back to scale(1.0)
```

### Scale Values by Element

| Element | Press Scale | Notes |
|---------|------------|-------|
| Cards | 0.97 | Subtle, large surface |
| Buttons | 0.95 | Slightly more pronounced |
| Icons | 0.90 | Small target, needs more feedback |
| List items | 0.98 | Very subtle, avoid jarring in lists |
| Tab bar items | 0.92 | Medium emphasis |

### React Native (Reanimated + Gesture Handler)

```typescript
const scale = useSharedValue(1);

const pressIn = () => {
  scale.value = withSpring(0.96, { damping: 15, stiffness: 400 });
  Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Light);
};
const pressOut = () => {
  scale.value = withSpring(1, { damping: 15, stiffness: 400 });
};

const animatedStyle = useAnimatedStyle(() => ({
  transform: [{ scale: scale.value }],
}));
```

### SwiftUI

```swift
struct ScaleButton: ButtonStyle {
    func makeBody(configuration: Configuration) -> some View {
        configuration.label
            .scaleEffect(configuration.isPressed ? 0.96 : 1)
            .animation(.spring(response: 0.3, dampingFraction: 0.7),
                       value: configuration.isPressed)
    }
}

// Usage
Button("Tap me") { }
    .buttonStyle(ScaleButton())
```

### Flutter

```dart
class ScaleOnPress extends StatefulWidget { ... }

// In build:
GestureDetector(
  onTapDown: (_) => _controller.reverse(),
  onTapUp: (_) => _controller.forward(),
  onTapCancel: () => _controller.forward(),
  child: ScaleTransition(
    scale: _animation, // Tween(begin: 0.96, end: 1.0)
    child: child,
  ),
)
```

### Jetpack Compose

```kotlin
val interactionSource = remember { MutableInteractionSource() }
val isPressed by interactionSource.collectIsPressedAsState()
val scale by animateFloatAsState(
    targetValue = if (isPressed) 0.96f else 1f,
    animationSpec = spring(dampingRatio = 0.7f, stiffness = 400f)
)

Box(
    modifier = Modifier
        .graphicsLayer { scaleX = scale; scaleY = scale }
        .clickable(interactionSource = interactionSource, indication = null) { }
)
```

---

## 5. Transition Patterns

### Hero Animation (Morphing)
Elements should transform into the next state, not simply slide.

| Stack | API |
|-------|-----|
| React Native | `react-native-shared-element` or layout animations |
| SwiftUI | `NavigationTransition` / `matchedGeometryEffect` |
| Flutter | `Hero` widget |
| Compose | `SharedTransitionLayout` (experimental) |

### Sheet/Modal Presentation
- **Enter:** Slide up + fade (300ms, gentle spring)
- **Dimming:** Background dims to 40% black over 200ms
- **Dismiss:** Velocity-based — fast flick = dismiss, slow = snap back
- **Reduced motion:** Instant appear/disappear, no animation

### The "Young" Factor — Acid Luxury Touches
- High saturation accents (Electric Blue, Acid Green) against deep black/white
- **Glow effects:** Subtle radial gradient behind accent elements
- **Variable blur:** Background blur increases on scroll (8→20pt)

---

## 6. First-Principles Motion Physics

> This section provides the theoretical foundation for *why* the above presets work — rooted in real-world physics and cognitive psychology.

### 6.1 The Ban on Linear Motion

**Theorem:** `Nothing in nature starts or stops instantly at constant speed.`

In the physical world, every object has mass and therefore inertia. Motion always involves acceleration and deceleration. Linear (constant-speed) animation feels synthetic and unsettling because it violates the brain's lifelong experience of how objects behave.

| Easing Type | Physics Analogy | When to Use |
|-------------|----------------|-------------|
| **Spring (preferred)** | Object attached to a spring — overshoots, settles | Almost everything: buttons, cards, modals, toggles |
| **Ease-out (decelerate)** | Ball thrown upward — fast start, slow stop | Elements entering the viewport |
| **Ease-in (accelerate)** | Ball dropped — slow start, fast end | Elements exiting the viewport |
| **Linear** | — (unnatural) | ❌ Never for UI motion. Only for continuous progress bars |

**Bézier Curve vs Spring Model:**

```
Bézier:  Predefined path, fixed duration.
         cubic-bezier(0.25, 0.1, 0.25, 1.0)  ← "Apple ease"
         ✅ Predictable timing, ❌ No overshoot, ❌ No mass feel

Spring:  Physics-based, duration is emergent from parameters.
         mass: 0.8, stiffness: 400, damping: 15  ← "snappy"
         ✅ Natural overshoot, ✅ Mass/inertia feel, ✅ Responds to interruption
```

**Rule:** Prefer spring for interactive UI (interruptions are common). Use Bézier only for sequenced animations where exact timing is needed (celebration choreography).

### 6.2 Staggered Choreography Theory (多米诺骨牌 / 水波纹)

**Theorem:** `Simultaneous appearance = shocking. Sequential appearance = elegant.`

When multiple elements appear at once, the brain receives a "flash" of information — overwhelming and unstructured. Adding 50–100ms delays between elements creates a **domino cascade** or **ripple effect** that the brain can naturally follow.

| Stagger Pattern | Direction | Effect | Use Case |
|----------------|-----------|--------|----------|
| **Waterfall** | Top → Bottom | Gravity-like natural flow | Vertical lists, card stacks |
| **Ripple** | Center → Edges | Expanding energy | Grid layouts, dashboard tiles |
| **Wave** | Left → Right | Reading-direction flow | Horizontal carousels, tab bars |
| **Cascade** | Back → Front | Depth revelation | Z-layered compositions |

**Optimal Parameters:**
- **Per-element delay:** 40–80ms (faster = energetic, slower = dramatic)
- **Max elements before batching:** 5 (beyond 5, group remaining into one batch)
- **Total sequence duration:** ≤ 500ms (longer feels sluggish)

### 6.3 Micro-Interaction Certainty (毫秒级确定性)

**Theorem:** `Touch → Response < 100ms = "I am in control." > 200ms = "Is it broken?"`

The human perception threshold for "instant" feedback is approximately 100ms. Every finger interaction (tap, press, swipe) must produce a visual + haptic response within this window to maintain the user's sense of **agency and control**.

| Response Time | User Perception | Design Action |
|--------------|-----------------|---------------|
| **< 50ms** | Instantaneous | Haptic fire + scale-down animation begins |
| **50–100ms** | Responsive | Visual state change visible (color, shadow) |
| **100–200ms** | Acknowledged | Animation completes, new state settles |
| **200–500ms** | Waiting | Show progress indicator if content loading |
| **> 500ms** | Broken | Immediate skeleton/spinner required |

**The "Press-Down" Contract:**

```
User finger touches screen (t=0):
  t=0ms:    Haptic fires (Light impact)
  t=0ms:    Scale animation begins (1.0 → 0.96)
  t=50ms:   Background color shifts to pressed state
  t=150ms:  Scale settles at 0.96 (spring physics)

User finger lifts (t=variable):
  t=0ms:    Scale springs back (0.96 → 1.0, with slight overshoot)
  t=0ms:    Background color returns to default
  t=0ms:    Action fires (navigation, API call, etc.)
```

This contract ensures the user **always** feels physically connected to the interface — digital buttons feel like physical buttons.
