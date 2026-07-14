# Providers And Stores

Read this file when the task involves shared Ariakit state, controlled or uncontrolled components, deep composition, or custom logic that needs to inspect or update store state directly.

## Provider Usage

- Component providers are an optional higher-level API over component stores.
- Use a provider when multiple related Ariakit components should connect to the same store implicitly.
- If you skip the provider, pass the same `store` prop to each top-level Ariakit component that participates in the interaction.
- Providers can also receive a `store` prop, so you can combine explicit store creation with provider-based context wiring.

Use providers when:

- the feature has several related subcomponents
- the store would otherwise be threaded through many layers
- you want a simpler controlled or uncontrolled wrapper API

Prefer explicit `store` props when:

- composition is shallow
- the code already passes the store cleanly
- you need to see state ownership clearly at the call site

## Controlled And Uncontrolled State

Provider and store APIs support the same three patterns:

1. Default state via `default*` props or store options.
2. State setters such as `setValue`, `setOpen`, or `setValues`.
3. Fully controlled state via `value`, `open`, `values`, or the equivalent state property.

Guidance:

- Use `default*` when the feature should initialize state and then let Ariakit manage it.
- Use the state setter callbacks for side effects, bridging to parent callbacks, and synchronization.
- Use controlled state only when a parent or sibling system already owns the data.
- Do not provide a controlled prop without its corresponding setter unless the component is intentionally read-only.
- When wrapping Ariakit in your own abstraction, forward `value` and `onChange` style contracts directly into the matching store or provider state and setter props.

## Store Reading

Use `useStoreState` for reactive reads:

- `useStoreState(store)` reads the entire state and re-renders on every state change.
- `useStoreState(store, "open")` reads a specific property and only re-renders when that property changes.
- `useStoreState(store, selector)` computes a derived value and only re-renders when the derived result changes.

Prefer specific property reads or computed selectors over reading the whole state unless the component truly needs the full object.

If you use a selector:

- keep it narrow
- compute only what the component needs
- avoid rebuilding unrelated objects inside the selector

## Reading State In Events

- Inside event handlers, use `store.getState()` instead of `useStoreState`.
- This avoids unnecessary subscriptions and gives access to the latest state snapshot.
- Use this for keyboard handlers, analytics, one-off logic branches, and integration callbacks.

## Store Writing

- Prefer specific store methods such as `setOpen`, `setValue`, `show`, `hide`, or `toggle` when available.
- `setState()` is valid, but dedicated methods are clearer and align with Ariakit’s API shape.
- Functional updates such as `dialog.setOpen((open) => !open)` are appropriate when the next state depends on the previous one.

## Context Hooks

- Passing `store` as a prop is usually the simplest option.
- Use context hooks such as `useMenuContext`, `useDialogContext`, or `useFormContext` when a child is deeply nested or the surrounding composition makes prop passing awkward.
- Context hooks are appropriate inside family-specific helper components that must adapt to the nearest parent store.

Use context carefully:

- only inside a known provider boundary
- only when the nearest matching store is actually the intended one
- only when prop-based ownership would be less clear

## Practical Rules

- Create the store close to the feature boundary.
- Choose one clear state owner.
- Use providers for shared tree-wide state, not as a reflex.
- Use `useStoreState` for reactive reads and `getState()` for event-time reads.
- Prefer dedicated setters and helpers over generic state mutation.
