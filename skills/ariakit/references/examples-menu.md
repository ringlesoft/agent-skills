# Menu Examples

Read this file when implementing Ariakit menus with search, nested submenus, motion, context-menu positioning, checked state, radio state, slide transitions, or tooltip-enhanced triggers.

Use these examples as pattern references, not as copy-paste targets.

## Searchable Menus

### Menu With Combobox

Source:

- https://ariakit.com/examples/menu-combobox

Use this when:

- a dropdown menu also needs inline filtering
- users should search within menu actions or insertable items

Key takeaways:

- combine `MenuProvider` and `ComboboxProvider`
- render the `Combobox` inside the menu surface
- use `resetValueOnHide` so the search resets when the menu closes
- use `startTransition` for responsive filtering when the list is large or computed
- use `setValueOnClick={false}` when choosing an item should not overwrite the search text

### Submenu With Combobox

Source:

- https://ariakit.com/examples/menu-nested-combobox

Use this when:

- nested menus also need Notion-style search and autocomplete behavior
- the information architecture is hierarchical, but each level still benefits from search

Key takeaways:

- combine nested menu composition with combobox filtering
- use this for advanced command and insertion menus, not simple action dropdowns
- treat it as a high-complexity pattern that should only be used when both nesting and search are essential

## Positioning And Trigger Variants

### Context Menu

Source:

- https://ariakit.com/examples/menu-context-menu

Use this when:

- a menu should open on right click or context gesture

Key takeaways:

- use `getAnchorRect` to anchor the menu to the pointer position
- open the menu from `onContextMenu` after preventing the browser default menu
- this is the correct pattern for desktop-style contextual actions

### Menu With Tooltip

Source:

- https://ariakit.com/examples/menu-tooltip

Use this when:

- the menu trigger needs a tooltip on hover or focus
- the trigger is icon-heavy or otherwise benefits from a hint

Key takeaways:

- compose `MenuButton` with `TooltipAnchor`
- coordinate `MenuProvider` and `TooltipProvider`
- use `VisuallyHidden` when the visible affordance alone is not descriptive enough

## Animation And Advanced Motion

### Menu With Motion

Source:

- https://ariakit.com/examples/menu-framer-motion

Use this when:

- the project already uses Motion
- menus need reusable open and exit animations

Key takeaways:

- abstract menu behavior into a reusable animated wrapper
- keep Ariakit responsible for focus, keyboard interaction, and open state
- pass motion props through the wrapper rather than rebuilding menu logic from scratch

### Sliding Menu

Source:

- https://ariakit.com/examples/menu-slide

Use this when:

- nested menus should slide horizontally instead of appearing as independent floating layers
- the UI wants panel-like submenu transitions

Key takeaways:

- use nested menus with CSS Scroll Snap for slide transitions
- this is an advanced presentation pattern suited to dense option browsers
- use it when the submenu experience should feel like progressive drill-down navigation

## Checked And Single-Choice Menu State

### MenuItemCheckbox

Source:

- https://ariakit.com/examples/menu-item-checkbox

Use this when:

- the menu controls multiple persistent toggle options

Key takeaways:

- use `MenuItemCheckbox` with `values` and `setValues`
- store the checked state in the menu provider values object
- this is the correct menu pattern for watchlists, filters, and multi-toggle settings

### MenuItemRadio

Source:

- https://ariakit.com/examples/menu-item-radio

Use this when:

- the menu should choose one option from a mutually exclusive set

Key takeaways:

- use `MenuItemRadio` for single-choice menu state
- keep the selected value in menu provider values
- this is the right pattern for sort order, display mode, and one-of-many settings

## Nested Menus

### Submenu

Source:

- https://ariakit.com/examples/menu-nested

Use this when:

- actions are hierarchical and should expand on hover or keyboard navigation

Key takeaways:

- compose nested menus instead of flattening all actions into one large surface
- use this for structured action trees, not as a default for shallow menus

## Selection Rules

- Use menu-plus-combobox patterns when search is the main requirement.
- Use context-menu positioning when the trigger is a pointer location rather than a button.
- Use checkbox or radio menu items when the menu owns persistent state.
- Use nested or sliding patterns only when the IA is genuinely hierarchical.
- Use tooltip-enhanced menu triggers when discoverability is the issue, not when the menu itself should explain the action.
