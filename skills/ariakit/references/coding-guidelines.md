# Coding Guidelines

Read this file when writing new Ariakit-heavy components, wrappers, examples, or documentation-quality code.

These guidelines are drawn from Ariakit’s own coding guidance. They are not hard requirements for every host codebase, but they are useful defaults when no stronger local convention exists.

## ForwardRef Style

Prefer named functions inside `React.forwardRef`:

- easier stack traces
- clearer component identity
- no separate `displayName` assignment needed

Preferred pattern:

```tsx
export const Combobox = React.forwardRef<HTMLInputElement, Props>(
  function Combobox(props, ref) {
    // ...
  },
);
```

Avoid anonymous arrow functions inside `forwardRef` unless the local codebase strongly prefers them.

## Import Style

When many Ariakit exports are needed in one file, prefer namespace imports for readability:

```tsx
import * as Ariakit from "@ariakit/react";
```

Use this when a destructured import would become long and noisy.

Notes:

- this is mainly a readability convention
- modern bundlers still tree-shake unused exports
- do not access `Ariakit[runtimeVariable]` or similar dynamic property lookups, because that defeats tree shaking

## Application Rule

Match the host repository first.

- If the project already uses named imports everywhere, do not churn files just to enforce namespace imports.
- If the project uses anonymous `forwardRef` wrappers consistently, preserve local style unless you are creating a new isolated wrapper layer.
- Use Ariakit’s coding style as a default only when the repository does not already establish a stronger pattern.
