# Platform Design Guidelines

Quick reference for cross-platform mobile design decisions — covering iOS, Android, and universal patterns.

---

## 1. Apple HIG — Core Touch Points

### Touch Targets

| Element | Minimum Size | Recommended | Notes |
|---------|-------------|-------------|-------|
| Buttons | 44×44pt | 48×48pt | Apple's absolute minimum |
| Icons (tappable) | 44×44pt | 44×44pt | Expand hit area, not visual size |
| List rows | 44pt height | 52-60pt | Comfortable thumb reach |
| Tab bar items | 48×49pt | Standard | System tab bar height |
| Navigation bar | — | 44pt height | Standard |

### Safe Areas & Spacing

| Device Feature | Inset | Notes |
|---------------|-------|-------|
| Status bar | 54pt (Dynamic Island) / 44pt | Varies by device |
| Home indicator | 34pt bottom | Must account for gesture area |
| Navigation bar | 96pt total | 44pt bar + 52pt status area |
| Keyboard | ~300pt | Varies; use platform keyboard avoidance |

### Navigation Patterns

| Pattern | When to Use | HIG Compliance |
|---------|------------|----------------|
| Tab bar | 3-5 top-level sections | ✅ Strongly recommended |
| Push navigation | Drill-down hierarchy | ✅ Standard |
| Modal/Sheet | Focused task, creation flows | ✅ Use bottom sheet |
| Full-screen modal | Immersive content (video, AR) | ⚠️ Use sparingly |
| Swipe-back | Return to previous | ✅ Never disable |

### SwiftUI Native Components

```swift
// Tab bar
TabView {
    HomeView().tabItem { Label("Home", systemImage: "house") }
    ProfileView().tabItem { Label("Profile", systemImage: "person") }
}

// Navigation stack
NavigationStack {
    List(items) { item in
        NavigationLink(item.title) { DetailView(item: item) }
    }
    .navigationTitle("Items")
}

// Bottom sheet
.sheet(isPresented: $showSheet) { SheetContent() }
.presentationDetents([.medium, .large])
.presentationDragIndicator(.visible)
```

---

## 2. Material Design 3 — Key Differences

| Aspect | Apple HIG | Material 3 |
|--------|-----------|------------|
| Corner radius | Continuous (Squircle) | Standard rounded |
| Primary action | Bottom-right or inline | FAB (Floating Action Button) |
| Navigation | Tab bar (bottom) | Navigation bar (bottom) or rail |
| Typography | SF Pro | Roboto / system |
| Elevation | Shadows + blur | Tonal elevation (color shift) |
| Sheets | Bottom sheet, pull to dismiss | Bottom sheet with handle |
| Switches | Green/gray toggle | Track + thumb with icons |

### Cross-Platform Decision Matrix

```
✅ Use for both:  Bottom navigation, bottom sheets, cards
⚠️ Platform-adapt: Back button (< iOS / ← Android), status bar style
❌ Avoid mixing:   FAB on iOS, swipe-back on Android Material
```

### Jetpack Compose Native Components

```kotlin
// Bottom navigation
NavigationBar {
    items.forEach { item ->
        NavigationBarItem(
            selected = currentRoute == item.route,
            onClick = { navigate(item.route) },
            icon = { Icon(item.icon, contentDescription = item.title) },
            label = { Text(item.title) }
        )
    }
}

// FAB
FloatingActionButton(onClick = { }) {
    Icon(Icons.Default.Add, contentDescription = "Add")
}

// Bottom sheet
ModalBottomSheet(onDismissRequest = { }) {
    SheetContent()
}
```

### Flutter Native Components

