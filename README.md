# Inscription Tester

A simple demo repo for testing a **single reusable Ordinals HTML receiver**.

The important part is this:

```text
/index.html          = GitHub Pages loader. Keep this file as the loader.
/build/index.html    = Your actual app/demo/build. Replace this file with your own app.
```

So users do **not** need to reinscribe a new receiver every time they change their app. They only replace the app inside the `build` folder.

---

## How it works

```text
1. User opens GitHub Pages:
   https://switch-900.github.io/Inscription-tester/

2. /index.html loads the inscribed Ordinals receiver in an iframe.

3. /index.html fetches:
   /build/index.html

4. The loader sends that HTML to the receiver using postMessage.

5. The receiver renders the app inside the ordinals.com content environment.
```

---

## Repo layout

```text
Inscription-tester/
├─ index.html                  ← GitHub Pages loader. Do not replace with your app.
├─ receiver-to-inscribe.html   ← Receiver HTML to inscribe once.
├─ metadata.json               ← Optional inscription metadata.
├─ .nojekyll                   ← Keeps GitHub Pages static paths clean.
└─ build/
   ├─ index.html               ← Replace this with your own app/build.
   └─ assets/                  ← Optional app assets, JS, CSS, images, etc.
```

---

## Quick use

### 1. Inscribe the receiver once

Inscribe:

```text
receiver-to-inscribe.html
```

After inscription, you will get a URL like:

```text
https://ordinals.com/content/YOUR_RECEIVER_INSCRIPTION_ID
```

### 2. Add the receiver URL to the loader

Open the root loader:

```text
/index.html
```

Find:

```js
var RECEIVER_URL = "https://ordinals.com/content/YOUR_RECEIVER_INSCRIPTION_ID";
```

Replace it with your real receiver inscription URL.

### 3. Replace the app build

To change what appears inside the receiver, replace this file:

```text
/build/index.html
```

That is the only file a simple HTML demo needs to replace.

For bigger apps, replace the whole `build` folder:

```text
/build/index.html
/build/assets/...
```

### 4. Open the GitHub Pages site

```text
https://switch-900.github.io/Inscription-tester/
```

The loader will fetch `/build/index.html` and display it inside the inscribed Ordinals receiver.

---

## Simple HTML app

Put your app here:

```text
/build/index.html
```

Example:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>My Test App</title>
</head>
<body>
  <h1>Hello from the build folder</h1>
</body>
</html>
```

---

## Vite / React app

For Vite, use relative asset paths so the receiver can resolve your JS and CSS correctly.

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  base: "./",
  build: {
    outDir: "build"
  }
});
```

Then your build output should be committed like this:

```text
/build/index.html
/build/assets/index-xxxxx.js
/build/assets/index-xxxxx.css
```

---

## Common mistakes

### The loader opens but the app does not show

Check that this file exists:

```text
/build/index.html
```

If it is missing, the loader will fail with a 404.

### The wrong file was replaced

Do not replace the root `/index.html` with your app.

The root `/index.html` is the loader.

Replace this instead:

```text
/build/index.html
```

### Assets do not load

Use relative paths where possible:

```html
<script src="./assets/app.js"></script>
<link rel="stylesheet" href="./assets/app.css" />
```

For Vite, use:

```js
base: "./"
```

---

## Security note

This receiver is designed to accept HTML from HTTPS web apps and render it inside the receiver.

Do not pass seed phrases, private keys, wallet passwords, or sensitive wallet data through this system.

For final immutable releases, inscribe the completed app directly.
