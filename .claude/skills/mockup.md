# Mock-up

Structured workflow for assembling a static HTML/Tailwind website mock-up from the brand's accumulated assets — strategy spec, approved copy, reference board, and design tokens. The heavy construction runs in a subagent; the consultant reviews the result with the client and iterates.

## When to Use

- All prior phases are complete: Brand DNA, web design strategy, copywriting, and reference gathering
- The client is ready to see their website take visual form
- A cloned reference exists and needs to be transformed into the client's brand

## Prerequisites

Before starting, verify these exist in `brands/<brand>/`:

| File | Source Phase | Required |
|---|---|---|
| `brand-dna.md` | `/discover-brand` | Yes |
| `web-design-strategy.md` | `/design-website` | Yes |
| `copy.md` | `/write-copy` | Yes |
| `references.md` | `/gather-references` | Recommended |
| `references/<domain>/` | `/gather-references` (clone) | Optional — enables clone-and-transform path |

If any required file is missing, redirect the client to the appropriate phase.

## Context Window Strategy

Mock-up construction is the most I/O-intensive phase — generating multiple HTML files, searching for and downloading images, writing CSS. **All construction happens in a subagent.** The consultant's main thread stays lightweight:

```
Main thread (consultant + client):         Subagent (builder):
┌──────────────────────────────────┐       ┌─────────────────────────────────┐
│ Brief the subagent with specs    │──────>│ Read all brand assets           │
│ Wait for build                   │       │ Search & download stock images  │
│ Serve mock-up (http-server)      │       │ Build HTML/Tailwind pages       │
│ Show key screenshots to client   │<──────│ Save to brands/<brand>/mock-up/ │
│ Discuss, note revisions          │       └─────────────────────────────────┘
│ Dispatch revision subagent       │──────>│ Apply revisions                 │
│ Review again                     │<──────│ Save updated files              │
│ Repeat until approved            │       └─────────────────────────────────┘
└──────────────────────────────────┘
```

## Two Build Paths

### Path A — Clone and Transform

If a cloned reference exists at `brands/<brand>/references/<domain>/`:

1. Copy the clone to `brands/<brand>/mock-up/` as the starting point
2. Apply the client's design tokens (colors, typography, spacing)
3. Replace all copy with approved text from `copy.md`
4. Replace imagery with sourced stock images matching Brand DNA visual codes
5. Add/remove sections per the `modifications_needed` in `references.md`
6. Adjust components (booking widgets, navigation, forms) per strategy spec

This typically produces a ~70% complete mock-up in the first pass.

### Path B — Build from Scratch

If no clone exists:

1. Create the HTML/Tailwind project structure in `brands/<brand>/mock-up/`
2. Build each page section by section, following the strategy spec's page specifications
3. Apply design tokens throughout
4. Insert approved copy from `copy.md`
5. Source and place stock imagery for each section
6. Build navigation, footer, and shared components

## The Mock-up Process

### Step 1 — Prepare the Brief (Main Thread)

Before dispatching the build subagent, gather any final input from the client:

- "We're ready to build your mock-up. Before I start, is there anything from the reference gathering that you want me to prioritize or any last thoughts on how the site should feel?"
- Confirm the primary CTA placement and language
- Confirm any imagery preferences not already captured ("Do you have any photos of your own space or practice you'd like included?")

If the client provides their own photos, save them to `brands/<brand>/mock-up/images/client/`.

### Step 2 — Dispatch Build Subagent

Dispatch a subagent with the full build brief (see Subagent Dispatch Pattern below). The subagent reads all brand assets and produces the complete mock-up.

### Step 3 — Review with Client (Main Thread)

When the build subagent completes:

1. **Serve the mock-up locally:**
   ```bash
   npx http-server brands/<brand>/mock-up/ -p 8080 -o
   ```
   Tell the client to open `http://localhost:8080` in their browser.

2. **Take key screenshots** for in-conversation discussion if the client can't view the browser:
   ```bash
   npx playwright screenshot --full-page "http://localhost:8080" brands/<brand>/mock-up/review/homepage-full.png
   npx playwright screenshot "http://localhost:8080" brands/<brand>/mock-up/review/homepage-viewport.png
   ```

3. **Walk through page by page** with the client:
   - "Here's the homepage. Does this feel like your brand?"
   - "Let's look at the hero — does the headline land right? Does the image set the right tone?"
   - "How does the flow feel as you scroll down?"
   - "Let's check the about page, services, booking..."

4. **Capture revision notes** — specific, actionable feedback:
   - "The hero image is too busy — I want something calmer"
   - "The green is too bright — more muted, like sage"
   - "Move the testimonials above the services section"
   - "The font feels too formal — something warmer"

### Step 4 — Iterate (Main Thread + Subagent)

For each round of revisions:

1. Compile the client's feedback into a specific revision list
2. Dispatch a revision subagent with the list (see below)
3. Review the updated mock-up with the client
4. Repeat until the client approves

Keep revision rounds focused — 3-5 changes per round is more effective than a 20-item list.

## Subagent Dispatch Patterns

