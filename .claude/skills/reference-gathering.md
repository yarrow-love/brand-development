# Reference Gathering

Structured workflow for discovering, capturing, and discussing competitor and inspiration websites with the client. The consultant drives the conversation in the main thread while dispatching subagents to handle the expensive I/O (searching, fetching, screenshotting) — preserving context window for the phases that follow.

## When to Use

- After copywriting is complete and before mock-up begins
- The client wants to explore what competitors or peers are doing
- The client struggles to articulate visual preferences without concrete examples
- The web design strategy named reference/anti-reference sites that haven't been visually examined

## Prerequisites

**Web design strategy must exist.** The strategy spec defines the brand's archetype, visual direction, and competitive positioning — these guide which sites to search for and how to evaluate them.

Before starting, verify:
1. Web design strategy exists at `brands/<brand>/web-design-strategy.md`
2. Brand DNA exists at `brands/<brand>/brand-dna.md`

The copywriting phase should ideally be complete too (`brands/<brand>/copy.md`), so references can be evaluated against the brand's established voice as well as its visual identity.

## Context

**Web design strategy:** Read `brands/<brand>/web-design-strategy.md` for:
- `architecture.archetype` — the site archetype guides which competitors are relevant
- `competitive.references` — any sites already named during the strategy consultation
- `tokens` — established design tokens to compare against
- `design_rules.never` — constraints that disqualify certain reference patterns

**Brand DNA:** Read `brands/<brand>/brand-dna.md` for:
- `positioning.competitors` — competitor brands named during discovery
- `visual_codes` — the established visual language to evaluate references against
- `design_rules` — always/never constraints

**Industry research:** Check `research/<industry>/web-design.md` for archetype patterns and case studies that suggest sites worth examining.

**Existing references:** Check `brands/<brand>/references/` for any previously captured references.

## Context Window Strategy

Reference gathering involves heavy I/O (web searches, page fetches, screenshot captures) that would rapidly consume the consultant's context window — context needed for the mock-up phase that follows. The solution: **delegate I/O to subagents, keep the conversation in the main thread.**

```
Main thread (consultant + client):     Subagents (disposable):
┌─────────────────────────────┐        ┌──────────────────────────┐
│ Ask client about competitors │───────>│ Search, fetch, screenshot │
│ Wait for results             │<───────│ Save to references/       │
│ Show ONE screenshot at a time│        │ Write summary to file     │
│ Discuss with client          │        └──────────────────────────┘
│ Show next screenshot         │
│ ...                          │
│ Synthesize reference board   │
└─────────────────────────────┘
```

**What stays in the main thread:** Client conversation, reactions, synthesis — lightweight text.
**What goes to subagents:** WebSearch queries, WebFetch page content, Playwright screenshots — heavy payloads that would bloat context.

### Subagent Dispatch Pattern

**Discovery subagent** — finds and captures reference sites:

```
Dispatch a subagent with this prompt:

"Search for and capture reference websites for a [modality] practitioner brand.

Brand Identity Context (use this to guide your search and evaluate sites):
- Brand archetype: [from strategy, e.g., "Sanctuary"]
- Personality: [from DNA, e.g., "warm, grounded, unhurried"]
- Color palette: [from DNA visual codes, e.g., "sage green (#A8B5A0), warm cream (#F5F0EB), dusty rose (#C4A882)"]
- Typography direction: [from DNA, e.g., "serif headings, clean sans-serif body, warm and traditional"]
- Spatial feeling: [from DNA, e.g., "a sunlit room with plants, wooden surfaces, linen curtains"]
- Brand essence: [from DNA, e.g., "grounded gentle presence"]
- Positioning: [from DNA, e.g., "accessible but not casual, spiritual but not mystical"]
- Design rules — never: [from DNA/strategy, e.g., "never clinical, never neon, never dark backgrounds"]

Search Context:
- Competitors already named: [from DNA/strategy]
- Location: [if relevant]
- Sites the client mentioned: [any URLs from conversation]

Tasks:
1. Use WebSearch to find 8-10 candidate sites. When selecting, prioritize sites
   whose visual tone aligns with or meaningfully contrasts the brand identity above:
   - 3-4 direct competitors (same modality, similar market)
   - 3-4 aspirational references (any industry, matching the [archetype] archetype
     and the brand's tonal qualities — look for sites with similar color warmth,
     spacing philosophy, and emotional register)
   - 2-3 anti-references (sites that represent what this brand is NOT — useful for
     contrast, e.g., overly clinical, too dark, too corporate, too chaotic)
2. For each site, use Playwright CLI to capture:
   - Full-page screenshot: npx playwright screenshot --full-page '[url]' 'brands/<brand>/references/[slug]-full.png'
   - Viewport screenshot: npx playwright screenshot '[url]' 'brands/<brand>/references/[slug]-viewport.png'
3. For each site, use WebFetch to extract:
   - Homepage headline and subheadline
   - Navigation structure
   - Color palette (note dominant colors and how they compare to the brand's palette)
   - Typography choices (serif/sans-serif, weight, spacing)
   - Spacing density (generous/tight/moderate)
   - Whether booking/scheduling is visible and how it's presented
   - Photography style (authentic/stock, warm/cool, subjects)
4. Write a summary to brands/<brand>/references/capture-notes.md listing each site with:
   - URL
   - Category (competitor/aspirational/anti-reference)
   - Screenshot file paths
   - Why you selected it (how it relates to the brand identity context above)
   - Brief visual analysis: color, typography, spacing, photography, overall mood
   - How it compares to the brand's established visual direction

Do NOT display screenshots in your output — just save the files. The consultant will display them to the client one at a time."
```

