# Copywriting

Structured conversational workflow for drafting website copy — section by section, guided by Brand DNA voice and web design strategy structure. The consultant drafts, the client critiques, and together they iterate until the copy sounds like the client and serves the audience.

## When to Use

- A brand has completed both Brand DNA and web design strategy and is ready for copy
- The client wants to draft or revise website copy before mock-up
- Copy exists but doesn't match the brand voice established in Brand DNA
- The client is struggling to write about their own work

## Prerequisites

**Both Brand DNA and web design strategy must exist.** Copywriting translates brand voice into page-specific content structured by the strategy spec. Without both, the copy has no voice anchor and no structural guide.

Before starting, verify:
1. Brand DNA exists at `brands/<brand>/brand-dna.md` — provides voice, personality, values, audience, and the "one sentence" brand distillation
2. Web design strategy exists at `brands/<brand>/web-design-strategy.md` — provides page specifications, section purposes, CTAs, and audience definitions

If either is missing, redirect the client to `/discover-brand` or `/design-website` first.

## Context

**Industry research:** Check `research/<industry>/copywriting.md` for industry-specific copywriting guidance — how to write about the client's modality, language their audience uses, compliance considerations, and SEO patterns.

**Brand DNA:** Read `brands/<brand>/brand-dna.md` for voice anchors:
- `personality_traits` — defines how the brand speaks
- `values` — defines what the brand emphasizes
- `brand_essence` — the 3–5 word distillation that every sentence should feel consistent with
- `audience.ideal_client` — who the copy speaks to
- `design_rules.one_sentence` — "This brand always feels like ___"

**Web design strategy:** Read `brands/<brand>/web-design-strategy.md` for structural guidance:
- `pages[].sections[]` — what sections need copy, their purpose, and their CTA
- `audiences.primary` — the visitor's needs and jobs to be done
- `business.primary_cta` — the action the entire site drives toward
- `design_rules.voice` — how the brand speaks on this site specifically

**Existing copy:** Check `brands/<brand>/copy.md` for any existing copy. If it exists, this is a revision session.

## The Conversational Process

### Step 1 — Establish Voice

Before drafting a single section, establish the voice with the client. Synthesize the Brand DNA personality into a concrete writing voice:

- Propose a voice direction in plain terms: "Based on your brand personality, I'd write in a tone that's [description] — like [analogy]. Does that feel right?"
- Give a short example — rewrite a generic sentence in the proposed voice
- Get explicit approval before proceeding

The voice established here becomes the reference standard for every section.

### Step 2 — Draft Section by Section

Work through the site in the order defined by the web design strategy spec. For each section:

1. **State the section's job.** "This is the homepage hero. Its job is to [purpose from strategy spec]. The primary audience is [audience]. The CTA is [CTA]."
2. **Draft the copy.** Write the headline, body text, and CTA text for the section. Use the client's own words from brand DNA wherever possible.
3. **Present the draft.** Show it to the client cleanly — headline, body, CTA clearly separated.
4. **Invite critique.** "Does this sound like you? What feels right and what feels off?"
5. **Revise based on feedback.** Adjust tone, specificity, emphasis. Repeat until the client approves.
6. **Move to the next section.** Carry the approved voice forward.

### Step 3 — Review for Consistency

After all sections are drafted, read through the complete copy document for:
- **Voice consistency** — does it sound like the same person throughout?
- **Message hierarchy** — do the most important ideas get the most prominent placement?
- **CTA flow** — does each section naturally lead toward the primary CTA?
- **Repetition** — are the same phrases or ideas repeated across sections?
- **Accuracy** — flag any claims the client should verify

Present the complete copy to the client for final review.

## Section Drafting Order

Follow the web design strategy's page specifications, but typically:

1. **Homepage hero** — sets the voice standard; gets the most iteration
2. **Homepage "who I help" statement** — names the audience's pain
3. **Homepage service overview** — introduces what the client offers
4. **About page** — origin story, philosophy, credentials
5. **Individual service pages** — one per offering
6. **Testimonials framing** — the introductory text around client stories
7. **FAQ** — addressing common objections and questions
8. **Contact/booking page** — the final invitation
9. **Footer** — tagline, newsletter signup text
10. **Meta content** — page titles, meta descriptions for SEO

## Writing Principles

### Voice Anchoring

Every sentence should pass the brand test: does this sound like [brand personality]? Could this have been said by [the brand-as-person from DNA]?

Practical checks:
- Read the sentence aloud — does it sound natural in the client's voice?
- Could a competitor say the exact same thing? If yes, it's not specific enough
- Does it reflect the values from Brand DNA, not just generic benefits?

### Client's Own Words

The Brand DNA document captured the client's language during the discovery interview. Mine it for:
- How they describe their purpose
- The words they use for their audience's pain
- Their natural speech patterns and vocabulary
- Phrases that felt particularly authentic or energized

