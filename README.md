# Tempora — Temperature Converter

**Simple • Accurate • Fast**
*Convert temperature instantly.*
A polished, futuristic temperature converter web app built for the **OIBSIP Web Development &
Designing internship**.

---

## 1. Project Name

**Tempora — Temperature Converter**
Dark premium single-page app that converts Celsius, Fahrenheit and Kelvin simultaneously, with
glassmorphism UI, gradient accents and full validation.

## 2. Objective

Build a complete, production-quality utility application that demonstrates:

- Semantic HTML5 structure (`header`, `nav`, `main`, `section`, `article`, `footer`, `form`, `fieldset`-style grouping)
- Modern CSS3: custom properties, Flexbox **and** CSS Grid, glassmorphism, ambient glow, rounded
  cards, focus glows, hover micro-interactions, media queries
- Vanilla-style JavaScript logic: correct bidirectional conversion maths, number formatting,
  three-layer input validation, dynamic status messaging, clipboard copy and reset behaviour
- Responsive layout across desktop, laptop, tablet and mobile with **no horizontal scrolling**,
  **no text overflow** and **no overlapping elements**
- Accessibility: visible labels, clear button text, `aria-live` status regions, `aria-invalid`
  + `aria-describedby` on the input, visible focus states, readable contrast, reduced-motion support

The result should feel like a real product, not a college assignment.

## 3. Technologies Used

| Technology | Usage |
| --- | --- |
| HTML5 | Semantic landmarks, labelled form controls, accessible result cards |
| CSS3 | Grid + Flexbox layout, custom properties, gradients, `backdrop-filter` glass, ambient blobs, hover/focus effects, media queries |
| Vanilla JavaScript | Conversion engine, validation rules, status logic, quick-try actions, clipboard copy, reset (no libraries, no `eval()`) |
| Google Fonts | **Space Grotesk** (headings, values, buttons) + **Inter** (body) |
| React 19 + Vite | Component organisation and bundling for the delivered single-file build |
| TypeScript | Typed units, validation results and formula helpers |

No external APIs, no backend, no framework-specific UI kit. Every icon and the thermometer artwork
are inline SVG, so nothing can break or 404.

## 4. Features

1. **Compact sticky header** — Tempora wordmark with thermometer mark, subtitle, section links and a
   live status badge that changes between **Ready → Converted → Check input**.
2. **Hero intro** — "SMART TEMPERATURE TOOL" eyebrow, headline *Convert Temperature Without the
   Guesswork.*, supporting line and an abstract SVG thermometer with a blurred gradient halo.
3. **Converter card** — glass panel with the *Enter Temperature* input, *Input Unit* dropdown, a
   large **Convert Temperature** button, a secondary **Reset** button, and helper hints such as the
   lowest valid value for the selected unit.
4. **Three result cards** — Celsius, Fahrenheit and Kelvin shown simultaneously, each with unit name,
   large converted value, unit symbol, the formula used with the current numbers substituted, and a
   **Copy** button. The card matching the input unit is highlighted with a ring and an "Input unit"
   tag — the other two stay fully visible.
5. **Temperature status** — contextual description after each valid conversion (Cold / Cool /
   Comfortable / Warm / Very hot) with the matching range shown underneath.
6. **Quick Try buttons** — `0°C`, `25°C`, `37°C`, `100°C` fill the input (selecting Celsius) and
   convert immediately.
7. **How it works** — the three reference formulas plus notes on absolute-zero limits, validation and
   rounding.
8. **About Tempora** — three concise cards: accurate by default, instant and clear, built for everyone.
9. **Footer** — Tempora mark, "Simple • Accurate • Fast", navigation links (Converter, How It Works,
   About), supported-unit links, placeholder social/contact links, and the copyright line.

## 5. Supported Temperature Units

| Unit | Symbol | Lowest accepted value |
| --- | --- | --- |
| Celsius | °C | −273.15 °C |
| Fahrenheit | °F | −459.67 °F |
| Kelvin | K | 0 K |

## 6. Conversion Formulas

```
Celsius → Fahrenheit   °F = (°C × 9/5) + 32
Fahrenheit → Celsius   °C = (°F − 32) × 5/9
Celsius → Kelvin       K  = °C + 273.15
Fahrenheit → Kelvin    K  = (°F − 32) × 5/9 + 273.15
Kelvin → Celsius       °C = K − 273.15
Kelvin → Fahrenheit    °F = (K − 273.15) × 9/5 + 32
```

Internally every input is normalised to Celsius first, then all three readings are derived from that
single source value — so the displayed Celsius, Fahrenheit and Kelvin values always agree.

## 7. Number Formatting

Results are formatted with `Intl.NumberFormat` using **minimum and maximum 2 decimal places**, so
values stay readable and consistent:

| Input | Celsius | Fahrenheit | Kelvin |
| --- | --- | --- | --- |
| 25 (°C) | `25.00 °C` | `77.00 °F` | `298.15 K` |
| 37 (°C) | `37.00 °C` | `98.60 °F` | `310.15 K` |
| 100 (°C) | `100.00 °C` | `212.00 °F` | `373.15 K` |
| 0 (°C) | `0.00 °C` | `32.00 °F` | `273.15 K` |
| 32 (°F) | `0.00 °C` | `32.00 °F` | `273.15 K` |
| 300 (K) | `26.85 °C` | `80.33 °F` | `300.00 K` |

