# Signal: the Coco design system

Status: **APPROVED by Boss 2026-09-30: all three editions (Lite, Color, Consult).**

Born from the Status Zero bake-off: 13 designs over 5 rounds, and Boss kept only the Signal family.
Boss names the editions **1. Lite · 2. Color · 3. Consult**; use these names everywhere.
Files: `layout.css` (structure), `signal.css` (core: tokens, type, components; this alone is Lite), and
`color.css` (the Color edition layer), and `consult.css` (the Consult layer, loaded after color.css).

## The philosophy in one line
**A calm page where only what is wrong speaks.** Ink on paper by default. Colour is a signal, never decoration.

## Five principles
1. **Colour means one thing, everywhere.** Blue = you are here, act, or in progress. Green = moving or done.
   Amber = needs a link (a gap). Red = stale. Nothing else gets colour. No gradients, glass, glows or emoji.
2. **Size, weight and rules carry hierarchy.** It uses heavy rules (2px under page titles, 1.5px under sections,
   1px inside), a grotesk for words and mono for machine facts (keys, counts, dates).
3. **Numbers first.** Tabular figures, units set small ("12 days"), and every count with its denominator ("1 of 2").
4. **Dense but breathable.** Rows are about 44px, titles are 40px at most, and one page shows the whole picture.
   Quick 240ms entrances; nothing bounces.
5. **Both themes are designed.** Light is warm paper (Lite) or white (Color); dark is near-black with lifted ink.
   Blue has a fill token and a text token, so every pairing stays AA.

## Three editions, one system
| | **Lite** | **Color** | **Consult** |
|---|---|---|---|
| Use for | Daily work tools, dense lists, power users, home tools | Overviews, dashboards, leadership, anything people present | Work and client-grade material: polished business-consulting feel |
| Paper | Warm #F3F2EE | White #FFFFFF | White #FFFFFF |
| Rail | Black ink column; the active item is a blue block | Light grey; the active item is a blue pill | Navy #051C2C column; the active item is an electric blue block |
| Corners | 0 | 10px controls, 14px tiles | 4px controls, 6px tiles |
| Key numbers | Ruled columns; the number takes the meaning colour | Solid tiles, coloured only when the number carries that meaning | An exhibit ramp of blues (navy, deep #0B3A7A, electric #2251FF, cyan #00A9F4); the state lives in the mark |
| Colour | Blue, green, amber, red | Blue, green, amber, red | Blues only, plus one quiet crimson #A4262C for stale |
| Primary buttons | Outlined ink, blue for the one main action | Filled blue | Filled electric blue; the rest outlined in a thin line |
Everything else is identical across editions: type, spacing, rules, marks, dark theme and motion.
Consult proves rule 2: it removes the status colours and still reads, because every state keeps its shape and word.

## Tokens (core)
- Type: Schibsted Grotesk (title 40/40 at 650 and -0.035em; section 17/22 at 700; body 14/21), Geist Mono 11-12 for labels.
- Blue: fill #1234FF / text #1234FF (dark: fill #2F4BFF, text #8FA2FF).
- Meaning colours: green #0B7A45 (fill #047857), amber #9A5200 (fill #F5B301 with dark ink), red #C42414 (fill #C8281E).
- Ink: #0B0B0B, ink-2 #3C3C37, ink-3 #5F5F58 (dark: #ECEAE4, #C1C0B9, #929089). All text pairs are AA or better.

## Rules for any agent building with Signal (anti-drift)
1. Before adding a colour, name the meaning it encodes. If it is not one of the four, use ink.
   (In Consult the blue ramp only ranks tiles and chart series; it never stands in for a state.)
2. Every state needs its word and its shape (● ◐ ○ ◇ ▲). Remove the colour and the screen must still read.
3. Build from the parts that exist: Plan ⟷ Truth row, mark, key number or tile, coverage bar, rule-headed
   section, toast, field, check, pressed filter button, rail label, skip link. A new component needs a reason in its PR.
4. Pick the edition per app; never mix rails or corner styles inside one app. Inside an app, the app's edition wins
   over this mapping (Status Zero's Monday note page is Consult).
5. Both themes are checked before any UI PR merges (light, dark, 390px phone).
6. Overview screens open with an action title: one sentence stating the takeaway with its numbers
   ("3 of 4 epics are in progress, but only 2 of 7 planned stories are moving..."), not a description of the page.

## Mapping (approved)
- **Color:** the standalone Monday note, leadership views, Coco Connect dashboards, client-facing pages.
- **Lite:** Hermes, KeyDeck, PortDeck, Coco Voice settings, internal consoles and bus and HQ tools.
- **Consult:** Status Zero (Boss, 2026-09-30), Coco Teams NG (from its restyle milestone after 2.0.0; Boss, 2026-10-01), anything for work or clients, such as decks turned into apps, client dashboards and work reporting views. No firm or client branding lives in the system itself.

## How to use it in an app
1. Fonts: npm apps `npm i @fontsource-variable/schibsted-grotesk @fontsource-variable/geist-mono`; plain HTML apps
   copy `fonts/` and load `fonts.css` first (it holds the two @font-face rules; licences are in `fonts/`).
2. Import in this order: (`fonts.css` for plain HTML) → `layout.css` → `signal.css` → (`color.css` for Color and Consult) → (`consult.css` for Consult).
3. Set `data-theme="light|dark"` on `<html>`; follow `prefers-color-scheme` on first load, and let a toggle persist the choice.
4. The class names (`.rail`, `.page-head`, `.kns`/`.kn`, `.rows`/`.row`, `.pt`, `.mark-*`, `.epic`, `.bar`, `.toast`) come from
   the reference build: the Status Zero bake-off app in `scratch/bakeoff-status0/c11-*`, `c12-*` and `c13-*`
   (Lite, Color, Consult). Copy its `ui.jsx` parts (Mark, Pair, KeyNumber, Toast) rather than re-inventing them.

