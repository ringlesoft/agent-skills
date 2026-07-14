---
name: ariakit
description: Use this skill when building or refactoring React interfaces with Ariakit, especially dialogs, menus, popovers, comboboxes, tabs, select controls, toolbars, and other accessible headless components that require explicit store wiring, provider setup, and keyboard-safe composition.
---

# Ariakit

Use this skill when the project already uses Ariakit or when the requested UI clearly benefits from Ariakit's accessible headless primitives.

Do not use this skill for generic React UI work unless Ariakit is already part of the stack or the user explicitly wants it.

Validate the installed Ariakit version before relying on a specific API shape. The guidance below is aligned with the official Ariakit API reference reviewed on July 14, 2026.

Baseline assumptions from Ariakit's getting-started guide:

- Ariakit is a React library for accessible, lower-level UI primitives.
- It expects `react` and `react-dom`; the guide states React 17 or newer.
- The main package is `@ariakit/react`.
- Components are unstyled by default.

## Read These References When Needed

- Read [references/providers-and-stores.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/providers-and-stores.md) when the task involves controlled state, uncontrolled defaults, shared stores, `useStoreState`, `getState()`, provider boundaries, or context-based helper components.
- Read [references/composition-and-styling.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/composition-and-styling.md) when the task requires `render`, custom elements, router integration, motion libraries, design-system wrappers, overlay animation, or advanced Ariakit styling.
- Read [references/coding-guidelines.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/coding-guidelines.md) when creating new Ariakit wrappers, examples, or documentation-quality code and the host repository does not already impose a different style.
- Read [references/examples-checkbox.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/examples-checkbox.md) when implementing custom checkbox visuals, checkbox-as-button toggles, or grouped checkbox selection.
- Read [references/examples-combobox.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/examples-combobox.md) when implementing advanced combobox behavior such as filtering, disclosure, cancel controls, grouped items, multi-select, links, textarea rendering, tabs, or Radix integration.
- Read [references/examples-dialog.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/examples-dialog.md) when implementing animated dialogs, command palettes, nested dialogs, router-controlled modals, custom backdrops, toast interoperability, or Radix-style dialog wrappers.
- Read [references/examples-disclosure-form-hovercard.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/examples-disclosure-form-hovercard.md) when implementing animated disclosures, form radios, form-integrated selects, or keyboard-accessible hovercards.
- Read [references/examples-menubar.md](/Users/ringle/Documents/PERSONAL/Projects/AI/agent-skills/skills/ariakit/references/examples-menubar.md) when implementing rich site or app navigation with `Menubar`, grouped submenus, and mixed link/menu top-level items.

## Workflow

1. Inspect the existing codebase first.
2. Confirm the project has `@ariakit/react` and compatible React dependencies before introducing new Ariakit code.
3. Confirm which Ariakit primitive matches the requested behavior.
4. Create the correct store hook for that primitive.
5. Share store state through the matching provider when multiple related subcomponents are involved.
6. Compose the UI from Ariakit primitives instead of rebuilding ARIA behavior manually.
7. Add styling separately; Ariakit does not provide presentation.
8. Verify focus handling, keyboard behavior, and open/close state after the change.
9. Prefer current API names over deprecated ones.

## Core Rules

### State

- Ariakit components are headless and state-driven.
- Prefer the primitive-specific store hook such as `useDialogStore`, `useMenuStore`, `useSelectStore`, or `useComboboxStore`.
- Update component state through the store API instead of ad hoc DOM manipulation.
- Prefer `useStoreState` for reactive reads and `store.getState()` for event-time reads.
- Prefer dedicated store helpers such as `setOpen`, `setValue`, `show`, `hide`, or `toggle` over generic mutation when available.
- Load the providers and stores reference file before implementing non-trivial controlled or shared state patterns.

### Composition

- Use the related subcomponents from the same Ariakit family.
- Prefer composition over custom event choreography.
- When a component family expects a provider, keep all related children inside it.
- Use labels, headings, descriptions, groups, rows, and separators from the same family so ARIA relationships are wired automatically.
- Prefer the `render` prop over rebuilding an Ariakit primitive manually.
- Custom components passed through `render` must be open for extension: they must forward refs, spread props, merge `className` and `style`, and chain events.
- Load the composition and styling reference file before implementing custom wrappers or alternate rendered elements.

