# DataJam 2026 — Storybook Redesign PRD

**Working title:** *The Hundred Acre Dataset*
**Owner:** CougarAI
**Status:** Draft v0.1 — awaiting art direction sign-off
**Target ship:** 3 weeks before event (Oct 17, 2026); soft launch Sept 30

---

## 1. Concept

A cougar walks into a jam jar. Not a joke — a motif.

The site borrows the **grammar of a Milne / Shepard storybook** (hand-lettered chapter titles, ink-and-wash illustrations, cream paper, generous margins, page numbers, small marginalia) and replaces the bear with **Shasta**, the UH cougar mascot, and the honey pot with a **jam jar** — because *DataJam*. Each jar on the site is a labeled prop: challenge tracks, sponsor tiers, prize slots, agenda beats. The jar becomes the site's unit of information.

The tone we're borrowing is the *tone of the original book*, not the Disney cartoon: dry, warm, a little melancholy, slightly literary. The tone we're avoiding is "quirky mascot with big eyes waving at the camera."

**Why this works for the event:**
- It's memorable and share-able in a crowded student-hackathon market where every landing page is a dark neon gradient.
- It gives sponsors an ownable object (a labeled jar) instead of a logo strip.
- It's affectionate toward UH without being a pep rally — Shasta is treated as a character, not a logo.
- The reading-book pacing gives us permission to write *long* copy that sponsors and participants actually read.

**Why this can fail:**
- If the illustration is bad, the whole thing collapses. There is no fallback aesthetic — this concept is 60% illustration, 30% typography, 10% code. Budget accordingly.
- If it reads as Disney fan-art it looks unlicensed and cheap. Section 2 exists to prevent that.
- If it drifts into "cutesy" the sponsor page dies. Shasta needs to be dignified in judging contexts.

## 2. Intellectual property — read this before drawing anything

The classic *Winnie-the-Pooh* text (A.A. Milne, 1926) and the original E.H. Shepard line illustrations entered the **US public domain in January 2022**. *The House at Pooh Corner* and Tigger followed in 2024. This means we may legally draw in the **line-and-wash storybook style** of the original books.

We may **not**:

- Use the Disney character designs — red shirt, that specific face, the Disney lettering, Tigger's stripes-as-drawn-by-Disney, Eeyore's ribbon color, etc.
- Call the site "Winnie the Pooh" or "Hundred Acre Wood" in any user-facing string (working titles are internal only).
- Use Shepard's actual drawings as raster assets. Style-reference only; every asset is drawn from scratch.
- Depict a bear at all. Our animal is a cougar. This is both the point and the clearest legal separation.

Every illustration ships with a signed release from the illustrator confirming original authorship and style-reference-only use. Legal review before public launch — not optional.

## 3. Art direction

**One-line brief for the illustrator:** *Ink and watercolor storybook, warm paper, a cougar with a jam jar. Draw it like you're illustrating a chapter book, not a mascot sheet.*

### Palette

The site is warm and paper-toned. UH scarlet stays, but it stops being the background — it becomes an accent, the color of the jam.

| Token              | Hex       | Role                                                             |
| ------------------ | --------- | ---------------------------------------------------------------- |
| `--paper`          | `#f4ecdc` | Page background. Slightly warmer than the current cream.         |
| `--paper-deep`     | `#e8ddc4` | Alt sections, card backgrounds. Not white — never white.         |
| `--ink`            | `#2b1d16` | Body text, illustration lines. Warm near-black, not `#000`.      |
| `--ink-soft`       | `#5b463a` | Secondary text, captions.                                        |
| `--jam`            | `#c8102e` | UH scarlet. Jam color, primary CTA, chapter numerals only.       |
| `--jam-deep`       | `#8a0a1f` | Hover, pressed states, drop-caps.                                |
| `--tape`           | `#d4a24a` | Ochre — used on jar labels and "washi tape" divider strips.      |
| `--forest`         | `#3f5a3a` | Rare accent (agenda day-2 marker, workshop tags).                |

