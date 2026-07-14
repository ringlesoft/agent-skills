# Composition And Styling

Read this file when the task requires custom rendered elements, integration with a design system, custom animation, overlay styling, or non-default DOM structure.

## Composition With `render`

The `render` prop is Ariakit’s main composition mechanism.

Use it to:

- change the underlying HTML element
- render a custom component
- inject motion or router primitives
- keep Ariakit behavior while matching an existing design system

Examples of appropriate use:

- render `Combobox` as a `textarea`
- render `Tab` as a router link
- render `Menu` as a motion-enabled element
- render a trigger with an alternate semantic element when the interaction still fits

## Element Replacement Rules

- Pass the replacement element through `render`, not by rebuilding the component manually.
- Keep Ariakit-specific props on the Ariakit component itself.
- Put element-specific props on the rendered element.
- Only replace the element when the interaction model still makes semantic sense.

## Prop Merging Rules

When `render` receives an element:

- Ariakit merges `style`, `className`, `ref`, and event props automatically.
- In most other prop collisions, the rendered element’s prop overrides the original prop.

Implication:

- avoid setting conflicting attributes in both places unless you intentionally want the rendered element to win
- keep important Ariakit behavior on the Ariakit component, not buried in the rendered element

## Render Functions

When `render` receives a function:

- Ariakit does not merge props automatically into the returned element
- you must merge props yourself

Preferred pattern:

- use a transitional `Role.*` element when possible
- let `Role` handle the prop merge in a type-safe way

Avoid ad hoc manual merging unless there is a concrete reason. It is easy to drop refs, class names, or event chaining.

## Open For Extension

Custom components used in `render` must be open for extension.

That means they must:

- spread incoming props to the underlying element
- forward the ref
- merge `className` and `style`
- chain event handlers instead of replacing them

If a custom component does not do this, Ariakit behavior may silently break.

## Child Structure

- Do not over-nest content inside the `render` prop when the main component can remain the outer shell.
- Prefer rendering the Ariakit component as another component rather than returning a deeply nested subtree from `render`.
- Keep the Ariakit component visually and structurally close to the element that owns keyboard and ARIA behavior.

## Styling Model

Ariakit is unstyled by default. Style it with your project’s normal system:

- plain CSS
- CSS modules
- Tailwind
- styled-components
- design system wrappers

The key rule is to style around Ariakit behavior, not against it.

## Styling Guidance

- Use classes and data attributes rather than fragile DOM traversal selectors.
- Preserve visible focus states.
- Style open, leave, and mounted states with Ariakit’s data attributes instead of manually duplicating state in React when CSS can handle it.
- Keep overlays resilient to portal rendering and viewport changes.

## Important Data Attributes

- `data-focus-visible`: mirrors focus-visible behavior and also works for composite items with virtual focus
- `data-enter`: useful for enter transitions
- `data-leave`: useful for exit transitions

Use these for focus and animation states instead of inventing parallel class toggles when Ariakit already exposes the state.

## Important CSS Variables

Use Ariakit’s exposed CSS variables when styling overlays:

- `--dialog-viewport-height`: accounts for the visual viewport, including virtual keyboards on mobile
- `--popover-transform-origin`: anchors transform origin to the popover’s placement relative to its anchor

Guidance:

- use `--dialog-viewport-height` for dialogs containing inputs or mobile-sensitive layouts
- combine it with `calc()` when the dialog uses inset or margins
- use `--popover-transform-origin` for scale or transform-based popover animations

## Overlay Styling Rules

- Assume dialogs, popovers, menus, and hovercards may render in portals.
- Do not rely on ancestor overflow, stacking, or transform contexts unless the portal behavior has been explicitly configured.
- If a custom backdrop or wrapper is needed, compose it through `render` without breaking the portal and accessibility structure.

## Practical Rules

- Prefer `render` over reimplementation.
- Prefer elements or custom components that preserve Ariakit props cleanly.
- Prefer official data attributes and CSS variables over shadow state.
- Treat focus styling, animation, and portal behavior as first-class constraints.
