# Disclosure, Form, And Hovercard Examples

Read this file when implementing animated disclosures, validated form radios, custom form selects, or keyboard-accessible hovercards.

Use these examples as pattern references, not as copy-paste targets.

## Disclosure

### Animated Disclosure

Source:

- https://ariakit.com/examples/disclosure-animated

Use this when:

- disclosure content should expand and collapse with CSS transitions

Key takeaways:

- animate `DisclosureContent` height with CSS rather than replacing disclosure behavior with custom mount logic
- treat this as the disclosure counterpart to animated dialog, combobox, and select patterns
- keep Ariakit in charge of disclosure state and semantics while CSS handles the motion

## Form

### FormRadio

Source:

- https://ariakit.com/examples/form-radio

Use this when:

- a required choice must be captured through radios inside an Ariakit form
- custom validation should block submission until one option is selected

Key takeaways:

- create the form with `useFormStore`
- group related radios with `FormRadioGroup`
- use `FormGroupLabel` and `FormError` so the grouped field stays understandable and accessible
- validate through the form store and submit through Ariakit form helpers rather than scattering ad hoc field state

### Form With Select

Source:

- https://ariakit.com/examples/form-select

Use this when:

- a custom Ariakit select must participate in browser form submission or validation

Key takeaways:

- combine `Form` and `Select` through a higher-level field abstraction instead of treating them as unrelated widgets
- this pattern is useful when the UI needs a styled select without giving up form semantics
- the example still references `FormField`; when authoring new code, prefer modern `FormControl`-style guidance unless compatibility requires older APIs

## Hovercard

### Hovercard With Keyboard Support

Source:

- https://ariakit.com/examples/hovercard-disclosure

Use this when:

- a hovercard must also be discoverable and openable from the keyboard

Key takeaways:

- use `HovercardDisclosure` so keyboard users have an explicit control to open the hovercard
- pair the disclosure with `VisuallyHidden` text when the visible control is icon-only
- keep `HovercardAnchor` for hover/focus behavior and `HovercardDisclosure` for explicit keyboard access

## Selection Rules

- Use animated disclosure when the only missing piece is motion.
- Use `FormRadio` when grouped radio validation is the main requirement.
- Use form-select composition when a styled select must still behave like a real form field.
- Use hovercard disclosure when hover-only discovery would fail keyboard users.
