# Tab, Toolbar, And Tooltip Examples

Read this file when implementing animated tab panels, router-controlled tabs, toolbar-integrated selects, or motion-enhanced tooltips.

Use these examples as pattern references, not as copy-paste targets.

## Tabs

### Animated TabPanel

Source:

- https://ariakit.com/examples/tab-panel-animated

Use this when:

- tab panels should transition visually as selection changes

Key takeaways:

- animate `TabPanel` transitions with CSS rather than replacing tab semantics with custom view logic
- keep `TabProvider`, `TabList`, `Tab`, and `TabPanel` as the structural backbone
- this is the tab counterpart to animated disclosure, dialog, combobox, and select patterns

### Tab With React Router

Source:

- https://ariakit.com/examples/tab-react-router

Use this when:

- tab state should be controlled by browser history
- each tab corresponds to route-driven content

Key takeaways:

- render tabs as router links
- keep keyboard tab navigation intact while letting routing own the selected state
- use this when tabs represent navigable application views, not just local UI state

### Tab With Next.js App Router

Source:

- https://ariakit.com/examples/tab-next-router

Use this when:

- the project uses Next.js App Router
- tab selection should be URL-controlled and server-rendered

Key takeaways:

- use parallel routes or URL-driven route segments for tab state
- keep the tab panel content route-backed instead of duplicating client-only selection state

## Toolbar

### Toolbar With Select

Source:

- https://ariakit.com/examples/toolbar-select

Use this when:

- a select control must behave as a toolbar item within a larger editing or formatting toolbar

Key takeaways:

- render `Select` as a `ToolbarItem`
- compose `Toolbar`, `ToolbarSeparator`, `SelectProvider`, `Select`, and `SelectPopover` rather than treating the select as an unrelated floating control
- this pattern is useful for editor toolbars and formatting controls

## Tooltip

### Tooltip With Motion

Source:

- https://ariakit.com/examples/tooltip-framer-motion

Use this when:

- tooltips need reusable motion-based enter and exit animation
- the project already uses Motion

Key takeaways:

- abstract tooltip behavior into a reusable custom component
- expose `render` on the custom anchor wrapper so callers can choose the underlying anchor element
- keep Ariakit tooltip semantics while layering motion and composition on top

## Selection Rules

- Use animated tab panels when motion is the only missing requirement.
- Use router-backed tabs when tabs represent navigable state.
- Use toolbar-select composition when the select belongs inside a keyboard-navigable toolbar.
- Use motion-enhanced tooltips when animation and reusable tooltip abstraction are the main requirements.
