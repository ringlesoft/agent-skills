# Select Examples

Read this file when implementing Ariakit selects with animation, search, tabs, grouped items, custom item rendering, grid navigation, multi-select behavior, or router-controlled value state.

Use these examples as pattern references, not as copy-paste targets.

## Animation

### Animated Select

Source:

- https://ariakit.com/examples/select-animated

Use this when:

- the select popover needs CSS-driven enter and exit transitions

Key takeaways:

- animate the select popover through Ariakit’s mounted and transition-aware behavior
- treat this as the select equivalent of animated dialog and animated combobox patterns

## Searchable Selects

### Select With Combobox

Source:

- https://ariakit.com/examples/select-combobox

Use this when:

- a select needs inline search over its options

Key takeaways:

- combine `Select` and `Combobox` through coordinated providers
- use `resetValueOnHide` when the search query should reset on close
- use feature-owned filtering logic for matching and result ordering

### Select With Combobox And Tabs

Source:

- https://ariakit.com/examples/select-combobox-tab

Use this when:

- the select options must be searchable and category-driven
- tabs should partition the option space within one dropdown experience

Key takeaways:

- combine `Select`, `Combobox`, and `Tab` as one higher-level abstraction
- this is an advanced pattern for dense datasets and structured pickers
- use it only when a plain searchable select is no longer enough

## Structured And Custom Option Layouts

### Select Grid

Source:

- https://ariakit.com/examples/select-grid

Use this when:

- options should be navigated in two dimensions instead of one
- the popover should behave like a grid of choices

Key takeaways:

- render the select popup with a `grid` role
- use this for visual position pickers, alignment controls, swatch matrices, and similar spatial choices

### SelectGroup

Source:

- https://ariakit.com/examples/select-group

Use this when:

- options belong to labelled categories

Key takeaways:

- use `SelectGroup` and `SelectGroupLabel`
- prefer grouped sections over long flat lists when the data has clear taxonomy

### Select With Custom Items

Source:

- https://ariakit.com/examples/select-item-custom

Use this when:

- each option needs richer presentation than a plain text label
- the selected value should display custom content

Key takeaways:

- customize both `SelectItem` children and the displayed selected value
- this is the correct pattern for avatar pickers, account switchers, and metadata-rich option rows

## Multi-Value And Router-Controlled State

### Multi-Select

Source:

- https://ariakit.com/examples/select-multiple

Use this when:

- users must choose multiple values from one select widget

Key takeaways:

- pass an array to the select provider default or controlled value
- model the selection as one multi-valued field instead of multiple separate selects

### Select With Next.js App Router

Source:

- https://ariakit.com/examples/select-next-router

Use this when:

- the selected value should be encoded in the URL
- the project uses Next.js App Router

Key takeaways:

- use routing as the state owner for select value
- optimistic updates can keep the UI responsive while navigation-driven state settles
- this is the right pattern when filters or selections should participate in sharable URLs and history

## Selection Rules

- Use animated select when motion is the only missing requirement.
- Use searchable select patterns when option discovery is the main problem.
- Use grid or grouped patterns when information structure is the main problem.
- Use custom-item rendering when presentation richness is the main problem.
- Use multi-select or router-controlled patterns when state shape or navigation integration is the main problem.