```dart
// Bottom navigation
NavigationBar(
  destinations: [
    NavigationDestination(icon: Icon(Icons.home), label: 'Home'),
    NavigationDestination(icon: Icon(Icons.person), label: 'Profile'),
  ],
  selectedIndex: _currentIndex,
  onDestinationSelected: (index) => setState(() => _currentIndex = index),
)

// FAB
FloatingActionButton(
  onPressed: () {},
  child: Icon(Icons.add),
)

// Bottom sheet
showModalBottomSheet(
  context: context,
  builder: (context) => SheetContent(),
);
```

---

## 3. React Native + NativeWind Quick Reference

### Common Premium Patterns

```typescript
// Premium card container
className="bg-white/5 dark:bg-white/5 backdrop-blur-xl
           rounded-2xl border border-white/10
           p-5 mx-4 my-2
           shadow-lg shadow-black/10"

// Hero title
className="text-3xl font-black tracking-tight
           text-pp-text-primary"

// Overline / category label
className="text-xs font-medium tracking-widest uppercase
           text-pp-text-secondary"

// Premium CTA button
className="bg-pp-primary-green px-6 py-4 rounded-xl
           active:scale-95 transition-transform"

// Glass surface (dark mode)
className="bg-black/40 backdrop-blur-2xl
           border border-white/8 rounded-3xl"
```

### Spacing Scale (8pt Grid)

```typescript
const spacing = {
  'p-1':  4,   // Micro gap
  'p-2':  8,   // Element internal
  'p-3':  12,  // Compact padding
  'p-4':  16,  // Standard padding
  'p-5':  20,  // Comfortable padding
  'p-6':  24,  // Premium padding
  'p-8':  32,  // Section spacing
  'p-10': 40,  // Large gap
  'p-12': 48,  // Ultra-premium spacing
};
```

---

## 4. Kotlin Multiplatform (KMP/CMP) Notes

When building with Compose Multiplatform:

- **iOS target:** Respect HIG safe areas, use `WindowInsets` for status bar and home indicator
- **Android target:** Follow Material 3 guidelines by default
- **Shared:** Use `expect`/`actual` for platform-specific haptics, navigation transitions
- **Typography:** Bundle fonts in `commonMain/resources` for cross-platform consistency
- **Squircle:** Use `RoundedCornerShape` on Android, add iOS-specific `UIBezierPath` for continuous corners

---

## 5. Accessibility Non-Negotiables

These are **not optional**, regardless of design approach:

| Rule | Minimum | Recommendation |
|------|---------|----------------|
| Color contrast (text) | 4.5:1 (AA) | 7:1 (AAA) |
| Color contrast (large text) | 3:1 | 4.5:1 |
| Touch target | 44×44pt | 48×48pt |
| Focus indicators | Visible | 2px+ solid ring |
| Motion | Respect `prefers-reduced-motion` | Always |
| Screen reader | All interactive elements labeled | Always |
| Text scaling | Support Dynamic Type / system font scaling | Up to 2× |

### Multi-Stack Accessibility

**React Native**
```typescript
<Pressable
  accessibilityRole="button"
  accessibilityLabel="Add to workout"
  accessibilityHint="Adds this exercise to your current routine"
>
```

**SwiftUI**
```swift
Button("Add") { }
    .accessibilityLabel("Add to workout")
    .accessibilityHint("Adds this exercise to your current routine")
```

**Flutter**
```dart
Semantics(
  label: 'Add to workout',
  hint: 'Adds this exercise to your current routine',
  button: true,
  child: ElevatedButton(onPressed: () {}, child: Text('Add')),
)
```

**Jetpack Compose**
```kotlin
Button(
    onClick = { },
    modifier = Modifier.semantics {
        contentDescription = "Add to workout"
    }
) { Text("Add") }
```

### Decorative Elements — Hide from Screen Readers

| Stack | API |
|-------|-----|
| React Native | `accessibilityElementsHidden={true} importantForAccessibility="no"` |
| SwiftUI | `.accessibilityHidden(true)` |
| Flutter | `ExcludeSemantics(child: ...)` |
| Compose | `Modifier.clearAndSetSemantics { }` |
