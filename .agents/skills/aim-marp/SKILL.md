---
name: aim-marp
description: Create AIM Robotics branded Marp presentations using the aim-style-marp-template theme. Use when the user asks for AIM slides, an AIM deck/宣讲/汇报 PPT, or any Marp presentation that should follow the AIM visual style.
---

# Making AIM decks with the template

The template repo is local at `/Users/LijieZhou/Development/AIM/aim-style-marp-template` — use it directly; clone or copy from it if that path is missing.

## Workflow

**Set up.** Skip if the project already has `themes/aim.css`:

```bash
mkdir -p <project>/themes <project>/assets
cp /Users/LijieZhou/Development/AIM/aim-style-marp-template/themes/aim.css <project>/themes/
cp /Users/LijieZhou/Development/AIM/aim-style-marp-template/assets/logo.png \
   /Users/LijieZhou/Development/AIM/aim-style-marp-template/assets/logo-dark.png <project>/assets/
```

The frontmatter is always the same three lines: `marp: true`, `theme: aim`, `paginate: true`. If the user works in VS Code, also register the theme in the project's `.vscode/settings.json` with `"markdown.marp.themes": ["themes/aim.css"]`.

**Write.** Copy the skeleton from the template repo's `template.md` and pick classes from the quick reference below. For the text: follow the user's language (the team writes Chinese decks for recruiting, English for external docs), no emoji, `#` only on the cover, titles on one line, `*italics*` as small gray notes. In roster tables, emails go in inline code and student IDs in italics.

The cover carries the white logo via a scoped style — copy the `<style scoped>` block from `template.md`'s cover page along with the cover itself.

**Render and check.** Never skip this:

```bash
marp slides.md --theme-set themes/aim.css --allow-local-files -o slides.pdf
```

Go over every page: cover band and mega words present, logo top-right; agenda's first row highlighted ink; table heads ink; side image full height with text clear of it; page number bottom-right from page 2 on and none on the cover; nothing overflowing or leaving a big blank patch. Finish with `npx markdownlint-cli slides.md`.

## Quick reference

| Class | How to write it |
| --- | --- |
| `lead` | `#` title, `##` subtitle, two paragraphs (speakers, date), `###`/`####` mega words |
| `agenda` | `##` plus an ordered list, 9 items at most |
| no class | `##` plus a list |
| `roster` | `##` plus a table (first column: name, email, ID) |
| `side` | `##` plus `###` tag blocks, `####` mega word, image as below |
| `ink` | `##` outlined word, `###` outlined number, `####` headline, `p` credit |
| `activities` | `##` plus `###` group tags, each with a list |
| `todo` | `##` plus `###` tag blocks |

Side images use a scoped style on the page; `--side-gap` is the image width plus margin (around 540 for posters, 360 for narrow banners):

```html
<style scoped>
section {
  --side-gap: 540px;
  background: #ffffff url('assets/poster.png') no-repeat right center / auto 100%;
}
</style>
```

## Don't step on these

- Never inline the theme into a deck's `<style>`. Marpit strips literal `content` from `section::after`, and PDF exports lose the cover band, the org name and the page numbers all at once. The theme only loads via `--theme-set` or extension registration;
- Never write a `section::after` rule without `content` — page-number rendering dies with it. To restyle a number, follow `section.ink::after` in the theme and repeat the attr() content;
- Local images in exports require `--allow-local-files`;
- The agenda tops out at 9 items.

More in the template repo: usage in `docs/usage.md`, implementation details and pitfall backstories in `README.md`.
