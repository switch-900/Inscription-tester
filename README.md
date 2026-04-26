# Inscription Tester

A small demo repo for testing a **single reusable Ordinals HTML receiver**.

The idea:

```text
GitHub Pages repo
  └─ ordinal-launcher.html
        ↓ fetches this repo's index.html
        ↓ opens your inscribed receiver on ordinals.com
        ↓ sends the HTML with postMessage

Universal Ordinal Receiver inscription
  └─ receives HTML
  └─ injects/uses baseUrl
  └─ document.write(html)
  └─ app displays inside ordinals.com/content/...
```

## Files

- `index.html` — demo app that will be loaded into the Ordinals receiver.
- `ordinal-launcher.html` — GitHub Pages launcher. Open this in the browser, paste your receiver inscription URL, then launch.
- `receiver-to-inscribe.html` — the reusable receiver code to inscribe once.
- `.nojekyll` — keeps GitHub Pages from altering static paths.

## How to use

1. Inscribe `receiver-to-inscribe.html` once.
2. Copy the resulting URL, for example:

```text
https://ordinals.com/content/YOUR_RECEIVER_INSCRIPTION_ID
```

3. Enable GitHub Pages for this repo from `main` branch/root.
4. Open:

```text
https://switch-900.github.io/Inscription-tester/ordinal-launcher.html
```

5. Paste your receiver URL and click **Open in Ordinals Receiver**.

The final app should open and run from the `ordinals.com/content/...` receiver window, while the editable code comes from GitHub Pages.

## Vite/React note

For a Vite build, use relative assets:

```js
export default defineConfig({
  base: "./"
});
```

Then add `ordinal-launcher.html` beside the built `index.html` in `dist`.