Contrast: body text `--ink` on `--paper` is 12.4:1. Every accent color pairs with `--ink` for text over it.

### Typography

Two families, no more.

- **Display / chapter titles:** a serif with hand-set warmth — **Fraunces** (variable, free) tuned to `opsz=144, SOFT=100, WONK=1`. This is the storybook feel without paying for a licensed face on day one. Fallback: Playfair Display.
- **Body / UI:** **Source Serif 4** for reading passages, **Inter** for UI chrome (buttons, tabs, form fields). Two serifs is the point — the UI chrome sans keeps forms from feeling twee.
- **Marginalia / captions / page numbers:** small-caps Fraunces or Source Serif 4 at `letter-spacing: 0.14em`.

We keep IBM Plex Mono nowhere. It's a great typeface, and it's the wrong one for this concept — mono type screams "hackathon flyer" and undoes the entire storybook conceit.

### Texture and paper

Every colored surface has a **subtle paper grain** — a single 512×512 tiling PNG at 6–10% opacity, blend-mode `multiply`. Not the fake "notebook lines" texture. Real cotton-rag paper scan. One asset, shipped once, cached forever.

Section edges use **torn-paper SVG masks** where two surfaces meet, so the site reads as pages layered on pages, not rectangles stacked on rectangles. One mask per section transition, hand-drawn, 4 variants shuffled deterministically so no two adjacent tears repeat.

### Illustration

- **Line quality:** brown-black ink (`--ink`), variable-width, drawn on a paper tablet or by hand and scanned. No vector-tool "brush" that looks like Illustrator's default calligraphic brush. If a designer submits work that looks like it came out of Figma's arrow tool, reject it.
- **Fills:** watercolor washes with visible edges. Never fully filled — the paper shows through. Compare: children's picture books, not modern flat-design mascot sheets.
- **Cougar character:** Shasta is drawn as a *tawny cougar cub* about the size of a house cat in the compositions. Big head-to-body ratio, expressive eyes, but *anatomically a cougar*. No hoodie. No sunglasses. No laptop keyboard puns. Reference: real cougars + storybook animals like *The Tiger Who Came to Tea*.

### The jam jar system

The jar is a **content component**, not a decoration. Spec:

- Jar body: watercolor glass, faint reflections. Content inside is a colored fill — scarlet for "prize jars," ochre for "workshop jars," forest for "sponsor jars."
- **Label:** hand-lettered, tied at the neck with twine. The label is where we put challenge names, sponsor names, prize tier. It's real text, not baked into the illustration — SVG text set in Fraunces so it's screen-reader accessible and easy to update.
- Six drawn jar shapes at ship (short, tall, squat, hex, mason, apothecary). We rotate through them; identical jars kill the illusion.

### Motion

Restrained. This is a book, not a website that jitters when you scroll.

- **Page-turn transitions** between the hero and the About section: a torn-paper wipe on scroll, 400ms, ease-out. Once, on entry. Not repeated.
- **Jars settle slightly** on hover (`translateY(-2px)`, 150ms). No wobble, no spring bounce.
- **Chapter numerals** (a large `01` `02` `03` on the section headings) fade in as they enter the viewport, `opacity 0→1` over 600ms. That's it.
- Zero parallax. Parallax is what tells the user the site was built in 2019.
- **Respect `prefers-reduced-motion`** — all of the above collapse to instant.

## 4. Information architecture

Pages, in reading order. Same eight sections as v1, re-cast as chapters.

