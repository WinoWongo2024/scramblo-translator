# Scramblo Translator

A polished, fully client-side two-way translator for **Scramblo**, a constructed language built on deterministic English word scrambling + repeated-letter compression.

Live demo: open `index.html` in any modern browser (or host via GitHub Pages).

## Features

- **English → Scramblo** and **Scramblo → English**
- Deterministic local engine (no AI / LLM calls)
- Live translation as you type
- Inverted question marks for questions (`¿ … ?`)
- Configurable scrambling tables and compression maps
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

Words of 1–2 letters are left unchanged. Words longer than 10 letters currently fall back to unchanged (edit `SCRAMBLE_RULES` to extend).

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

## Examples

| English       | Scramblo      |
|---------------|---------------|
| Hello         | Olehl         |
| How are you?  | ¿Hwo Rae Ouy? |
| Time          | Eimt          |
| Where         | Hêwr          |
| Please        | Eplaß         |
| Food          | Dôf           |
| Computer      | Romputec      |
| Hospital      | Lospitah      |
| Ambulance     | Emuacabln     |
| Telephone     | Êehntlpo      |
| Breakfast     | Trafsbeka     |
| Weather       | Rahweet       |
| Railway       | Yiwrâl        |
| Emergency     | Ymrecêgn      |
| Friend        | Drefni        |
| Family        | Yaiflm        |

## Extending the language

All rules live at the top of the `<script>` block in `index.html`:

```js
const LANGUAGE_NAME = "Scramblo";
const SCRAMBLE_RULES = { ... };
const COMPRESS_MAP = { ... };
```

Change a single entry and the entire translator (including reverse direction and the Rules panel) updates automatically.

## Tech

- Pure HTML / CSS / vanilla JavaScript
- No build step, no dependencies
- Works offline

## License

MIT — feel free to fork and evolve Scramblo.
