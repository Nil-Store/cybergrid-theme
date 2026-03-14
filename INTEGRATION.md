# Cybergrid Theme Integration Guide

This guide is for future agents and maintainers integrating `@nil-store/cybergrid-theme` into another repo.

## Integration contract

The package is responsible for:

- visual tokens
- Tailwind preset mapping
- shared surface/background utilities
- generic visual React exports like `LivingGrid`

The consuming app remains responsible for:

- product-specific routes and copy
- branded assets
- wallet/storage/provider/business logic
- where and when the visual primitives are mounted

## Recommended setup

### 1. Add the dependency

Prefer a tag or commit pin:

```json
{
  "dependencies": {
    "@nil-store/cybergrid-theme": "git+https://github.com/Nil-Store/cybergrid-theme.git#<commit-or-tag>"
  }
}
```

This keeps installs reproducible and makes visual changes traceable.

### 2. Import the shared CSS once

In the app entrypoint:

```ts
import "@nil-store/cybergrid-theme/theme.css";
```

Import it before app-local CSS so local app overrides can stay intentional.

### 3. Use the Tailwind preset

```js
import cybergridPreset from "@nil-store/cybergrid-theme/tailwind-preset";

export default {
  darkMode: "class",
  presets: [cybergridPreset],
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"]
};
```

Keep `darkMode: "class"` explicit in the consumer.

### 4. Mount the background in the layout shell

The usual pattern is:

```tsx
import { LivingGrid } from "@nil-store/cybergrid-theme/react/living-grid";

function Layout() {
  return (
    <div className="min-h-screen bg-background text-foreground">
      <div className="fixed inset-0 pointer-events-none z-0 overflow-hidden">
        <div className="absolute inset-0 opacity-20 dark:opacity-40 cyber-grid-layer" />
        <LivingGrid />
      </div>

      <main className="relative z-10">{/* app UI */}</main>
    </div>
  );
}
```

The static `cyber-grid-layer` provides the grid language. `LivingGrid` is optional and should remain route- or app-controlled.

## Upgrade workflow

When the theme changes:

1. Commit and push the theme repo first.
2. Update the consumer dependency pin.
3. Reinstall dependencies.
4. Run the consumer build/lint smoke tests.
5. Remove any duplicated local implementation that the package now owns.

## Recommended policy for consumers

- Do not fork package utilities locally unless the consumer truly needs app-specific behavior.
- If a generic visual primitive becomes reused in multiple apps, move it here.
- If a component is business/domain specific, keep it in the app.

## Good extraction candidates

- generic buttons/cards/pills
- modal shell
- nav chrome primitives
- background effects
- surface utilities and semantic tokens

## Bad extraction candidates

- dashboard business logic
- provider onboarding flows
- deal explorers
- product-specific docs/copy
- product logos/wordmarks

## Notes on TypeScript

If a React export is shipped from this package, also ship a `.d.ts` file through the package `exports` map. Consumers should not need local `declare module` shims.
