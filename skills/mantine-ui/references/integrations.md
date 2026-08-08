# Mantine Integrations

This reference summarizes official guidance for integrating Mantine with component tooling, language tooling, tests, AI agents, and icon libraries.

## Storybook

Source: [official Storybook guide](https://mantine.dev/guides/storybook/).

- The guide supports Storybook 10 and later. Add Storybook through its normal framework-specific setup, then install and enable `@storybook/addon-themes`.
- Export the Mantine theme from a shared module and use it in both the app and Storybook; do not duplicate its definition.
- In `.storybook/preview.tsx`, import `@mantine/core/styles.css` and all used extension styles. Decorate every story with `MantineProvider theme={theme}` and `ColorSchemeScript`.
- Expose a Storybook toolbar global for light/dark mode and pass it to `MantineProvider` as `forceColorScheme`. Disable Storybook backgrounds when Mantine controls the color scheme.

## TypeScript and JavaScript

Sources: [TypeScript](https://mantine.dev/guides/typescript/) and [JavaScript](https://mantine.dev/guides/javascript/).

- Mantine is fully typed and is best used with TypeScript. Type checking catches invalid props and breaking API changes during upgrades.
- Component packages export `{Component}Props` types; components also expose associated namespace types such as `Button.Props`.
- When extending a regular component, extend its props type. For polymorphic components, combine its props type with `ElementProps<Element, keyof ComponentProps>` to include native element props without collisions.
- Use `MantineTheme` for functions that receive a complete theme and `MantineThemeOverride` for theme-override inputs. Add a project `.d.ts` module augmentation only when stricter custom theme tokens, colors, sizes, or variants are needed.
- JavaScript is supported and benefits from shipped editor type definitions. Convert TypeScript documentation examples by removing type annotations and type-only imports, but prefer TypeScript for maintainability and safer migrations.

## Jest and Vitest

Sources: [Jest](https://mantine.dev/guides/jest/) and [Vitest](https://mantine.dev/guides/vitest/).

- Build a shared React Testing Library `render` helper that wraps tested UI in `MantineProvider theme={theme} env="test"`; re-export the helper and standard testing utilities from one test-utils module.
- Mock browser APIs missing from jsdom: `matchMedia`, `ResizeObserver`, `document.fonts`, `scrollIntoView`, and the delegated `getComputedStyle`. Register these mocks in the test runner setup file.
- Jest setup is framework-dependent. Add the test setup file through `setupFilesAfterEnv` and use the framework's recommended Jest integration.
- Vitest guidance targets Vite projects. Install Vitest, jsdom, and React Testing Library packages; configure `globals: true`, `environment: 'jsdom'`, and a setup file in Vite's `test` configuration. Import `@testing-library/jest-dom/vitest` and use `vi.fn()` in the mocks.

## oxc-config-mantine

Source: [official oxc-config-mantine guide](https://mantine.dev/oxc-config-mantine/).

- `oxc-config-mantine` provides Mantine's shared Oxlint and Oxfmt conventions. Install it with `oxlint` and `oxfmt` as development dependencies.
- Extend its `oxlint` export in `oxlint.config.ts`; extend or spread its `oxfmt` export in `oxfmt.config.ts` to add project-specific ignore patterns.
- Add scripts for `oxlint` and `oxfmt --write` over the relevant source and CSS files. The lint configuration extends recommended rules and adds React, TypeScript, JSX accessibility, and Jest rules.

## LLMs and MCP

Source: [official LLM guide](https://mantine.dev/guides/llms/).

- Use `https://mantine.dev/llms.txt` for a compact, release-updated index of Mantine's LLM-friendly documentation. Use `llms-full.txt` only when a client benefits from the complete single-file reference.
- The documentation covers setup, components, hooks, theming, styles, and FAQs. State the application's actual Mantine version in prompts so generated code targets the installed API.
- Mantine publishes agent skills for comboboxes, forms, and custom components in the `mantinedev/skills` repository. Explicitly name an installed skill in the agent prompt.
- The experimental `@mantine/mcp-server` exposes static documentation through item-listing, documentation, prop, and search tools. Configure it with `npx -y @mantine/mcp-server` in an MCP-compatible client; use its optional data URL environment variable only when an alternate source is required.

## Icon Libraries

Source: [official icon libraries guide](https://mantine.dev/guides/icons/).

- Mantine accepts React components from any icon library. Phosphor is the documented default; Tabler, Feather, Radix, React Icons, and Font Awesome also work.
- Size icons explicitly in pixels using the library's `size`, `width`, or `height` prop. Avoid `rem` values in SVG dimensions because they are invalid SVG attributes and can trigger browser warnings.
- Prefer icon React components over static assets. Set `stroke` and/or `fill` to `currentColor` in custom SVGs so they inherit Mantine component colors, including disabled and variant states.

## Integration Checklist

1. Share the same theme object between the app, Storybook, and test render helpers.
2. Import Mantine CSS in every independent rendering environment, including Storybook and Gatsby/browser entry points.
3. Use `env="test"` and browser API mocks for unit tests that render Mantine components.
4. Keep AI-provided documentation and prompts aligned to the installed Mantine version.