| # | Chapter                          | Purpose                                             | Key content |
|---|----------------------------------|-----------------------------------------------------|-------------|
| — | Cover                            | Emotional hook, one CTA                             | Title, date, cougar-with-jar illustration, single CTA |
| 01 | In Which There Is a DataJam       | What the event is, why it exists                    | About copy, stats strip (participants/teams/prizes) |
| 02 | The Agenda                        | Day-by-day plan                                     | Two-column agenda, per current site content |
| 03 | The Jam Jars (Challenges)         | Sponsor-contributed problem statements              | 3–6 challenge jars with sponsor name on the label; expandable rows |
| 04 | The Prizes                        | What winners get, who funds them                    | Three jars: 1st / 2nd / 3rd, with sponsor attribution |
| 05 | Good Questions                    | FAQ                                                 | Existing FAQ, re-styled |
| 06 | Where and When                    | Venue + logistics                                   | Building/room TBD block, lunch note, parking note |
| 07 | For Companies                     | Sponsorship pitch                                   | Copy adapted from the sponsor PDF; three sponsor tiers as jars |
| — | Endpapers                         | Contact, credits, footer CTA                        | Emails, register CTA, small print |

**New vs current site:** chapters 03 (Challenges) and 07 (Companies) are new. Companies exists because the source PDF is a sponsor pitch and the current landing buries that. Challenges exists because it's the sponsor-facing hook — sponsors want to see their name on a jar mockup before they commit.

## 5. Component redesign, specifically

Concrete before-and-after. If a component isn't listed, it inherits the palette/typography above with no structural change.

### 5.1 Cover / Hero
- Full-bleed `--paper` background with paper grain.
- Title set in Fraunces at `clamp(64px, 12vw, 180px)`, `font-optical-sizing: auto`, weight 500. The word "Jam" gets a **drop-cap treatment** — the J is oversized, drawn in scarlet ink with a small watercolor bleed behind it. Handmade SVG, one asset.
- Cougar illustration: Shasta seated, holding a jam jar labeled `2026`. Occupies the right third at desktop, moves above the headline at mobile.
- CTA: a single scarlet button, labeled **"Sign up to compete."** No secondary button in the hero. The secondary "See the agenda" link becomes a small underlined phrase below the button, not a competing button.
- Stats strip stays, restyled: numerals in Fraunces italic, labels in small-caps at `--ink-soft`.

### 5.2 Chapter headings (01–07)
- Large scarlet numeral in Fraunces, `clamp(80px, 14vw, 220px)`, aligned to the outside margin.
- Chapter title beside it in Fraunces regular. No uppercase. No monospace kicker.
- A single **washi-tape divider** below — a 320×24px scan of ochre paper tape at `--tape`, one of four variants.

### 5.3 The Jam Jars (Challenges) — new section
- Grid: three across at desktop, one across on mobile. Each jar is ~280px wide, illustrated.
- Label text is HTML `<figcaption>` over the jar's twine — challenge name, sponsor byline, a short one-line hook.
- Click/tap the jar → the row below expands with the full challenge brief. Uses `<details>` for accessibility; no custom accordion JS.
- At v1, populated with three placeholder jars ("The Data Cleaning Challenge," "The Model Bake-Off," "The Visualization Prize") so the section renders before sponsors sign.

### 5.4 Prizes
- Three jars, drawn full-height (600–700px on desktop), stood in a row on a wooden-plank illustrated shelf. The shelf is one flat SVG, no realism.
- Jars are labeled 1st / 2nd / 3rd in ink, with the sponsor name below when known ("Sponsored by ___").
- No metallic gradients, no gold/silver/bronze visual cliché. First place gets a fuller scarlet jam, third gets a lighter fill — that's it.

### 5.5 FAQ
- Two-column reading layout: heading on the left, questions on the right, as in the current design.
- Each question uses `<details><summary>` — clicking a question opens the answer with a 200ms height animation.
- Small "chapter" numerals in the margin next to every third question, decorative.

### 5.6 Sponsorship section (new)
- Three tiers as three jars of different sizes — **Presenting Jar**, **Challenge Jar**, **Prize Jar**. Copy adapted from the sponsor PDF.
- Contact CTA is a mailto: link written as if from the book: *"Write to us at cougarai@uh.edu."*
- No sponsor logo strip on v1 — we replace that anti-pattern with the labeled jars. If a sponsor insists on logo placement, it goes on the jar label as text.

