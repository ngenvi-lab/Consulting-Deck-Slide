---
name: consulting-deck
description: House style for every slide and deck - a consulting-style ("McKinsey/BCG-like") look with takeaway titles, numbered callouts tied to markers in tables and charts, actual-blue vs forecast-orange, source footers and scripted speaker notes, plus the storyline and logic rules that go with it. Use this skill whenever the user asks to create, build, draft, redo or restyle a deck, presentation, slide, slides, one-pager slide, consulting deck, consulting slide, exec/CFO slide, board slide, or to "put this on a slide" / "turn this into slides" - even if they don't say "consulting" - and whenever adding or editing slides in a deck that already uses this style (class "wc" sections, deck.css). Prefer it over generic slide styling.
---

# Consulting deck

The user's preferred style for any slide work: a consulting-style deck that leads with the answer, proves it with one piece of evidence per slide, and guides the audience with numbered markers. The rules below were refined through many rounds of feedback on real decks, then generalised. The skill contains no real data.

Two things matter equally: **the look** (deck.css, layout patterns) and **the logic** (each slide makes one claim the visual actually proves). The user catches logic gaps quickly, so treat the logic rules as part of the style.

## Output format

- **Default: the Slides artifact type.** Run the Artifact quickstart with intent "slides", create from the Slides type, and publish `assets/deck.css` as the deck's shared stylesheet (`format.shared: ["project/deck.css"]`, Inter font face). Each slide is one `slides/<id>.html` file holding `<section id="<id>" class="wc">…</section>` with an `<aside>` of speaker notes. Follow the Slides type's own instructions for the file format; this skill only adds the style and content rules.
- **If the user names a file format** (.pptx, Google Slides): use that format's skill, but carry over the palette, type scale, slide anatomy and logic rules below.
- Reuse the classes in `assets/deck.css` rather than inventing new ones. Add slide-specific classes at the end of deck.css under a comment naming the slide. Copy the CSS as-is; don't restyle it.

## Storyline

Straight to the point: show only what's needed to make the case. Default main flow (adapt the labels to the topic):

1. **The problem**: what's wrong, with the key numbers and a like-for-like comparison (e.g. same months last year) that rules out the obvious excuse (seasonality).
2. **How we know**: the evidence against history (e.g. a 22-month chart of the one ratio that shows the break).
3. **Where it comes from**: the drill-down / trace-back list (segments, customers, lines) so owners know what to fix.
4. **Actions**: 2–4 cards with Why / What / owner · date.

Then an **Appendix** divider slide, followed by profiles, alternative explanations tested, and definitions & method. Supporting detail goes in the appendix, and main slides point to it ("Profile: appendix"). Avoid a flow where slide N raises something, N+1 and N+2 support it, and then N+3 returns to it: put the evidence before the conclusion that uses it.

Before building a multi-slide deck, give the user the slide-by-slide storyline (one line each) unless they already set one.

## Slide anatomy

Every content slide, top to bottom (see `references/examples/`):

- **Eyebrow** (`p.eyebrow`, accent, caps): `N · SECTION · SCOPE · UNITS`, e.g. `2 · HOW WE KNOW IT IS LIKELY WRONG · 22 MONTHS OF ACTUALS`. Appendix slides use `APPENDIX · TOPIC · …`.
- **Title** (`h1.title`): one full-sentence takeaway with the decisive numbers, at most about two lines. Not a topic label.
- **Rule** (`hr.rule`).
- **Body**: arrange it to suit the evidence. There's no fixed layout. What stays constant is the pairing: each numbered callout (`.co` > `.num` + `.ct` with `h3` + `p.d`, a short claim plus one or two sentences with the numbers) sits next to, above or below the evidence it refers to, under a caps header (`p.rhead`) where useful. Common arrangements:
  - one table or chart on the left with a callout column on the right (the default for a single piece of evidence)
  - callouts across the top, with one wide chart or table below
  - stacked rows, each pairing a callout with its own small chart or table (good for 2–3 separate pieces of evidence)
  - two evidence panels side by side or top and bottom (e.g. this year vs last year), with callouts beneath or beside them
  - a full-width table with a comment column (as in the outlier slide), or cards only (actions)
  
  Choose by asking what the audience needs to compare, and put those things next to each other.
- **Markers**: the small numbered circles (`.mk` > `.mn`) placed on the table cells or chart bars that callout N talks about. Callout numbers and marker numbers must match. Mark only the cells that prove the point.
- **Note line** (`p.note`, with `<b>Note:</b>`) for supporting information that the visual doesn't show. A numbered callout is only for something you can point to on the visual.
- **Source footer** (`p.src`, absolute at the bottom): source, basis, as-of date, A = actual / F = forecast, formulas and definitions behind any ratio, and pointers ("Definitions: appendix").
- **Speaker notes** (`<aside>`): a script in plain spoken sentences. Say what the visual shows and how to read it, then walk through each point by number. End with the bridge to the next slide. Put the full monthly data behind any chart here, so numbers can be checked.

Other patterns in deck.css:
- Action cards: `.acts` > `.acard` with WHY / WHAT labels and an owner line.
- Ranked outlier tables: `.otab` / `.orow`, with `.ohi` shading for the key rows, `.ooth` for "all others" and `.otot` for the total.
- Profile key-value tables: `.kvt` / `.kvr`.
- Definitions tables: `.mtab` / `.mrow`.
- Dark verdict box: `.vd`.
- KPI tiles: `.tiles`.

