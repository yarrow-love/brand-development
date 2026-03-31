# Web Design Strategy

Structured consultation workflow for establishing a website's strategic foundation — purpose, audience, structure, and design direction — before any visual design or development work begins.

## When to Use

- A brand has completed Brand DNA and is ready to plan its website
- The client wants to build or redesign a brand website
- Before starting mock-up or development work on a web presence
- The client is discussing website goals, pages, or structure without an explicit strategy document

## Prerequisites

**Brand DNA must exist.** Web design strategy translates brand identity into web-specific decisions. Without a Brand DNA document, the consultation has no foundation to build on.

Before starting, verify:
1. A Brand DNA document exists at `brands/<brand>/brand-dna.md`
2. It contains populated visual codes, personality traits, and audience definition

If no Brand DNA exists, redirect the client to `/discover-brand` first.

## Context

**Industry research:** Check `research/<industry>/web-design.md` for research relevant to the client's industry or website type. If relevant research exists, read it for web design patterns, case studies, and conventions specific to their field.

**Brand DNA:** Read `brands/<brand>/brand-dna.md` for the identity foundation this strategy will translate into web-specific decisions.

**Existing strategy:** Check `brands/<brand>/web-design-strategy.md` for any existing strategy. If a document exists, this is a revision session — acknowledge what's already captured and focus on gaps or areas the client wants to evolve.

## Identifying the Brand

The `brands/` directory contains one subdirectory per brand. At the start of a consultation:

1. **If the client names a brand** — look for its directory. If missing, ask whether to create a new brand directory.
2. **If only one brand directory has a populated Brand DNA** — confirm with the client: "I see Brand DNA for [brand]. Are we designing a website for them?"
3. **If multiple brands have DNA** — ask which brand this consultation is for.
4. **Never assume.** Always confirm the target brand before writing any output.

## Interview Structure

Six phases, funnel from business context to design direction. **Do not treat these as a checklist** — use them as conversation guides. Follow the client's energy.

### Phase 1 — Context & Business Foundation

Why is this website happening now, and what business outcome depends on it?

- What's prompting this project (new site, redesign, brand evolution)
- Brand lifecycle stage (pre-launch, launching, growing, scaling)
- Business objectives in priority order (awareness, bookings, sales, community, education, credibility)
- The single most important action a first-time visitor should take
- What the website must do that social media cannot

### Phase 2 — Audience & Relationship

Who does the site serve, in priority order?

- Three types of people most likely to visit, ranked by importance
- For each: what they're looking for, what would cause them to leave
- The question a first-time visitor is trying to answer
- The emotional experience of visiting the site
- Professional audiences (partners, press, referral sources) and their specific needs

### Phase 3 — Site Purpose & Structure

Lock the primary CTA, then build the sitemap.

- If the site had only four pages, what would they be?
- The most important page — the one doing the most work
- E-commerce or booking: requirement, nice-to-have, or out of scope
- Content needs: blog, resources, testimonials, portfolio, case studies
- Editorial content and who produces it

**Sitemap exercise:** Propose a structure based on what the client has shared. Walk through it together. Adjust.

### Phase 4 — Visual Direction

Bridge from Brand DNA to web-specific design language.

- How brand visual codes (from DNA) should translate to the website
- 2-3 reference websites the client admires, with specifics about why
- 2-3 websites that represent exactly what the site should NOT look like
- Photography and imagery inventory: what exists, what needs to be created
- Brand voice on the site: minimal, warm, authoritative, conversational, poetic
- First thing a visitor's eye should land on

**Photography dependency check:** Surface this early. No other factor affects brand website quality more than photography. If quality imagery doesn't exist, name it as a dependency.

### Phase 5 — Content & Constraints

What the client can actually provide, realistic scope, dependencies.

- Available photography and visual assets
- Existing copy (about, services, story, testimonials)
- Who writes the website copy
- Update frequency after launch
- Platform preferences or commitments (WordPress, Squarespace, custom, etc.)
- Who maintains the site post-launch, their skill level
- Timeline and hard deadlines
- Budget constraints that shape scope

### Phase 6 — Competitive Context

Market positioning for differentiation.

- 2-3 competitor or peer websites: what they do well, what they get wrong
- What the site should do that none of those references accomplish
- Where the brand sits relative to peers in their field

## Conducting the Consultation

### Pacing

