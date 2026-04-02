# Brand Discovery

Structured interview workflow for capturing Brand DNA — the foundational identity specification that grounds all subsequent design, strategy, and creative work.

## When to Use

- Starting work with a new brand that has no existing DNA document
- The client wants to revisit or revise their brand identity
- Before any downstream phase (web design, art direction, product development)
- The client shares references or inspirations but hasn't articulated *why* they resonate

## Context

**Industry research:** Read `research/<industry>/brand-dna.md` for research relevant to the client's industry or trade. This contains market-specific patterns, visual conventions, audience expectations, and interview considerations. If no relevant research exists, recommend generating it via `/research` before proceeding.

**Existing DNA:** Check `brands/<brand>/brand-dna.md` for any existing DNA. If a document exists, this is a revision session — acknowledge what's already captured and focus on gaps or areas the client wants to evolve.

## Interview Structure

Six phases, funnel from abstract identity to concrete visual specification. **Do not treat these as a checklist** — use them as conversation guides. Follow the client's energy. If they start with visual language, meet them there and backfill the conceptual layers later.

### Phase 1 — Origin & Purpose

Establish the core: why does this brand exist?

- Origin story — the moment, experience, or calling that started it all
- Purpose — what would be missing from the world without this brand
- Communities, traditions, or movements that shaped the founder's perspective
- The feeling people should have when experiencing the brand's work

### Phase 2 — Personality & Values

Define character: who is this brand as a person?

- Brand-as-person exercise: how do they carry themselves, what do they talk about, how do they make people feel
- 3-5 non-negotiable values
- Admired brands (any industry) and what specifically resonates
- Anti-patterns: what is the opposite of this brand? What would feel wrong?

### Phase 3 — Audience & Relationship

Who does this brand serve, and what's the connection?

- Ideal client/customer by mindset, life stage, and needs — not demographics
- Discovery pathway — how do people find the brand?
- Relationship model: trusted guide, open community, intimate partnership, cultural voice
- Who the brand does *not* serve — defining the boundary sharpens the center

### Phase 4 — Visual Translation

Bridge from values to design language. This is the most critical phase for downstream work.

- Reference images, brands, or environments (any medium) that feel like the brand, with explanation of why
- Color instincts — what colors feel right, what colors are off-limits
- Texture and materiality — smooth, rough, organic, clean, layered, minimal
- Typography instincts — formal, warm, hand-crafted, modern, classic
- The client's own work or spaces that best express the brand
- If the brand were a physical space, what would it look, feel, and sound like?

### Phase 5 — Constraints & Rules

Design guardrails that prevent drift.

- Trends the brand actively resists
- Signature elements that should recur across everything
- A one-sentence distillation: "This brand always feels like ___"
- Rejection criteria: what would make a design feel wrong for this brand

### Phase 6 — Competitive Positioning

Market context for differentiation.

- Adjacent brands or practitioners and what separates this one from them
- Where the brand sits on relevant spectra (accessible-exclusive, traditional-innovative, clinical-spiritual, etc.)
- Price positioning and its implications for how the brand presents itself

## Conducting the Interview

### Pacing

- **Progressive disclosure**: Phases 1-2 are essential before any downstream work. Phases 3-4 are needed before visual work. Phases 5-6 are enrichment that can happen across multiple sessions.
- **Follow energy**: If the client gives a rich, detailed answer, go deeper. If they're brief, don't force it — move on and circle back later.
- **One question at a time**: Don't dump all questions from a phase. Ask one, listen, follow up, then decide whether to continue the thread or move to the next question.

### Synthesis

After each phase, reflect back what you've heard in concise, precise language. This serves two purposes:
1. Validates your understanding — the client can correct misinterpretations immediately
2. Progressively builds the DNA document in real-time, so the final output isn't a surprise

Watch for contradictions between phases (e.g., values of "authenticity" but visual references that are highly polished and trend-driven). Surface these gently as discussion points, not corrections.

### Visual Bridge

Phase 4 is where abstract identity becomes concrete design language. Push for specificity:
- "Calming" -> what kind of calm? A forest? A library? A meditation room? An empty beach?
- "Natural" -> wild and untamed, or cultivated and orderly? Raw wood or polished stone?
- "Professional" -> which lineage? Clinical, corporate, artisanal, academic?

Connect visual codes back to the values and personality established in earlier phases. Every visual choice should be traceable to a core identity element.

