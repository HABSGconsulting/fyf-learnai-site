# 03 — Pyodide Setup

## What Is Pyodide

Pyodide is CPython compiled to WebAssembly. It runs a full Python interpreter in the browser — no server, no backend, no install. Students write Python and run it directly on the lesson page.

---

## Where the Shortcode Lives

The Pyodide shortcode lives in the **shared theme repo**:

```
themes/fyf-hugo-theme/layouts/shortcodes/pyodide.html
```

Do **not** edit it in `fyf-learnai-site`. Edit it in `HABSGconsulting/fyf-hugo-theme` — changes apply to all consumer sites.

---

## How It Works

1. Loads Pyodide from CDN once per page (guarded so it loads only once even with multiple cells)
2. Captures stdout into a buffer
3. Runs the student's code asynchronously
4. Displays output below the cell in green
5. Shows errors in red
6. Browser caches the Pyodide WASM bundle after first load — subsequent visits are instant

---

## Usage in Markdown

```
{{< pyodide id="my-cell" >}}
from collections import Counter
words = ["the", "cat", "sat"]
print(Counter(words))
{{< /pyodide >}}
```

- `id` must be **unique per page** (use descriptive names: `count-words`, `build-probs`)
- Multiple cells per page: fine — each is independent (no shared state between cells)
- The code between tags is the default starter code shown to the student
- Students can edit and re-run freely

---

## Controlling the Pyodide Version

The CDN version is **not** hardcoded in the shortcode. It reads from `config.yaml`:

```yaml
# config.yaml
params:
  pyodideVersion: "0.27.0"
```

To upgrade Pyodide across the entire site: change this one value in `config.yaml` and push. The shortcode file never needs to change.

Current version: **0.27.0**

---

## Supported Libraries

All Python standard library works out of the box: `collections`, `random`, `json`, `re`, `math`, `itertools`, etc.

To use scientific packages (numpy, pandas), add before `runPythonAsync` in the shortcode:
```javascript
await py.loadPackage("numpy");
```

Note: package loading adds latency. Keep lab exercises to stdlib where possible.

---

## Performance Notes

- First page load: ~10MB download (Pyodide WASM bundle from CDN)
- Browser caches after first load — subsequent visits are instant
- Code execution: typically < 100ms for simple scripts
- Not suitable for: file I/O, network requests, heavy ML training
