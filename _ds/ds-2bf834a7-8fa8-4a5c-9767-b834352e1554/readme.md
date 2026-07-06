# Taiga UI Design System

A faithful design-system recreation of **Taiga UI** — the open-source Angular component library built by **Tinkoff / T‑Bank** (taiga-family). This project reconstructs Taiga's tokens, typography, iconography and component primitives as framework-agnostic React + CSS so designers and agents can produce on-brand Taiga interfaces, mockups and prototypes.

> Taiga UI describes itself as "a fully-treeshakable Angular UI Kit consisting of multiple base libraries and several add-ons." It is one of the largest open-source design systems, used across Tinkoff/T‑Bank's fintech products.

## Source of truth

- **Figma:** "Taiga 3.0 (Community)" — attached to this project and mined directly (tokens, component dimensions, icon geometry, semantic color descriptions). The official community file exists only for Taiga **2.x / 3.x**; this system targets the **v3** token vocabulary (`--tui-base-01`, `--tui-primary`, `--tui-text-01`, status `*-fill` / `*-bg` pairs).
- **Upstream project:** `github.com/taiga-family/taiga-ui` · docs at `taiga-ui.dev`.
- Color values were verified against the Figma's measured color frequencies (primary `#526ED3`, primary-hover `#6C86E2`, ink `#1B1F3B`, info `#70B6F6`, warning `#FF8C67`, brand yellow `#FFDD2D`).

The Figma file carries **no Figma Variables / text styles** (colors live as Figma color *styles*), so tokens here were authored from Taiga's documented v3 default theme and cross-checked against the file — not auto-extracted. Icons **were** extracted directly from the file as real path geometry.

---

## CONTENT FUNDAMENTALS

