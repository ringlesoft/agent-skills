# Provider And Theme

Read this file when the task involves `MantineProvider`, color scheme behavior, CSS variable configuration, or provider-level theme control.

This guidance is based on MantineProvider docs reviewed on July 14, 2026.

## MantineProvider Role

- `MantineProvider` provides the theme context.
- It manages color scheme changes.
- It injects CSS variables.
- It should be rendered once at the application root.

## Core Provider Pattern

Typical root usage:

```tsx
import { createTheme, MantineProvider } from '@mantine/core';

const theme = createTheme({
  // theme overrides
});

export function AppRoot() {
  return <MantineProvider theme={theme}>{/* app */}</MantineProvider>;
}
```

## Important Props

### `theme`

- Use `theme` for provider-level theme overrides.
- Prefer central theme customization for repeated visual changes.

### `colorSchemeManager`

- Controls how color scheme is read from and written to external storage.
- By default, Mantine uses `window.localStorage`.
- Use this only when the application has a real need for custom persistence behavior.

### `defaultColorScheme`

- Used when stored color scheme cannot be read, such as SSR or first load.
- Supported values include `light`, `dark`, and `auto`.
- Use this intentionally instead of relying on implicit defaults when color scheme behavior matters.

### `forceColorScheme`

- Forces light or dark mode and bypasses normal manager/default behavior.
- Use sparingly and only when the application truly needs a fixed scheme.

### `cssVariablesSelector`

- Controls where Mantine CSS variables are injected.
- Defaults apply to `:root` and `:host`.
- Change this only when the application has a strong reason to scope variables differently.

### `withCssVariables`

- Controls whether Mantine injects theme CSS variables at runtime.
- Leave this enabled unless the project deliberately manages all theme variables manually.

### `deduplicateCssVariables`

- Controls whether default-theme-equivalent CSS variables are omitted from runtime output.
- Default behavior is usually correct.
- Only disable this when there is a concrete reason to emit the full variable set.

## Practical Rules

- Mount `MantineProvider` once, at the root.
- Put global theming decisions here, not in many component-level patches.
- Change provider props only when there is a clear application-level need.
- Be conservative with advanced provider configuration unless the project architecture requires it.
