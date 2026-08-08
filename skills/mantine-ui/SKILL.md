---
name: mantine-ui
description: Use this skill when building or refactoring React interfaces with Mantine UI, especially when working with @mantine/core components, MantineProvider setup, theme overrides, CSS imports, responsive layout primitives, overlays, form-oriented inputs, navigation components, or Mantine-based application shells.
---

# Mantine UI

Use this skill when the project already uses Mantine or when the user explicitly wants Mantine UI components and patterns.

Do not use this skill for generic React UI work unless Mantine is already in the stack or introducing Mantine is a deliberate requirement.

Validate the installed Mantine version before relying on a specific API shape. The guidance below is aligned with the official Mantine docs reviewed on July 14, 2026.

Baseline assumptions from Mantine's getting-started and `@mantine/core` package docs:

- Mantine is a React UI library with accessible, production-ready components and hooks.
- The main foundation packages are `@mantine/core` and `@mantine/hooks`.
- Mantine requires app-level setup, not just individual component imports.
- Mantine components require CSS imports from the packages you use.

## Read These References When Needed

- Read [references/setup.md](references/setup.md) when the task involves initial installation, provider setup, theme creation, CSS imports, SSR color scheme setup, PostCSS configuration, or deciding which `@mantine/*` packages to add.
- Read [references/extensions.md](references/extensions.md) when the requested feature may require Mantine dates, charts, notifications, spotlight, carousel, dropzone, modals, rich text editor, navigation progress, or a Mantine-compatible community extension.
- Read [references/form-and-hooks.md](references/form-and-hooks.md) when the task involves `@mantine/form`, input binding, validation, `getInputProps`, uncontrolled form mode, or Mantine hooks for custom interactions and state management.
- Read [references/provider-and-theme.md](references/provider-and-theme.md) when the task involves advanced `MantineProvider` behavior, color scheme persistence, forced color schemes, CSS variable injection, or root-level theme configuration.
- Read [references/styling.md](references/styling.md) when the task involves CSS imports, CSS modules, style props, inline styles, stylesheet ordering, CSS layers, or theme-token-based styling.
- Read [references/theme-system.md](references/theme-system.md) when the task involves `createTheme`, theme object overrides, custom colors, semantic colors, color schemes, or app-wide component defaults.
- Read [references/migration-guides.md](references/migration-guides.md) when upgrading between Mantine major versions or Tiptap 2 to 3.
- Read [references/framework-guides.md](references/framework-guides.md) when configuring Mantine with Next.js, Vite, React Router, Gatsby, or RedwoodJS.
- Read [references/integrations.md](references/integrations.md) when the task involves Storybook, TypeScript or JavaScript usage, Jest or Vitest, Oxlint/Oxfmt, LLM documentation or MCP, or icon libraries.

## Workflow

1. Inspect the existing codebase first.
2. Confirm the project already has Mantine installed, or determine whether adding Mantine is actually intended.
3. Confirm which `@mantine/*` packages are needed for the requested feature.
4. Ensure root setup is correct before adding feature components.
5. Prefer Mantine primitives and patterns over rebuilding equivalent UI behavior from scratch.
6. Keep theme, layout, and component composition aligned with existing project conventions.
7. Verify responsive behavior, focus behavior, and provider-level setup after the change.

## Core Rules

### Setup

- `@mantine/core` is required for Mantine component usage.
- `@mantine/hooks` is also part of the standard foundation setup.
- Mantine components should live under a correctly configured `MantineProvider`.
- Load required CSS files at the app root, including additional package styles only for packages actually used.
- Import `@mantine/core` styles before any other Mantine package styles.
- If the app uses SSR, set up `ColorSchemeScript` and `mantineHtmlProps` correctly to avoid hydration warnings.
- `MantineProvider` should be mounted once at the application root.
- Use advanced provider props only when the application actually needs them.

### Package Selection

- Start with `@mantine/core` and `@mantine/hooks`.
- Add additional packages only when the requested feature needs them, for example:
  - `@mantine/form`
  - `@mantine/dates`
  - `@mantine/notifications`
  - `@mantine/modals`
  - `@mantine/spotlight`
  - `@mantine/charts`
- Avoid installing broad package sets by default.
- Prefer official Mantine extensions before custom-building complex feature areas that Mantine already covers.
- Treat community extensions as optional and verify fit before adopting them.
- `@mantine/form` is the default Mantine form-state package when form complexity exceeds trivial local state.

### Component Strategy

- Prefer Mantine components for layout, inputs, overlays, navigation, typography, and feedback when Mantine is the UI system in use.
- Use Mantine layout primitives such as `AppShell`, `Container`, `Grid`, `Flex`, `Group`, and `Stack` before inventing custom layout wrappers.
- Use Mantine overlay primitives such as `Modal`, `Drawer`, `Popover`, `Menu`, `Tooltip`, `Dialog`, and `HoverCard` when they fit the interaction model.
- Use Mantine input and selection components before custom-building routine form controls.
- Use official Mantine extensions when the requested feature is closer to a specialized subsystem than a single component.
- Use Mantine hooks to support custom interaction logic when they clearly reduce glue code and fit the existing stack.