## Output Format

When the interview reaches clear alignment, write the DNA specification to `brands/<brand>/brand-dna.md` using **pure markdown** — no YAML code blocks. The document should read like a brand identity brief, not a config file. Use headings for structure, prose for narrative content, bullet lists for enumerated items, and tables where structured data genuinely benefits from it (color palettes, brand spectra).

Write the DNA to `brands/<brand>/brand-dna.md` using this structure:

```markdown
---
title: Brand DNA
tags: [brand, identity, core]
last_updated: YYYY-MM-DD
---

# Brand DNA — {Brand Name}

## Identity

**Name:** {name}
**Tagline:** {tagline}

### Origin Story

{Multi-line narrative in the client's own words}

### Communities & Lineages

- {traditions, movements, subcultures that shaped the brand}

---

## Core

### Purpose

{What would be missing from the world without this brand}

### Values

1. **{Value}** — {Description}
{3-5 values, numbered for priority}

### Personality

- **{Trait}** — {Description}
{3-5 traits}

**Archetype:** {Jungian or custom — whichever fits}
**Brand essence:** {3-5 word distillation}

---

## Role

{Who the practitioner/founder is and how they see their work — in their own words}

### Philosophy

{Their worldview and approach, in their own language}

---

## Offerings

{Brief intro connecting the offerings to the brand identity}

### {Offering Name} *(signature offering)*

{Description — what it is, what it does, why it matters}

### {Offering Name}

{Description}

{Repeat for each offering}

---

## Audience

### Ideal Client

{By mindset, life stage, and needs — not demographics}

### How They Find {Name}

{Discovery pathway}

### Relationship Model

{The model of connection}

### Not For

{Who the brand does not serve — defining the boundary sharpens the center}

---

## Visual Codes

### Color Palette

| Role | Color | Quality |
|---|---|---|
| Primary | {Color name} | {What it expresses} |
| Secondary | {Color name} | {What it expresses} |
| Accent | {Color name} | {What it expresses} |

**Color mood:** {The overall feeling of the palette — in the client's own words where possible}

### Typography

{Direction, characteristics, and rationale — in prose}

### Imagery

{Style, mood, and subject matter — in prose}

**Subjects:** {Key visual subjects}

**Textures & materials:** {Material qualities}

### Spatial Feeling

{If the brand were a physical space, what would it look, feel, and sound like — in the client's own words}

### Cultural References

- {References that inform the visual and conceptual world}

---

## Positioning

### Market Context

{Where the brand sits in its landscape}

### Differentiation

{What sets this brand apart — the edge}

### Price Positioning

{Pricing philosophy and its implications}

### Brand Spectra

| Axis | Position |
|---|---|
| {Spectrum} | {Where the brand sits} |

### Competitors

{Known competitors or "to be explored in reference gathering phase"}

---

## Design Rules

### Always

- {Actionable constraint}

### Never

- {Actionable constraint}

### Signature Elements

{Elements that should recur — or "to emerge through reference gathering and mock-up"}

### One Sentence

> This brand always feels like {___}.
```

### Writing Guidelines

- **Pure markdown, no YAML.** The document should read like a brand identity brief. Headings provide structure; prose carries the narrative; tables and lists organize structured data.
- Use the client's own words wherever possible — DNA should sound like them, not like a branding agency
- Be specific in visual codes — "burnt orange (#CC5500)" not just "orange"
- Keep values and traits to 3-5 items each — more than that means nothing is prioritized
- Design rules should be actionable constraints, not aspirational statements
- The Always / Never / Signature Elements sections are the most operationally important — invest time getting them right
- Include an Offerings section when the client has defined their services — downstream phases (especially web design and copywriting) need to know what they're building around
- Include a Role section when the client has articulated their identity and philosophy in their own words — this grounds the voice for copywriting

## Integration with Downstream Phases

Once recorded, Brand DNA becomes persistent context for all subsequent work:

- **Web design strategy**: Visual codes translate to design tokens; personality shapes voice and interaction patterns; audience defines user journeys
- **Art direction**: Design rules and visual codes guide creative output; `always` and `never` become direct constraints
- **Product development**: Values and purpose inform product decisions; audience shapes feature priorities
- **Content strategy**: Personality traits define voice; brand essence guides messaging

The DNA document at `brands/<brand>/brand-dna.md` should be read at the start of any consultation session for that brand.
