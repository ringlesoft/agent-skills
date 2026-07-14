# Setup

Read this file when adding Mantine to a project for the first time, verifying Mantine root configuration, choosing packages, or handling SSR and PostCSS setup.

This guidance is based on Mantine getting-started and `@mantine/core` package documentation reviewed on July 14, 2026.

## Foundation Packages

Standard Mantine foundation setup:

- `@mantine/core`
- `@mantine/hooks`

Install additional packages only if the feature needs them, for example:

- `@mantine/form`
- `@mantine/dates`
- `@mantine/notifications`
- `@mantine/code-highlight`
- `@mantine/tiptap`
- `@mantine/dropzone`
- `@mantine/carousel`
- `@mantine/spotlight`
- `@mantine/modals`
- `@mantine/nprogress`
- `@mantine/charts`

For official Mantine extensions beyond the basic setup, also see [extensions.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/mantine-ui/references/extensions.md).

## Root Setup

Mantine should be configured once near the application root.

Typical root pattern:

1. Import core styles.
2. Import additional package styles only for packages in use.
3. Create a theme with `createTheme` if theme overrides are needed.
4. Wrap the app with `MantineProvider`.

For provider-specific behavior beyond basic setup, see [provider-and-theme.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/mantine-ui/references/provider-and-theme.md).

Core docs pattern:

```tsx
import { createTheme, MantineProvider } from '@mantine/core';
import '@mantine/core/styles.css';

const theme = createTheme({
  // theme overrides
});

export function AppRoot() {
  return <MantineProvider theme={theme}>{/* app */}</MantineProvider>;
}
```

## CSS Imports

- `@mantine/core/styles.css` is required for Mantine core components.
- Additional package CSS is required only when using those package components.
- Import these styles once at the root, not repeatedly inside leaf components.

Examples of optional package styles:

- `@mantine/dates/styles.css`
- `@mantine/dropzone/styles.css`
- `@mantine/code-highlight/styles.css`

## SSR Setup

If the application uses SSR:

- add `ColorSchemeScript` in the document head
- spread `mantineHtmlProps` on the `<html>` element

This avoids hydration warnings and color-scheme mismatch issues.

## PostCSS And Non-Template Setup

If the project is not using an official Mantine template and relies on Mantine PostCSS features:

- configure `postcss-preset-mantine`
- configure `postcss-simple-vars`
- ensure the framework or bundler supports PostCSS correctly

Mantine docs show breakpoint variables such as:

- `mantine-breakpoint-xs`
- `mantine-breakpoint-sm`
- `mantine-breakpoint-md`
- `mantine-breakpoint-lg`
- `mantine-breakpoint-xl`

Use this setup only when the project’s styling flow actually depends on Mantine’s PostCSS tooling.

## Framework Guidance

Mantine docs recommend:

- Vite for SPA-style applications
- Next.js for SSR applications

Mantine also provides templates and guides for:

- Next.js app router
- Next.js pages router
- Vite
- React Router
- Gatsby
- Redwood

For new projects, prefer official templates when possible because they include the required baseline setup.

## Create React App

- Mantine docs do not recommend Create React App for new projects.
- Starting with Mantine v7, some styling features are no longer officially supported in CRA.
- If maintaining an existing CRA codebase, treat Mantine integration as compatibility work, not the default happy path.

## `@mantine/core` Scope

`@mantine/core` covers a broad component surface, including:

- layout primitives
- form inputs
- combobox-based inputs
- buttons
- navigation components
- feedback components
- overlays
- typography and data display components

It is also required by many other `@mantine/*` packages.

For forms and hooks beyond the root setup phase, see [form-and-hooks.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/mantine-ui/references/form-and-hooks.md).

## Practical Rules

- Install only the packages the feature needs.
- Verify root provider and CSS setup before debugging component issues.
- Prefer template-backed setups for new projects.
- Use theme overrides for shared visual changes instead of one-off overrides everywhere.
