# aim-style-marp-template

The Marp slide theme for AIM Robotics — a monochrome fork of
[CompPsyUnion/cpu-style-marp-template](https://github.com/CompPsyUnion/cpu-style-marp-template),
recolored from CPU yellow to pure black & white to match the AIM wordmark.

To make slides, read [docs/usage.md](docs/usage.md).

## Repository layout

```bash
tree -a --dirsfirst -I .git
.
├── .agents
│   └── skills
│       └── aim-marp
│           └── SKILL.md             # agent skill body, cross-agent location
├── .claude
│   └── skills -> ../.agents/skills  # symlink so Claude Code picks it up in-repo
├── .vscode
│   └── settings.json                # Marp theme registration
├── assets
│   ├── logo.png                     # white wordmark, for dark backgrounds
│   ├── logo-dark.png                # black wordmark, for light backgrounds
│   └── poster.png                   # placeholder poster for the side-image demo
├── docs
│   └── usage.md                     # usage guide
├── themes
│   └── aim.css                      # the theme — all styles live in this one file
├── .editorconfig                    # documentation standards
├── .markdownlint.json               # (paired with the line above)
├── README.md
└── template.md                      # sample deck, one page per slide type
```

## How the theme is organized

`themes/aim.css` is a standalone Marpit theme (first line `/* @theme aim */`), in four layers from top to bottom:

1. `:root` variables. Colors and fonts are defined here and nowhere else;
2. Base layer. Canvas size, guide lines, page numbers, plus default styles for paragraphs and inline elements. A standalone theme has no Marp default theme to fall back on, so all of this has to be written out;
3. Shared elements. Things every page runs into: the `h2` title (ink, dashed underline, an `AIM` glyph hanging in the top-right corner), `h3` ink tags, square list markers, tables;
4. Page classes. Layout rules under `section.<class>`, one class per slide type.

## Differences from the CPU theme

- **Recolored to monochrome.** Every yellow became ink or gray: tags, list markers and table heads are solid ink; nested markers and agenda numbers are gray; zebra rows are `#f2f2f2`;
- **The section divider class is `ink`** (was `yellow`): black page, white outlined word top-right, an outlined number, a solid white headline and a gray credit line — the number is outlined so it stays distinct from the headline without a second color;
- **The cover carries the logo.** The default band top-right shows "AIM Robotics" as display text; a scoped style on the slide swaps it for the white wordmark from `assets/logo.png` (see docs/usage.md). Layout logic is unchanged from CPU;
- Fonts, canvas, page classes and the flex/tag-block mechanics are identical to the upstream theme.

## Design tokens

| Variable | Value | Used for |
| --- | --- | --- |
| `--ink` | `#111111` | Brand ink: banner, tags, list markers, table heads, divider pages, mega words |
| `--ink-soft` | `#444444` | Inline code text |
| `--gray` | `#8c8c8c` | Secondary text (italics redefined as gray upright text), page numbers, divider credit |
| `--grid` | `#d9d9d9` | Dashed guide lines, the rule under titles, nested markers, agenda numbers |
| `--stripe` | `#f2f2f2` | Zebra table rows, inline code background |
| `--sans` | Noto Sans SC, PingFang SC, … | Body |
| `--display` | Archivo Black, Arial Black, … | Mega words, big numbers, the `AIM` glyph |
| `--mono` | ui-monospace, SF Mono, … | Emails, page numbers |

Recolors and font swaps only touch `:root`.

## Pitfalls we hit (inherited from upstream — still true here)

1. Marpit reserves `section::before/::after` for pagination and strips literal `content` from `::after`. Text like the org name never paints if written into `section::after`; it has to ride on another pseudo-element — the theme uses `h2::after`. Never inline the theme into a deck's `<style>`; load it as a file via `--theme-set` or the extension registration;
2. Any `section::after` rule without a `content` property kills page-number rendering. To restyle the number on a specific page, follow `section.ink::after` and repeat the attr() content; the cover hides its number with `color: transparent`, again with content present;
3. CLI exports referencing local images must pass `--allow-local-files`, otherwise the images are silently blocked by the security policy with nothing but a warning to tip you off;
4. Fonts load from Google Fonts; offline you get the system fallbacks, with `Arial Black` standing in when `Archivo Black` is unavailable.

## Adding a slide type

Add a `section.<class>` rule block to `themes/aim.css` — copy `todo` for a plain layout, `side` for one with an image. Any `::after` rule must carry content (see above). Then sync three places: an example page in `template.md`, a row in the `docs/usage.md` table, a row in the SKILL.md quick reference. Run the regression below before committing.

## Regression checklist

```bash
marp template.md --theme-set themes/aim.css --allow-local-files -o /tmp/tpl.pdf
```

Check page by page (pixel sampling beats squinting at a clean export):

- Cover: ink band on top, logo top-right, mega words bottom-right;
- Agenda: first row highlighted ink;
- Roster: ink table head;
- Side-image page: image full height, text clear of it;
- Both divider pages solid `#111111`;
- Page number bottom-right from page 2 on, none on the cover;
- `npx markdownlint-cli README.md docs/usage.md template.md` passes.