**Additional capture subagent** — if the client names specific sites during discussion:

```
"Capture screenshots of [url]:
- Full-page: npx playwright screenshot --full-page '[url]' 'brands/<brand>/references/[slug]-full.png'
- Viewport: npx playwright screenshot '[url]' 'brands/<brand>/references/[slug]-viewport.png'
- Mobile: npx playwright screenshot --viewport-size='375,812' '[url]' 'brands/<brand>/references/[slug]-mobile.png'
Save files only. Do not display."
```

**Clone subagent** — when a reference site is identified as the closest structural match (see Step 3.5):

```
Dispatch a subagent with this prompt:

"Clone the front-end of [url] to produce an editable HTML reference for mock-up development.

Output directory: brands/<brand>/references/[domain]/
(e.g., brands/healing-roots/references/example.com/)

Use Playwright to extract the rendered page. Write a Node.js script to:

1. Launch a headless browser and navigate to [url]
2. Wait for the page to fully render (networkidle)
3. Extract the full rendered DOM via page.content()
4. Extract all computed stylesheets:
   - Inline <style> blocks (already in the HTML)
   - External stylesheets: fetch each via page.evaluate or direct HTTP request,
     save to [domain]/css/[filename].css, update <link> hrefs to relative paths
5. Extract key assets:
   - Images used in the layout (backgrounds, icons, logos): save to [domain]/images/
   - Update src/url references to relative paths
   - Skip large hero/photography images — these will be replaced with the client's imagery
6. Save the complete HTML to [domain]/index.html
7. Do the same for key subpages if specified: [list pages, e.g., /about, /services]

Post-processing:
- Remove all <script> tags (JavaScript not needed for a static mock-up reference)
- Remove analytics, tracking pixels, cookie banners, chat widgets
- Remove third-party embeds (social feeds, maps) — leave a placeholder comment
- Ensure all asset paths are relative so the page renders when served locally
- Add a comment at the top of index.html:
  <!-- CLONED REFERENCE: [url] — [date] -->
  <!-- This is a structural reference for mock-up development. -->
  <!-- All content, imagery, and branding will be replaced. -->

Test: The cloned page should render recognizably when served with 'npx http-server brands/<brand>/references/[domain]/'
Some visual degradation is expected (web fonts may not load, JS-dependent
interactions won't work). What matters is that the layout structure, spacing,
color relationships, and section flow are preserved.

Write a brief summary to brands/<brand>/references/[domain]/clone-notes.md:
- What was captured successfully
- What degraded or was removed (JS interactions, third-party embeds, etc.)
- Which sections map to which parts of the client's web design strategy
- Suggestions for which elements to keep vs. replace during mock-up"
```

## The Gathering Process

### Step 1 — Seed the Search (Main Thread)

Gather search context from the client before dispatching:

- Ask: "Who are your closest competitors — practitioners doing similar work in your area?"
- Ask: "Whose website have you visited and thought 'I wish mine felt like that'? Doesn't have to be in your field."
- Ask: "Any websites you've seen that you absolutely don't want yours to resemble?"

Combine their answers with competitors from Brand DNA, references from web design strategy, and case studies from industry research.

**Dispatch the discovery subagent** with this combined list. While it runs, continue the conversation — discuss what qualities matter most, what the client imagines when they picture their ideal site.

### Step 2 — Present One at a Time (Main Thread)

When the subagent completes:

1. Read `brands/<brand>/references/capture-notes.md` for the summary
2. **Display one viewport screenshot at a time** using the Read tool — this shows the client the above-the-fold first impression without loading the full page into context
3. Ask for the client's gut reaction before showing more detail
4. If the client wants to see the full page, display the full-page screenshot
5. Move to the next site

**Key:** Only load one or two screenshots into context at a time. Previous images will naturally compress out of context as the conversation progresses. This is the core context-saving mechanism.

### Step 3 — Guided Discussion (Main Thread)

For each reference site, guide the client through these reactions:

**First impression (viewport screenshot):**
- "What's your gut reaction? Does this feel right or wrong for your brand?"
- "What's the first thing your eye lands on?"
- "What emotion does this site create in the first three seconds?"

**Structure and flow (full-page screenshot — only if client wants to go deeper):**
- "How does the page flow? Does the pacing feel right?"
- "What sections stand out? What feels unnecessary?"
- "How does this compare to the page structure we defined in your strategy?"

**Specific elements:**
- "What do you think of their color palette? Their typography?"
- "How does their about page / services page / booking flow work?"
- "What would you steal from this site? What would you reject?"

**Comparison to Brand DNA:**
- "Does this feel aligned with your brand values, or does it contradict them?"
- "Could your copy live on a site that looks like this?"
- "Where does this sit on the clinical-spiritual spectrum compared to where we placed your brand?"

If the client names additional sites during discussion, dispatch a quick capture subagent for those specific URLs.

### Step 3.5 — Clone the Closest Reference (Optional)

During discussion, one site may emerge as structurally closest to what the client wants — the right layout, the right pacing, the right feel, even if the colors, copy, and imagery are wrong. When this happens:

1. **Confirm with the client:** "This site's structure and flow seem very close to what we've defined for your brand. If I cloned its layout as a starting point, the mock-up could work from that structure and apply your design tokens, copy, and imagery — rather than building from scratch. Would you like to do that?"
2. **If yes, dispatch the clone subagent** (see Subagent Dispatch Pattern above). The clone saves to `brands/<brand>/references/<domain>/`.
3. **Continue the reference discussion** while the clone runs — it doesn't block the conversation.

**When to offer cloning:**
- The client says something like "I want my site to feel like this one"
- The site's section structure maps closely to the web design strategy's page specifications
- The site's spacing, density, and layout philosophy match the brand archetype

**When NOT to clone:**
- The client likes only one specific element (e.g., "I love their color palette but nothing else") — that's a note in the reference board, not a clone
- The site is highly JavaScript-dependent (single-page app, heavy animation framework) — the clone will be too degraded to be useful
- The client is drawn to the content/imagery but not the structure — the structure is what the clone provides

