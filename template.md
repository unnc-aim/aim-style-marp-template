---
marp: true
theme: aim
paginate: true
---

<!--
   AIM Marp template sample · the comment at the top of each page explains how
   that page is written (it doubles as a presenter note).
   Usage guide: docs/usage.md. Keep theme: aim in the frontmatter.
   Only the cover uses h1; every other page starts at h2. Titles stay on one
   line. No emoji.
-->

<style scoped>
/* Cover logo: the white wordmark painted onto the ink banner, top-right.
   It replaces the default "AIM Robotics" text, so silence h2::after. */
section.lead::before {
  background: var(--ink) url('assets/logo.png') no-repeat right 84px center / auto 72px;
}
section.lead h2::after {
  content: none;
}
</style>

<!-- _class: lead -->
<!-- Cover: # main title (inside the ink band) · ## subtitle · p speakers
     (<br> per line) + p date · ###/#### mega words bottom-right (outlined /
     solid; either can be dropped). The scoped style above puts the white logo
     top-right — copy it along with the cover. -->

# Presentation Title Here

## Subtitle — occasion, audience, or one-line summary

Speaker One (Captain)<br>Speaker Two (Mechanical Lead)<br>Speaker Three (Software Lead)

AIM Robotics · 1 January 2027

### OUTLINE

#### AIM 2026/27

---

<!-- _class: agenda -->
<!-- Agenda: ordered list of 2–6 items (9 at most; numbers 01–09 are generated,
     first row auto-highlighted); *italics* render as gray secondary text -->

## What we'll cover today

1. First Section *one-line note for the section*
2. Team Roster *the new team — who is who*
3. Competition Plan *key events for the season*
4. Support & Discussion *where the School can help*

---

<!-- Regular content page (no class): the h2 title gets its rule and AIM glyph ·
     lists get ink square markers · **bold** as the lead-in · nested lists
     are smaller and lighter -->

## 01 · Regular content slide

- **Bold lead-in** — one line of description text
- **Bold lead-in** — one line of description text
   - *nested note renders in gray*
- **Bold lead-in** — one line of description text

---

<!-- _class: roster -->
<!-- Roster page: ink-headed table with black borders, zebra rows; the first
     column is fixed at 350px (fits name | role | duties) · inside a cell:
     **Name** + <br> + `email` + *ID* -->

## 02 · Roster table

| Member | Role | Key responsibilities |
| --- | --- | --- |
| **Name One**<br>`email1@nottingham.edu.cn` · *20999999* | Captain | duty · duty · duty |
| **Name Two**<br>`email2@nottingham.edu.cn` · *20999999* | Mechanical Lead | duty · duty · duty |

- *footnote line in gray italics*

---

<!-- _class: side -->
<!-- Side-image page: the image is a pure right-side background (pinned right,
     full height, no layout space); set it with the scoped style below, along
     with --side-gap (image width + margin; 360px for narrow images) ·
     ### tag blocks distribute vertically on their own · #### is the outlined
     mega word bottom-left -->

<style scoped>
section {
  --side-gap: 540px;
  background: #ffffff url('assets/poster.png') no-repeat right center / auto 100%;
}
</style>

## 03 · Side-image slide

### TAG BLOCK ONE

One short sentence under the tag.

### TAG BLOCK TWO

One short sentence under the tag.

#### MEGA

---

<!-- _class: ink -->
<!-- Section divider: ## outlined word top-right (all caps) · ### outlined
     number · #### big white headline · p credit line at the bottom -->

## SECTION NAME

### 04

#### Section Headline

Credit line — Name One · Name Two · Name Three

---

<!-- _class: activities -->
<!-- Grouped timeline: ### ink group tags each with a list, packed tighter
     than a regular page; good for around 3 groups -->

## 04 · Grouped timeline

### AUTUMN

- **Activity name** — one-line description
- **Activity name** — one-line description

### SPRING

- **Activity name** — one-line description

### ALL YEAR

- **Activity name** — one-line description

---

<!-- _class: todo -->
<!-- TODO page: ### tag blocks spread out vertically on their own; a list can
     follow the last sentence -->

## TODO

### ITEM ONE

What to arrange, and where.

### ITEM TWO

What to check, and when.

- Room A — purpose
- Room B — purpose

---

<!-- _class: ink -->
<!-- Closing page: same structure as the section divider -->

## THANK YOU

### Q&A

#### Closing Headline

Closing line — AIM Robotics · 1 January 2027