### Initial Build Subagent

```
Dispatch a subagent with this prompt:

"Build a static HTML/Tailwind website mock-up for [brand name].

Output directory: brands/<brand>/mock-up/

Read these files for complete context:
- brands/<brand>/brand-dna.md (voice, values, visual codes, design rules)
- brands/<brand>/web-design-strategy.md (page specs, design tokens, architecture)
- brands/<brand>/copy.md (approved copy for every section)
- brands/<brand>/references.md (reference board with adopt/avoid guidance)
[If clone exists:]
- brands/<brand>/references/<domain>/ (cloned reference — start from this)
- brands/<brand>/references/<domain>/clone-notes.md (what maps where)

## Build Instructions

### Project Structure
Create this structure in brands/<brand>/mock-up/:
```
index.html              # Homepage
about.html              # About page
services.html           # Services overview (or individual service pages)
contact.html            # Contact/booking page
[additional pages per strategy spec]
css/
  style.css             # Custom styles beyond Tailwind
images/
  [sourced stock images]
  client/               # Client-provided photos (if any)
  attribution.md        # Image source attribution
review/                 # Screenshots for review (generated after build)
```

### Technology
- Use Tailwind CSS via CDN link (no build step needed for mock-up)
- Semantic HTML5 structure (nav, main, section, footer)
- Mobile-responsive (Tailwind responsive classes)
- No JavaScript required — this is a visual mock-up, not a functional site

### Design Direction
The web design strategy provides direction, not a paint-by-numbers spec.
Use the strategy's visual codes, color mood, typography choices, and spacing
philosophy as your guide — but make informed creative decisions within that
direction. Choose specific hex values, spacing values, and visual treatments
that serve the brand's described feeling.
- Color: use the palette direction and mood from the strategy (e.g., "luminous sky blue,
  aqua, opalescent white") to select specific hex values that achieve the intended feeling
- Typography: use the specified typefaces (load from Google Fonts CDN)
- Spacing: follow the density philosophy described (e.g., "Sanctuary density — generous,
  meditative") and choose specific values that feel right
- Shape: choose border-radius, edge treatments, and visual effects (e.g., glassmorphism)
  that align with the brand's described spatial feeling
- Motion: CSS transitions per the motion philosophy (for hover states)

### Copy
Insert the approved copy from copy.md exactly as written. Do not rewrite,
summarize, or paraphrase. The copy has been through a client approval process.
- Headlines → <h1>, <h2> elements
- Body text → <p> elements
- CTA labels → <a> or <button> elements
- If copy.md doesn't cover microcopy (form labels, nav items, footer text),
  write it in the brand voice described in copy.md's voice reference section.

### Images
For each section that needs imagery:
1. Read the Brand DNA visual codes for imagery direction (subjects, mood, lighting)
2. Read the photography direction from references.md mock-up guidance
3. Use WebSearch to find appropriate stock images:
   - Search Unsplash: '[mood] [subject] unsplash' (e.g., 'warm natural light massage room unsplash')
   - Search Pexels: '[mood] [subject] pexels'
   - Prefer images that match the brand's color palette and spatial feeling
4. Use WebFetch to get the direct image URL from the search results
5. Download the image using curl/wget to brands/<brand>/mock-up/images/
6. Use images that fit the section's purpose:
   - Hero: wide landscape, atmospheric, sets emotional tone
   - About: practitioner portrait or workspace (use client photo if provided)
   - Services: modality-specific imagery
   - Testimonials: subtle texture or nature background
7. Record each image source in brands/<brand>/mock-up/images/attribution.md:
   - Image filename
   - Source URL
   - Photographer credit
   - License (Unsplash/Pexels are free for commercial use)

### Structure
[If clone path:] Start from the cloned reference. Follow the modifications_needed
checklist in references.md. Keep the clone's layout structure where it aligns with
the strategy spec. Add/remove sections as specified.

[If scratch path:] Build each page following the page specifications in
web-design-strategy.md. Each page has defined sections with purpose, content,
and visual direction.

### Shared Components
Build these once and include in every page:
- Navigation (per strategy spec: links, logo placement, utility items)
- Footer (per strategy spec: columns, newsletter, social, legal)
- CTA sections (reusable call-to-action blocks)

### Visual Inspection Loop

**Critical:** Do not build blind. Use an iterative render-inspect-adjust cycle
to verify that your design choices actually achieve the intended feeling.
Writing HTML/CSS without seeing the result is guessing. Seeing is designing.

**Process:**

1. **Build the homepage first** — get it to a complete state
2. **Serve it locally:**
   ```bash
   npx http-server brands/<brand>/mock-up/ -p 8080 &
   ```
3. **Screenshot with Playwright:**
   ```bash
   npx playwright screenshot 'http://localhost:8080' 'brands/<brand>/mock-up/review/homepage-viewport.png'
   npx playwright screenshot --full-page 'http://localhost:8080' 'brands/<brand>/mock-up/review/homepage-full.png'
   npx playwright screenshot --viewport-size='375,812' 'http://localhost:8080' 'brands/<brand>/mock-up/review/homepage-mobile.png'
   ```
4. **Read and evaluate the screenshots** — compare against the Brand DNA visual codes:
   - Does the color palette feel luminous/earthy/clinical/whatever the direction specifies?
   - Does the spacing feel generous enough? Too tight? Too sparse?
   - Does the typography hierarchy read clearly?
   - Does the overall composition feel harmonious?
   - Does this pass the "squint test" — at arm's length, does the rhythm feel right?
5. **Adjust and re-screenshot** — iterate until the homepage meets the brand direction
6. **Then build remaining pages** using the homepage as the established standard
7. **Screenshot each page** for review — catch inconsistencies across pages

**Repeat the inspect-adjust cycle for each page.** The review/ directory should
contain viewport, full-page, and mobile screenshots of every page by the time
the build is complete.

**Kill the server when done:**
```bash
kill $(lsof -t -i:8080) 2>/dev/null
```

### Quality Checks
Before finishing:
- [ ] All pages render cleanly at desktop (1440px) and mobile (375px) widths
- [ ] All copy from copy.md is placed — no lorem ipsum anywhere
- [ ] All images are downloaded and display (no broken images)
- [ ] Color choices serve the brand's described mood and feeling
- [ ] Specified typefaces are loaded and rendering correctly
- [ ] Primary CTA is prominent and consistent across pages
- [ ] Navigation works (links between pages use relative paths)
- [ ] Visual inspection screenshots exist for every page in review/
- [ ] The site can be served with 'npx http-server brands/<brand>/mock-up/'

Write a build summary to brands/<brand>/mock-up/build-notes.md:
- What was built (pages, sections)
- Which images were sourced and from where
- Design decisions made: specific hex values chosen, spacing values, visual effects
- What the visual inspection revealed and what was adjusted
- Any open questions or areas where the strategy was ambiguous
- Suggestions for the client review"
```

