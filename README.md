# Chalmers Beamer Template (2026 visual identity)

> **Unofficial template.** This is a community Beamer theme that approximates the 2026 Chalmers visual identity using the Chalmers logotypes and the English PowerPoint master as references. It is **not** an official Chalmers product. For brand-critical or ceremonial materials, consult the Chalmers Brand Portal and your local communications officer.
>
> **Vibe-coded.** I put this together informally while working on a deck for my own use. Bug reports and feature ideas are welcome at <https://github.com/wenlzhang/chalmers-beamer> — I cannot promise to address everything, but I would rather share what I have than keep it private. Treat any pull-request review as best-effort.

A LaTeX Beamer theme that approximates the **Chalmers University of Technology 2026 group-wide visual identity** — the purple-based brand launched in spring 2026, derived from the official PowerPoint master (`Powerpoint template – Chalmers University of Technology (english).potx`).

**Project:** <https://github.com/wenlzhang/chalmers-beamer>
**Author:** Wenliang Zhang, Chalmers University of Technology

The theme is intentionally **lightweight**: a single `.sty` file defines the colour palette, fonts, frame layouts, cover, and section dividers. The accompanying `chalmers-beamer.tex` is a minimal skeleton that you can copy and adapt.

---

## File layout

| File | Purpose |
|------|---------|
| `beamerthemeChalmers.sty` | The theme — colours, fonts, frame templates. **Do not edit unless necessary.** |
| `chalmers-beamer.tex`     | Self-documenting tutorial deck (cover, outline, sections, blocks, customisation). |
| `README.md`               | This file — full command reference and customisation notes. |
| `logographics/`           | Chalmers logos (PNG). |
| `LICENSE`                 | MIT licence (covers the LaTeX/Beamer code only). |
| `NOTICE`                  | Brand notice (Chalmers logos are Chalmers trademarks; not covered by MIT). |

---

## Quick start

```latex
\documentclass[aspectratio=169]{beamer}
\usetheme{Chalmers}

\title{Presentation Title}
\subtitle{Optional subtitle}
\author{Author Name}
\institute{Department, Chalmers University of Technology}
\date{2026-05-22}                          % ISO 8601 recommended
\shorttitle{Short title for the footer}    % optional

% Optional: pick the logo style (default 'logo')
% \chalmersheadline{logo+word}

\begin{document}
    \titleframe                            % purple cover slide
    \outlineframe                          % outline of all sections
    \section{Introduction}                 % auto-inserts a divider
    \begin{frame}{Topic}
        Hello, world.
    \end{frame}
\end{document}
```

Compile with `pdflatex chalmers-beamer.tex` (run twice — once for the `.toc`, once for the section dividers to render). For 4:3 slides, use `\documentclass[aspectratio=43]{beamer}` instead.

---

## Visual identity reference

### Colour palette

All colours below are defined as named `xcolor` colours by the theme, so you can write `\textcolor{ChalmersPurple}{...}`, `fill=ChalmersGreen`, etc. anywhere in the document.

| Name | Hex | Role |
|------|-----|------|
| `ChalmersPurple`       | `#472DBE` | **Primary brand colour** (titles, bullets, rules) |
| `ChalmersPurpleDark`   | `#332085` | Pressed / hover variant |
| `ChalmersPurpleLight`  | `#6746EB` | Lighter purple |
| `ChalmersPurpleSoft`   | `#9E92E8` | Soft purple (backgrounds) |
| `ChalmersCream`        | `#F0EDE6` | Warm off-white (block bodies) |
| `ChalmersBlack`        | `#222222` | Body text (not pure black) |
| `ChalmersGrey`         | `#7F7F7F` | Muted text / subtitles |
| `ChalmersGreen`        | `#00B356` | Accent — success / example |
| `ChalmersLime`         | `#ADD739` | Accent — lime |
| `ChalmersCyan`         | `#36B7F6` | Accent — cyan |
| `ChalmersTeal`         | `#61E9D2` | Accent — teal |
| `ChalmersRed`          | `#D52515` | Accent — alert / warning |
| `ChalmersOrange`       | `#ED7122` | Accent — orange |
| `ChalmersYellow`       | `#F6D62A` | Accent — yellow |
| `ChalmersPink`         | `#D987BA` | Accent — pink |

The primary, neutral, and accent colours mirror the official PowerPoint theme (`ppt/theme/theme1.xml`) verbatim.

