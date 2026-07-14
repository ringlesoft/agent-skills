# Theme System

Read this file when the task involves global theming, theme object overrides, custom colors, color tokens, color scheme logic, or app-wide design decisions.

This guidance is based on Mantine theming docs reviewed on July 14, 2026.

## Theme Object

Use `createTheme` for shared visual configuration.

The theme object is the right place for global decisions such as:

- colors
- spacing
- radius
- shadows
- breakpoints
- typography
- heading styles
- default component props
- component-level theme overrides

High-value theme areas to check first:

- `primaryColor`
- `primaryShade`
- `defaultRadius`
- `fontFamily`
- `headings`
- `spacing`
- `radius`
- `shadows`
- `breakpoints`
- `components`

Use theme overrides when the change should apply consistently across many components, not just one local call site.

## Component Theme Overrides

- Use `theme.components` for shared component-level default props and styles.
- Prefer this over repeating the same prop choices across many call sites.
- Use local props only when the customization is truly local.

## Colors

Mantine color scales are built around 10 shades per color.

Important rules:

- custom colors should fit Mantine’s 10-shade model
- use theme colors instead of hardcoded values when the choice should remain globally adjustable
- keep semantic color decisions consistent with the rest of the theme

### `colorsTuple`

Use `colorsTuple` when:

- one flat color must be converted into a Mantine-compatible 10-shade tuple
- a dynamic array needs to be typed and treated as a Mantine color tuple

### `virtualColor`

Use `virtualColor` when:

- a color should resolve differently in light and dark schemes
- the application needs a semantic adaptive color alias

This is useful for theme-level semantic colors that should not hardcode one fixed palette path.

## Color Schemes

Mantine supports `light`, `dark`, and `auto` color schemes.

Practical guidance:

- `useMantineColorScheme` is for reading and changing the current scheme
- `toggleColorScheme` and `setColorScheme` should be used intentionally, not scattered arbitrarily
- `useComputedColorScheme` is useful when `auto` must resolve to the actual active scheme

Important caveat:

- if the current scheme is `auto`, `colorScheme` itself remains `auto`
- do not branch UI styling logic on raw `colorScheme` when you actually need the resolved light/dark result
- use the computed scheme for those cases

## Provider-Level Theme Behavior

Theme behavior lives at the provider boundary.

Important props and concerns:

- `theme`
- `defaultColorScheme`
- `forceColorScheme`
- `colorSchemeManager`
- CSS variable injection

Prefer conservative provider configuration:

- use defaults unless the application really needs different persistence or forced-scheme behavior
- centralize theme behavior rather than re-implementing color mode logic in feature components

## Practical Rules

- Put shared design tokens in `createTheme`.
- Use `theme.components` for repeated component defaults.
- Use Mantine color tokens instead of hardcoded values.
- Use `colorsTuple` and `virtualColor` when building real custom theme colors.
- Use computed scheme logic when `auto` matters.
