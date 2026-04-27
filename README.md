# Inscription Tester 

Test your Ordinals HTML builds before spending sats. The biggest diffrence with this and other tester is that you can share your build and test with others, great for multiplayer. note: that some wallets like Xverse won't connect via iframe. This does not mean that it cannont work just thhat it wont connect via Iframe. 

This repo lets you load a build from GitHub Pages into an existing Ordinals HTML receiver, so you can quickly test your app in the `ordinals.com` content environment.

Receiver used:

```text
https://ordinals.com/content/33064f05445f5c4d97d6a70585e70cdabb0b52690e61d611afb2b4091aca614bi0
```

---

## Quick start

1. Fork this repo.
2. Add your app to the `build` folder.
3. Make sure your main file is:

```text
/build/index.html
```

4. Turn on GitHub Pages for your fork.
5. Open your GitHub Pages link.

The loader will automatically fetch your build and send it into the Ordinals receiver.

---

## Repo layout

```text
Inscription-tester/
├─ index.html          ← GitHub Pages loader. Do not replace this.
├─ .nojekyll           ← Keeps GitHub Pages paths clean.
└─ build/
   ├─ index.html       ← Replace this with your app/build.
   └─ assets/          ← Optional JS, CSS, images, etc.
```

The important part:

```text
/index.html        = the loader
/build/index.html  = your app
```

Do **not** replace the root `index.html`.

Replace this file instead:

```text
/build/index.html
```

---

## How it works

```text
1. You open the GitHub Pages site.

2. The root index.html checks for:
   /build/index.html

3. If a build exists, it loads the Ordinals receiver.

4. The loader sends your build HTML to the receiver using postMessage.

5. The receiver renders your app inside the ordinals.com environment.
```

This means you can update your build in GitHub without reinscribing a new test file every time.

---

## Simple HTML build

Put this in:

```text
/build/index.html
```

Example:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>My Ordinals Test</title>
</head>
<body>
  <h1>Hello from GitHub Pages</h1>
  <p>This is being loaded into the Ordinals receiver.</p>
</body>
</html>
```

---

## Vite / React builds

For Vite, use relative paths:

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

Then commit the output like this:

```text
/build/index.html
/build/assets/...
```

---

## Why use this?

- Test before inscribing
- Save sats
- Share a GitHub Pages link
- Check your build on different devices
- Quickly update and retest builds
- Test Ordinals paths like `/content/...` and `/r/...`

---

## Common issues

### My app does not load

Check this file exists:

```text
/build/index.html
```

### I replaced the wrong file

Do not replace:

```text
/index.html
```

Replace:

```text
/build/index.html
```

### My assets do not load

Use relative paths:

```html
<script src="./assets/app.js"></script>
<link rel="stylesheet" href="./assets/app.css" />
```

For Vite, make sure you use:

```js
base: "./"
```

---

## Notes

This is a testing tool.

For final immutable releases, inscribe your finished app directly.

Do not use this with seed phrases, private keys, wallet passwords, or sensitive wallet data.
