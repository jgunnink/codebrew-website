# Code Brew Studio | Design System & Style Guide

## 1. Core Identity & Concept

**Aesthetic:** Architectural Brutalism / Engineered Editorial
**Concept:** A "Living System" & "Skin in the game"
**Vibe:** Premium, raw, deeply technical, and strictly anti-template.

The Code Brew Studio brand positions you as a boutique, high-end technical consultancy. The design language actively avoids the soft,
generic, "cookie-cutter" tech look (no drop shadows, no frosted glass, no bubbly shapes, no generic 3D tech illustrations).

Instead, it relies on strict structural grid lines, massive typography, stark negative space, and abstract geometry. It is designed to look
like a raw, running architectural blueprint or an editorial feature in a high-end engineering magazine. It signals that you are a serious
engineer who understands deep structural systems and scalability.

---

## 2. Color Palette

The site uses a strict "Subdued Light Theme." It relies on high contrast between the background and text, using visible grid lines to create structure, and exactly _one_ accent color to draw the eye without overwhelming the layout.

| Color Name           | Hex Code  | CSS Variable      | Usage                                                                                                                              |
| :------------------- | :-------- | :---------------- | :--------------------------------------------------------------------------------------------------------------------------------- |
| **Bone / Off-White** | `#F4F3EF` | `--bg`            | The primary canvas. Warm enough to reduce eye strain, stark enough to feel like high-quality drafting paper.                       |
| **Heavy Charcoal**   | `#1C1B1A` | `--text`          | Primary text, heavy headings, buttons, and solid blocks. Avoid absolute black (`#000000`) to prevent harsh screen glare.           |
| **Blueprint Grey**   | `#C8C6BC` | `--border`        | Used strictly for the `1px solid` structural grid lines that map out the page architecture.                                        |
| **Muted Rust**       | `#B85038` | `--accent`        | A subtle nod to the "Brew" (coffee/heat). Used sparingly for hover states, critical CTAs, Beta badges, and pulsing SVG data nodes. |
| **Warm Grey**        | `#EBEAE4` | `--hover`         | Used for card hover states, visual containers, and massive CTA backgrounds to create depth without using shadows.                  |
| **Image Base**       | `#D9D8D0` | `N/A`             | The required background color placed strictly behind grayscale portraits for CSS blending.                                         |
| **Softened Text**    | `#444`    | `--softened-text` | Paragraph text, often softened to contrast with the heavy charcoal headings.                                                       |

---

## 3. Typography System

The typography hierarchy relies on extreme contrast: massive, brutalist headings paired with highly legible body copy and technical
monospace accents. All fonts are served via Google Fonts.

### 1. Primary Display (Headings)

- **Font:** `Space Grotesk`
- **Weights:** 500 (Medium), 700 (Bold)
- **Styling:** ALWAYS `text-transform: uppercase`. Tightly tracked (`letter-spacing: -0.04em`) and compressed line height
  (`line-height: 0.95`).
- **Usage:** `h1`, `h2`, `h3`, massive CTA text, and the Brand Logo. It should feel like massive concrete blocks of text.

### 2. Body Copy

- **Font:** `Inter`
- **Weights:** 400 (Regular), 500 (Medium)
- **Styling:** Standard sentence case. Generous line height (`line-height: 1.6`) for maximum readability. Max-width on paragraphs should
  ideally not exceed `700px` to maintain optimal reading lengths.
- **Usage:** `<p>`, general descriptions, long-form copy. Often softened to `#444` to contrast with the heavy charcoal headings.

### 3. Technical Accents (Metadata)

- **Font:** `Space Mono`
- **Weights:** 400 (Regular)
- **Styling:** ALWAYS `text-transform: uppercase`. Wide tracking (`letter-spacing: 0.05em`) and small font size (`0.75rem`).
- **Usage:** `.mono` class. Grid coordinates (`[ 01 ] INFRA`), navigation links, badges, and system outputs. It grounds the site in a
  terminal/code aesthetic.

---

## 4. Layout & Architecture (The Grid)

The layout relies on native CSS Grid and Flexbox to create a literal "blueprint" on the screen.

- **The Container:** The main content is capped at `max-width: 1600px` and centered horizontally. It is flanked by left and right borders so
  the site looks like a physical document sitting on a desk.
- **Visible Borders:** Elements do not "float." They are separated by explicit borders (`border-bottom`, `border-right`) matching the
  `--border` color. There are no invisible margins separating major sections; everything touches a physical grid line.
- **Asymmetry:** Grids are rarely 50/50. They are usually `1.2fr 0.8fr` (or vice versa) to create an editorial, magazine-like tension.
- **Fluid Padding:** Negative space is a premium asset. Elements sit strictly within their border-defined grid cells, utilizing massive
  viewport-based padding (e.g., `8vw 2.5rem`) to let the heavy typography breathe on large monitors.