### Typography

Arial is the official Chalmers typeface. We approximate it with **Helvetica** via the `helvet` package, which ships with every TeX Live distribution. `\familydefault` is set to `\sfdefault`, so prose is sans-serif everywhere; mathematics stays in Computer Modern for legibility.

### Layout

- **Aspect ratio:** 16:9 by default (the PowerPoint master is 13.33″ × 7.5″).
- **Left / right margins:** 8 mm.
- **Logo position:** top-right on every slide — cover, section divider, normal frame, and any custom purple frame — with identical 2 mm top / 6 mm right margins. The colour adapts automatically (purple on light slides, white on the purple cover / dividers).
- **Cover slide:** full-bleed Chalmers Purple background, white logo top-right, title / subtitle / author / institute / date stacked centre-left.
- **Section divider:** full-bleed Chalmers Purple background, list of all sections with the current one highlighted in solid white + bold (the `progress` preset; alternatives below).
- **Normal frame:** white background, frame title in Chalmers Purple, slim purple rule above the footer, footer in 7 pt purple.
- **Footer (normal frames):** `<date> | <short title> | <slide number>` separated by `\hfill`.

---

## Command reference

### Metadata

| Command | Purpose |
|---------|---------|
| `\title{...}`           | Main title (used by `\titleframe`). |
| `\subtitle{...}`        | Optional subtitle on the cover. |
| `\author{...}`          | Author name(s). |
| `\institute{...}`       | Department / affiliation. |
| `\date{...}`            | Date string — ISO 8601 (`2026-05-22`) recommended. |
| `\shorttitle{...}`      | Shorter title shown in the footer (optional; defaults to `\title`). |

### Theme switches (preamble, after `\usetheme{Chalmers}`)

| Command | Effect |
|---------|--------|
| `\chalmersheadline{<key>}`        | Logo style on every slide. Keys: `logo` (default), `word`, `logo+word`, `logo+word+sub`. |
| `\chalmerssectiondividers{<key>}` | Section-divider style. Keys: `progress` (default), `solid`, `none`. |
| `\chalmersoutline{<key>}`         | Whether `\outlineframe` renders. Keys: `show` (default), `hide`. |
| `\chalmersfooterpages{<key>}`     | Page-number format. Keys: `current` (default — "5"), `both` ("5 / 20"). |

### Frame helpers

| Command | What it does |
|---------|--------------|
| `\titleframe`             | Renders the purple cover slide (call once). |
| `\outlineframe`           | Renders an outline frame with `\tableofcontents`. Becomes a no-op under `\chalmersoutline{hide}`. |
| `\section{Name}`          | Inserts the configured section divider, then begins the section. |
| `\begin{frame}{Title}...` | Standard content frame (white, purple title). |
| `\begin{chalmerscover}...`| Custom purple-bg frame with the white logo top-right — for closing slides, hand-crafted dividers, etc. |

### Block environments

| Environment | Title colour | Body colour |
|-------------|--------------|-------------|
| `block`        | Chalmers Purple | `ChalmersCream`     |
| `alertblock`   | Chalmers Red    | `ChalmersRed!8`     |
| `exampleblock` | Chalmers Green  | `ChalmersGreen!8`   |

---

## Headline logo style

Pick the style once in the preamble:

```latex
\chalmersheadline{logo}            % avancez emblem only       (DEFAULT)
\chalmersheadline{word}            % CHALMERS wordmark only
\chalmersheadline{logo+word}       % avancez + CHALMERS (compact)
\chalmersheadline{logo+word+sub}   % avancez + CHALMERS + UNIV. OF TECH.
```

| Style | What it looks like | When to use |
|-------|--------------------|-------------|
| `logo`          | Just the avancez emblem (round seal)            | **Default** — most visual, most compact, leaves the most body height for content |
| `word`          | Bold purple "CHALMERS" only                     | Dense data slides, minimal brand presence |
| `logo+word`     | Avancez emblem + "CHALMERS" (no subtitle)       | Mid-formality; recognisable wordmark next to the seal |
| `logo+word+sub` | Full logo + "UNIVERSITY OF TECHNOLOGY" subtitle | Formal / external audiences who don't already know the brand |

The colour adapts automatically: purple on light frames, white on the cover, section dividers, and any custom `chalmerscover` frame. You never need to specify the colour by hand. A 12 mm headline band is reserved regardless of style so the frame title always lands at the same vertical position.

