# felizhappyeCard
Multi-lingual HTML e-card generator (birthdays/holidays) - option to include gift card

Self-contained browser app for creating personalised birthday and holiday e-cards â complete with multilingual wishes, custom images, embedded gift cards, and animated confetti. No server, no dependencies, no installation. Just open the HTML file and send.

> **Conceived and designed by [@teowaits](https://github.com/teowaits) Â· Vibe coded with [Claude Sonnet 4.6](https://www.anthropic.com/claude) by Anthropic**

---

## What It Does

The studio generates a fully **self-contained `.html` e-card file** that recipients can open in any browser with no internet connection required after generation, no apps to install.

### Card Features
- **Birthday** or **Holiday** mode - red banner with coloured confetti for birthdays; deep green banner with falling snowflakes for holidays
- **29 languages** for multilingual wish strips (up to 6 selectable), with a filter search box
- **Custom image** embedded directly in the card
- **Gift card support** - provider name, value, and a full PDF rendered page-by-page inside the card using PDF.js (no white-page iframe issues)
- Animated confetti (birthday) or âsnowflakes (holidays) on open

### Builder Features
- Live **side-by-side preview** â updates instantly as you type or click
- Language filter/search across 29 languages
- One-click **Generate Card** â downloads a ready-to-send `.html` file
- Zero server required â entirely client-side

---

## Getting Started

### Use It Right Now

Download [`ecard_builder.html`](./ecard_builder.html) and open it in any modern browser (Chrome, Firefox, Safari, Edge). That's it.

```bash
git clone https://github.com/teowaits/felizhappyeCard.git
cd felizhappyeCard
open ecard_builder.html   # macOS
# or just double-click the file in Finder / Explorer
```

No `npm install`. No build step. No server.

---

## Project Structure

```
felizhappyeCard/
ecard_builder.html    # The entire app â one self-contained file
README.md             # This file
```

The entire application - UI, logic, card generator, PDF renderer integration, and all styles - lives in a single HTML file. This is intentional: the app is designed to be trivially shareable and forkable without any toolchain.

---

## How It Works

### The Builder (`ecard_builder.html`)

A two-panel layout built with vanilla HTML, CSS, and JavaScript:

| Left Panel | Right Panel |
|---|---|
| Form with all card options | Live card preview |

When you click **Generate Card**, `buildCardHTML()` assembles a complete standalone HTML document using string concatenation (deliberately avoiding template literals, which caused browser parser conflicts with embedded `<script>` tags). The output is downloaded as a `.html` file.

### The Generated Card

Each generated card is a **single self-contained `.html` file** containing:
- All CSS and JS inline
- The uploaded image as a base64 data URI
- The gift card PDF as a base64 string, decoded and rendered at runtime using [PDF.js](https://mozilla.github.io/pdf.js/) (loaded from CDN)
- Confetti or snowflake animations via pure CSS + JS

### Languages

Languages are defined in the `ALL_LANGS` array in the builder. Each entry has:

```js
{ code: 'it', flag: 'ð®ð¹', label: 'Italian', birthday: 'Buon Compleanno', holidays: 'Buone Feste' }
```

Adding a new language is a one-liner addition to that array.

---

## Contributing

Contributions are very welcome! This is a personal family project that grew into something more â if you find it useful or want to improve it, please go ahead.

### Ways to Contribute

- **Add more languages** â edit the `ALL_LANGS` array in `ecard_builder.html`
- **New occasion types** â e.g. Valentine's Day, graduation, new baby (extend `COPY` and `setOccasion`)
- **New themes / colour schemes** â the CSS variables make this straightforward
- **Custom font options** â currently uses Playfair Display + Dancing Script from Google Fonts
- **Bug fixes** â especially cross-browser compatibility
- **Accessibility improvements** â keyboard navigation, ARIA labels

### How to Submit Changes

1. Fork the repo
2. Create a branch: `git checkout -b feature/your-feature-name`
3. Make your changes to `ecard_builder.html`
4. Test by opening the file in at least two browsers
5. Test that **Generate Card** produces a working output `.html` file
6. Open a Pull Request with a clear description of what you changed and why

### Key Technical Notes for Contributors

- **No build toolchain** â everything is plain HTML/CSS/JS. No bundler, no transpiler.
- **Avoid template literals in `buildCardHTML()`** â the function generates HTML as a string that will be injected into a `<script>` context. Nested backtick template literals and literal `<script>` / `</script>` strings inside JS string values cause browser HTML parser failures. Use string concatenation (`+`) exclusively in that function.
- **Escape `<script>` inside JS strings** â if you need to emit a `<script>` tag from JS, write it as `'\\x3cscript'` to prevent the browser's HTML scanner from misinterpreting it.
- **File inputs must be outside their clickable zones** â placing `<input type="file">` inside a clickable `<div>` causes a double file dialog (the input fires natively, then the div's `onclick` fires it again programmatically). Always keep file inputs hidden and outside the zone, triggered via `.click()` only.
- **PDF rendering** uses [PDF.js 3.11.174](https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js) from cdnjs. The generated card loads it from CDN, so recipients need an internet connection to view embedded PDFs.

---

## Authorship & Transparency

This project was **conceived, designed, and directed by [@teowaits](https://github.com/teowaits)**. The idea, UX structure, feature set, aesthetic direction, and all design decisions are his.

The code was **vibe coded with [Claude Sonnet 4.6](https://www.anthropic.com/claude)** by Anthropic â an AI assistant that iteratively implemented, debugged, and refined the application through a conversational design session. All bugs were identified and diagnosed collaboratively, with fixes reviewed before being applied.

---

## License

MIT License - feel free to fork, adapt, and build on this for your own family, friends, or projects. A credit back to [@teowaits](https://github.com/teowaits) is appreciated but not required.

---

## The Family

The Cavalleri-Cortes family sends cards from Brooklyn, New York.