The best copy will feel to the client like "I could have written this, but better."

### Writing for the Audience

The web design strategy defines the primary audience and their jobs to be done. Copy should:
- Address the visitor directly ("you")
- Name their specific experience, not generic pain
- Show empathy before presenting solutions
- Use the language they use, not the practitioner's professional jargon
- Create a sense of "this person understands me"

### Headlines

- Lead with the client's benefit or emotional state, not the practitioner's credentials
- Be specific: "Find relief from the anxiety that keeps you up at night" over "Anxiety treatment"
- Match the brand personality — a Sanctuary brand uses different headline energy than a Wise Guide
- The homepage headline is the single most important piece of copy on the site

### Calls to Action

- Match the CTA language to the commitment level: "Schedule a free conversation" (low barrier) vs. "Book your first session" (higher commitment)
- The primary CTA should use the exact language from the web design strategy
- Every section should have a natural next step, even if it's just reading the next section
- Avoid generic CTAs ("Learn More," "Click Here") — make them specific and warm

### Length

- Long-form copy converts better for high-consideration decisions (health, therapy, healing)
- But every sentence must earn its place — length should come from depth, not filler
- Use short paragraphs (2–4 sentences) for scanability
- Use single-sentence paragraphs for emphasis
- Service descriptions can be substantial — people making health investments need information

## Output Format

Write the completed copy to `brands/<brand>/copy.md`:

```markdown
---
title: Website Copy
tags: [copy, content, voice]
last_updated: YYYY-MM-DD
brand: {brand-name}
voice: "{one-line voice description approved by client}"
---

# Website Copy — {Brand Name}

## Voice Reference

```yaml
personality: ""        # from Brand DNA
tone: ""               # approved voice direction
speaks_like: ""        # analogy or description
avoids: []             # words, phrases, or tones that are off-brand
```

## Homepage

### Hero
```yaml
headline: ""
subheadline: ""
cta:
  label: ""
  destination: ""
supporting_text: ""    # optional paragraph below headline
```

### Who I Help
```yaml
lead: ""               # 1-2 sentences naming the pain
body: ""               # expanded description
```

### Services Overview
```yaml
intro: ""              # framing sentence
services:
  - name: ""
    description: ""    # 1-2 sentences
    cta: ""
```

### About Preview
```yaml
lead: ""               # hook that draws visitor to full about page
cta: ""
```

### Social Proof
```yaml
intro: ""              # framing text for testimonials
testimonials_note: ""  # guidance on which testimonials to feature
```

### Final CTA
```yaml
headline: ""
body: ""
cta:
  label: ""
  destination: ""
```

## About Page

```yaml
headline: ""
origin_story: |
  Multi-paragraph narrative
philosophy: ""
approach: ""
credentials: ""        # woven in naturally, not listed
closing_cta:
  text: ""
  label: ""
  destination: ""
```

## Services

### {Service Name}
```yaml
headline: ""
what_it_is: ""         # plain language explanation
who_its_for: ""        # specific audience for this service
what_to_expect: ""     # session description
outcomes: ""           # what clients experience (not health claims)
pricing: ""
cta:
  label: ""
  destination: ""
```

## FAQ

```yaml
intro: ""
questions:
  - q: ""
    a: ""
```

## Contact / Booking

```yaml
headline: ""
body: ""               # warm invitation to take the next step
details: ""            # location, telehealth, hours
cta:
  label: ""
  destination: ""
```

## Footer

```yaml
tagline: ""
newsletter:
  headline: ""
  description: ""
  cta: ""
```

## Meta Content

```yaml
pages:
  - page: ""
    title: ""          # browser tab / search result title
    description: ""    # meta description for search results
```
```

### Writing Guidelines

- Use the client's own words wherever possible — copy should sound like them, not like a copywriter
- Be specific — "Tuesday evening anxiety that won't let you sleep" over "stress and anxiety"
- Keep service descriptions in client language, not practitioner jargon
- Frame outcomes as client experiences, not health claims: "Clients often report feeling..." not "This treatment cures..."
- The `voice` field in the frontmatter is the consistency anchor — reference it throughout
- Every section's copy must serve that section's stated purpose from the web design strategy
- Flag any factual claims that the client needs to verify

## Integration with Mock-up Phase

The completed copy document becomes a direct input for the mock-up:

- **Headlines and body text** are placed directly into the HTML — no lorem ipsum
- **CTA labels** become button text
- **Section structure** matches the web design strategy spec, so copy slots into the layout
- **Voice reference** guides any additional microcopy the mock-up agent needs to generate (button hover states, form labels, error messages)

The copy document at `brands/<brand>/copy.md` should be read alongside the web design strategy when producing mock-ups.
