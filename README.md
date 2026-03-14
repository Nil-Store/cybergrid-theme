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

## Use the CSS theme

Import the stylesheet once near your app root:

```ts
import "@nil-store/cybergrid-theme/theme.css";
```

To enable dark mode, toggle a `dark` class on a parent element such as `<html>` or `<body>`.

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
