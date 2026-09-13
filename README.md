# Scramblo Translator

A polished, fully client-side two-way translator for **Scramblo**, a constructed language built on deterministic English word scrambling + repeated-letter compression.

Live demo: open `index.html` in any modern browser (or host via GitHub Pages).

## Features

- **English → Scramblo** and **Scramblo → English**
- Deterministic local engine (no AI / LLM calls)
- Live translation as you type
- **History** — last 40 translations, click to restore (stored in localStorage)
- **Text-to-speech** — Speak buttons for input and output (Web Speech API)
- Inverted question marks for questions (`¿ … ?`)
- Configurable scrambling tables and compression maps
- Support for words of any length (3–10 fixed rules; 11+ generated consistently)
- Dark / light mode
- Responsive mobile-friendly UI
- Examples panel + collapsible Language Rules
- Copy, clear, and swap controls
- Character & word counts

## Language rules (summary)

### Scrambling (by word length)

| Length | Permutation (1-based) |
|--------|-----------------------|
| 3      | 1-3-2                 |
| 4      | 4-2-3-1               |
| 5      | 5-4-2-1-3             |
| 6      | 6-2-4-1-5-3           |
| 7      | 7-3-5-1-6-2-4         |
| 8      | 8-2-3-4-5-6-7-1       |
| 9      | 9-2-4-6-8-1-3-5-7     |
| 10     | 10-2-4-6-8-1-3-5-7-9  |
| 11+    | last, then remaining evens, then odds |

Words of 1–2 letters are left unchanged. Longer words (11+) use a deterministic extension that continues the spirit of the 9/10 rules.

### Repeated-letter compression (after scrambling)

| Pair | Character |
|------|-----------|
| aa   | â         |
| ee   | ê         |
| ii   | î         |
| oo   | ô         |
| uu   | û         |
| ss   | ß         |
| ll   | ł         |

Three identical letters → special + remaining letter (e.g. `eee` → `êe`).

### Capitalization & punctuation

- Only the **first character** of the final transformed word is uppercase.
- Punctuation, numbers, emojis, apostrophes and hyphens are preserved.
- Spaces and newlines are preserved; each word is processed independently.
- Questions automatically receive a leading `¿`.

## Extending the language

All rules live at the top of the `<script>` block in `index.html`:

```js
const LANGUAGE_NAME = "Scramblo";
const SCRAMBLE_RULES = { ... };  // fixed 3–10
// generateLongRule() handles 11+
const COMPRESS_MAP = { ... };
```

Change a single entry and the entire translator (including reverse direction and the Rules panel) updates automatically.

## Tech

- Pure HTML / CSS / vanilla JavaScript
- No build step, no dependencies
- Works offline
- History & theme preference stored in localStorage

## License

MIT — feel free to fork and evolve Scramblo.
