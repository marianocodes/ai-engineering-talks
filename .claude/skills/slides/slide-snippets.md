# Slide snippets

Copy these blocks verbatim into the `<!-- SLIDES_PLACEHOLDER -->` region of `template.html`. The first slide must carry the `active` class — the runtime swaps it as the user navigates.

Substitute the `__TOKEN__` placeholders. Do not rewrite layout, spacing, or colors — the theme is calibrated.

---

## 1. Title / section divider

Use for: deck opener, section breaks, closing slide.

```html
<section class="slide active items-center justify-center text-center">
  <div class="brand-bar"></div>
  <div class="stagger max-w-5xl">
    <div class="text-cobalt uppercase tracking-[0.3em] text-sm font-semibold">__EYEBROW__</div>
    <h1 class="mt-6 text-7xl font-extrabold leading-tight bg-telescoped-1 bg-clip-text text-transparent">
      __TITLE__
    </h1>
    <p class="mt-8 text-2xl text-neutral-80 font-light">__SUBTITLE__</p>
    <div class="mt-12 flex items-center justify-center gap-3 text-neutral-60">
      <span class="w-2 h-2 rounded-full bg-cobalt animate-pulse-dot"></span>
      <span class="text-base">__SPEAKER__ · __VENUE_OR_DATE__</span>
    </div>
  </div>
</section>
```

Variants:
- For a section divider (not the opener), drop the `__EYEBROW__` div and use a smaller `h1` (`text-6xl`).
- For a closing slide, replace the subtitle with a call-to-action and the dot line with a URL/handle.

---

## 2. Bullet content slide

Use for: most content. Heading + 3–6 bullets.

```html
<section class="slide flex-col justify-center">
  <div class="brand-bar"></div>
  <div class="max-w-5xl">
    <div class="text-cobalt uppercase tracking-[0.25em] text-xs font-semibold mb-3">__SECTION_LABEL__</div>
    <h2 class="text-5xl font-extrabold text-secondary-100 mb-10">__HEADING__</h2>
    <ul class="stagger space-y-5 text-2xl text-neutral-120 leading-snug">
      <li class="flex gap-4"><span class="text-cobalt font-bold mt-1">▸</span><span>__BULLET_1__</span></li>
      <li class="flex gap-4"><span class="text-cobalt font-bold mt-1">▸</span><span>__BULLET_2__</span></li>
      <li class="flex gap-4"><span class="text-cobalt font-bold mt-1">▸</span><span>__BULLET_3__</span></li>
      <li class="flex gap-4"><span class="text-cobalt font-bold mt-1">▸</span><span>__BULLET_4__</span></li>
    </ul>
  </div>
</section>
```

Rules:
- Keep each bullet under ~12 words. If it wraps to 3 lines, split it.
- 3–6 bullets max. More than 6 means it should be two slides.
- For emphasis, wrap a fragment in `<span class="text-secondary-100 font-semibold">…</span>`.

---

## 3. Code block slide

Use for: showcasing a code snippet. Set `language-xxx` to the language (e.g. `language-python`, `language-typescript`, `language-bash`).

```html
<section class="slide flex-col justify-center">
  <div class="brand-bar"></div>
  <div class="max-w-6xl w-full mx-auto">
    <div class="text-cobalt uppercase tracking-[0.25em] text-xs font-semibold mb-3">__SECTION_LABEL__</div>
    <h2 class="text-4xl font-extrabold text-secondary-100 mb-8">__HEADING__</h2>
    <pre class="language-__LANG__"><code class="language-__LANG__">__CODE__</code></pre>
    <p class="mt-6 text-lg text-neutral-80">__CAPTION__</p>
  </div>
</section>
```

Rules:
- HTML-escape the code body: `<` → `&lt;`, `>` → `&gt;`, `&` → `&amp;`.
- Keep snippets to 12–15 lines max. Anything longer should be trimmed with `# ...` markers.
- The optional caption sits below; omit the `<p>` if you don't need one.

---

## 4. Two-column / comparison

Use for: before/after, pros/cons, concept-vs-implementation, diagram + text.

```html
<section class="slide flex-col justify-center">
  <div class="brand-bar"></div>
  <div class="max-w-6xl w-full mx-auto">
    <div class="text-cobalt uppercase tracking-[0.25em] text-xs font-semibold mb-3">__SECTION_LABEL__</div>
    <h2 class="text-4xl font-extrabold text-neutral-120 mb-10">__HEADING__</h2>
    <div class="grid grid-cols-2 gap-8 stagger">
      <div class="rounded-lg border border-neutral-20 bg-gray-dark p-8 shadow-shadow-12">
        <div class="text-cobalt font-bold text-lg uppercase tracking-wider mb-4">__LEFT_TITLE__</div>
        <ul class="space-y-3 text-xl text-neutral-120">
          <li class="flex gap-3"><span class="text-cobalt mt-1">▸</span><span>__LEFT_POINT_1__</span></li>
          <li class="flex gap-3"><span class="text-cobalt mt-1">▸</span><span>__LEFT_POINT_2__</span></li>
          <li class="flex gap-3"><span class="text-cobalt mt-1">▸</span><span>__LEFT_POINT_3__</span></li>
        </ul>
      </div>
      <div class="rounded-lg border border-neutral-20 bg-gray-dark p-8 shadow-shadow-12">
        <div class="text-secondary-100 font-bold text-lg uppercase tracking-wider mb-4">__RIGHT_TITLE__</div>
        <ul class="space-y-3 text-xl text-neutral-120">
          <li class="flex gap-3"><span class="text-secondary-100 mt-1">▸</span><span>__RIGHT_POINT_1__</span></li>
          <li class="flex gap-3"><span class="text-secondary-100 mt-1">▸</span><span>__RIGHT_POINT_2__</span></li>
          <li class="flex gap-3"><span class="text-secondary-100 mt-1">▸</span><span>__RIGHT_POINT_3__</span></li>
        </ul>
      </div>
    </div>
  </div>
</section>
```

Variants:
- **Pros/cons** — left header to `text-success`, right header to `text-danger`; matching bullet markers.
- **Before/after** — left header "BEFORE" / `text-neutral-80`; right header "AFTER" / `text-secondary-100`.
- **Code + commentary** — replace one column's `<ul>` with the `<pre><code class="language-__LANG__">…</code></pre>` block from snippet #3 (drop the surrounding card if the code already has its own background).

---

## Composition rules

1. Exactly one slide must have the `active` class — the very first one.
2. Every slide must be a direct child `<section class="slide">` of `<main id="deck">`.
3. Don't add `<script>` tags inside slides. The deck has one global script.
4. Keep total deck under ~40 slides — beyond that, performance dips because all slides are in the DOM.
5. The `brand-bar` div is optional on the title slide but recommended on every content slide for visual consistency.
