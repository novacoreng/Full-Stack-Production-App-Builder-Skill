# Mobile
Build mobile-first for iOS and Android. Support safe areas, system bars, keyboard/insets, dynamic type, permissions, lifecycle, deep links, notifications, offline behavior, and state restoration. Test compact, standard, large, tablet, portrait, landscape, and resizable environments.


## Runtime/device QA
Before production readiness, discover Android/iOS targets actually available. Verify Android targets through ADB; verify iOS only when macOS/Xcode tooling can actually run it. Install/launch the real app where possible, test navigation/forms/media/theme/network/restart/permissions and product-specific journeys, monitor Metro/Logcat/native/runtime logs, and distinguish EMULATOR/SIMULATOR VERIFIED from PHYSICAL DEVICE VERIFIED. Physical hardware may be required for camera, biometrics, real push, background execution, deep links, microphone/voice, Bluetooth, NFC, real network transitions, and provider SDK behavior. Follow `device-interactive-qa.md`.

## Mandatory iPhone and Android safe-area enforcement
Always enable and consume platform-provided safe-area and system-bar insets for every mobile app and mobile web/PWA screen. Never assume fixed universal pixel values for iPhone notches, Dynamic Island, status bars, home indicators, Android status/navigation bars or gesture navigation. Measurements are dynamic and must be read from the actual device/window, including orientation, display cutouts, immersive/edge-to-edge modes, keyboard and inset changes.

For React Native/Expo, configure the supported safe-area provider at the application root and use safe-area insets or SafeAreaView correctly for screen content, sticky headers, bottom tabs, floating actions, sheets and dialogs. Handle Android WindowInsets and edge-to-edge behavior for the installed Android SDK and target. Do not double-apply insets when navigation or components already consume them.

For native iOS use UIKit safeAreaLayoutGuide or SwiftUI safeAreaInset/safe-area layout behavior. For native Android use WindowInsetsCompat/WindowInsets, display-cutout handling and edge-to-edge layout as appropriate. For mobile web/PWA use viewport-fit=cover where appropriate, CSS env(safe-area-inset-top/right/bottom/left) and robust fallbacks.

Measure and verify top, bottom, left and right inset handling in portrait/landscape, with keyboard open/closed, gesture and three-button Android navigation, cutout/notch devices, small and large screens. Ensure touch targets, CTA buttons, tab bars, forms, scroll endpoints, modal actions and keyboard-focused fields remain visible and reachable. Record actual device/emulator coverage and any unavailable targets as NOT TESTED/BLOCKED. Safe-area failure blocks mobile UI phase lock.
