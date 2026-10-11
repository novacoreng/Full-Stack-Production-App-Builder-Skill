# Adaptive Layouts
Adapt composition to available window size. Use bottom navigation in compact layouts and rail/sidebar or multi-pane navigation when space permits. Reflow single-column into multi-column/list-detail layouts and adapt sheets/cards/grids rather than merely scaling.

## Device safe-area measurements
All mobile/adaptive layouts must use live iOS/Android safe-area and system inset measurements rather than fixed padding assumptions. Include top/bottom/left/right insets for portrait, landscape, foldables, tablets, edge-to-edge and keyboard transitions. Test sticky headers, bottom navigation, floating actions, dialogs, scrolling and content visibility. See `workflows/mobile.md` for platform-specific enforcement and device QA.