---

## Section dividers

Every `\section{...}` triggers a divider slide. Three presets:

```latex
\chalmerssectiondividers{progress}   % DEFAULT — list of all sections, current one
                                     % in big bold solid white, others smaller and dim
\chalmerssectiondividers{solid}      % purple full-bleed, current section name centred
\chalmerssectiondividers{none}       % disable section dividers entirely
```

For a fully custom divider, redefine `\AtBeginSection` in your `.tex` file after `\usetheme{Chalmers}` — your definition overrides the active preset.

Implementation note: the `progress` preset reads the `.toc` file directly with a custom `\beamer@sectionintoc` redefinition. This side-steps a Beamer quirk where `\tableofcontents` called from `\AtBeginSection` can silently drop the current section.

---

## Outline frame

`\outlineframe` renders a Beamer frame with `\tableofcontents`. Use `\chalmersoutline{hide}` in the preamble to make it a no-op without removing the call from your `.tex`. Convenient when you want to keep the same source file but drop the outline for a short talk.

If you want a per-section progress outline inserted between sections, the standard Beamer idiom still works:

```latex
\section{Methods}
\begin{frame}{Outline}
    \tableofcontents[currentsection, hideallsubsections]
\end{frame}
% ... section content
```

---

## Footer

The default footer is:

```text
<date>          <short title>          <slide number>
```

Toggle the slide-number format with `\chalmersfooterpages`:

```latex
\chalmersfooterpages{current}   % "5"        (default)
\chalmersfooterpages{both}      % "5 / 20"   (current / total)
```

For a fully custom footer, redefine the `footline` template after `\usetheme{Chalmers}`:

```latex
\setbeamertemplate{footline}{%
    \usebeamercolor[fg]{footline}\usebeamerfont{footline}%
    \vspace{1mm}%
    \hbox to \paperwidth{\hspace{8mm}\insertdate%
        \hfill\insertshorttitle@chalmers%
        \hfill Slide \Chalmersinsertpagenumber%
        \hspace{8mm}}%
    \vspace{1mm}%
}
```

Available macros inside the template: `\insertdate`, `\insertshorttitle@chalmers`, `\insertframenumber`, `\inserttotalframenumber`, `\Chalmersinsertpagenumber` (respects `\chalmersfooterpages`), `\insertauthor`, `\insertinstitute`, `\insertsection`, `\insertsubsection`.

---

## Custom cover / closing slides

The `chalmerscover` environment gives you a purple-background frame with the white logo in the same top-right corner as every other slide — no footer, no frame title. Drop in whatever content you want:

```latex
\begin{chalmerscover}
    \vfill
    \begin{center}
        {\color{white}\Huge\bfseries Thank you}\\[6mm]
        {\color{white}\Large Questions?}
    \end{center}
    \vfill
\end{chalmerscover}
```

Use it for the cover, closing slides, hand-crafted section dividers, "quote of the day" slides, etc. `\titleframe` itself is just the default layout wrapped in this environment, so you can fully replace the cover by writing your own `chalmerscover` block.

---

## Logos

The `logographics/` folder ships every official 2026 Chalmers logo asset in three colours. Four shape variants are available, in three colour variants each, plus the plain wordmark.

| Shape variant | Avancez emblem | "CHALMERS" | "UNIVERSITY OF TECHNOLOGY" | Layout |
|---------------|:--------------:|:----------:|:--------------------------:|--------|
| `logo`           | yes | yes | yes | horizontal |
| `logo-horiz`     | yes | yes | no  | horizontal |
| `logo-vert`      | yes | yes | no  | vertical   |
| `logo-vert-full` | yes | yes | yes | vertical   |
| `wordmark`       | no  | yes | no  | text-only  |
| (`emblem`)       | yes | no  | no  | square     |

| Colour variant | Use on |
|----------------|--------|
| `purple` | Light / white slides |
| `white`  | Purple / dark slides (cover, section dividers, thank-you) |
| `black`  | Monochrome / print, posters |

> **Note on terminology.** The `\chalmersheadline` key `logo` corresponds to the standalone *emblem* — that is the most compact mark and the default for normal slides. The PNG-naming family `Chalmers-logo-*.png` refers to the horizontal combined logo (emblem + CHALMERS + subtitle). The two namespaces overlap by name but are kept distinct in code: see the dispatcher in `beamerthemeChalmers.sty` §7.