### Styling

- Prefer component-specific props such as `variant`, `color`, `size`, and `radius` first.
- Prefer CSS modules for most substantial component styling work.
- Use style props for small, isolated adjustments, not as a primary styling system.
- Use inline `style` only for narrow exceptions or CSS variable injection.
- Use CSS layers when framework stylesheet ordering is unreliable.

### Theming

- Centralize visual decisions in Mantine theme overrides when the change affects more than one component.
- Prefer `createTheme` and provider-level customization over one-off ad hoc styling when the change is systemic.
- Match the host repository’s styling and theming approach before introducing new conventions.
- Keep provider configuration conservative unless the project explicitly needs custom color scheme persistence or CSS variable scoping.
- Use theme tokens and theme object overrides instead of hardcoded styling values when the decision is global or reusable.

## High-Value Component Families

- Layout: `AppShell`, `Container`, `Grid`, `SimpleGrid`, `Flex`, `Group`, `Stack`
- Inputs: `TextInput`, `Textarea`, `NumberInput`, `Checkbox`, `Radio`, `Switch`, `NativeSelect`, `FileInput`
- Combobox family: `Autocomplete`, `Combobox`, `MultiSelect`, `Select`, `TagsInput`, `TreeSelect`
- Buttons: `Button`, `ActionIcon`, `CloseButton`, `UnstyledButton`
- Navigation: `NavLink`, `Tabs`, `Pagination`, `Stepper`, `Breadcrumbs`
- Feedback: `Alert`, `Notification`, `Loader`, `Progress`, `Skeleton`
- Overlays: `Dialog`, `Drawer`, `HoverCard`, `Menu`, `Menubar`, `Modal`, `Popover`, `Tooltip`
- Data display and typography: `Card`, `Avatar`, `Badge`, `ThemeIcon`, `Text`, `Title`, `List`, `Code`

## High-Value Supporting Packages

- `@mantine/form`: `useForm`, validation, submission, field wiring
- `@mantine/hooks`: DOM, state, utility, and lifecycle hooks for custom behavior

## High-Value Extensions

- `@mantine/dates`: date and time pickers, calendars
- `@mantine/charts`: charts and data visualization
- `@mantine/notifications`: app-wide notifications
- `@mantine/spotlight`: command palette and global search
- `@mantine/carousel`: carousels
- `@mantine/dropzone`: drag-and-drop file capture
- `@mantine/modals`: centralized modal manager
- `@mantine/tiptap`: rich text editing
- `@mantine/nprogress`: navigation progress indicators
- `@mantine/code-highlight`: syntax-highlighted code blocks

## Implementation Guidance

- If the task is bootstrapping a Mantine project, prefer an official Mantine template when that fits the environment.
- For new SPAs, Mantine docs recommend Vite.
- For SSR applications, Mantine docs recommend Next.js.
- Avoid Create React App for new Mantine work unless the repository already depends on it and there is no migration scope.
- If a framework is not officially supported, verify that PostCSS and Mantine CSS setup are explicitly handled.
- If the requested feature maps directly to an official extension, check that package before designing a custom subsystem.
- If the feature is a non-trivial form, check whether `@mantine/form` should own state and validation before building custom form plumbing.
- If the feature needs custom interaction logic, check whether a Mantine hook already solves the problem before adding bespoke utilities.
- If the styling change affects many components, move it into `createTheme` or component defaults instead of repeating local overrides.
- If color scheme logic depends on resolved light or dark mode, use computed scheme logic instead of branching on raw `auto`.

## Failure Modes To Check

- `MantineProvider` missing or mounted too low in the tree.
- Required package CSS files not imported.
- Mantine style imports in the wrong order.
- SSR app missing `ColorSchemeScript` or `mantineHtmlProps`, causing hydration warnings or color-scheme flashes.
- Feature implemented with custom wrappers where Mantine already provides a better primitive.
- Unnecessary `@mantine/*` packages added without an actual feature need.
- Community extension adopted without checking maintenance, compatibility, or necessity.
- Form implemented with fragmented state where `@mantine/form` would be more coherent.
- Provider configured multiple times or with unnecessary advanced options.
- Too many style props or inline styles used where CSS modules or theme overrides would be more maintainable.
- Raw `colorScheme === 'dark'` checks used where `auto` mode makes computed scheme necessary.
- Project styling conflicts caused by bypassing existing Mantine theme structure.

## Output Expectations

When using this skill, produce code that:

- uses Mantine components and packages intentionally
- preserves proper provider and CSS setup
- fits the host framework and rendering model
- uses Mantine layout and overlay primitives where appropriate
- keeps global theming decisions centralized
- avoids unnecessary package sprawl
