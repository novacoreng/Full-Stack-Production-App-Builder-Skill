# Mobile
Build mobile-first for iOS and Android. Support safe areas, system bars, keyboard/insets, dynamic type, permissions, lifecycle, deep links, notifications, offline behavior, and state restoration. Test compact, standard, large, tablet, portrait, landscape, and resizable environments.


## Runtime/device QA
Before production readiness, discover Android/iOS targets actually available. Verify Android targets through ADB; verify iOS only when macOS/Xcode tooling can actually run it. Install/launch the real app where possible, test navigation/forms/media/theme/network/restart/permissions and product-specific journeys, monitor Metro/Logcat/native/runtime logs, and distinguish EMULATOR/SIMULATOR VERIFIED from PHYSICAL DEVICE VERIFIED. Physical hardware may be required for camera, biometrics, real push, background execution, deep links, microphone/voice, Bluetooth, NFC, real network transitions, and provider SDK behavior. Follow `device-interactive-qa.md`.