**What the clone produces:**
The cloned site at `brands/<brand>/references/<domain>/` is a static HTML snapshot — layout structure, spacing, color relationships, and section flow preserved. JavaScript is stripped, third-party embeds are removed, and large images are skipped (they'll be replaced anyway). It's an editable structural reference, not a pixel-perfect copy.

The mock-up phase can then start from this clone and apply:
- The client's design tokens (colors, typography, spacing from strategy)
- The client's approved copy (from `/write-copy`)
- The client's imagery (when available)
- Structural adjustments (add/remove sections per the strategy spec)

This typically gets the mock-up to ~70% in the first pass, versus building from a blank page.

### Step 4 — Synthesize into Reference Board (Main Thread)

After reviewing all sites, synthesize the findings:

1. **Identify patterns** — what did the client consistently respond to positively?
2. **Name the visual territory** — "Based on your reactions, your site lives in [description]"
3. **Extract specific elements** — concrete things to adopt or avoid
4. **Reconcile with strategy** — confirm or adjust design tokens based on what the client responded to
5. **Write the reference document**

## Output Format

Write the reference board to `brands/<brand>/references.md`:

```markdown
---
title: Reference Board
tags: [references, competitive, visual-direction]
last_updated: YYYY-MM-DD
brand: {brand-name}
---

# Reference Board — {Brand Name}

## Visual Territory

```yaml
summary: ""            # 2-3 sentences describing where the brand lives visually
archetype_confirmed: "" # confirmed or adjusted from strategy
key_qualities: []      # 3-5 qualities the client consistently responded to
```

## Reference Sites

### {Site Name}
```yaml
url: ""
category: ""           # competitor | aspirational | anti-reference
screenshots:
  viewport: ""         # path to viewport screenshot
  full_page: ""        # path to full-page screenshot
  mobile: ""           # path to mobile screenshot (if captured)
first_impression: ""   # client's gut reaction, in their words
what_works: []         # specific elements to adopt
what_doesnt: []        # specific elements to reject
specific_elements:
  color: ""            # client's reaction to their palette
  typography: ""       # client's reaction to their type
  layout: ""           # client's reaction to their structure
  photography: ""      # client's reaction to their imagery
  booking_flow: ""     # if applicable
relevance_to_brand: "" # how this relates to established Brand DNA
```

## Anti-Patterns Identified

```yaml
patterns: []           # things the client rejected across multiple sites
```

## Design Direction Refinements

```yaml
confirmed: []          # design decisions from strategy that references validated
adjusted: []           # decisions that should shift based on reference reactions
new_insights: []       # things that emerged from seeing real examples
token_updates: {}      # any design token adjustments suggested by the reference review
```

## Mock-up Guidance

```yaml
adopt: []              # "use [element] from [site] because [reason]"
avoid: []              # "never do [element] — client rejected it on [site] because [reason]"
open_questions: []     # things to test in mock-up, informed by reference reactions
```

## Cloned Reference (if applicable)

```yaml
source_url: ""         # the site that was cloned
clone_path: ""         # e.g., brands/<brand>/references/example.com/
clone_rationale: ""    # why this site was chosen as the structural starting point
pages_cloned: []       # which pages were captured (index, about, services, etc.)
structural_alignment:  # how the clone maps to the web design strategy
  matching_sections: [] # sections in the clone that correspond to strategy spec
  sections_to_add: []  # sections in strategy not present in clone
  sections_to_remove: [] # sections in clone not needed
modifications_needed:
  tokens: ""           # "apply client's color palette, typography, spacing"
  copy: ""             # "replace all text with approved copy from copy.md"
  imagery: ""          # "replace all photography with client's brand imagery"
  structure: ""        # specific layout changes needed
  components: ""       # booking widget, forms, navigation adjustments
```
```

### Writing Guidelines

- Capture the client's own words when describing reactions — "it feels cold" is more useful than "the client found the aesthetic uninviting"
- Be specific about elements — "their hero section uses a full-bleed video with no text overlay" not "their hero is nice"
- The `mock_up_guidance` section is the most operationally important — it translates reactions into direct instructions for the mock-up phase
- Always note the screenshot file paths so the mock-up agent can re-examine specific references

## Integration with Mock-up Phase

The reference board becomes a companion document to the web design strategy during mock-up:

- **Positive references** show the mock-up agent concrete examples of what the client approved — "make the hero feel like [site]'s hero but with our color palette"
- **Anti-references** prevent the mock-up agent from making plausible-but-wrong decisions — "never use a navigation style like [site]"
- **Screenshots** can be re-examined during mock-up iteration to diagnose misalignment
- **Design direction refinements** may update tokens from the strategy spec

**If a clone exists**, the mock-up phase changes fundamentally:

- **Without clone:** Mock-up agent builds from scratch using strategy spec + copy + design tokens. Creative but slower, more iteration needed.
- **With clone:** Mock-up agent starts from `brands/<brand>/references/<domain>/`, applies the client's tokens, inserts approved copy, replaces imagery, and adjusts structure per the `cloned_reference` section of `references.md`. Faster, more predictable, less invention risk.

The `modifications_needed` section in the reference board gives the mock-up agent a concrete transformation checklist rather than an open-ended brief.

The reference board at `brands/<brand>/references.md` should be read alongside the web design strategy and copy when producing mock-ups.
