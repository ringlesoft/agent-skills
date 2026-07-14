# Popover Examples

Read this file when implementing Ariakit popovers with lazy loading, responsive positioning, text-selection anchoring, or standalone custom anchoring.

Use these examples as pattern references, not as copy-paste targets.

## Popover Loading And Performance

### Lazy Popover

Source:

- https://ariakit.com/examples/popover-lazy

Use this when:

- the popover content is expensive or code-split
- the bundle should avoid loading popover content until the user opens it

Key takeaways:

- lazy load the popover body with `React.lazy`
- control popover open state explicitly through `PopoverProvider`
- use transitions to defer loading without blocking the trigger interaction
- if a loading indicator is shown, make it perceptible enough to avoid flicker

## Responsive And Adaptive Layout

### Responsive Popover

Source:

- https://ariakit.com/examples/popover-responsive

Use this when:

- default anchored positioning works on large screens but needs overriding on smaller screens

Key takeaways:

- use `updatePosition` when responsive behavior must override Ariakit’s default positioning styles
- read store state when applying custom responsive positioning logic
- use this pattern when the popover must switch from anchored placement to a more screen-filling mobile layout

## Dynamic Anchoring

### Selection Popover

Source:

- https://ariakit.com/examples/popover-selection

Use this when:

- the popover should appear relative to selected text
- the trigger is a text selection rather than a button or anchor element

Key takeaways:

- use `getAnchorRect` to anchor the popover to the current selection
- disable autofocus when showing the popover if focus should remain with the text interaction
- customize outside-interaction behavior so the popover only closes when selection context is truly lost

### Standalone Popover

Source:

- https://ariakit.com/examples/popover-standalone

Use this when:

- you need popover behavior without `PopoverDisclosure` or `PopoverAnchor`
- the trigger and positioning logic are fully custom

Key takeaways:

- abstract popover usage around `getAnchorRect`
- use this pattern for custom trigger systems that do not map cleanly to Ariakit’s standard disclosure and anchor components
- preserve Ariakit focus and popup behavior even when the outer API is custom

## Selection Rules

- Use lazy loading when payload size or content cost is the main issue.
- Use responsive positioning when mobile layout constraints are the main issue.
- Use selection anchoring when the target is a text range.
- Use standalone popovers only when the standard disclosure and anchor model is not a fit.
