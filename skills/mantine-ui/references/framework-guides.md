# Mantine Framework Guides

Use this reference when adding Mantine to an application with a supported framework. In every framework, install `@mantine/core` and `@mantine/hooks`, import `@mantine/core/styles.css` plus the stylesheets of any extension packages used, and mount one application-level `MantineProvider`.

For CSS Modules using Mantine mixins or breakpoint variables, install `postcss`, `postcss-preset-mantine`, and `postcss-simple-vars`. Configure the preset and define the Mantine breakpoint variables in the framework's PostCSS configuration.

## Next.js

Source: [official Next.js guide](https://mantine.dev/guides/next/).

- Prefer a Mantine Next.js template when bootstrapping; templates include PostCSS and color-scheme setup. Both App Router and Pages Router are supported.
- Pages Router: import styles and mount `MantineProvider` in `pages/_app.tsx`. Add `ColorSchemeScript` in `pages/_document.tsx`, and spread `mantineHtmlProps` onto `<Html>`. This is required even if the application only exposes one color scheme.
- App Router: import styles, render `ColorSchemeScript` in `<head>`, spread `mantineHtmlProps` onto `<html>`, and mount `MantineProvider` in `app/layout.tsx`. Configure both entry points when an application uses both routers.
- Mantine package entry points already declare `'use client'`, so standard Mantine component imports need no extra directive. However, compound syntax such as `Popover.Target` cannot run in a Server Component. Either mark the component with `'use client'` or use the standalone `PopoverTarget` / `PopoverDropdown` exports.
- Use polymorphic components with `next/link`, for example `<Button component={Link} href="/path" />`. For App Router bundle optimization, consider Next's `experimental.optimizePackageImports` for `@mantine/core` and `@mantine/hooks`.

## Vite

Source: [official Vite guide](https://mantine.dev/guides/vite/).

- Mantine recommends its full or minimal Vite template for new projects; otherwise create a standard Vite React application.
- Add the Mantine PostCSS preset and breakpoint variables in a root `postcss.config.cjs` when using Mantine PostCSS features.
- Import package CSS and mount `MantineProvider` in the root component, usually `src/App.tsx`. Vite's standard client-rendered setup does not require `ColorSchemeScript`.

## React Router

Source: [official React Router guide](https://mantine.dev/guides/react-router/).

- For a framework-mode React Router application, configure Mantine in `app/root.tsx`.
- Import the installed Mantine package styles there. In `Layout`, spread `mantineHtmlProps` onto `<html>`, render `ColorSchemeScript` in `<head>`, and wrap route children with `MantineProvider` in `<body>`.
- Retain React Router's document components (`Meta`, `Links`, `ScrollRestoration`, and `Scripts`) alongside Mantine's setup.
- Configure the same root-level PostCSS plugins and breakpoint variables when using Mantine CSS Modules or mixins.

## Gatsby

Source: [official Gatsby guide](https://mantine.dev/guides/gatsby/).

- Select PostCSS when creating a new Gatsby project. Put Mantine PostCSS configuration at the project root.
- Define a shared theme, commonly in `src/theme.ts`, and use the same theme in both Gatsby rendering entry points.
- In `gatsby-ssr.tsx`, add `ColorSchemeScript` through `onPreRenderHTML` and wrap pages with `MantineProvider` through `wrapPageElement`.
- In `gatsby-browser.tsx`, import Mantine and extension CSS, then wrap pages with the same themed `MantineProvider`. This parity prevents server/client visual mismatches.
- Gatsby CSS Modules use namespace imports: `import * as classes from './Component.module.css'`, not a default import.

## RedwoodJS

Source: [official RedwoodJS guide](https://mantine.dev/guides/redwood/).

- Install Mantine dependencies from the Redwood `web` directory; the guide recommends Yarn over npm. Place `postcss.config.js` in `web` as well.
- In `web/src/App.tsx`, import package CSS, render `ColorSchemeScript`, and wrap `RedwoodApolloProvider` / `Routes` with `MantineProvider` while preserving Redwood's `FatalErrorBoundary` and `RedwoodProvider`.
- Keep `ColorSchemeScript` before the provider and routing tree so color-scheme initialization occurs before the application renders.

## Framework Checklist

1. Import core CSS before extension CSS, and import each extension's stylesheet only when that extension is installed.
2. Mount `MantineProvider` once at the framework's true application root.
3. In SSR-capable frameworks, render `ColorSchemeScript` in the HTML head and apply `mantineHtmlProps` to the root HTML element where the framework permits it.
4. Test a light/dark first paint and hydration after setup, then verify PostCSS processing if CSS Modules use Mantine mixins or breakpoint variables.