### 5.7 Endpapers / footer
- Register CTA repeats.
- Credits line: *Illustrated by ___. Built by CougarAI. 2026.*
- No newsletter signup. This is a one-time event; a newsletter is friction that yields nothing.

## 6. Copy voice

Rewrite every user-visible string. The v1 copy is fine — it's not what we want. Voice guide:

- Warm, dry, first-person plural. *"We put the challenge prompts in jars,"* not *"Challenges will be distributed at kickoff."*
- Short sentences. Occasional em dash.
- Never use "innovative," "cutting-edge," "unleash," "elevate," "empower," "journey," "unlock." If the copy reads like a hackathon-landing-page template, rewrite it.
- Numbers in body copy are spelled out below ten (*four teammates, not 4 teammates*) except in the stats strip and agenda.
- Address the reader as *you*.

Example rewrite — hero subtitle:

> **Before:** "A two-day data science and machine learning competition. Get a real-world problem and a dataset, build a solution with your team, and demo it to industry judges."
>
> **After:** "For two days in November, we hand you a real dataset and a real problem. You bring three friends, a laptop, and whatever you already know. On Sunday afternoon, industry judges come by your table to see what you built."

## 7. Illustration deliverables

Priced and scheduled as a single commission. All originals kept in `assets/illustration/originals/` as layered files, exports live in `assets/illustration/exports/`.

- **Cover cougar with jar (hero).** Detailed, ~2000px wide. `.svg` where flats allow, `.webp` for washes.
- **Six jam jar shapes**, unlabeled, `.svg` line + separate `.svg` fill layer so label and color can be composed at build.
- **One "shelf" SVG** for the prizes section.
- **Four washi-tape strips**, `.png` with transparency, ~640×48px.
- **Four torn-paper edge masks**, `.svg`.
- **One paper-grain tile**, `.png`, 512×512, seamless.
- **Three small marginalia sketches** for FAQ and footer (a cougar paw print, a spilled data point, a rolled-up scroll).
- **Favicon:** the cougar's silhouette holding a jar, 32/180/512px `.png` + `.ico`.

Style-consistency check: illustrator delivers a single "family shot" first — cougar plus two jars plus a torn paper edge — before drawing any other asset. If the family shot doesn't sell the concept, we redirect before we've paid for twenty pieces.

## 8. Accessibility

- Every illustration ships with meaningful `alt` text or, if decorative, `alt=""` and `role="presentation"`. The cougar-with-jar hero image: *"A cougar cub holding a jar of jam labeled '2026'."*
- Color is never the sole carrier of meaning. Prize jars are labeled 1st/2nd/3rd in text; challenge jars use both fill color and a category tag.
- All interactive components (jar accordions, FAQ) are `<details>`/`<summary>` — keyboard, focus, and screen-reader native.
- Body copy targets a minimum 17px on mobile, 18px desktop. Chapter serifs are tested at 200% zoom.
- `prefers-reduced-motion: reduce` disables the page-turn transition and any hover translate.
- Contrast measured at each palette pair; report shipped with the launch PR.

## 9. Performance

The site is illustration-heavy, so this matters.

- **Hero image budget:** ≤ 90KB delivered (`.webp` q=80, `.avif` fallback via `<picture>`).
- **Total page weight target:** ≤ 350KB above the fold, ≤ 900KB full page. Current v1 is ~10KB — we can afford the increase.
- Every illustration served responsively via `<picture>` with 1x/2x sources. No 4K assets served to phones.
- Font subsetting for Fraunces/Source Serif/Inter to Latin only; `font-display: swap`.
- Ship on Vercel, root `./`, no build step (static HTML/CSS + a single small JS for the countdown and the reveal-on-scroll). Lighthouse target: Performance ≥ 95, Accessibility 100, Best Practices ≥ 95, SEO 100.

## 10. Build