### Accessibility

- Preserve Ariakit's keyboard and focus behavior.
- Do not replace built-in semantics with custom ARIA unless there is a concrete gap to solve.
- Supply missing labels such as `aria-label` or `aria-labelledby` when the UI would otherwise be ambiguous.
- When a family exposes `Heading`, `Description`, `GroupLabel`, or similar components, prefer those over hand-managed ids.
- Keep focus-visible styling intact. Ariakit exposes focusable state such as `data-focus-visible` on focus-aware elements.

### Styling

- Ariakit ships unstyled primitives.
- Add classes, CSS modules, Tailwind utilities, or styled wrappers explicitly.
- Avoid coupling behavior to visual selectors when the store state already expresses intent.
- Prefer data attributes, store state, and documented composition points over DOM structure assumptions.
- Preserve focus-visible treatment and prefer Ariakit data attributes for transitions.
- Use Ariakit overlay CSS variables when viewport height or transform origin matter.

## Canonical Family Pattern

Most Ariakit families follow this structure:

1. `useXStore` creates state.
2. `XProvider` optionally provides the store to descendants.
3. Root and subcomponents consume the store through `store` props or context.
4. Labels, headings, descriptions, groups, rows, arrows, dismiss buttons, and value renderers are composed as separate primitives.

Default approach:

- Create the store near the feature boundary.
- Use the provider when the family includes multiple coordinated descendants or when you want implicit context wiring.
- Pass `store` explicitly when composition is shallow or local.
- Keep business logic in surrounding React code; let Ariakit own interaction semantics.
- If provider-vs-store ownership is unclear, read the providers and stores reference file before coding.

## Primitive Selection

- `Dialog`: modal or non-modal overlays, confirmation flows, side panels.
- `Menu` or `Menubar`: action menus, context menus, app-style menus.
- `Popover` or `Hovercard`: anchored floating content that is not a modal dialog.
- `Combobox`: searchable option pickers and autocomplete inputs.
- `Select`: accessible custom selects with controlled open state.
- `Tab`: tabbed panels with keyboard navigation.
- `Disclosure`: show/hide sections and accordion-like interactions.
- `Toolbar`: grouped controls with directional keyboard support.
- `Tooltip`: short non-interactive help text.
- `Checkbox`, `Radio`, and `Select`: controlled choice inputs.
- `Form`: form state, validation, field descriptions, error output, and dynamic array operations.
- `Composite`: low-level roving focus and typeahead foundations when higher-level primitives are not a fit.
- `Collection`, `Group`, `Heading`, `Separator`, `Portal`, `Role`, `Focusable`, `FocusTrap`, and `VisuallyHidden`: support primitives for custom composition.

If the requested behavior mixes patterns, choose the primitive based on interaction model first, not on appearance.

Use higher-level families before low-level ones. Reach for `Menu`, `Select`, `Tab`, `Toolbar`, `Dialog`, or `Combobox` before building from `Composite` or `Role`.

## Family-Specific Guidance

### Button and Focusable

- `Button` is the accessible default for clickable actions.
- If rendering a non-button element as an action, prefer Ariakit primitives that add the necessary accessibility behavior rather than recreating it manually.
- `Focusable` is useful when an element must participate in keyboard focus behavior outside a normal form control or button.

### Dialog

- Standard composition is `useDialogStore` + `DialogDisclosure` + `Dialog` + optional `DialogHeading`, `DialogDescription`, and `DialogDismiss`.
- `Dialog` renders in a portal by default, so account for layering, scroll locking, and test setup.
- Use dialog-specific heading and description components to wire `aria-labelledby` and `aria-describedby`.
- Prefer `DialogDismiss` for close controls inside the surface rather than custom buttons that manually toggle state.

### Disclosure

- Use `Disclosure` with `DisclosureContent` for toggled content regions and accordion-like sections.
- Keep the content in `DisclosureContent` rather than conditionally removing semantics yourself unless the feature specifically requires custom mounting behavior.