How Taiga writes copy (observed in the file's color/type guides and upstream docs):

- **Voice:** plain, technical, understated. Documentation-grade clarity over marketing flourish. Example from the file: *"Each color has a purpose in Taiga UI. Check out color description to know what you customize."*
- **Person:** addresses the developer directly as **"you"** ("You can change font family…", "to know what you customize"). First-person plural ("we") only when describing the library's own choices ("On mobile devices we use system font by default").
- **Casing:** **Sentence case** everywhere — labels, buttons, headings, menu items. Not Title Case. Tokens and component names are lowercase-hyphenated (`primary-hover`, `tui-button`).
- **Tone:** instructive and matter-of-fact; tells you the *purpose* of a thing ("Background of buttons, marker icons"), not its mood.
- **Microcopy:** short, imperative button labels ("Choose a file or drag & drop it here"), terse helper text. No exclamation marks, no hype.
- **Emoji:** not used in product UI. (Upstream README uses a few section emoji, but the interface itself never does.) **Do not** use emoji in Taiga interfaces.
- **Numbers / data:** financial framing is common (income vs. expense, "stock price grow/fall") — Taiga's heritage is fintech, so positive/negative value coloring is a first-class concern.

---

## VISUAL FOUNDATIONS

**Overall vibe.** Calm, neutral, content-first. A near-white canvas, navy ink, one confident blue for action, and the unmistakable Tinkoff **yellow** reserved as a brand accent. Generous radii and soft, low-contrast shadows give a friendly-but-serious fintech feel.

**Color.**
- Surfaces ride a 9-step greyscale (`base-01` white → `base-09` near-black) used for page/tile/border/hover layers.
- A single **primary blue `#526ED3`** carries almost all interaction (buttons, links, focus rings, selection). `*-hover` lightens, `*-active` darkens.
- **Accent = brand yellow `#FFDD2D`** on ink text — used sparingly for brand moments and highlight CTAs, never as body or status color.
- Text is **navy ink `#1B1F3B`** (not pure black), with `text-02` grey for secondary and `text-03` for hints/placeholders.
- Status is expressed as **fill + tinted-background pairs**: success (teal-green), error (`#F45725` orange-red), info (`#70B6F6` blue), warning (`#FF8C67` salmon), neutral (grey). Backgrounds are ~12% alpha of the fill.
- Positive/negative value colors exist independently for finance (green / orange-red).
- A full **dark theme** is provided under `[data-tui-theme="dark"]`.

**Type.** **Manrope** (free, Google Fonts) is the documented Taiga face. Headings use **ExtraBold 800** (h1–h2) / **Bold 700** (h3–h6) with slight negative tracking on display sizes; body uses **Medium 500**, bold variants at 700. On mobile, Taiga falls back to the system font. The component text scale clusters at 13 / 15 / 17 px. Mono is the system monospace.

**Spacing & layout.** 4px base grid. Control heights are fixed by size: **XS 24 · S 32 · M 44 · L 56**. Inputs and buttons share these heights so forms align. Layouts favor roomy padding and clear separation over density.

**Radii.** Soft and size-proportional: `xs 4 · s 8 · m 12 · l 16 · xl 24`. Buttons round more at larger sizes (M = 12, L = 16). Cards/islands use `l` (16). Avatars/markers are circles or ~28%-rounded squares. Pills use a `round` radius.

**Cards / "islands".** Taiga calls surfaces *islands*. Three elevations: **flat** (base-02 fill, no border), **outlined** (white + 1px `base-04` hairline — the default), **raised** (white + soft shadow). Corners `l`. No colored left-border accents.

**Shadows.** Low-contrast, cool, layered: `small` (subtle lift) → `medium` (cards) → `large` / `dropdown` (popovers, with a 1px hairline ring) → `modal` (deep). Built from black at 8–24% alpha. No glow, no colored shadows.

**Borders.** Hairline `1px` in `base-04` (or `base-border` alpha) for tiles, tables, inputs-at-rest. Inputs show a **filled secondary background** by default and reveal a **primary-blue 1px border on focus** (error → error-fill border).

**Backgrounds.** Predominantly solid `base-01` / `base-02`. **No gradients** in product chrome, no decorative imagery, no patterns. Imagery (when present) sits inside avatars/cards. Avoid bluish-purple gradients entirely — not part of this brand.

**Motion.** Quick and crisp. `--tui-duration-fast 150ms` for color/state, `--tui-duration 300ms` for progress/layout, eased with a standard in-out curve. Hover changes background/color; **press deepens color** (active token) — no bounces, minimal scale. Spinners rotate at ~0.7s linear. Respect reduced-motion.

**Hover / press states.** Hover → `*-hover` token (lighter for primary/accent, tinted fill for ghost/secondary). Press/active → `*-active` (darker). Links shift `link → link-hover`. Disabled → **opacity 0.56** (measured from the file) + `not-allowed`.

**Transparency & blur.** Used for scrims (modal backdrop ≈ ink/75%) and the loader overlay (white/72% + 1px blur). `secondary` and `clear` tokens are alpha-based so controls tint correctly over any surface.

**Iconography color.** Icons inherit `currentColor` — grey (`text-02`/`text-03`) at rest, primary when active/interactive, status-fill inside markers and notifications.

---

## ICONOGRAPHY

- Taiga ships its **own icon set** (`tuiIcon*`). This project extracted **191 glyphs** straight from the Figma as real SVG path data — **not redrawn**. They live in `assets/icons/icon-data.js` and render through `assets/icons/Icon.jsx`.
- Icons come in **16px** and **24px** masters with a consistent ~1.5–2px optical stroke; many are outline style with rounded joins, some filled (`*-circle`, status). 16px is the UI default; 24px (the `…Large24` masters) for larger controls.
- **Single-color, `currentColor`-driven** — recolor with the CSS `color` property; never hard-code icon fills.
- Friendly aliases: `<Icon name="chevron-down" />`, `<Icon name="search" />`, `<Icon name="trash" />` resolve to the verbose export names (prefixes/sizes stripped, 16px wins ties). Full export names (`PxTuiIconChevronDown16`) also work. See `assets/icons/Icon.d.ts` for the full name index.
- **No emoji, no Unicode glyph hacks.** If a needed icon is missing, substitute the closest Taiga glyph rather than introducing a foreign icon family.

---

## INDEX / MANIFEST

Root files
- `styles.css` — global entry point (imports only). Link this one file.
- `tokens/` — `colors.css` (light + dark), `typography.css`, `spacing.css` (spacing/radius/shadow/motion), `fonts.css` (Manrope via Google Fonts), `base.css` (resets + type helper classes).
- `assets/icons/` — `icon-data.js` (191 glyphs), `Icon.jsx` / `Icon.d.ts`, `icons.card.html`.
- `foundations/` — specimen cards: Colors (primary, base, status, text), Type (headings, body), Spacing (scale, radius/shadow), Brand.
- `readme.md` (this file) · `SKILL.md` (Agent-Skill manifest).

Components (`components/<group>/`) — React primitives, each `<Name>.jsx` + `.d.ts` (+ card per group). Mount via `window.TaigaUIDesignSystem_2bf834.<Name>`.
- **buttons/** — Button, ButtonSplit, Link, Action
- **badges/** — Badge, BadgeNotification, Tag, Tags, MarkerIcon
- **forms/** — Input, Textarea, InputSearch, InputTag, InputNumber, InputFiles, File, Select, Checkbox, CheckboxBlock, Radio, RadioBlock, Toggle, Slider, RangeSlider, PinInput, Rating
- **navigation/** — Tabs (+ vertical), Filter, Segmented, Stepper (+ vertical), Pagination, Breadcrumbs, Accordion, AccordionItem, List, ListItem, Dropdown, DropdownItem
- **feedback/** — Notification, Push, Tooltip, Hint, Dialog, Loader, ProgressBar, ProgressCircle
- **surfaces/** — Card, Scrollbar
- **data/** — Avatar, AvatarStack, Calendar, Table, ChartRing, ChartArc, Carousel
- **assets/icons/** — Icon

UI kits (`ui_kits/<product>/`) — full-screen interactive recreations composing the primitives above.

---

## Caveats

- Tokens are authored from Taiga v3's documented default theme (the Figma has no Variables), then cross-checked against the file's color data. The warm reds/oranges (negative/error) and middle greys are matched closely but may differ by a few percent from a specific Taiga release.
- **Manrope** is loaded from Google Fonts rather than shipped as local `.woff2` — swap in self-hosted binaries for production.
- Components are pixel-accurate *cosmetic* recreations, not the Angular originals; behavior is simplified.
