# Combobox Examples

Read this file when implementing Ariakit comboboxes with filtering, grouped content, custom triggers, router links, multi-select behavior, or integration with non-Ariakit primitives.

Use these examples as pattern references, not as copy-paste targets.

## Basic Interaction Patterns

### Animated Combobox

Source:

- https://ariakit.com/examples/combobox-animated

Use this when:

- the popover needs CSS-driven enter and exit transitions

Key takeaways:

- animate the combobox popover with CSS transitions
- keep Ariakit in control of visibility so the popover waits for the exit transition before fully hiding
- prefer Ariakit styling hooks over custom mount-delay state

### ComboboxCancel

Source:

- https://ariakit.com/examples/combobox-cancel

Use this when:

- the input needs a dedicated clear button

Key takeaways:

- use `ComboboxCancel` instead of wiring a generic clear button manually
- this keeps clear behavior consistent with combobox state
- pairs well with `autoSelect`, `sameWidth`, and anchored popover layouts

### ComboboxDisclosure

Source:

- https://ariakit.com/examples/combobox-disclosure

Use this when:

- the combobox should support explicit open and close behavior from an adjacent button

Key takeaways:

- use `ComboboxDisclosure` rather than a generic button
- this is the right pattern for hybrid input-plus-disclosure UIs

## Filtering Patterns

### Combobox Filtering

Source:

- https://ariakit.com/examples/combobox-filtering

Use this when:

- filtering is owned by the feature code
- large or expensive matching work should not block typing

Key takeaways:

- drive filtering from combobox value updates
- use `startTransition` so typing stays responsive during list recomputation
- keep the filtered list outside Ariakit when the feature needs explicit matching control

### Combobox With Integrated Filter

Source:

- https://ariakit.com/examples/combobox-filtering-integrated

Use this when:

- you want a higher-level reusable combobox abstraction with built-in filtering

Key takeaways:

- wrap Ariakit primitives in a reusable component
- use `useDeferredValue` to smooth filtering in a higher-level API
- this is useful when the same searchable combobox pattern appears repeatedly

## Structured Content Patterns

### ComboboxGroup

Source:

- https://ariakit.com/examples/combobox-group

Use this when:

- search results should be organized into labelled sections

Key takeaways:

- use `ComboboxGroup` and `ComboboxGroupLabel`
- group matched items by type or category before rendering
- prefer groups over separator-heavy menus when the data is categorical

### Combobox With Tabs

Source:

- https://ariakit.com/examples/combobox-tabs

Use this when:

- the search surface needs category switching plus combobox behavior
- tab changes and filtering should remain responsive

Key takeaways:

- combine `Combobox` with `Tab` primitives rather than rebuilding keyboard coordination manually
- use `startTransition` for responsive tab-driven filtering and view changes
- this is a strong pattern for advanced search panels or command surfaces

## Content Type Variants

### Combobox With Links

Source:

- https://ariakit.com/examples/combobox-links

Use this when:

- results should navigate to destinations
- the combobox acts like page search or command navigation

Key takeaways:

- render `ComboboxItem` as links
- preserve keyboard and mouse activation semantics
- this is the canonical pattern for searchable navigation results

### Textarea With Inline Combobox

Source:

- https://ariakit.com/examples/combobox-textarea

Use this when:

- suggestions are triggered inline inside multiline text
- mention-like or token-triggered completion is needed

Key takeaways:

- render `Combobox` as a `textarea`
- drive popup visibility and suggestions from parsed trigger characters
- use this pattern for mentions, inline commands, and structured text helpers

## Selection Variants

### Multi-Selectable Combobox

Source:

- https://ariakit.com/examples/combobox-multiple

Use this when:

- users must choose multiple values from one searchable combobox

Key takeaways:

- pass an array to `selectedValue`
- treat combobox selection state as multi-valued rather than simulating multiple independent comboboxes
- this pattern fits tokenized or tag-like selection UIs

## Integration Patterns

### Radix Combobox

Source:

- https://ariakit.com/examples/combobox-radix

Use this when:

- the project already uses Radix UI
- you only need Ariakit’s combobox/autocomplete behavior layered onto that stack

Key takeaways:

- use only the Ariakit primitives necessary for combobox behavior
- prefer this integration path when replacing the full host component library is unrealistic

### Radix Select With Combobox

Source:

- https://ariakit.com/examples/combobox-radix-select

Use this when:

- the project already has a Radix Select and needs search/typeahead

Key takeaways:

- layer primitive Ariakit combobox behavior into the Radix Select surface
- use this only when the project is constrained by an existing Radix investment
- if the team can use Ariakit select components directly, prefer the native Ariakit path instead

## Selection Rules

- Use filtering examples when search logic complexity is the main problem.
- Use grouped or tabs patterns when result structure is the main problem.
- Use links, textarea, or multi-select patterns when item behavior differs from a plain single-select list.
- Use Radix integration examples only when the host stack already depends on Radix and migration is not practical.
