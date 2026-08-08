# Mantine Migration Guides

Use this reference to scope and execute a Mantine major-version upgrade. It summarizes the high-impact changes from the official guides; review the linked guide and release changelog for package-specific changes not listed here.

## 6.x to 7.x

Source: [official 6.x to 7.x guide](https://mantine.dev/guides/6x-to-7x/).

- Choose a styling path before upgrading. The default v7 approach is CSS Modules with `postcss-preset-mantine`; alternatively, install and configure `@mantine/emotion` to retain CSS-in-JS patterns.
- `createStyles` and `Global` are removed from `@mantine/core`. With Emotion, import them from `@mantine/emotion`; with CSS Modules, replace them with module CSS and a global stylesheet imported at the application entry point.
- Without `@mantine/emotion`, replace `sx` with `className` or narrow inline `style` usage. Inline styles cannot express nested selectors, media queries, or pseudo-classes.
- Replace nested selectors in `styles` with CSS Module classes passed through `classNames`. Simple, non-nested `styles` entries remain supported.
- Replace theme-object values in styles with Mantine CSS variables, for example `theme.colors.red[6]` becomes `var(--mantine-color-red-6)` and `theme.spacing.xl` becomes `var(--mantine-spacing-xl)`.
- `theme.colorScheme` was removed. For conditional styles use `light-dark()` or the PostCSS `@mixin light` / `@mixin dark` mixins. In SSR, do not conditionally render based on color scheme; use CSS to show or hide scheme-specific content.

## 7.x to 8.x

Source: [official 7.x to 8.x guide](https://mantine.dev/guides/7x-to-8x/).

- If importing individual core global styles, replace `@mantine/core/styles/global.css` with `baseline.css`, `default-css-variables.css`, and `global.css`. Projects importing `@mantine/core/styles.css` need no change.
- `Portal` enables `reuseTargetNode` by default. If this causes a stacking-context or `z-index` regression, set its theme default to `false`.
- `Switch` now displays a checked thumb indicator. Set the theme default `withThumbIndicator: false` to preserve its v7 appearance.
- `@mantine/dates` callbacks now use date strings, such as `YYYY-MM-DD`, rather than `Date` instances. Migrate state and downstream code to strings, or explicitly convert at the boundary. Remove `DatesProvider`'s unsupported `timezone` setting and handle time zones with a date library.
- Rename `DateTimePicker`'s `timeInputProps` to `timePickerProps` because it now uses `TimePicker`.
- `@mantine/code-highlight` now uses Shiki. To continue using Highlight.js, add it explicitly and configure `CodeHighlightAdapterProvider` with `createHighlightJsAdapter` and a Highlight.js stylesheet.
- Replace `Menu.Item[data-hovered]` styling with `:hover` and `:focus`. `Popover` now defaults `hideDetached` to `true`; set the default to `false` only if the previous detached-target behavior is required.
- Upgrade `@mantine/carousel` to Embla 8: install `embla-carousel` and `embla-carousel-react` 8.x, move supported Embla props into `emblaOptions`, remove unsupported `speed` and `draggable`, remove `useAnimationOffsetEffect`, and import `EmblaCarouselType` from `embla-carousel`.

## 8.x to 9.x

Source: [official 8.x to 9.x guide](https://mantine.dev/guides/8x-to-9x/).

- Upgrade the React runtime to 19.2 or later before installing Mantine 9. Upgrade every `@mantine/*` package together; also upgrade Tiptap to 3.x and Recharts to 3.x when those extensions are used.
- In `useForm`, the second generic is now the transformed-values type, not the transform-function type. For Standard Schema-compatible validators such as Zod v4, Valibot, and ArkType, replace package-specific resolvers with `schemaResolver` from `@mantine/form`.
- Replace `color` with `c` on `Text` and `Anchor`. Rename `TypographyStylesProvider` to `Typography`, remove `positionDependencies` from `Popover` and `Tooltip`, use `expanded` instead of `Collapse.in`, and use `Spoiler.defaultExpanded` instead of `initialState`.
- Account for visual default changes: `light` variant colors are now solid rather than transparent, and the default radius changed from `sm` to `md`. Use `v8CssVariablesResolver` and/or `defaultRadius: 'sm'` temporarily if retaining v8 visuals is necessary.
- Replace `useFullscreen` with `useFullscreenDocument` for the document or `useFullscreenElement` for a target ref. Use `useMousePosition` for document coordinates and `useMouse` for a target element. Rename external-target `useMutationObserver` calls to `useMutationObserverTarget`.
- Rename hook types: `UseScrollSpyReturnType` to `UseScrollSpyReturnValue`, `StateHistory` to `UseStateHistoryValue`, and `OS` to `UseOSReturnValue`.
- Replace `Grid.gutter` with `gap`; use `rowGap` and `columnGap` when needed. Remove legacy `overflow="hidden"` workarounds because Grid now uses native CSS gap instead of negative margins.
- `useLocalStorage`, `readLocalStorageValue`, `useSessionStorage`, and `readSessionStorageValue` now return `undefined` when no `defaultValue` is supplied. Handle the nullable result or provide a default. `useHeadroom` now returns `{ pinned, scrollProgress }` rather than a boolean.
- Notifications now pause all visible notification timers when any notification is hovered. Pass `pauseResetOnHover="notification"` to keep v8's per-notification behavior.

## Tiptap 2 to 3

Source: [official Tiptap 2 to 3 guide](https://mantine.dev/guides/tiptap-3-migration/).

- Update all `@tiptap/*` packages together to 3.x.
- Set `shouldRerenderOnTransaction: true` in `useEditor` so active control styling updates correctly.
- In Next.js or any SSR framework, set `immediatelyRender: false` to avoid hydration mismatches.
- Tiptap 3 `StarterKit` includes underline and link. Remove a separately added underline extension; when using Mantine's `Link`, configure `StarterKit` with `{ link: false }` before adding Mantine's extension to prevent a duplicate.
- Import `BubbleMenu` and `FloatingMenu` from `@tiptap/react/menus`, not `@tiptap/react`.

## Upgrade Process

1. Upgrade one Mantine major version at a time and keep all `@mantine/*` packages on the same major/minor release.
2. Run type checking first to find renamed props, hook signatures, and type changes; then search CSS for removed data attributes, `sx`, nested `styles`, and obsolete theme-color-scheme checks.
3. Visually test portals, overlays, dates, Grid layouts, light variants, border radii, notifications, and rich-text editing after each upgrade.
4. For a complete breaking-change inventory, consult the version's official migration guide and changelog before declaring the upgrade complete.