### Popover and Hovercard

- Use `PopoverAnchor` or `PopoverDisclosure` when content must be positioned relative to another element.
- Use `PopoverHeading`, `PopoverDescription`, `PopoverArrow`, and `PopoverDismiss` when those semantics are needed.
- Use `Hovercard` only for hover/focus-triggered supplemental content, not for essential actions or modal interactions.
- Keyboard access matters for hovercards: Ariakit exposes `HovercardDisclosure` so keyboard users can intentionally open the content.

### Menu and Menubar

- Standard menu composition is `useMenuStore` + `MenuButton` + `Menu` or `MenuList` + `MenuItem` variants.
- Use `MenuItemCheckbox` and `MenuItemRadio` when menu options map to persistent values. These require a `name` prop tied to menu store values.
- Use `MenuGroup` and `MenuGroupLabel` for grouped options, and `MenuSeparator` for visual division.
- Use `Menubar` and `useMenubarStore` for application-style horizontal menu systems. Avoid deprecated `MenuBar` and `useMenuBarStore`.

### Combobox

- Standard composition is `useComboboxStore` + `Combobox` + `ComboboxPopover` or `ComboboxList` + `ComboboxItem`.
- Use `ComboboxLabel` for labeling and `ComboboxDisclosure` when the popup needs an explicit toggle button.
- Use `ComboboxItemValue` when you want highlighted matching text without hand-splitting display strings.
- Use `ComboboxGroup` and `ComboboxGroupLabel` for grouped suggestions.
- Use `ComboboxRow` only for two-dimensional arrow-key navigation.
- Avoid `ComboboxSeparator`; it is deprecated in favor of grouped content with CSS borders.
- The popup role defaults to `listbox`, but Ariakit allows other valid combobox popup roles such as `menu`, `tree`, `grid`, or `dialog`. Only override the role when the interaction model truly changes.

### Select

- Standard composition is `useSelectStore` + `Select` + `SelectPopover` or `SelectList` + `SelectItem`.
- Use `SelectLabel` instead of a native `<label>` when labeling the trigger.
- Use `SelectValue` to render current state and `SelectArrow` for disclosure affordance.
- Use `SelectGroup`, `SelectGroupLabel`, and `SelectHeading` for grouped or structured option lists.
- Use `SelectRow` only for two-dimensional navigation.
- Prefer `SelectGroup` with CSS borders over deprecated `SelectSeparator`.
- The popup role defaults to `listbox`; only change it to another valid popup role when the design genuinely requires it.

### Checkbox and Radio

- Use `Checkbox` and `useCheckboxStore` when the state may be boolean, scalar, or an array of selected values.
- `CheckboxProvider` is useful when multiple checkboxes share the same state source.
- Use `Radio` inside `RadioGroup` with `useRadioStore` for mutually exclusive choices.

### Tabs

- Standard composition is `useTabStore` + `TabList` + `Tab` + `TabPanel`.
- Keep each `Tab` inside a `TabList`; keep each panel as `TabPanel` so selection and labeling relationships remain intact.

### Toolbar

- Use `Toolbar` and `ToolbarItem` for grouped interactive controls with arrow-key navigation.
- Use `ToolbarContainer` when a toolbar item needs to wrap another interactive widget.
- Avoid deprecated `ToolbarInput`; prefer `ToolbarItem render={<input />}>` patterns.

### Tooltip

- Use `TooltipAnchor` + `Tooltip` for brief explanatory content on hover/focus.
- Tooltips should stay non-interactive and concise.
- If the content contains actions, form controls, or substantial layout, use `Popover` or `Dialog` instead.

### Form

- Use `useFormStore` when Ariakit should control form values, submission state, validation, and field metadata.
- `FormInput` is for native input-like elements where `value` and `onChange` should flow through automatically.
- `FormControl` is the abstraction for custom controls whose value contract is not the native `value`/`onChange` pair.
- Use `FormLabel`, `FormDescription`, and `FormError` to keep field semantics wired correctly.
- Use `FormGroup`, `FormGroupLabel`, `FormRadioGroup`, and `FormRadio` for grouped controls.
- Use `FormPush` and `FormRemove` for array fields, `FormReset` for reset behavior, and `FormSubmit` for submit behavior.
- Prefer `FormField` only when maintaining older code; it is deprecated in favor of `FormControl`.
- `FormSubmit` supports an accessible disabled state during submission. Preserve that instead of replacing it with custom button-locking logic.