- **Progressive disclosure**: Phases 1-3 are essential before any design work. Phase 4 is critical for mock-up preparation. Phases 5-6 are enrichment that can happen across sessions.
- **Follow energy**: If the client gives a rich, detailed answer, go deeper. If they're brief, move on and circle back.
- **One question at a time**: Don't dump all questions from a phase. Ask one, listen, follow up.
- **Lock the primary CTA early**: Every other decision flows from it. A strategy without a single, unambiguous primary call to action is incomplete.

### Synthesis

After each phase, reflect back what you've heard. This serves two purposes:
1. Validates understanding — the client can correct misinterpretations immediately
2. Progressively builds the strategy document so the final output isn't a surprise

Watch for contradictions (e.g., wanting an "intimate" feel but also wanting to scale to thousands of visitors). Surface these as discussion points.

### Key Principles

1. **Surface the photography dependency early.** Most common blocker for brand websites across all industries.
2. **Distinguish what the brand wants to say from what visitors need to find.** Jobs-To-Be-Done questions bridge this gap.
3. **Name a primary audience.** A website designed for everyone is designed for no one.
4. **Produce assertions, not notes.** "We recommend X because Y" is strategy. "The client mentioned X" is a transcript.
5. **Flag content dependencies as blockers.** Design cannot proceed until dependencies are resolved.
6. **Capture visual references and anti-references.** These do more work than verbal descriptions.

## Output Format

When the consultation reaches clear alignment, write the web design strategy specification to `brands/<brand>/web-design-strategy.md`:

```markdown
---
title: Web Design Strategy
tags: [web, strategy, design]
last_updated: YYYY-MM-DD
brand: {brand-name}
---

# Web Design Strategy — {Brand Name}

## Site Purpose Statement
[1-2 sentences: why this website exists, for whom, what it accomplishes]

## Business Context

```yaml
lifecycle_stage: ""
objectives: []       # in priority order
primary_cta: ""      # the single most important visitor action
success_metrics: []
```

## Audiences

```yaml
primary:
  description: ""
  jobs_to_be_done: []
  what_would_make_them_leave: ""
secondary: []
anti_visitor: ""     # who the site is not for
```

## Site Architecture

```yaml
sitemap: []          # page list with hierarchy
navigation_model: "" # how visitors move through the site
most_important_page: ""
content_inventory:
  exists: []
  needs_creation: []
  dependencies: []   # blockers before design can proceed
```

## Design Tokens

```yaml
color:
  palette: {}        # from Brand DNA, with hex values
  semantic: {}       # background, text, accent, cta mappings
typography:
  headings: ""       # specific typeface
  body: ""           # specific typeface
  scale: ""          # approach to size hierarchy
spacing: ""          # density philosophy (airy, balanced, compact)
shape: ""            # border radius, edge treatment approach
motion: ""           # animation philosophy (gentle, none, energetic)
```

## Interactions

```yaml
hover: ""
scroll: ""
page_transitions: ""
microinteractions: ""
```

## Page Specifications

```yaml
# per key page:
- page: ""
  purpose: ""
  sections: []
  primary_action: ""
  visual_direction: ""
```

## Design Rules

```yaml
always: []
never: []
voice: ""            # how the brand speaks on this site
photography_direction: ""
```

## Competitive Context

```yaml
references: []       # sites admired, with what specifically
anti_references: []  # sites to avoid resembling, with why
differentiation: ""  # what this site does that peers don't
```

## Constraints

```yaml
platform: ""
timeline: ""
maintenance: ""      # who maintains, their skill level
budget_scope: ""
```

## Open Questions
[Unresolved items before mock-up can begin]
```

### Writing Guidelines

- Use the client's own words wherever possible
- Be specific in tokens — `"#0A0A0A"` not "black", `"Inter"` not "sans-serif"
- The `design_rules.never` list is the most operationally important field for mock-up work — invest time getting it right
- Every design token must trace back to a Brand DNA visual code or a deliberate web-specific decision made during the consultation
- Flag any open questions that must be resolved before design work can begin

## Integration with Design Pipeline

Once recorded, the web design strategy specification becomes the primary input for design and development:

- **Mock-up generation**: The design intent narrative prevents plausible-but-wrong interpretive decisions. The token spec prevents invented values.
- **Iteration**: When designs miss the mark, the strategy provides the diagnostic framework — is this a token issue, a layout issue, or a strategic misalignment?
- **Brand consistency**: The translation chain (Brand DNA -> Web Tokens -> Design) ensures the website is a faithful expression of the brand identity, not an aesthetic coincidence.

The strategy document at `brands/<brand>/web-design-strategy.md` should be read at the start of any web design or development session for that brand.
