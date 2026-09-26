# UI Quality, Loading States, Semantic Color, and Accessibility

This workflow applies to every project with a user interface. It is part of the UX/UI, implementation, testing, and production-readiness gates.

## 1. Skeleton loaders

Use skeleton loaders for content that has a predictable structure and is expected to take meaningful time to load.

Requirements:
- Match the approximate geometry of the final content so layout does not jump when data arrives.
- Use skeletons for lists, cards, profile/content blocks, dashboards, tables, and other repeatable content where appropriate.
- Do not use skeletons for instant operations where they add unnecessary visual noise.
- Preserve surrounding navigation and stable controls while content is loading.
- Provide accessible loading status semantics where appropriate.
- Do not expose skeleton placeholders as misleading interactive controls.
- Respect reduced-motion preferences; avoid unnecessary animated shimmer when motion should be reduced.
- Test slow, intermittent, offline, timeout, empty, and error states—not only the successful fast response.

A loading state is a real product state and must be designed, implemented, and tested rather than treated as an afterthought.

## 2. Semantic colors

Use semantic color tokens instead of scattering raw color values through components.

At minimum define tokens for the meanings the product actually needs, such as:
- background/surface
- text/primary/secondary/muted
- border/divider
- interactive/action
- focus
- selected/active
- success
- warning
- error/destructive
- info
- disabled
- overlay

Rules:
- Color must communicate meaning consistently across the product.
- Do not rely on color alone to communicate status, errors, selection, or required actions; pair it with text, icons, shape, position, or another perceivable cue where appropriate.
- Ensure semantic tokens work across light/dark themes when the product supports them.
- Verify text, controls, icons, focus indicators, disabled states, and important non-text UI against applicable contrast requirements.
- Do not choose colors solely because they look good in a design mockup; verify them in the implemented UI.
- Preserve brand identity while allowing accessible semantic states.

## 3. Clutter and visual hierarchy audit

Actively check for cluttered UI elements rather than accepting every requested control as a separate visible element.

Inspect:
- excessive buttons/actions in one region
- repeated labels or redundant information
- competing primary actions
- unnecessary icons
- dense cards and dashboards
- excessive borders/dividers
- excessive badges/chips/tags
- repeated navigation controls
- long forms without grouping
- modal-on-modal flows
- too many persistent controls
- cramped mobile layouts
- controls too close to one another
- unnecessary decorative elements
- content competing with the primary task
- duplicate information across header/body/footer

For each clutter issue, evaluate whether to:
- remove it;
- merge it;
- group it;
- move it into an overflow/menu;
- progressively disclose it;
- reduce visual weight;
- simplify the copy;
- change the information hierarchy.

Do not hide important functionality merely to make a screen look cleaner. Preserve discoverability and accessibility while reducing unnecessary cognitive load.

## 4. Accessibility compliance audit

Accessibility must be checked against the applicable platform and project requirements. For web projects, use the current applicable WCAG baseline; for mobile, use platform accessibility APIs and assistive-technology behavior.

Audit at minimum where applicable:
- semantic structure and accessible names
- headings and landmarks
- labels and form instructions
- keyboard navigation
- focus order and visible focus
- screen-reader behavior
- touch target sizing and spacing
- text scaling/dynamic type
- zoom and responsive reflow
- contrast
- non-text contrast
- error identification and recovery
- validation messaging
- status/live-region announcements
- dialogs and sheets
- menus and popovers
- reduced motion
- orientation changes
- captions/transcripts for relevant media
- accessible authentication flows
- accessible loading, empty, success, and error states

Never declare accessibility complete from an automated scanner alone. Combine automated checks with keyboard, screen-reader, text-scaling, touch, and manual interaction testing appropriate to the platform.

## 5. Responsive and adaptive accessibility

Verify accessibility at the same time as responsive behavior.

Test:
- compact phone
- standard/large phone
- foldable cover and inner displays
- folded/unfolded/half-open states where relevant
- tablet
- portrait/landscape
- split-screen/multi-window
- desktop/resizable browser
- large text/dynamic type
- keyboard visible
- safe-area/inset changes

Ensure controls remain reachable, readable, and understandable after layout changes. Do not let adaptive navigation hide critical functionality from keyboard or assistive-technology users.

## 6. UI state completeness

Every significant component/flow should be checked for:
- initial/loading
- skeleton/loading progress where appropriate
- success
- empty
- partial data
- validation error
- server error
- offline
- retry
- disabled
- permission denied
- expired session
- destructive-action confirmation
- accessibility announcement/state

## 7. Verification gate

Before locking a UI phase, record:
- skeleton/loading states verified
- semantic color tokens verified
- contrast checks completed
- clutter audit completed
- responsive/adaptive layouts verified
- keyboard/touch interaction verified where applicable
- screen-reader/accessibility checks completed where applicable
- reduced-motion/text-scaling checks completed where applicable
- loading/empty/error/success states verified
- visual regression evidence captured where available

A UI phase must not be locked if a material accessibility violation, severe layout clutter, unusable loading state, or semantic-color failure remains unresolved.