### Low-Level Foundations

- `Composite` is the right foundation when building a custom roving-focus widget that does not fit an existing Ariakit family.
- `CompositeRow` and `CompositeTypeahead` support grid-like arrow navigation and typeahead.
- `Collection` is useful when you need item registration and ordering without a full interaction family.
- `Group` and `GroupLabel` are generic grouping helpers when a more specialized family is not available.
- `Heading` and `HeadingLevel` help preserve heading hierarchy when DOM element choice varies.
- `Portal` and `PortalContext` let you control where content is portaled.
- `Role` is an escape hatch for advanced composition. Use it sparingly and prefer more specific primitives when available.
- `FocusTrap` and `FocusTrapRegion` are lower-level focus containment tools when a full dialog or popover pattern is not appropriate.
- `VisuallyHidden` is the preferred way to hide assistive text without removing it from the accessibility tree.

## Implementation Guidance

- If Ariakit is not installed yet and the task requires adding it, install `@ariakit/react` rather than older package names or ad hoc subpackages.
- Do not use the CDN setup for production work; the getting-started guide presents it as development-only.
- Keep open state controlled when the surrounding feature already owns it.
- Use the `render` prop or supported element overrides when integration with an existing design system requires different DOM elements.
- Expect overlays such as dialogs, popovers, and hovercards to use portals unless configured otherwise.
- When integrating with forms or routing, let Ariakit manage interaction behavior and keep business logic in surrounding React code.
- Prefer official subcomponents over manual ids and aria attributes when a family provides them.
- Prefer context hooks such as `useDialogContext`, `useMenuContext`, `useSelectContext`, or similar only inside components that genuinely live within that family boundary.
- If a design system wrapper is needed, wrap Ariakit primitives without stripping their store, role, focus, or labeling behavior.
- Match the host repository’s style before applying Ariakit’s own documentation-style conventions for imports or `forwardRef`.

## Deprecated APIs To Avoid

- `MenuBar` and `MenuBarProvider`: use `Menubar` and `MenubarProvider`.
- `useMenuBarStore` and `useMenuBarContext`: use `useMenubarStore` and `useMenubarContext`.
- `ComboboxSeparator`: use `ComboboxGroup` plus CSS borders.
- `SelectSeparator`: use `SelectGroup` plus CSS borders.
- `FormField`: use `FormControl`.
- `ToolbarInput`: use `ToolbarItem` with a rendered input.

## Failure Modes To Check

- Store created but not passed to the rendered components.
- Related subcomponents rendered outside the matching provider.
- Custom styling breaking focus visibility.
- Custom click handlers fighting store state.
- Popover or dialog layout issues caused by portal assumptions.
- Menu, dialog, popover, hovercard, select, or form labels/descriptions rendered without the matching family wrappers, which breaks automatic `aria-labelledby` or `aria-describedby`.
- Using tooltip or hovercard patterns for interactive content that should actually be a popover or dialog.
- Replacing `FormControl` with native assumptions for a custom component and silently dropping value synchronization.
- Changing popup roles from the defaults without updating the surrounding interaction model.
- Reintroducing deprecated APIs from old examples or older codebases.
- Passing a custom component through `render` that does not forward props and refs correctly.
- Styling overlays as if they were rendered inline when they are actually portaled.
- Reading whole-store state in many child components when a narrow property or computed selector would be more stable.

## Output Expectations

When using this skill, produce code that:

- uses the correct Ariakit primitive family
- wires store state explicitly
- preserves accessible keyboard behavior
- keeps styling separate from behavior
- uses the correct Ariakit subcomponents for headings, descriptions, labels, groups, and dismiss controls
- avoids deprecated APIs unless maintaining existing code requires compatibility
- fits the surrounding project patterns instead of forcing a standalone demo
