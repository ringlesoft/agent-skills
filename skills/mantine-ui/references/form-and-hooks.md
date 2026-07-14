# Form And Hooks

Read this file when the task involves Mantine form state, validation, input wiring, custom interactive behavior, or standalone hook usage.

This guidance is based on Mantine `@mantine/form` and `@mantine/hooks` package docs reviewed on July 14, 2026.

## `@mantine/form`

- `@mantine/form` provides `useForm` for form state, validation, and submission.
- Mantine inputs are compatible with `useForm` out of the box.
- The package is standalone and can be used with native inputs or non-Mantine inputs as well.

### Form Usage Rules

- Use `@mantine/form` when the feature needs structured form state, validation, touched/dirty status, nested fields, or reusable field wiring.
- Prefer `useForm` over many disconnected `useState` calls once the form has more than trivial complexity.
- Use `getInputProps` to bind Mantine inputs consistently.
- In uncontrolled mode, use `form.key(field)` where needed so input identity resets correctly with form state.

### Form Strategy

- Use Mantine inputs with `useForm` as the default Mantine form stack.
- Use schema or field-level validation when requirements are explicit.
- Keep submission logic inside `form.onSubmit(...)` instead of scattering ad hoc event handlers across fields.

## `@mantine/hooks`

- `@mantine/hooks` provides more than 70 hooks.
- It is required by most other Mantine packages.
- It is standalone and can be used even outside Mantine component usage.
- Some state-management hooks are also compatible with React Native.

### Hook Families

Mantine hooks broadly cover:

- UI and DOM interaction
- state management
- utilities
- lifecycle helpers

Examples of high-value hooks:

- `use-disclosure`
- `use-debounced-value`
- `use-debounced-state`
- `use-throttled-value`
- `use-local-storage`
- `use-media-query`
- `use-click-outside`
- `use-hotkeys`
- `use-scroll-into-view`
- `use-focus-trap`
- `use-hover`
- `use-id`
- `use-uncontrolled`

### Hook Usage Rules

- Prefer Mantine hooks when they directly solve the needed interaction pattern and the project already depends on Mantine.
- Use hooks to support custom component logic or to bridge Mantine primitives with application behavior.
- Do not force Mantine hooks into places where native React logic is already simpler and established.

## Practical Rules

- Use `@mantine/form` for real forms, not just because there is one input.
- Use `@mantine/hooks` to reduce boilerplate in custom component logic.
- Keep form wiring predictable with `getInputProps`.
- Prefer Mantine’s hook and form primitives when they clearly reduce glue code and stay aligned with the rest of the Mantine stack.
