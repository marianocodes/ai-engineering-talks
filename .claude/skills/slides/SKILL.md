---
name: slides
description: Generate a self-contained HTML slide deck for an AI Engineering talk from a user-provided outline. Use when the user asks to "create slides", "make a deck", "generate a presentation", "build a talk" — especially mentioning AI Engineering. Produces a single slides.html using the Telescoped dark theme (Nunito, purple/cobalt accents, gradient titles) with arrow-key navigation.
---

# slides

Builds a self-contained HTML presentation for a talk (typically about AI Engineering). One file out: `slides.html`. No build step.

## When to use

Triggered when the user wants slides, a deck, a presentation, or a talk. The skill is opinionated about theme — it always produces the Telescoped dark style (purple/cobalt accents, Nunito font, gradient title text). If the user wants a different theme, this skill is the wrong tool.

## What you need from the user

If the user hasn't already provided these in their message, ask for the missing ones in a single round of questions:

1. **Talk title** (and optional subtitle).
2. **Speaker line** — name, venue, date — whatever should appear on the title slide.
3. **Outline** — a list of slides. Each entry should imply a *type*:
   - "Title: ..." → title slide
   - 3–6 bullets → bullet slide
   - A code snippet (with language) → code slide
   - Two labeled lists / a comparison → two-column slide
4. **Output path** — default to `slides.html` in the working directory.

If the user gives you a freeform outline without specifying types, infer them. Reuse common shapes: opener title, agenda bullets, several content slides, a closing/Q&A slide.

## How to build the deck

1. Read [`template.html`](template.html) — it's the scaffold (theme config, CSS, navigation JS, Prism for syntax highlighting). It contains a `<!-- SLIDES_PLACEHOLDER -->` comment inside `<main id="deck">`.
2. Read [`slide-snippets.md`](slide-snippets.md) — copy the matching snippet for each outline entry and substitute the `__TOKEN__` placeholders.
3. Read [`example-deck.html`](example-deck.html) if you need a structural reference for spacing, density, or how the snippets compose end-to-end.
4. Build the output:
   - Start from `template.html`.
   - Replace `__DECK_TITLE__` in the `<title>` tag with the talk title.
   - Replace the `<!-- SLIDES_PLACEHOLDER -->` with the concatenated `<section class="slide">…</section>` blocks.
   - The **first** slide must have the `active` class (the snippet already includes it on the title slide). All others must **not**.
   - Update the initial counter (`<span id="counter">1 / 1</span>`) to `1 / N` where N is the total slide count.
5. Write the result to `slides.html` (or the path the user specified).

## Hard rules

- Single file output. Do not split into multiple HTML files or extract CSS/JS.
- Do not add external assets beyond the CDN links already in `template.html` (Tailwind, Prism, Google Fonts).
- Do not modify the theme tokens (colors, fonts, gradients, shadows). They are tuned.
- HTML-escape user-provided code (`<` → `&lt;`, `>` → `&gt;`, `&` → `&amp;`) before placing it in code slides.
- Keep slides under 40 total — beyond that, the all-in-DOM approach gets sluggish.
- Bullet slides: 3–6 bullets, each under ~12 words. If content exceeds this, split into two slides.

## After writing the file

Tell the user:
- The output path.
- How to open it: `open slides.html` (macOS) or just double-click.
- Keys: `←` / `→` (or `space`) to navigate, `f` for fullscreen, `Home` / `End` to jump.
