# Checkbox Examples

Read this file when implementing Ariakit checkbox UI beyond the default native checkbox presentation.

Use these examples as pattern references, not as copy-paste targets.

## Example Patterns

### Checkbox As Button

Source:

- https://ariakit.com/examples/checkbox-as-button

Use this pattern when:

- the interaction is logically a toggle
- the design system wants a button-like visual treatment
- native input rendering is not required

Key takeaways:

- render `Checkbox` as `<button />` through the `render` prop
- read checkbox state with `useStoreState` when label or visual content depends on checked state
- when the checkbox is rendered as a non-input element, style checked state with `[aria-checked="true"]` rather than `:checked`
- Ariakit automatically enables Enter activation for non-native checkbox render targets

Do not use this pattern when:

- form submission relies on native checkbox behavior
- browser-native input semantics or integrations are required

### Custom Checkbox

Source:

- https://ariakit.com/examples/checkbox-custom

Use this pattern when:

- the design requires a fully custom visual checkbox
- you still want a real checkbox control under the hood

Key takeaways:

- keep the Ariakit checkbox accessible while hiding the default presentation with `VisuallyHidden`
- separate the visible UI shell from the actual control semantics
- prefer this pattern over the button-rendered pattern when native checkbox behavior matters

### Checkbox Group

Source:

- https://ariakit.com/examples/checkbox-group

Use this pattern when:

- multiple checkboxes share one array-backed selection state
- the UI represents multi-select choices

Key takeaways:

- use `CheckboxProvider` to hold the shared array of selected values
- model group state as an array rather than many disconnected booleans when selections belong to one field
- pair grouped checkboxes with an appropriate label or surrounding group structure

## Selection Rules

- Use the custom checkbox pattern when you need native checkbox semantics with custom visuals.
- Use the button-rendered pattern when the UI is functionally a toggle button but still needs checkbox accessibility.
- Use the group pattern when the state belongs to one multi-select field.
