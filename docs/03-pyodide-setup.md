# 03 — Pyodide Setup

## What Is Pyodide

Pyodide is CPython compiled to WebAssembly. It runs a full Python interpreter in the browser — no server, no backend, no install. Students write Python and run it directly on the lesson page.

## How It's Integrated

The shortcode lives at `layouts/shortcodes/pyodide.html`. It:
1. Loads Pyodide from CDN (once per page, cached by browser after first visit)
2. Captures stdout into a buffer
3. Runs the student's code
4. Displays output below the cell in green
5. Shows errors in red

## Usage in Markdown

```
{{< pyodide id="my-cell" >}}
from collections import Counter
words = ["the", "cat", "sat"]
print(Counter(words))
{{< /pyodide >}}
```

- `id` must be **unique per page** (use descriptive names: `count-words`, `build-probs`)
- Multiple cells per page: fine — each is independent
- The code between tags is the default starter code shown to the student
- Students can edit before running

## Pyodide Version

Currently pinned to `v0.27.0`. To upgrade, update the CDN URL in `layouts/shortcodes/pyodide.html`.

## Supported Libraries

All Python standard library works out of the box: `collections`, `random`, `json`, `re`, `math`, `itertools`, etc.

To use scientific packages (numpy, pandas), add before `runPythonAsync`:
```javascript
await py.loadPackage("numpy");
```

## Performance Notes

- First page load: ~10MB download (Pyodide WASM bundle from CDN)
- Browser caches after first load — subsequent visits are instant
- Code execution: typically < 100ms for simple scripts
- Not suitable for: file I/O, network requests, heavy ML training