- Stay static. No React, no framework. `index.html` grows to ~600 lines, split into an `assets/` and `styles/` directory once it's over ~800.
- CSS as one hand-authored file. Tokens as CSS custom properties. No Tailwind — Tailwind's utility soup fights the storybook aesthetic and pushes toward template-y patterns.
- One JS file for: the countdown, IntersectionObserver reveals, and the page-turn transition. Under 3KB minified.
- Metadata: `og:image` is a still of the cougar-with-jar illustration, 1200×630. Twitter card `summary_large_image`. Descriptive title tag.
- The current `index.html` becomes `index.legacy.html` for one commit so reviewers can diff visually, then is deleted.

## 11. Milestones

Working backward from Nov 7 event, target Oct 17 (three weeks out).

| Week | Milestone                                                                                           |
|------|-----------------------------------------------------------------------------------------------------|
| W-6 (Sept 21)  | PRD sign-off. Illustrator briefed. Legal review of concept.                             |
| W-5 (Sept 28)  | Illustrator's "family shot" delivered. Go / no-go on style. Copy first draft.           |
| W-4 (Oct 5)    | All illustration assets delivered. HTML/CSS scaffolding in place with placeholders.     |
| W-3 (Oct 12)   | Full site assembled with real assets. Accessibility + Lighthouse pass. Internal review. |
| W-2 (Oct 17)   | **Soft launch.** Shared to CougarAI list and first-round sponsors.                      |
| W-1 (Oct 24)   | Registration open, sponsor jars labeled, minor copy fixes only.                         |
| Event (Nov 7)  | Freeze site content. Post-event: swap hero for "See you next year." card by Nov 10.     |

## 12. Risks and how we handle them

- **Illustration quality doesn't hit.** *Mitigation:* pay for the family shot up front, kill the concept if it doesn't land. Have a backup plan: keep the current v1 design in `index.legacy.html` and ship it if we run out of runway.
- **Perceived Disney association.** *Mitigation:* the animal is a cougar, palette is not Disney yellow-and-red, no character named Pooh anywhere. Legal review before public URL.
- **Sponsors don't materialize by Oct 17.** *Mitigation:* jars ship with placeholder challenge names in CougarAI's voice ("The Cleaning Jar," "The Model Jar"); sponsor names swap in without a redesign.
- **Storybook tone reads as unserious to industry judges.** *Mitigation:* sponsor and prize sections are written in a plainer register — the whimsy stays in the hero, the About, and the FAQ, not in the sponsorship pitch.
- **Copy drifts into AI-slop during handoff.** *Mitigation:* one copy owner writes every user-visible string. Reject anything containing the banned words in §6.

## 13. Explicit non-goals

- No animated Shasta character. Not a game, not a chatbot, not a Duolingo mascot. He appears in illustrations, not in interaction.
- No dark mode. This is a paper book. A paper book does not have a dark mode.
- No 3D. No WebGL. No Three.js jar.
- No signup form on-site — registration lives in the university's system (link out or `mailto:`).
- No blog, no press page, no team bios. The site's job is: explain the event, get you registered.

## 14. Open questions for the team

1. Do we have illustrator budget in the $2–4K range, or do we need to scope down to a single illustrator-week?
2. Registration platform — CougarAI's own form, UH Get Involved, Devpost, or `mailto:`?
3. UH branding office sign-off on Shasta likeness — required or "cousin of Shasta, not officially licensed"?
4. Sponsor confirmations expected by which date? Drives whether §5.3 ships with real jar labels or placeholders.
5. Photography — do we want any real photos of past events, or is the site 100% illustrated?

## 15. Success metrics

- ≥ 400 unique visitors in the first 72 hours after soft launch.
- ≥ 80 registrations by event day (matches expected participation).
- ≥ 3 sponsor conversations attributable to the sponsor page (tracked via `mailto:` UTM or a scheduling link).
- Qualitative: at least one sponsor or student describes the site unprompted as *"not like other hackathon sites."* This is the actual bar.