## 8. Validation Rules

Validation runs in this order on every **Convert** click:

| Case | Condition | Message shown |
| --- | --- | --- |
| 1 | Input is empty or only whitespace | “Please enter a temperature.” |
| 2 | Input is not a valid number (letters, symbols, multiple decimals, `Infinity`) | “Please enter a valid numeric temperature.” |
| 3 | Value below absolute zero for the selected unit | “Temperature cannot be below absolute zero. The lowest possible value in *unit* is *value*.” |

Behaviour on error: the input is marked `aria-invalid`, a `role="alert"` message appears directly
under the field, the results are cleared instead of showing misleading values, the header badge
switches to **Check input**, and the app never crashes or logs errors to the visitor. Typing again
clears the error immediately.

## 9. How To Run The Project

```bash
# 1. install dependencies
npm install

# 2. start the development server
npm run dev
# open the printed URL (e.g. http://localhost:5173)

# 3. production build (single self-contained dist/index.html)
npm run build
npm run preview
```

The page opens straight into the working converter — there is no code viewer, documentation page,
console output or technical explanation on the site.

## 10. Project File Structure

```
OIBSIP/
└── WebDev-L1-TemperatureConverter/
    ├── index.html        → app shell: meta, Google Fonts, favicon      = /index.html
    ├── style.css         → full design system + media queries          = /src/styles/tempera.css
    ├── script.js         → conversion engine, validation, status logic = /src/scripts/temperature.ts
    ├── README.md         → this file
    ├── screenshots/      → desktop, tablet and mobile captures
    └── src/
        ├── App.tsx       → page composition + app state
        └── components/
            ├── Header.tsx        → sticky header + live status badge
            ├── Intro.tsx         → hero intro + thermometer visual
            ├── Converter.tsx     → input, unit selector, results, quick try, reset
            ├── Formulas.tsx      → "How it works" formulas and notes
            ├── AboutTempora.tsx  → about section
            ├── TpFooter.tsx      → footer with links & placeholders
            └── Icons.tsx         → inline SVG icon set + thermometer artwork
```

For a plain static submission: run `npm run build` and copy the generated `dist/index.html` to
`WebDev-L1-TemperatureConverter/index.html`; keep `src/styles/tempera.css` as the reference
`style.css` and `src/scripts/temperature.ts` as the reference `script.js`.

## 11. Responsive Design

| Breakpoint | Adjustments |
| --- | --- |
| ≤ 1040px | Converter card padding tightens |
| ≤ 900px | Header links hide (badge remains), input/unit stack into one column, results become 2 columns, footer becomes 2 columns |
| ≤ 640px | Smaller type scale, single-column results, full-width Convert/Reset buttons, Quick Try chips become a 2×2 grid, footer stacks vertically |
| ≤ 380px | Compact brand and badge, Quick Try chips go full width |

Guaranteed everywhere: `overflow-x: hidden` on the body, fixed ambient blobs clipped inside their
own layer, percentage-based visuals, `overflow-wrap: anywhere` on result values and formulas, and
tap-friendly control sizes — so there is no horizontal scrolling, clipping or overlap.

## 12. OIBSIP Internship Task Information

- **Programme:** Oasis Infobyte — Web Development & Designing Internship (OIBSIP)
- **Task:** Level 1, Task 3 — Temperature Converter
- **Deliverables:** working web app (HTML5 + CSS3 + vanilla JavaScript), README documentation,
  screenshots
- **Design brief:** dark navy/black base, blue + cyan + violet gradient accents, glassmorphism, soft
  ambient glow, rounded cards, large readable temperature values, clean typography, subtle animation

## 13. Final Testing Checklist

- [x] Celsius input converts correctly (25 °C → 25.00 °C / 77.00 °F / 298.15 K)
- [x] Fahrenheit input converts correctly (32 °F → 0.00 °C / 32.00 °F / 273.15 K)
- [x] Kelvin input converts correctly (300 K → 26.85 °C / 80.33 °F / 300.00 K)
- [x] Convert button triggers conversion; all three outputs update together
- [x] Reset clears input, restores Celsius, clears results and errors, badge returns to Ready
- [x] Quick Try buttons (0, 25, 37, 100 °C) fill and convert instantly
- [x] Temperature status reacts to the Celsius reading (Cold / Cool / Comfortable / Warm / Very hot)
- [x] Empty input, non-numeric input and absolute-zero violations each show the correct message
- [x] Decimal values accepted (e.g. 37.5, -4.25) and results rounded to 2 decimals
- [x] Responsive at desktop, laptop, tablet and mobile widths
- [x] No horizontal scrolling, no overlapping elements, no broken images
- [x] No visible source code, no debug output, no external API or backend
- [x] Semantic HTML5, labelled controls, ARIA live regions, visible focus states
