# Dialog Examples

Read this file when implementing Ariakit dialogs with animation, nested overlays, router-controlled state, command-palette behavior, interoperability layers, or custom portal/backdrop behavior.

Use these examples as pattern references, not as copy-paste targets.

## Animation And Presentation

### Animated Dialog

Source:

- https://ariakit.com/examples/dialog-animated

Use this when:

- a modal dialog needs CSS enter and exit transitions
- the backdrop should animate with the surface

Key takeaways:

- animate both the dialog and the backdrop with Ariakit `data-enter` and `data-leave` state
- let Ariakit keep the dialog mounted until the transition completes
- use `DialogDismiss` for the close action inside the surface

### Dialog With Motion

Source:

- https://ariakit.com/examples/dialog-framer-motion

Use this when:

- the project already uses Motion or Framer Motion style animation primitives
- you need declarative initial and exit animation control

Key takeaways:

- compose Ariakit dialog behavior with motion-based rendering rather than replacing Ariakit state and focus logic
- animate the backdrop and surface together

### Dialog With Scrollable Backdrop

Source:

- https://ariakit.com/examples/dialog-backdrop-scrollable

Use this when:

- the dialog can exceed viewport height
- the backdrop container must scroll while the dialog remains semantically modal

Key takeaways:

- disable the default backdrop and render a custom scrollable wrapper through `render`
- keep the dialog itself inside that wrapper
- use this pattern for tall content rather than forcing the surface into an unusable fixed viewport

## Command Palette Patterns

### Command Menu

Source:

- https://ariakit.com/examples/dialog-combobox-command-menu

Use this when:

- building a Raycast-style or command-palette modal
- users need to search grouped commands inside a dialog

Key takeaways:

- combine `Dialog` and `Combobox` rather than treating the command palette as a plain menu
- abstract the implementation into higher-level components when the feature becomes a reusable command surface
- render explicit empty states when no command matches

### Command Menu With Tabs

Requested source:

- https://ariakit.com/examples/dialog-combobox-tab-command-menu

Status:

- the page could not be retrieved reliably during authoring

Use this expected pattern when:

- the command palette also needs category switching
- tab state and search state must coordinate inside one dialog surface

Implementation hint:

- combine the command-menu approach with the combobox-and-tabs pattern documented in [examples-combobox.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/examples-combobox.md)

## Structure And Nesting

### Dialog With Details And Summary

Source:

- https://ariakit.com/examples/dialog-details

Use this when:

- progressive enhancement before JavaScript hydration is a hard requirement

Key takeaways:

- combine Ariakit with native `details` and `summary` only for constrained enhancement cases
- Ariakit’s own guidance warns that router-based dialogs are usually a better accessibility strategy for no-JS-first flows

### Nested Dialog

Source:

- https://ariakit.com/examples/dialog-nested

Use this when:

- a dialog must open a confirmation dialog inside itself
- destructive or disruptive actions need an explicit second step

Key takeaways:

- nested dialogs are appropriate for confirmation flows
- preserve explicit headings, descriptions, and dismiss actions for both layers
- use nesting carefully and only when a second modal decision is justified

### Warning On Dialog Hide

Source:

- https://ariakit.com/examples/dialog-hide-warning

Use this when:

- a dialog contains unsaved changes
- closing the dialog should require confirmation

Key takeaways:

- intercept close intent and route it through a nested confirmation dialog
- this is the right pattern for accidental-dismiss prevention

### Dialog With Menu

Source:

- https://ariakit.com/examples/dialog-menu

Use this when:

- a modal dialog contains an embedded dropdown menu

Key takeaways:

- compose `Menu` inside `Dialog` rather than flattening the interaction into one primitive
- this pattern is useful when a modal contains secondary action menus or option pickers

## Integration Patterns

### Radix Dialog

Source:

- https://ariakit.com/examples/dialog-radix

Use this when:

- the team wants Radix-like dialog APIs on top of Ariakit internals
- you need features like `asChild`, `forceMount`, `onOpenChange`, or outside-interaction hooks

Key takeaways:

- Ariakit is extensible enough to support a Radix-style wrapper API
- this is a wrapper-building reference, not the default way to use dialogs in an Ariakit-first codebase

### Dialog With React-Toastify

Source:

- https://ariakit.com/examples/dialog-react-toastify

Use this when:

- toasts or notification portals must remain usable while a modal is open

Key takeaways:

- use `getPersistentElements` to keep external notification elements interactive or visible
- this applies broadly to toast libraries, not just React-Toastify

## Router-Controlled Dialogs

### Dialog With React Router

Source:

- https://ariakit.com/examples/dialog-react-router

Use this when:

- dialog visibility should be controlled by browser history
- back and forward navigation should open or close the modal predictably

Key takeaways:

- use routing as the dialog state owner
- prefer this over ad hoc no-JavaScript dialog hacks when the modal is part of navigation

### Dialog With Next.js App Router

Source:

- https://ariakit.com/examples/dialog-next-router

Use this when:

- the app uses Next.js App Router
- the dialog should be URL-driven and server-renderable

Key takeaways:

- use parallel routes for modal state
- this is the preferred Next.js pattern when modal navigation should participate in history and server rendering

## Selection Rules

- Use animated or motion patterns when transitions are the main requirement.
- Use scrollable-backdrop patterns when content height is the main constraint.
- Use nested or hide-warning patterns when the problem is interruption safety.
- Use router-controlled dialogs when the modal represents navigable application state.
- Use Radix-style wrappers only when compatibility or wrapper extensibility is the actual goal.