- **Sharp Edges Only:** `border-radius: 0;` across the board. The only exception is small, pill-shaped `.badge` elements.

---

## 5. Visual Assets & Imagery

### The "Moody Portrait" Execution

To prevent standard full-color corporate photos from ruining the brutalist aesthetic, all human photography must be processed via CSS to
look like a raw, grayscale magazine print.

**The CSS Formula:**

```css
.portrait-wrap {
  background: #d9d8d0; /* Required base color */
}
.portrait-img {
  filter: grayscale(100%) contrast(140%) brightness(0.9);
  mix-blend-mode: multiply; /* Blends the shadows directly into the background */
}
```

### Abstract Wireframes (SVGs)

Instead of uploading actual UI screenshots (which date quickly and cause clients to fixate on the wrong details), use abstract geometric
SVGs. This forces the client to imagine _systems_ rather than scrutinizing specific UI elements.

- Drawn using simple `<rect>`, `<circle>`, `<line>`, and `<polygon>` elements.
- Strokes are strictly `0.5px`, `1px` or `2px`.
- Colors are strictly limited to `--text`, `--border`, and `--accent`.

---

## 6. Motion & Interaction (The "Living System")

Motion is deliberate, slow, and continuous. It should give the impression of a powerful server running quietly in the background without
distracting the user from the copy. If it catches the eye instantly, it's too fast.

- **Marching Wires:** Moving dashed SVG lines to represent data flow.
- _CSS:_ `stroke-dasharray: 4 4; animation: dash 4s linear infinite;`

- **Pulsing Nodes:** Dots that slowly fade in and out to represent server/system health or recording states.
- _CSS:_ `animation: pulse 3s ease infinite;`

- **Slow Rotation:** Geometric shapes rotating on a massive loop.
- _CSS:_ `animation: rotate 30s linear infinite;`

- **Hover States:** Button hovers are instantaneous color inversions. Card hovers are a simple, instant background color shift to
  `var(--hover)`, grounding the interaction without using drop-shadows.

---

## 7. UI Component Library

### Buttons (`.btn`)

Buttons are massive, geometric, and text-heavy. Strict `0px` border-radius.

- **Primary:** Dark background (`var(--text)`), Light text (`var(--bg)`). Hover: Inverts to transparent background.
- **Outline (`.btn-outline`):** Transparent background, colored border. Hover: Fills with border color.
- **Massive CTA (`.btn-massive`):** Uses the `--accent` color to draw the eye at the end of the user journey. Larger typography (`1.5rem`)
  and padding.

### Badges (`.badge`)

Used to label the state of a project.

- _Styling:_ `border-radius: 50px; border: 1px solid; padding: 0.25rem 0.75rem;`
- **Live/Prod:** Charcoal border/text.
- **Early Access/Beta:** Rust (`--accent`) border/text to draw the eye to active development.

### Section Labels (`.section-label`)

Inverted bars (Charcoal background, Bone text) that span the width of the container to strictly divide major concepts. Features the title on
the left and a `.mono` numeric identifier on the right (e.g., `01 // SERVICES`).

---

## 8. Tone of Voice & Copywriting

When writing new pages, case studies, or blog posts, adhere to these voice guidelines:

- **Authoritative & Direct:** Cut the corporate fluff. Use short, punchy sentences. (e.g., "Enterprise-grade infrastructure. We don't just advise—we build.")
- **Show 'Skin in the Game':** Constantly reinforce that you are an engineer who writes code and deploys real products natively, not just an armchair advisor.
- **Technical but Pragmatic:** Use exact engineering terminology (GCP, CI/CD, Asynchronous, Low-latency) to signal competence to other
  engineers, but frame the _outcomes_ so business leaders understand the value (scale, reliability, high-availability).
- **Code as Punctuation:** Use technical syntax like double slashes `//` or brackets `[ ]` in small monospace text to frame sections (e.g.,
  `[ 01 ] INFRA`, `SYS.ARCH // CONSULTANCY`).
- **Avoid Clichés:** Never use words like "synergy," "digital transformation," or "innovative solutions." Stick to raw, undeniable
  capabilities.

---

## 9. Development Principles (For Future Pages)

If you add new pages (e.g., `/case-studies`), adhere strictly to this formula:

1. **Maintain the Grid:** Ensure the outer `.container` and `1px` internal borders remain continuous. Never break the grid.
2. **Zero Dependencies:** Stick to vanilla HTML and CSS Grid/Flexbox whenever possible. The speed, purity, and 100/100 Lighthouse score of
   the code is a testament to your engineering standards.
3. **Semantic HTML:** Use proper `<header>`, `<nav>`, `<section>`, and `<footer>` tags for accessibility and SEO.
4. **Mobile Breakdown:** On screens under `1024px`, collapse CSS Grids to `1fr` (single column), and swap `border-right` for `border-bottom`
   so the blueprint lines stack horizontally like a ladder.