Copy structure from the closest example file before writing a new slide.

The files in `references/examples/` are templates with a fictional company and made-up numbers. Reuse their structure, and always replace the content with the user's own data:

| File | Pattern |
|---|---|
| `ex-problem-table.html` | Problem slide: actual/forecast table with markers, a like-for-like last-year table, 2 callouts |
| `ex-history-chart.html` | 24-month bar chart with a forecast band, a dashed benchmark line, month and year label rows, callouts plus a Note |
| `ex-ranked-table.html` | Full-width ranked trace-back table: numbered rows, shaded key rows, "all others" and total |
| `ex-components.html` | Component breakdown table with indented "days" sub-rows and callouts |
| `ex-actions.html` | Three action cards (WHY / WHAT / owner · date) |
| `ex-definitions.html` | Definitions and method table |

## Visual system

- **Canvas**: 1920×1080, paper background `#F7F6F2`, padding 96/112/140.
- **Fonts**: Inter, minimum 24px everywhere; titles 44px. Tabular numerals in tables.
- **Colour scheme**: the default palette is the one in deck.css: ink `#14213D`, body `#3E4A5C`, muted `#6B7585`, paper `#F7F6F2`, accent `#B4471A`, actual blue `#2B5C8A`.
  - Another scheme is fine when the user asks for one, or when the topic or brand calls for it. Change the `:root` tokens and the few hard-coded tints (forecast cell `#FBE9DF`, total-in-forecast `#F6D5C2` / `#9A3A12`, chart blues `#A9BCD0`) rather than restyling every rule.
  - Keep the roles whatever the colours: one accent for the story's flags, markers and numbers; a calm colour for actual/baseline; a contrasting colour for forecast/scenario; muted grey for context.
- **Actual vs forecast** (or baseline vs scenario) must be obvious at a glance:
  - Actual columns: blue headers (`.ha`).
  - Forecast columns: orange headers (`.hf`) and light-orange cells (`.fc`), with a dashed divider at the first forecast column (`.fs`).
  - Labels carry "(A)" and "(F)", so the split survives black-and-white printing. A band above the table can say "ACTUAL · Sep–Oct" / "FORECAST · Nov–Dec" (`.grp`).
  - In charts: light blue for last year's actuals, dark blue for this year's actuals, orange for forecast, and a light-orange background band behind the forecast months.
- **Totals**: total rows (`.tot`) keep their emphasis across the forecast columns too, using a deeper orange `#F6D5C2` with dark-orange `#9A3A12` numbers.
- **Flags**: abnormal values in accent orange (`.flag`).
- **Charts**: inline SVG bars, with axis labels, month labels and value labels as positioned HTML `<p>` elements.
  - Months are labelled 1–12, not J F M…, which is ambiguous. Show years on a row below.
  - Add a dashed reference line for the meaningful benchmark (lowest or highest actual month), named in the legend.
  - Label the outlier value directly.
- **Sign conventions** stated in the row label, e.g. "A/P (− = owed)".

## Logic rules (the user checks these)

1. **Each finding must stand on its own.** Ask of every callout: could this be normal by itself? If two signals are only abnormal together (e.g. stock rising *while* payables fall), make them one point.
2. **Test every claim against history before flagging it.** If the forecast value sits inside the actual range, it isn't evidence; drop it or say it's normal. Make sure no slide contradicts another (e.g. "A/R is abnormal" on one slide and "the customer side is normal" on the next).
3. **Comparisons are like-for-like.** A comparison table has exactly the same rows and units as the main table. Compare against the business's own history (range, lowest or highest month) rather than abstract norms.
4. **Pick the most intuitive metric**, one a finance reader understands without explanation, and say what 1.0× means in the chart header. Define every ratio in the footer and on the method slide. If there is a judgment call about what to include (e.g. whether relief counts as supplier funding), explain the options with numbers and let the user choose.
5. **Title, chart and callouts use the same measure.** Don't put an amount-based claim in the title over a ratio-based chart.
6. **Everything named on the slide is shown on the slide.** Otherwise demote it to a Note or the speaker notes.
7. **Never cut silently.** If space forces a trade-off (dropping rows, shortening a comparison), flag it to the user and let them decide.
8. **After any restructure or reorder**, re-run rules 1–6 on every slide and fix cross-references ("previous slide", "slide 3", "appendix") and the speaker-note bridges.

## Layout constraints (the Slides format and readability)

- The Slides format refuses a slide if one div directly holds more than 24 absolutely positioned elements; the page then shows the slide read-only. Charts hit this first, because every axis label, month label and value label is a positioned element. Split them into sibling `position:relative` rows (e.g. `.morow` for months, `.yrrow` for years), each under 24; see `ex-history-chart.html`.
- Column widths: at 24px, allow ~13px per character plus 20px of cell padding. Headers like "Nov 26 (F)" need ≥150px; label columns with indented sub-rows need ~250–300px. Widen the table and narrow the callout column rather than letting headers wrap.
- Keep everything inside 1920×1080, with the footer clear of the body.
- When unsure whether something fits, say so in the reply ("not visually checked") rather than claiming it renders.

## Working with the user

- The user edits decks in the page and in comment threads. Before editing a slide, re-read its current file from the artifact, so their edits aren't overwritten.
- For a comment that asks a question ("how was this calculated?", "why this metric?"), answer with the method and numbers. Propose a change and make it when the user agrees.
- Keep owner and date placeholders in [brackets] until the user supplies real ones.
