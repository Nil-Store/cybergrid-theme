# Cybergrid Theme

Reusable cyber-grid visual theme package for apps that want:

- a tactical light/dark palette
- grid-based background styling
- glass-panel and industrial-border surface language
- standardized inset surfaces, section labels, CTA shadow, and readable form fields
- a Tailwind preset that maps semantic tokens to CSS variables

This package is intentionally product-agnostic. It does not include NilStore-specific copy, routes, or business components.

## Install

```bash
npm install @nil-store/cybergrid-theme
```

For GitHub-pinned consumers, prefer an explicit commit or tag instead of a floating branch:

```json
{
  "dependencies": {
    "@nil-store/cybergrid-theme": "git+https://github.com/Nil-Store/cybergrid-theme.git#<commit-or-tag>"
  }
}
```

## Use the CSS theme

Import the stylesheet once near your app root:

```ts
import "@nil-store/cybergrid-theme/theme.css";
```

To enable dark mode, toggle a `dark` class on a parent element such as `<html>` or `<body>`.

## Minimal app wiring

Most apps need exactly three steps:

1. Import `theme.css` once at the app root.
2. Use the Tailwind preset in `tailwind.config`.
3. Render the static `cyber-grid-layer` and, if desired, `LivingGrid` in the app shell.

Example:

```tsx
import "@nil-store/cybergrid-theme/theme.css";
import { LivingGrid } from "@nil-store/cybergrid-theme/react/living-grid";

export function AppShell() {
  return (
    <div className="min-h-screen bg-background text-foreground">
      <div className="fixed inset-0 pointer-events-none z-0 overflow-hidden">
        <div className="absolute inset-0 opacity-20 dark:opacity-40 cyber-grid-layer" />
        <LivingGrid />
      </div>

      <main className="relative z-10">{/* app content */}</main>
    </div>
  );
}
```

## Use the Tailwind preset

```js
import cybergridPreset from "@nil-store/cybergrid-theme/tailwind-preset";

/** @type {import('tailwindcss').Config} */
export default {
  presets: [cybergridPreset],
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"]
};
```

## React exports

```js
import { LivingGrid } from "@nil-store/cybergrid-theme/react/living-grid";
```

`LivingGrid` is the canvas-based animated conduit effect used as a fixed background layer behind app content.

It is intentionally exported as a React component instead of being baked into CSS so apps can:

- mount it only on the routes that benefit from it
- disable it on constrained surfaces if needed
- keep the theme package as the single source of truth for the effect

## Utility classes

The package provides both generic `cg-*` classes and compatibility aliases used in existing apps.

Examples:

- `cg-glass-panel` or `glass-panel`
- `cg-industrial-border` or `industrial-border`
- `cg-industrial-border-accent` or `industrial-border-accent`
- `cg-inset` or `nil-inset`
- `cg-section-label` or `nil-section-label`
- `cg-section-title` or `nil-section-title`
- `cg-body-copy` or `nil-body-copy`
- `cg-input` or `recessed-input`
- `cg-cta-shadow` or `cta-shadow`

## Included visual system

- CSS variable tokens for background, foreground, primary, accent, success, muted, border, ring, and input
- static base page grid
- animated `cyber-grid-layer`
- glass panel surface with light blur
- industrial corner brackets in primary or accent variants
- readable inset panels and form controls

## Scope

This package is for theme and surface language. It does not ship branded assets or app-specific React components.

## What belongs here

Good candidates for this package:

- design tokens and semantic color roles
- reusable surface utilities
- background systems
- generic React primitives that are visual, not product-specific

Keep these outside the package:

- branded copy and assets
- app routing
- business/domain components
- storage/provider/wallet logic specific to one product

## Upgrading consumers

Recommended workflow:

1. Make and push the theme change in this repo.
2. Pin the consumer app to the new commit or tag.
3. reinstall dependencies
4. run the consumer app's lint/build smoke tests

For a more detailed integration checklist, see [`INTEGRATION.md`](./INTEGRATION.md).
