# Menubar Examples

Read this file when building Ariakit menubars for site or application navigation.

Use these examples as pattern references, not as copy-paste targets.

## Menubar

### Navigation Menubar

Source:

- https://ariakit.com/examples/menubar-navigation

Use this when:

- the top-level navigation mixes direct links and submenu sections
- the navigation must remain tabbable and accessible with keyboard and screen readers

Key takeaways:

- use `Menubar` as the root navigation structure
- compose top-level entries as menu buttons or direct links depending on whether they expand
- use grouped submenu content with `MenuGroup`
- use `MenuItem` for submenu navigation items, including descriptive content when the IA benefits from it
- this pattern is appropriate for rich site navigation, not just application command menus

Selection rules:

- use menubar navigation when the problem is global navigation structure
- do not substitute a menubar for a simple dropdown button or inline action menu