### Revision Subagent

```
Dispatch a subagent with this prompt:

"Apply revisions to the website mock-up at brands/<brand>/mock-up/.

Read brands/<brand>/mock-up/build-notes.md for context on the current state.

Revisions requested by the client:
[list specific revisions, e.g.:]
- Hero image: replace with something calmer — current image is too busy.
  Search for 'serene nature morning light soft' on Unsplash.
- Green accent color: change from #4CAF50 to #A8B5A0 (more muted sage)
  throughout all pages
- Move testimonials section above services section on homepage
- Heading font: switch from Playfair Display to Cormorant Garamond
- Add more whitespace between sections — increase section gap from 64px to 96px

Apply each revision across all affected pages. Maintain consistency.

Update brands/<brand>/mock-up/build-notes.md with what was changed.
Update brands/<brand>/mock-up/images/attribution.md if images were swapped."
```

## Output Structure

The mock-up lives at `brands/<brand>/mock-up/`:

```
brands/<brand>/mock-up/
├── index.html              # Homepage
├── about.html              # About page
├── services.html           # Services (or per-service pages)
├── contact.html            # Contact / booking
├── [additional pages]
├── css/
│   └── style.css           # Custom styles beyond Tailwind
├── images/
│   ├── hero.jpg
│   ├── about-portrait.jpg
│   ├── [section images]
│   ├── client/             # Client-provided photos
│   └── attribution.md      # Image sources and credits
├── review/
│   ├── homepage-full.png   # Screenshots for in-conversation review
│   └── homepage-viewport.png
└── build-notes.md          # Build log, decisions, open questions
```

Serve with: `npx http-server brands/<brand>/mock-up/ -p 8080`

## Writing Guidelines

- The mock-up is a visual artifact, not production code — prioritize appearance over engineering
- Use Tailwind utility classes for speed; custom CSS only where Tailwind can't express the design
- Design decisions should be grounded in the strategy's direction and the Brand DNA's visual codes — creative interpretation within the established direction, not arbitrary invention
- Images should feel intentional, not decorative — each image serves the section's purpose
- The mock-up should pass the "squint test" — viewed at arm's length, does the overall color, density, and rhythm feel like the brand?
- **Visual inspection is not optional.** The render-inspect-adjust cycle is the core quality mechanism. Never deliver a mock-up you haven't seen rendered in a browser via Playwright screenshots.

## Integration with Final Build

The approved mock-up becomes the visual specification for the final build phase. Check `research/<industry>/tech-stack.md` for the recommended production stack (e.g., Astro + Cloudflare Pages + Cal.com + Decap CMS for healing practitioners).

The final build converts the mock-up into a production site:

- **HTML structure** → Astro components (`.astro` files)
- **Tailwind CDN** → `@astrojs/tailwind` integration (build-time CSS)
- **Copy** → structured content files (YAML/Markdown) editable via CMS
- **Images** → placeholders until professional brand photography is produced (or remain if stock is acceptable)
- **Scheduling** → Cal.com embed (or equivalent) replacing placeholder booking sections
- **build-notes.md** documents every interpretive decision for the developer

The mock-up at `brands/<brand>/mock-up/` should be preserved as a visual reference even after the final build is complete.