### Placing a logo manually

```latex
\chalmerslogo{<variant>}{<colour>}{<height>}
```

`<variant>` is one of `logo`, `logo-horiz`, `logo-vert`, `logo-vert-full`, `wordmark`, `emblem`. `<colour>` is one of `purple`, `white`, `black`. `<height>` is any LaTeX length.

```latex
\chalmerslogo{logo}{purple}{12mm}            % horizontal full logo, purple
\chalmerslogo{logo-vert-full}{white}{30mm}   % big vertical logo for a dark splash
\chalmerslogo{emblem}{black}{14mm}           % standalone avancez emblem
\chalmerslogo{wordmark}{black}{6mm}          % compact monochrome wordmark
```

The theme also pre-declares `ChalmersLogo`, `ChalmersLogoWhite`, `ChalmersLogoHoriz`, `ChalmersLogoVert`, `ChalmersLogoVertFull`, `ChalmersWordmark`, `ChalmersEmblem` (and their `White` / `Black` variants) via `\pgfdeclareimage` for use with `\pgfuseimage`.

> The Chalmers brand reserves the avancez-emblem variants for *formal, academic, and ceremonial* contexts — exactly what academic presentations are. The plain `wordmark` is a good choice if you want a less prominent mark on dense data slides.

---

## Speaker notes

Add notes with `\note{...}` inside a frame:

```latex
\begin{frame}{Some content}
    Slide content here.
    \note{Hidden speaker note for the presenter view.}
\end{frame}
```

Enable notes in the preamble:

| Setting | Result |
|---------|--------|
| `\setbeameroption{hide notes}`                       | (default) no notes in the PDF |
| `\setbeameroption{show notes}`                       | notes interleaved with slides |
| `\setbeameroption{show notes on second screen=right}`| presenter view (handout + notes) |

---

## Customisation

### Override a colour

```latex
\definecolor{ChalmersPurple}{HTML}{332085}     % switch to the dark variant
\setbeamercolor{frametitle}{fg=ChalmersBlack}  % black frame titles
```

Place such redefinitions **after** `\usetheme{Chalmers}` so they override the theme defaults.

### Adjust a font

```latex
\setbeamerfont{frametitle}{family=\sffamily,series=\bfseries,size=\large}
```

### Add a partner / funder logo

Drop the partner's PNG into `logographics/` (or anywhere on the TeX path) and place it manually:

```latex
\pgfdeclareimage[height=8mm]{partnerlogo}{logographics/your-partner-logo}

\begin{frame}{...}
    \begin{tikzpicture}[remember picture,overlay]
        \node[anchor=north east,xshift=-50mm,yshift=-5mm]
            at (current page.north east) {\pgfuseimage{partnerlogo}};
    \end{tikzpicture}
    ...
\end{frame}
```

Tune `xshift` so the partner logo does not overlap the Chalmers headline logo in the top-right.

### Handout mode (printable PDF, no overlays)

```latex
\documentclass[aspectratio=169,handout]{beamer}
```

---

## Brand compliance

This template implements the publicly documented 2026 Chalmers visual identity (see the Chalmers intranet pages on *Graphic profile and logotypes* and *Chalmers presentations*). For ceremonial materials (theses, diplomas, official certificates), consult the Chalmers Brand Portal and your local communications officer — those contexts have additional requirements that this template does not encode.

Logo files in `logographics/` are taken from the official Chalmers download portal and are subject to the Chalmers brand-use guidelines. See `NOTICE` for details.

---

## Licence

This repository ships under a **dual-licence** model:

- **MIT licence** (see `LICENSE`) covers the LaTeX/Beamer code — the `.sty` file, the example `.tex`, and this `README.md`. You may use, modify, redistribute, and sublicense them with attribution.
- **Chalmers brand assets** (see `NOTICE`) — every PNG under `logographics/` (wordmark, avancez emblem, combined logos) is a trademark of Chalmers University of Technology. Those marks are **not** MIT-licensed; their use is governed by the Chalmers Brand Portal and the Chalmers brand guidelines. If you are not affiliated with Chalmers, swap them out for your own institution's marks before publishing.

For ceremonial or brand-critical materials, consult the Chalmers Brand Portal and your local communications officer.
