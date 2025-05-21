# Brotli_UI
# Brotli UI

A **zero‑dependency browser interface** for compressing and decompressing files with [Brotli](https://github.com/google/brotli) directly in the client. Drop it onto any static host (GitHub Pages, Netlify, Vercel, S3…) and you have an instant utility without servers or build steps.

---

## ✨ Features

| Capability                   | Details                                                                                 |
| ---------------------------- | --------------------------------------------------------------------------------------- |
| 🔄 **Compress & Decompress** | Supports any file type. Produces/reads the standard `.br` format.                       |
| 🎚️ **Quality Slider 0‑11**  | Adjust Brotli’s `quality` parameter to balance speed & size.                            |
| ⚡ **Pure WebAssembly**       | Uses the official `google/brotli` C code compiled to WASM. No Node, no native binaries. |
| 📈 **Performance Log**       | Shows timing and size statistics for every operation.                                   |
| 🌓 **Dark‑mode UI**          | Tailwind CSS + custom styling that matches GitHub’s dark theme.                         |

---

## 🚀 Quick start

1. **Clone or download** this repo.
2. Open `brotli-ui.html` in your browser – that’s it!
3. For production, push the file to GitHub Pages (or any static host). No build pipeline required.

```bash
# Example: publish from the root of your repo
$ git add brotli-ui.html
$ git commit -m "Add Brotli UI"
$ git push origin main
# enable GitHub Pages → done
```

---

## 🏗️ How it works

* The page loads **`brotli-wasm`** at runtime:

  ```js
  import brotliPromise from 'https://unpkg.com/brotli-wasm@3.0.1/index.web.js?module';
  const brotli = await brotliPromise; // exposes compress() & decompress()
  ```
* `brotli-wasm` is a thin ESM wrapper around the canonical [google/brotli] source compiled to WebAssembly via Emscripten.
* File data is read into a `Uint8Array`, processed in the browser, then saved with `URL.createObjectURL`.

---

## 🛠️ Development

If you’d rather bundle the UI yourself or hack on the WASM binary:

```bash
# 1 – Clone google/brotli & build WASM
$ git clone https://github.com/google/brotli.git
$ cd brotli && ./scripts/build-wasm.sh   # requires emscripten

# 2 – Copy the generated brotli.js / brotli.wasm into ./lib

# 3 – Serve the UI locally
$ npx serve .
```

---

## 📄 License

This project is released under the **Apache 2.0** license, the same as [google/brotli]. See `LICENSE` for details.

---

## 🙏 Acknowledgements

* **Google Brotli team** – for the original compression algorithm and open‑source implementation.
* **brotli‑wasm** – for the ready‑made WASM/ESM build that makes instant browser use possible.

[google/brotli]: https://github.com/google/brotli
