# Styling

Read this file when the task involves styling Mantine components, importing Mantine CSS, overriding styles, choosing between style props and CSS modules, or dealing with stylesheet order issues.

This guidance is based on Mantine styling docs reviewed on July 14, 2026.

## Preferred Styling Strategy

Mantine exposes several styling paths, but they are not equal.

Preferred order:

1. Component-specific props like `variant`, `color`, `size`, `radius`
2. CSS modules for most real component styling
3. Small numbers of style props for isolated single-property changes
4. `style` prop for one-off inline styles or CSS variable injection

## Component Props First

- Prefer component-specific props when they express the desired visual change.
- Props like `color`, `variant`, `size`, and `radius` usually control multiple CSS properties coherently.
- This is the most maintainable first step for ordinary Mantine customization.

## CSS Modules Are The Default For Real Styling

- Mantine recommends CSS modules as the main styling mechanism for most component customization.
- They are the most flexible and performant general-purpose path.
- Prefer CSS modules when a component needs more than a few visual changes or stateful selectors.

Use CSS modules when:

- multiple CSS properties must change together
- data attributes or responsive selectors are involved
- styling should remain maintainable over time

## Style Props

- Style props can be used on any Mantine component.
- Each style prop maps to one CSS property.
- They are applied inline and cannot be overridden with normal CSS without `!important`.

Use style props for:

- small spacing adjustments
- simple typography tweaks
- isolated layout adjustments

Do not use style props as the primary styling system for large components.

Rule of thumb:

- if you are adding more than about 3-4 style props to one component, move to CSS modules

## `style` Prop

- `style` works like React’s inline style prop
- it can also set CSS variables
- it is useful for one-off layout or variable injection cases

Use it for:

- a single inline layout property
- dynamic CSS variable values
- tightly scoped exceptions

Do not treat it as the main styling system for reusable component work.

## Theme Tokens In Styles

Mantine theme values are exposed as CSS variables.

Use theme tokens in:

- CSS modules via `var(--mantine-...)`
- style props via shorthand values like `bg="red.5"` or `mt="xl"`
- `style` props via either CSS variables or theme callbacks

Prefer token-driven styling over hardcoded values when the value should stay aligned with the shared theme.

## Style Imports

- Import `@mantine/core/styles.css` for core components.
- Import additional `@mantine/{package}/styles.css` files only for packages in use.
- `@mantine/core` styles must be imported before styles from other Mantine packages.
- Your application styles should be imported after Mantine styles so your rules win.

Correct order:

1. `@mantine/core/styles.css`
2. other `@mantine/*/styles.css`
3. app styles

## Per-Component Style Imports

- `@mantine/core` supports importing styles for individual components.
- This can reduce CSS bundle size.
- Some components depend on other internal components, so verify style dependencies before using per-component imports.
- This per-component import pattern is only available for `@mantine/core`, not for other Mantine packages.

## CSS Layers

Use `.layer.css` imports when the framework or bundler does not guarantee stylesheet order.

Examples:

- Next.js style order issues
- combining Mantine with other styled component libraries

Rules:

- use either `styles.css` or `styles.layer.css`, not both
- your non-layered app styles will override Mantine layer styles
- CSS layers are useful when you need deterministic ordering without relying on import order

## Practical Rules

- Start with component props.
- Use CSS modules for most component styling.
- Keep style props and inline styles small and intentional.
- Respect Mantine style import order.
- Reach for CSS layers when the framework makes import order unreliable.
