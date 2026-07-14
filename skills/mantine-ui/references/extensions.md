# Extensions

Read this file when the requested feature goes beyond `@mantine/core` and may require an official Mantine extension or a vetted community extension.

This guidance is based on Mantine extensions documentation reviewed on July 14, 2026.

## Extension Model

- Mantine extensions are additional packages built on top of `@mantine/core` and `@mantine/hooks`.
- Official extensions use the `@mantine/` scope.
- Community extensions are maintained independently and do not follow the same release cadence guarantees as official Mantine packages.

## Official Extensions

Reach for official Mantine extensions first when the requested feature matches one of these domains:

- `@mantine/dates`
  - date and time pickers
  - calendars
  - date-related inputs
- `@mantine/charts`
  - charts and data visualization
  - built on Recharts
- `@mantine/notifications`
  - app-wide notification system
- `@mantine/code-highlight`
  - themed code highlighting
- `@mantine/spotlight`
  - command center or `Ctrl + K` style search
- `@mantine/carousel`
  - carousel UIs
  - built on Embla
- `@mantine/dropzone`
  - drag-and-drop file capture
  - built on react-dropzone
- `@mantine/modals`
  - centralized modal management
- `@mantine/tiptap`
  - rich text editor
  - built on Tiptap
- `@mantine/nprogress`
  - navigation progress indicators

## Extension Selection Rules

- Prefer official extensions over custom implementations when the feature is already covered cleanly.
- Do not install an extension just because it exists if the requested UI only needs basic `@mantine/core` behavior.
- When introducing an extension, also verify whether its package-specific styles or setup are required at the application root.

## Community Extensions

Community extensions can be useful when the requested feature is specialized and not covered by official Mantine packages.

Examples listed in Mantine docs include:

- data tables
- context menus
- onboarding flows
- QR codes
- lightboxes
- advanced media players
- specialized animated or visual effect components

Use community extensions carefully:

- prefer them only when they materially reduce implementation risk or time
- verify maintenance quality and compatibility with the installed Mantine version
- avoid assuming they are interchangeable with official Mantine packages

## Practical Rules

- Start with `@mantine/core`.
- Add official extensions only for real feature needs.
- Treat community extensions as optional integrations, not as default building blocks.
- If a feature needs a command palette, notifications manager, date picker, carousel, rich text editor, or drag-and-drop input, check official extensions before inventing custom infrastructure.
