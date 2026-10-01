# Coco Design Language

Signal: a calm interface where only what is wrong speaks.

## What it is

Signal is a CSS design system for application screens.
`layout.css` is the structure. `signal.css` is the tokens, type, and components, and on its own it is the Lite edition.
`color.css` and `consult.css` are optional layers for the Color and Consult editions.

## The philosophy

1. Colour means one thing, everywhere. Blue means you are here, act, or in progress. Green means moving or done. Amber means a gap that needs a link. Red means stale. Nothing else is coloured. No gradients, glass, glows, or emoji.
2. Size, weight, and rules carry hierarchy. A grotesk is for words. Mono is for keys, counts, and dates.
3. Numbers come first. Figures are tabular. Units stay small. Every count shows its denominator.
4. Dense, with room to read. Rows sit near 44px. Titles stay at 40px or under. Entrances last 240ms. Nothing bounces.
5. Both themes are designed. Light is warm paper in Lite and white in Color and Consult. Dark is near-black with lifted ink. Blue keeps a separate fill and a separate text colour so the pairs stay AA.

## Three editions

| Edition | When to use |
| --- | --- |
| Lite | Daily work tools, dense lists, and power users |
| Color | Overviews, dashboards, and anything people present |
| Consult | Polished business material: white paper, a navy rail, and one blue ramp |

## Quick start

Link the files in `signal/` in this order.

```html
<link rel="stylesheet" href="signal/fonts.css">
<link rel="stylesheet" href="signal/layout.css">
<link rel="stylesheet" href="signal/signal.css">
<link rel="stylesheet" href="signal/color.css">
<link rel="stylesheet" href="signal/consult.css">
```

Stop after `signal.css` for Lite. Add `color.css` for Color. Add `consult.css` for Consult, and only after `color.css`. `fonts.css` loads `signal/fonts/` with a URL relative to itself, so keep that file next to the `fonts/` folder.

Light and dark follow one attribute. Light tokens are on `:root`. In `signal.css` that block sets `color-scheme: light`. Dark tokens are in `[data-theme="dark"]`, which is in `signal.css`, `color.css`, and `consult.css`. In `signal.css` that block sets `color-scheme: dark`. Put `data-theme="dark"` on the `html` element for the dark palette. Omit the attribute for light. No other value is styled, and no media query changes the theme.

## Tokens

| Meaning | Use | Text | Fill | Dark |
| --- | --- | --- | --- | --- |
| Blue | You are here, act, or in progress | #1234FF | #1234FF | Fill #2F4BFF, text #8FA2FF |
| Green | Moving or done | #0B7A45 | #047857 | |
| Amber | Needs a link (a gap) | #9A5200 | #F5B301, with dark ink on the fill | |
| Red | Stale | #C42414 | #C8281E | |

Ink is the default text, with no meaning colour: #0B0B0B, #3C3C37, and #5F5F58. Dark ink is #ECEAE4, #C1C0B9, and #929089. The core list gives dark hexes for blue and for ink. Green, amber, and red also change inside `[data-theme="dark"]` in `signal.css`.

Consult does not use green or amber for state. On `:root` in `consult.css`, stale is crimson #A4262C (`--red` and `--red-fill`). The light tile ramp is navy #051C2C, deep #0B3A7A, electric #2251FF, and cyan #00A9F4 (`--navy`, `--deep`, `--electric`, `--cyan`). That ramp ranks tiles. It does not stand in for a state.

## Accessibility

AA. `signal.css` splits blue into `--blue` (fill) and `--blue-text` (text) in both themes so those pairs stay AA. Green, amber, and red use the same split: `--green` and `--green-fill`, `--amber` and `--amber-fill`, `--red` and `--red-fill`.

Focus. `:focus` sets `outline: none`. `:focus-visible` sets `outline: 2px solid transparent` and `box-shadow: var(--focus)`. In `signal.css`, `--focus` is `0 0 0 2px var(--bg), 0 0 0 4px var(--blue)`. Consult sets `--focus` to `0 0 0 2px var(--bg), 0 0 0 4px var(--electric)`. `.page-head h1:focus` and `.page-head h1:focus-visible` set `box-shadow: none`. `.person:focus-visible` uses `box-shadow: inset 0 0 0 2px var(--accent)`. `.person[aria-current="true"]:focus-visible` uses `--blue` in `signal.css` and `--electric` in `consult.css`. `.skip:focus` applies `var(--focus)`.

Targets. `layout.css` gives `.row` and `.toast` `min-height: 44px` at every width. Above 799px, `.btn` stays `min-height: 32px` and `.icon-btn` stays 34px by 34px. Inside `@media (max-width: 799px)` in `signal.css`, `.btn`, `.row-actions .btn`, `.nav-item`, `.nav-off .nav-item`, `.field`, and `label.check` become `min-height: 44px`, and `.icon-btn` becomes 44px by 44px.

Motion. `@media (prefers-reduced-motion: reduce)` in `signal.css` sets `transition-duration` and `animation-duration` to `0.01ms`, and `animation-delay` to `0ms`, on `*`, `*::before`, and `*::after`.

## Fonts

Words use Schibsted Grotesk. Machine facts use Geist Mono. `fonts.css` registers the families `Schibsted Grotesk Variable` and `Geist Mono Variable`. `signal.css` applies them through `--font` and `--mono`. Both files are Latin subsets under `signal/fonts/`, licensed under the SIL Open Font License, Version 1.1. The licence texts are `signal/fonts/OFL-schibsted-grotesk.txt` and `signal/fonts/OFL-geist-mono.txt`.

## License

CSS and these docs are MIT. See `LICENSE`. The font files stay under the SIL Open Font License, Version 1.1. The MIT grant does not replace the font licence.
