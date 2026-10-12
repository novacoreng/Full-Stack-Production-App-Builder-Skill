# Expo Dynamic Notifications Capability

Source: user-uploaded `expo-dynamic-notifications-main.zip`. This is a reusable capability assessment, not a forced dependency for every app.

## What the supplied project actually does
The project provides animated **Dynamic Island-style in-app notifications** for Expo / React Native. It is a UI overlay, not Apple's native Dynamic Island or Live Activities API, and not a substitute for remote push notifications, background scheduling, APNs, FCM, or Android system notifications.

The uploaded README documents a `DynamicNotifications` root provider, `useDynamicNotifications()` hook, `trigger()` and `dismiss()`, tap handlers, dismissal callbacks, configurable duration, per-notification title/message/avatar/symbol/accent, custom rendering, and configurable geometry/Skia morph animations.

## When to use
- Evaluate for React Native / Expo apps that explicitly need prominent, animated in-app alert banners.
- Do not install by default or replace the project's existing design/notification behavior without approval.
- Do not promise that this UI can display when the app is closed, locked or backgrounded. Those scenarios require actual OS notifications, and native iOS Live Activities/ActivityKit where the product specifically needs supported Dynamic Island surfaces.
- For Android, an in-app island-like overlay does not imply Android OS-level Dynamic Island support.
- Respect reduced motion, screen readers, focus/touch behavior, safe-area insets, status bars, keyboard, notch/cutout differences and notification preferences.

## Integration guidance
1. Check Expo SDK, React Native and library compatibility with the current project, rather than adopting the uploaded template versions automatically.
2. Evaluate peer dependencies from the supplied README: Skia, Reanimated, Worklets, Gesture Handler, Safe Area Context, Expo Blur, Expo Image and Expo Symbols.
3. In the supplied example, wrap the app navigation with `GestureHandlerRootView`, `SafeAreaProvider` and `DynamicNotifications` at the root. Avoid duplicate providers if the existing app already has them.
4. Trigger only from appropriate app events; support tap-to-route and dismissal, and do not expose sensitive content in a public overlay.
5. Use live safe-area measurements for top placement, verify portrait/landscape and iPhone/Android display cutouts, and avoid covering actionable UI.
6. Test repeated notifications, dismissal, duration, replacement behavior, navigation, screen readers, reduced motion, performance and low-end devices.
7. Keep actual push notification and background-delivery infrastructure separate, following `workflows/mobile.md` and `workflows/phased-github-infrastructure.md`.

## Licensing and provenance
The archive includes an MIT LICENSE with Expo/650 Industries copyright attribution. Before copying source files into another repository, verify provenance, third-party asset/font licensing and required notices. Do not assume that the entire repository and bundled assets have independently verified rights based solely on the root license.

## Skill usage gate
Mark this capability REQUIRED only when the accepted product design calls for this in-app animation. Otherwise mark NOT APPLICABLE with reason. Evidence must distinguish IN-APP ANIMATION TESTED from PUSH DELIVERY TESTED and NATIVE LIVE ACTIVITY TESTED. Never claim the latter two based on the uploaded code.
