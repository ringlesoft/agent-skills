---
name: ariakit
description: Use this skill when building or refactoring React interfaces with Ariakit, especially dialogs, menus, popovers, comboboxes, tabs, select controls, toolbars, and other accessible headless components that require explicit store wiring, provider setup, and keyboard-safe composition.
---

# Ariakit

Use this skill when the project already uses Ariakit or when the requested UI clearly benefits from Ariakit's accessible headless primitives.

Do not use this skill for generic React UI work unless Ariakit is already part of the stack or the user explicitly wants it.

## Workflow

1. Inspect the existing codebase first.
2. Confirm which Ariakit primitive matches the requested behavior.
3. Create the correct store hook for that primitive.
4. Share store state through the matching provider when multiple related subcomponents are involved.
5. Compose the UI from Ariakit primitives instead of rebuilding ARIA behavior manually.
6. Add styling separately; Ariakit does not provide presentation.
7. Verify focus handling, keyboard behavior, and open/close state after the change.

## Core Rules

### State

- Ariakit components are headless and state-driven.
- Prefer the primitive-specific store hook such as `useDialogStore`, `useMenuStore`, `useSelectStore`, or `useComboboxStore`.
- Update component state through the store API instead of ad hoc DOM manipulation.

### Composition

- Use the related subcomponents from the same Ariakit family.
- Prefer composition over custom event choreography.
- When a component family expects a provider, keep all related children inside it.

### Accessibility

- Preserve Ariakit's keyboard and focus behavior.
- Do not replace built-in semantics with custom ARIA unless there is a concrete gap to solve.
- Supply missing labels such as `aria-label` or `aria-labelledby` when the UI would otherwise be ambiguous.

### Styling

- Ariakit ships unstyled primitives.
- Add classes, CSS modules, Tailwind utilities, or styled wrappers explicitly.
- Avoid coupling behavior to visual selectors when the store state already expresses intent.

## Primitive Selection

- `Dialog`: modal or non-modal overlays, confirmation flows, side panels.
- `Menu` or `Menubar`: action menus, context menus, app-style menus.
- `Popover` or `Hovercard`: anchored floating content that is not a modal dialog.
- `Combobox`: searchable option pickers and autocomplete inputs.
- `Select`: accessible custom selects with controlled open state.
- `Tab`: tabbed panels with keyboard navigation.
- `Disclosure`: show/hide sections and accordion-like interactions.
- `Toolbar`: grouped controls with directional keyboard support.
- `Tooltip`: short non-interactive help text.

If the requested behavior mixes patterns, choose the primitive based on interaction model first, not on appearance.

## Implementation Guidance

- Keep open state controlled when the surrounding feature already owns it.
- Use the `render` prop or supported element overrides when integration with an existing design system requires different DOM elements.
- Expect overlays such as dialogs, popovers, and hovercards to use portals unless configured otherwise.
- When integrating with forms or routing, let Ariakit manage interaction behavior and keep business logic in surrounding React code.

## Failure Modes To Check

- Store created but not passed to the rendered components.
- Related subcomponents rendered outside the matching provider.
- Custom styling breaking focus visibility.
- Custom click handlers fighting store state.
- Popover or dialog layout issues caused by portal assumptions.

## Output Expectations

When using this skill, produce code that:

- uses the correct Ariakit primitive family
- wires store state explicitly
- preserves accessible keyboard behavior
- keeps styling separate from behavior
- fits the surrounding project patterns instead of forcing a standalone demo
