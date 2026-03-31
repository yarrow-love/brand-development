# Web Design Strategy for Streetwear Brands

Web design strategy is the phase between brand identity and visual design — the work that determines why a website exists, who it serves, and what it must accomplish before a single pixel is placed. For streetwear, where the website functions as a cultural artifact as much as a commercial tool, strategy is the difference between a site that converts and one that merely looks good. This research distils discovery frameworks, streetwear-specific patterns, and specification methodologies into an actionable consultation workflow for the Atelier design consultant agent.

---

## Context

The Atelier consultant currently has a Brand DNA discovery workflow that captures foundational brand identity — origin story, values, personality, visual codes, audience, positioning. What's missing is a structured process for translating that DNA into web-specific strategic decisions *before* wireframing or mock-up work begins.

A web design strategy consultation slots into the pipeline between Brand DNA and visual design:

```
BRAND DNA → WEB DESIGN STRATEGY → MOCK-UP → DEVELOPMENT
```

The strategy document becomes a persistent specification consumed by a mock-up agent (Claude Code) to produce web designs grounded in explicit strategic intent rather than aesthetic assumption.

Relevant existing docs:
- Brand DNA research: `research/streetwear/brand-dna.md`
- Brand DNA specification: `brands/<brand>/brand-dna.md`
- Web design skill: `.claude/skills/web-design.md`
- Consultant agent: `.claude/agents/consultant.md`

---

## Findings

### 1. Terminology & Phase Definitions

The user asked the research to "clarify terminology." Web design terminology is inconsistently used across the industry — the same word means different things in different contexts. The following definitions establish the vocabulary the consultation agent should use.

#### The Standard Phases of a Web Design Project

Across methodologies and agencies, web design projects follow this sequence:

1. **Discovery / Strategy** — research the problem space, define goals, audiences, and site purpose
2. **Information Architecture** — determine site structure, page hierarchy, navigation model
3. **Wireframing** — low-fidelity structural layouts solving hierarchy and flow
4. **Visual Design (Mock-up)** — high-fidelity static designs showing exact appearance
5. **Prototype** — interactive simulation linking mock-up screens for flow testing
6. **Development** — implementation in code
7. **Testing & Launch** — QA, deployment, post-launch optimization

Different frameworks name and group these differently, but the functions are universal:

| Methodology | Phase 1 | Phase 2 | Phase 3 | Phase 4 |
|---|---|---|---|---|
| Agency Standard | Discovery & Strategy | IA + Wireframes | Visual Design | Development |
| Double Diamond | Discover → Define | Develop | Deliver | — |
| Design Thinking | Empathize → Define | Ideate | Prototype → Test | — |
| Lean UX | Think (hypothesize) | Make (build MVP) | Check (measure) | (repeat) |

#### What Phase 2 Is Called

In Atelier's workflow, "Web Design Purpose" corresponds to what the industry most precisely calls **Web Design Strategy** — the phase where known brand inputs (from Brand DNA) are translated into web-specific goals, audiences, structure, and direction.

It is distinct from "Discovery" because Brand DNA has already performed the foundational brand research. Strategy takes those inputs and asks: "Our brand is X — what does that mean a website should do, feel like, and contain?"

Other viable names, ranked by precision:
1. **Web Design Strategy** — most precise for Atelier's workflow
2. **Discovery & Strategy** — appropriate when combined with brand research
3. **Strategic Foundation** — clear but less industry-standard
4. **Discovery** — slightly misleading when brand research is already complete

#### Key Term Distinctions

**Wireframe vs. Mock-up vs. Prototype:**

| Artifact | Fidelity | Interactive | Purpose |
|---|---|---|---|
| **Wireframe** | Low (grayscale boxes) | No | Validate structure and layout cheaply |
| **Mock-up** | High (real colors, typography, imagery) | No | Communicate final visual design |
| **Prototype** | High | Yes (clickable) | Test user flows and interactions |

Wireframes solve *where things go*. Mock-ups solve *what things look like*. Prototypes solve *how things behave*. Jumping directly from strategy to mock-up without wireframing risks expensive visual rework when structural decisions prove wrong — though for simple brand sites (4–6 pages), wireframing can be lightweight.

**UX vs. UI:**

- **UX (User Experience)** — the entire journey: how the product works, whether it meets user goals, how it feels to navigate. Deliverables: personas, journey maps, wireframes, usability tests.
- **UI (User Interface)** — the visual and interactive surface: screens, components, typography, color, motion. Deliverables: mock-ups, design systems, component libraries.

UX is the floor plan. UI is the finishes. Every UI decision should be grounded in UX research.

**Strategy deliverables in the gap between discovery and visual design:**

| Deliverable | Fidelity | Purpose |
|---|---|---|
| **Mood Board** | Low (borrowed references) | Establish aesthetic direction — aspirational, not prescriptive |
| **Style Tile** | Medium (original design work) | Define visual language at component level — typefaces, colors, UI samples |
| **Design Direction** | Variable | Propose an interpretive approach to the design problem |
| **Design System** | High | Reusable components and tokens — single source of truth for UI |
| **Sitemap** | Structural | Page hierarchy and navigation relationships |
| **Design Brief** | Written | Align all parties before visual work begins |

Style tiles (coined by Samantha Warren) are particularly relevant to the Atelier workflow — they validate visual language at the component level before investing in full-page mock-ups. A style tile shows specific typeface choices, a concrete color palette, and UI component samples without committing to page layout.

### 2. Web Design Strategy: What It Produces

Professional agencies treat strategy as the phase that converts research into direction. The output is opinionated — it makes recommendations, not summaries. "We recommend a newsletter CTA because the brand is pre-launch with no inventory" is strategy. "The client mentioned a newsletter" is a transcript.

Dan Brown (EightShapes) characterizes strategy outputs as **assertions** — conclusions drawn from research:

| Assertion Type | What It States |
|---|---|
| **Principles** | What the design should or should not do (grounded in research) |
| **Concepts** | The overall design approach, expressed as a central theme |
| **Models** | Abstract representations of structure, flow, or architecture |
| **Requirements** | What the product must do (functional and content) |
| **Constraints** | What the product cannot do (technical, budget, timeline) |
| **Priorities** | What matters most when trade-offs must be made |

A strong strategy document contains all six. A weak one contains only requirements and constraints — it tells the designer what to build but not why or according to what principles.

#### The Deliverables

The strategy phase should produce these specific artifacts:

1. **Site Purpose Statement** — one or two sentences capturing why this website exists
2. **Business Objectives** — prioritized SMART goals with measurable success criteria
3. **Audience Definitions** — 3–5 personas with goals, needs, and behaviors
4. **Jobs to Be Done** — functional, social, and emotional jobs visitors hire the site for
5. **Primary Call to Action** — the single most important action the site drives toward
6. **Proposed Sitemap** — page hierarchy and navigation model
7. **Page Purpose Matrix** — purpose, primary audience, and primary CTA per page
8. **Content Inventory** — what content exists, what must be created, what blocks design
9. **Competitive Reference Matrix** — 3–5 reference sites with differentiation intent
10. **Design Direction Brief** — visual and tonal territory translated from Brand DNA
11. **Success Metrics** — KPIs and measurement methods per business objective

#### Jobs to Be Done Applied to Website Strategy

The JTBD framework (Christensen, Ulwick) reframes the question from "what features should this site have?" to "what jobs are visitors hiring this site to do?" This is particularly powerful for streetwear because the emotional and social jobs often dominate.

Three job types:
- **Functional jobs** — find a stockist, check sizing, place an order
- **Social jobs** — discover a brand before it's mainstream, signal cultural literacy
- **Emotional jobs** — feel inspired, validated, part of something exclusive

A visitor may not be "hiring" a streetwear website to buy a shirt — they may be hiring it to decide whether the brand is worthy of their identity. Understanding this shifts design priorities: the site may need to demonstrate cultural credibility and aesthetic authority before a product page ever appears.

#### Content-First Design

Content-first methodology holds that real content — actual words, actual images, actual structure — should exist before layouts are designed. The rationale: content shape determines layout shape. A hero section with a three-sentence manifesto requires a different layout than one with a 40-word tagline. If design begins before content exists, the finished design breaks when real content is inserted.

For the consultation: this means surfacing what content the founder already has and what they need to create. A founder who cannot produce copy, photography, and collection imagery has a scoping problem that must be named before any designer begins.

### 3. Streetwear Brand Website Archetypes

Streetwear brand websites are not conventional e-commerce sites. The website is a cultural artifact — a statement of positioning as much as a sales channel. Five distinct archetypes emerge:

#### The Drop Machine

The site's sole purpose is executing product releases. Navigation is minimal, the homepage is a countdown or announcement, and product pages exist to process a transaction in a narrow window. Supreme is canonical — notoriously stark, functional to the point of hostility. Palace operates a variant with predictable Friday 11am drops that create ritual. The design communicates: come here to buy, not to browse.

#### The Brand World / Editorial Hub

The site is a magazine and a store simultaneously. Aimé Leon Dore pioneered this — the site reads like a curated mood board: playlists, archival photography, lookbooks with atmospheric narrative, café presence, event announcements. The commercial relationship is secondary to the cultural one. ALD pulled out of wholesale after LVMH investment specifically to control this presentation.

#### The Lifestyle Platform

Kith is the primary example — merging product drops, editorial content, collaborations, and community. Closer to a media company than a streetwear label. High AOV, high engagement, built on Shopify Plus with custom development that achieved 235% conversion rate increase after systematic redesign.

#### The Underground Collective

Access is the product. Corteiz's site is password-gated — codes released through Instagram. Brain Dead prominently features event pages, creative studios, and community spaces alongside product. Anti-discoverability is deliberate positioning.

#### The Minimalist Luxury Statement

Fear of God, Rhude, post-Abloh Off-White. Quiet, restrained, Helvetica at light weights with generous letter-spacing. No banners, no urgency mechanics, no countdown timers. The restraint is the message: the brand doesn't need to sell you this. Price point is the scarcity signal.

#### Archetype Selection by Brand Stage

| Brand Stage | Primary Archetype | Site Job | Primary CTA |
|---|---|---|---|
| Pre-launch | Minimal single-page | Build anticipation, capture contacts | Newsletter / waitlist |
| Launch / Drop | Drop Machine | Convert high-intent visitors from social | Purchase |
| Growing / Established | Brand World or Lifestyle | Multiple audiences, editorial depth | Browse → Buy |
| Wholesale-seeking | Minimalist Luxury | Professional credential | Wholesale inquiry |
| Underground | Underground Collective | Reward the community | Password-gated access |

#### What Distinguishes Streetwear Sites from Traditional Fashion

| Dimension | Streetwear | Traditional Fashion |
|---|---|---|
| Time | Drops create artificial urgency windows | Seasonal collections with long shelf life |
| Community | Audience already wants the product before arriving | Site must convince and convert |
| Discoverability | Anti-SEO can be a credibility signal | SEO is always desirable |
| Scarcity | Limited drops, password gates, queue mechanics | Price and distribution access |
| Homepage function | Album cover — communicate everything without explaining | Editorial calendar and navigation hub |
| Photography role | Authenticity of image > technical quality (early stage) | Technical quality is baseline |

### 4. Case Studies: How Streetwear Brands Approach Web Design

#### Supreme

Functionally austere. White background, red logo, product grid. The weekly Thursday drop goes live with zero site announcement — you either know or you don't. The site design has barely changed in 20 years, and that rigidity is itself brand communication. **Lesson:** Supreme's approach only works with Supreme's cultural equity. A new brand attempting this level of minimalism without the history reads as unfinished, not intentional.

#### Corteiz (CRTZ)

Password-protected homepage. The password is released through Instagram before drops — a two-gate system requiring active community membership. No paid advertising, ever. No free seeding to influencers. The friction is authentic, not artificial — Clint Ogbenna built these mechanics from genuine ideology. **Lesson:** Password gates work when the audience has been built first. They don't create an audience; they reward one.

#### Aimé Leon Dore

Deliberately understated but rich. Clean navigation, high-resolution lookbooks, atmospheric editorial photography featuring vintage objects and archival imagery. Integrates café presence, playlists, events. Teddy Santis cast genuine friends in lookbooks. After LVMH investment: full DTC pivot, pulled from all wholesale. **Lesson:** Build the world before building the store. **Caution:** The "ALD aesthetic" has been cloned industry-wide — adopting their visual decisions instead of their strategic decisions reads as derivative.

#### Kith

Shopify Plus, extensively customized. The redesign focused on "emotion, identity, and value" — lookbooks and narrative woven throughout the product experience, not siloed in a separate "Journal." Monday Program drop mechanic has its own app. Results: 235% conversion rate increase, 15% AOV increase, 50% mobile conversion surge. **Lesson:** Brand storytelling and conversion optimization are not in conflict. Editorial content within the purchase flow directly improves commercial performance.

#### Fear of God

Quiet. Neutral palette, generous white space, minimal typography, premium photography. Three-tier brand architecture (Fear of God, Athletics, Essentials) within one brand family. $725–$6,500+ pricing. No urgency mechanics, no countdown timers. **Lesson:** When price point is the scarcity signal, the site must not undercut it with retail-style urgency tactics. A countdown timer on a $2,000 hoodie is brand-damaging.

#### Brain Dead

Dark backgrounds, white text, full-width hero imagery. Navigation features both product categories and experience categories (Brain Dead Studios, Fantasy Fest, Store Locations). Newsletter signup is prominent. **Lesson:** Brain Dead's navigation structure communicates that clothing is one output among many — the collective produces culture. This architectural decision is itself a brand statement.

#### Anti-Patterns

Eight failure modes specific to streetwear web design:

1. **Mistaking minimalism for anti-design.** Supreme's sparsity communicates 30 years of cultural authority. For an unknown brand, the same design reads as "didn't bother finishing." Test: remove the logo — can you still tell whose site it is?
2. **Intentional friction without earned audience.** Password gates on a brand nobody follows create an empty room behind a locked door.
3. **Beautiful site, broken commerce.** Over-investing in visual identity while CTAs are too small to tap on mobile and checkout has 10 fields.
4. **Editorial content that doesn't convert.** A "Journal" section with one post from a year ago signals the brand abandoned its own content strategy. If it won't be maintained, it shouldn't exist.
5. **Photography mismatch.** Dark web design populated with light-background studio product shots — the photography was shot for a different context.
6. **Over-animating the commerce experience.** Complex entrance animations on pages where users are trying to complete a purchase create friction that reduces conversion.
7. **Running sales on an exclusivity brand.** A 30% off event on a scarcity-positioned brand tells the customer the product wasn't desirable enough and trains the next customer to wait.
8. **Copying the ALD aesthetic.** Studying their visual decisions (color palette, prop styling) instead of their strategic decisions (world-building, DTC control, deliberate scarcity).

### 5. Translating Brand DNA to Web Design Decisions

The critical gap: how does abstract brand DNA become concrete web design? The existing Brand DNA research document establishes an adjective-to-token mapping for generation work. Web design requires a parallel translation — from brand identity to web-specific design tokens, layout patterns, and interaction behaviors.

#### The Translation Chain

```
Brand DNA Document → Web Design Strategy → Web Token Specification → Mock-up
```

The web design strategy consultation bridges this gap by translating brand values, visual codes, and personality traits into a structured specification that a mock-up agent can execute.

#### Color Palette → Web UI Color System

A brand palette is not a UI color system. The translation requires mapping brand colors to semantic roles. Three tiers:

**Tier 1 — Primitive palette** (from Brand DNA):
```yaml
palette:
  black: "#0A0A0A"
  white: "#F8F7F5"
  accent: "#C8FF00"      # brand's signature accent
  never: ["#4169E1"]     # from Brand DNA "never" field
```

**Tier 2 — Semantic UI roles** (what the mock-up agent uses):
```yaml
semantic:
  bg:
    base: ""              # page canvas
    raised: ""            # cards, elevated surfaces
    overlay: ""           # modal backdrops
    inverse: ""           # inverted sections
  text:
    primary: ""           # default body text
    secondary: ""         # metadata, supporting
    inverse: ""           # text on dark surfaces
    accent: ""            # highlights, links
  interactive:
    default: ""           # button background
    hover: ""             # hover state
    focus: ""             # keyboard focus ring
  border:
    subtle: ""            # dividers
    default: ""           # component borders
    strong: ""            # emphasis borders
```

**Tier 3 — Component tokens** (resolved by the mock-up agent during implementation):
```yaml
button.background.default: "{semantic.interactive.default}"
button.background.hover: "{semantic.interactive.hover}"
```

**Archetype-to-color behavior:**

| Archetype | Background Bias | Accent Application | Interactive Color |
|---|---|---|---|
| Ruler/Elevated | White or near-black, never gray | Gold or primary only on CTAs | Monochrome with opacity shift |
| Outlaw | Dark foundation (#0A0A0A–#1A1A1A) | Neon accent, sparingly | Accent on hover, black default |
| Creator | Off-white or unexpected tint | Unpredictable, high-contrast | Concept-specific, may change per page |
| Explorer | Warm off-white or earth tone | Safety orange or signal color | Earth tones, high contrast |

#### Typography → Web Type Scale

Brand typography direction translates to web through a two-step process:

**Step 1 — Resolve typefaces** from Brand DNA's typography direction:
```yaml
brand_direction: "sans-serif, heavy, condensed"
resolved:
  display: "Neue Haas Grotesk Display"
  body: "Neue Haas Grotesk Text"
  accent: "IBM Plex Mono"  # optional, for technical/label text
```

**Step 2 — Establish the scale** using a ratio appropriate to brand personality:

| Brand Trait | Scale Ratio | Leading | Tracking | Weight Range |
|---|---|---|---|---|
| Dense / aggressive | 1.2–1.25 | Tight (0.9–1.1) | Negative on display | Heavy (700–900) |
| Editorial / elevated | 1.333–1.5 | Generous (1.4–1.7) | Slightly wide | Range (300–700) |
| Minimal / restrained | 1.25–1.333 | Moderate (1.4–1.6) | Wide on labels/nav | Light/Regular (300–400) |
| Rebellious | Irregular | Compressed on display | Tight or wide, not neutral | Extreme weights only |

#### Brand Personality → Web Design Pattern Mapping

Each personality trait carries a predictable web design vocabulary:

**"Rebellious" / Outlaw:**
- Layout: Deliberately broken grid, asymmetric alignment, full-bleed collisions
- Spacing: Compressed — elements crowd each other
- Interaction: Abrupt — no easing curves, cuts not fades, instant hover states
- Motion: None or deliberately jarring

**"Elevated" / Ruler:**
- Layout: Centered, symmetrical, generous negative space, single column preferred
- Spacing: Generous — sections breathe, padding signals premium
- Interaction: Fluid, slow ease-in-out, understated hover (opacity shift, not color change)
- Motion: Minimal — subtle fade-in on scroll, no parallax

**"Minimal" / Explorer-Creator:**
- Layout: Grid-strict, rational column system, clear whitespace hierarchy
- Spacing: Consistent increments (8px grid), spacing communicates structure
- Interaction: Standard — predictable hover, clear focus states, no surprises
- Motion: Purposeful transitions only, 200–300ms, ease-in-out

**"Community" / Outlaw-Everyman:**
- Layout: Product-density first, mobile-native, imagery large, details compressed
- Spacing: Tight — prioritize showing more products
- Interaction: Fast — cart action feels like copping, not shopping
- Motion: Quick transitions (100–150ms), countdown timers, restocking alerts

#### Spacing and Density

```yaml
spacing_system:
  base_unit: 8px  # industry standard

  density_profiles:
    editorial:     # generous, premium
      section_gap: "96px–160px"
      component_padding: "32px–48px"
      element_gap: "16px–24px"

    streetwear:    # product-forward, functional
      section_gap: "48px–64px"
      component_padding: "16px–24px"
      element_gap: "8px–12px"

    minimal:       # grid-strict, rational
      section_gap: "64px–96px"
      component_padding: "24px–32px"
      element_gap: "12px–16px"
```

### 6. Web Design Strategy Specification

The consultation should produce a single structured YAML document with two embedded layers:

1. **Design Intent Narrative** — human-readable context and personality descriptions that give the mock-up agent interpretive room
2. **Token + Layout Specification** — machine-executable constraints that eliminate ambiguity

The mock-up agent consumes this with the preamble: "Build a web mock-up for this brand. Use the design tokens exactly. Use the design intent narrative to make interpretive decisions where the specification leaves room. Never invent colors, fonts, or spacing values outside the token spec."

#### Why Two Layers Are Necessary

Research from Jane Street's design workflow and Addy Osmani's AI spec writing guide converge on the same finding: AI agents produce better results when they understand *why*, not just *what*. Without narrative intent, an agent given `border_radius: 0` and `color.accent: #C8FF00` might produce a design that is technically compliant but emotionally wrong — using the neon accent too liberally or arranging elements in a conventional pattern that contradicts the brand's register.

The narrative constrains the interpretive space. The tokens constrain the execution space. Both are necessary.

#### Why "Never" Rules Are More Actionable Than "Always" Rules

Constraints on what *not to do* are more deterministic for AI agents because:
1. They eliminate a category of incorrect outputs entirely
2. They match how brand identity works (brands are more certain about anti-patterns than positive expressions)
3. They are testable — a mock-up either violates a never rule or it doesn't

The `never` fields throughout the specification should receive as much attention as positive specifications during the consultation.

#### The Full Specification Format

```yaml
# ============================================================
# Web Design Strategy Specification
# Output of: Web Design Strategy consultation
# Consumer: Claude Code mock-up agent
# ============================================================

meta:
  brand: ""
  date: ""
  purpose: ""             # 1-sentence site purpose statement
  design_intent: |        # Multi-line narrative — emotional register and visual atmosphere
    [3–5 sentences describing what this design should feel like.
    Example: "The site should feel like entering a private archive — quiet
    authority, no performance. Typography dominates. Imagery is editorial,
    never commercial. The visitor discovers; the brand does not explain itself."]

  audience: ""            # Who uses this site and what they're looking for
  non_goals: []           # What this site explicitly does NOT do

  reference_sites:        # 2-3 sites whose approach is directionally correct
    - url: ""
      what_to_reference: ""    # specific quality, not "copy this site"
    - url: ""
      what_to_reference: ""


# ============================================================
# BUSINESS CONTEXT
# ============================================================

business:
  objectives:
    primary: ""           # The single most important thing this site must achieve
    secondary: []         # Supporting objectives, in priority order
    out_of_scope: []      # Explicitly excluded

  success_metrics:
    - objective: ""
      kpi: ""
      measurement: ""
      target: ""

  primary_cta: ""         # The single action the site is designed to drive

  site_purpose_statement: |
    # One or two sentences that capture the website's entire reason for existing.
    # Example: "This website exists to give cultural credibility to a brand
    # that most visitors discover on Instagram — converting curiosity into
    # conviction and conviction into newsletter subscribers who become
    # first customers."


# ============================================================
# AUDIENCE
# ============================================================

audiences:
  primary:
    name: ""              # Persona name (e.g., "The Cultural Insider")
    who: ""               # 2–3 sentences
    goal: ""              # What they want when visiting
    trust_signals: ""     # What they need to believe the brand is credible
    failure_modes: ""     # What would cause them to leave immediately
    jtbd:
      functional: ""      # Practical task
      social: ""          # How they want to be perceived
      emotional: ""       # How they want to feel

  secondary: []           # Same structure, abbreviated, per additional audience

  anti_visitor: ""        # Who this site is NOT for


# ============================================================
# SITE ARCHITECTURE
# ============================================================

architecture:
  archetype: ""           # drop-machine | brand-world | lifestyle | underground | minimal-luxury

  sitemap:                # Page hierarchy
    - page: "Home"
      url: "/"
      purpose: ""
      primary_audience: ""
      primary_cta: ""
      children: []

    - page: "About / Story"
      url: "/about"
      purpose: ""
      primary_audience: ""
      primary_cta: ""

    # ... additional pages

  navigation:
    model: ""             # "horizontal-top" | "minimal-logo-only" | "hamburger-only"
    primary_links: []     # 3–5 items max
    utility: []           # "search", "account", "cart"
    secondary: []         # footer or utility nav items

  content_inventory:
    available_now: []     # What the founder can provide immediately
    must_create: []       # What needs to be produced before design can start
    blockers: []          # Content dependencies blocking design


# ============================================================
# DESIGN TOKENS
# ============================================================

tokens:

  color:
    palette:              # Primitive values (from Brand DNA)
      primary: ""
      secondary: ""
      accent: ""
      neutral_light: ""
      neutral_dark: ""
      never: []           # Colors that must never appear

    semantic:             # UI roles (what the mock-up agent uses)
      bg:
        base: ""          # page canvas
        raised: ""        # cards, elevated surfaces
        overlay: ""       # modal backdrops, drawers
        inverse: ""       # for inverted sections
      text:
        primary: ""       # default body text
        secondary: ""     # metadata, supporting text
        inverse: ""       # text on inverse/dark surfaces
        accent: ""        # highlight color, links
        disabled: ""
      border:
        subtle: ""        # dividers, faint outlines
        default: ""       # standard component borders
        strong: ""        # emphasis borders
        focus: ""         # keyboard focus ring
      interactive:
        default: ""       # button background, link base
        hover: ""         # hover state
        active: ""        # pressed/active state
        disabled: ""
      status:
        sold_out: ""
        new: ""

  typography:
    typefaces:
      display: ""         # headlines, hero text
      body: ""            # paragraphs, UI text
      accent: ""          # optional — secondary typeface for contrast

    scale:
      display:  { size: "", weight: "", tracking: "", leading: "" }
      h1:       { size: "", weight: "", tracking: "", leading: "" }
      h2:       { size: "", weight: "", tracking: "", leading: "" }
      h3:       { size: "", weight: "", tracking: "", leading: "" }
      body:     { size: "16px", weight: "", tracking: "", leading: "" }
      small:    { size: "14px", weight: "", tracking: "", leading: "" }
      label:    { size: "11px", weight: "", tracking: "0.08em", transform: "uppercase" }
      caption:  { size: "12px", weight: "", tracking: "", leading: "" }
      nav:      { size: "12px", weight: "", tracking: "0.1em", transform: "uppercase" }

  spacing:
    base_unit: "8px"
    density: ""           # "editorial" | "streetwear" | "minimal"
    scale:
      xs: "4px"
      sm: "8px"
      md: "16px"
      lg: "24px"
      xl: "32px"
      2xl: "48px"
      3xl: "64px"
      4xl: "96px"
      section: ""         # space between page sections
      container: ""       # horizontal page padding

  shape:
    border_radius: ""     # "0" | "4px" | "8px+" | "9999px"
    image_aspect_ratio:
      product: "3:4"      # standard portrait
      editorial: "16:9"   # widescreen
      hero: ""            # full-viewport or specific ratio

  motion:
    duration:
      fast: "100ms"
      default: "200ms"
      slow: "350ms"
    easing:
      default: "ease-in-out"
      enter: "ease-out"
      exit: "ease-in"
    philosophy: ""        # "abrupt" | "fluid" | "minimal"


# ============================================================
# INTERACTIONS
# ============================================================

interactions:
  hover:
    links: ""             # e.g., "opacity 0.7 transition"
    buttons: ""           # e.g., "background darkens 12%"
    product_cards: ""     # e.g., "secondary image crossfade"
    nav_items: ""         # e.g., "underline draws from left"

  scroll:
    nav_behavior: ""      # e.g., "transparent over hero, opaque on scroll past 80px"
    section_reveal: ""    # e.g., "fade + translateY 24px on viewport entry"
    parallax: ""          # "none" | "hero only at 0.3x speed"

  page_transitions: ""    # "none" | "fade 200ms"


# ============================================================
# PAGE SPECIFICATIONS
# ============================================================

pages:

  - id: "home"
    url: "/"
    purpose: ""
    emotional_register: ""  # evocative description of how page should feel

    sections:

      - id: "navigation"
        component: "global-nav"
        content:
          brand_mark: ""    # "wordmark" | "logotype" | "icon-only"
          links: []
          utility: []
        visual:
          default_style: "" # "transparent-dark" | "white" | "black"
          scroll_transition: true

      - id: "hero"
        type: "campaign-hero"
        purpose: ""
        content:
          headline: ""      # actual copy or placeholder directive
          subline: ""
          cta:
            label: ""
            destination: ""
          imagery: ""       # photography direction description
        visual:
          height: "100vh"
          text_position: "" # "bottom-left" | "centered" | "bottom-center"
          overlay: ""       # "none" | "gradient-bottom" | "dark-50"

      # ... additional sections per page

      - id: "footer"
        component: "global-footer"
        content:
          columns: []
          newsletter: true
          social: []
          legal: true

  # ... additional pages


# ============================================================
# COMPONENT SPECIFICATIONS
# ============================================================

components:

  product_card:
    purpose: "Present individual products in grid — communicate desirability and availability"
    states: ["default", "hover", "sold-out", "new-arrival"]
    content:
      primary_image: "required"
      secondary_image: "optional — hover reveal"
      name: "required"
      price: "required"
      availability: "required — sold-out visually distinct"
    visual:
      aspect_ratio: "{tokens.shape.image_aspect_ratio.product}"
      image_weight: "75% of card height"
      text_position: "below image"
      sold_out_treatment: "" # "overlay" | "muted image" | "strikethrough price"
    hover: "{interactions.hover.product_cards}"
    constraints: []

  # ... additional components as needed


# ============================================================
# DESIGN RULES
# ============================================================

design_rules:
  always:
    - ""    # e.g., "use brand wordmark in full, never icon-only in nav"
    - ""    # e.g., "product photography always on white or brand context"

  never:
    - ""    # e.g., "never use drop shadows"
    - ""    # e.g., "never center-align body copy"
    - ""    # e.g., "never use rounded corners"
    - ""    # e.g., "never use carousel/slider components"

  agent_boundaries:
    always_do:
      - "use only token values for colors, never hardcode hex"
      - "maintain semantic HTML structure (nav, main, section, footer)"
      - "ensure all interactive elements have keyboard focus states"

    ask_first:
      - "any structural page change not specified above"
      - "adding sections not listed in the page specification"
      - "choosing between multiple valid interpretations of a design rule"

    never_do:
      - "use colors from the never list"
      - "use placeholder lorem ipsum in final mock-up"
      - "add features not specified (social proof, chat widgets, etc.)"


# ============================================================
# COMPETITIVE CONTEXT
# ============================================================

competitive:
  references:
    - url: ""
      strengths: ""       # what they do well
      weaknesses: ""      # what they do poorly
      differentiation: "" # how our site will differ

  positioning: ""         # where this site sits relative to competitors


# ============================================================
# CONSTRAINTS
# ============================================================

constraints:
  technical:
    platform: ""          # Shopify, custom, etc.
    integrations: []      # existing systems
    mobile_priority: ""   # "mobile-first" | "desktop-first"

  timeline:
    target_launch: ""
    milestones: []

  maintenance:
    who: ""               # who maintains the site post-launch
    skill_level: ""       # their technical capacity
    update_frequency: ""  # how often content changes


# ============================================================
# OPEN QUESTIONS
# ============================================================

open_questions: []        # anything unresolved before mock-up can begin
```

#### Mandatory vs. Deferrable Fields

| Field | Criticality | Rationale |
|---|---|---|
| `meta.design_intent` | **Critical** | Prevents plausible-but-wrong interpretive decisions |
| `business.primary_cta` | **Critical** | Every other decision flows from it |
| `audiences.primary` | **Critical** | Design for no one if you don't name someone |
| `tokens.color` (palette + semantic) | **Critical** | All color decisions derived from this |
| `tokens.typography` | **Critical** | Typography is the primary brand signal on web |
| `tokens.spacing.density` | **High** | Density communicates brand tier |
| `pages[].sections[]` | **Critical** | This is the layout contract |
| `design_rules.never` | **Critical** | Most actionable constraint category |
| `agent_boundaries` | **High** | Defines when mock-up agent should ask vs. decide |
| `interactions` | **Medium** | Reinforces brand personality; can iterate |
| `tokens.motion` | **Medium** | Deferrable to mock-up phase |
| Component-level Tier 3 tokens | **Deferrable** | Resolved during mock-up |

### 7. Web Design Strategy Interview

The following interview structure is designed for the Atelier consultant agent. It follows a funnel from business context to design direction, using progressive disclosure to avoid overwhelming the founder.

**Conversation design principles:**
- One thread at a time — never ask two questions in the same message
- Reflect answers back before probing — "So the site's primary job is X — does that feel right?"
- Use the founder's own words as the basis for the next question
- Lock the primary CTA before moving to structure or visual territory
- Surface the photography dependency early — for a streetwear brand, this is the most common blocker

#### Phase 1 — Context & Business Foundation

Establish where the brand is, why the website project is happening now, and what business outcome depends on it.

- "What's prompting this website project right now? Is this a new site, a redesign, or something else?"
- "Where is the brand in its lifecycle — just launched, growing, pivoting, or scaling?"
- "If this website works perfectly, what business result does that produce?"
- "Are you trying to build awareness, drive direct sales, attract press, find stockists — and in what priority order?"
- "What is the single most important action you want a first-time visitor to take?"
- "How will you know, six months from now, whether this website succeeded?"
- "What does the brand need the website to do that Instagram or TikTok cannot?"

#### Phase 2 — Audience & Relationship

Identify who the site serves, in priority order, and what those people need.

- "Who visits your site today (if you have one)? Who do you *want* to visit it?"
- "If you listed the three types of people most likely to visit, who are they?"
- "Which of those three matters most to you right now?"
- "For each type: what are they looking for, and what would cause them to leave immediately?"
- "What question is a first-time visitor trying to answer when they land on your site?"
- "What should visiting your website *feel* like, emotionally?"
- "What is the one thing a visitor must understand about the brand that they can't get from social media alone?"
- "Are there professional audiences — press, wholesale buyers — who need specific access?"

#### Phase 3 — Site Purpose & Structure

Lock in the primary goal, primary CTA, and content hierarchy.

- "If the site had only four pages, what would they be?"
- "What is the most important page — the one that does the most work for the brand?"
- "Is e-commerce a requirement, a nice-to-have, or out of scope?"
- "How will drops be handled? Password gates, countdowns, open release, or no drops?"
- "Does the brand need editorial content (lookbooks, journal, cultural features)? If so, who produces it and how often?"
- "Is there anything on your current site (if you have one) that must be carried forward?"

**Sitemap exercise:** "Let's map the site together. Based on what you've told me, I'd propose this structure: [proposed sitemap]. Does this feel right? What's missing?"

#### Phase 4 — Visual Direction

Bridge from Brand DNA to web-specific design language. This phase draws heavily from the existing Brand DNA document but translates it to web context.

- "Looking at your Brand DNA, your visual codes include [X, Y, Z]. How should those translate to how the website feels? For example, should the site feel like the same room we described in brand discovery?"
- "Name two or three websites — inside or outside fashion — that you wish your site resembled. What specifically about each one resonates?"
- "Name two or three websites that represent exactly what your site should NOT look like."
- "How much photography do you currently have? Is it campaign-quality editorial or product-on-white?"
- "How should the brand speak on the website? Minimal and cold, or warm and conversational? Ironic or earnest?"
- "What is the first thing a visitor's eye should land on — photography, a headline, the logo, or something else?"

**Photography dependency check:** "No other single factor affects the quality of a brand website more than photography. Do you have campaign-quality imagery ready, or is a photo shoot part of this project?" If the founder does not have editorial-quality imagery, this must be named as a blocker before any designer begins.

#### Phase 5 — Content & Constraints

Audit what the founder can provide, establish realistic scope, and surface dependencies.

- "What photography and visual assets do you currently have?"
- "Do you have product copy, a brand story, or any written content ready?"
- "Who will write the website copy — you, a copywriter, or will the agent draft it?"
- "How frequently will you update the site after launch? Seasonal drops? New editorials?"
- "Are there existing platforms you're committed to (Shopify, Squarespace, custom)?"
- "Who will maintain the site after it goes live? What's their technical skill level?"
- "What is the timeline for launch? Are there any hard deadlines?"

#### Phase 6 — Competitive Context & Positioning

Market context for differentiation.

- "Name two or three competitor websites, and tell me what they do well and what they get wrong."
- "What should your site do or feel that none of those references accomplish?"
- "Where does your brand sit on the spectrum from underground to luxury? How should the site signal that?"

#### Synthesis & Output

After completing the interview:

1. **Reflect back the site purpose statement** — confirm with the founder before proceeding
2. **Present the proposed sitemap** — verify page list and hierarchy
3. **Summarize design direction** — visual territory, personality traits, references, anti-references
4. **Name content blockers** — what must be provided before mock-up work can begin
5. **Write the full specification** to the structured YAML format defined in Section 6

**Key principles for the agent:**

1. **Lock the primary CTA before everything else.** An agent that fails to establish a single, unambiguous primary call to action has not completed strategy.
2. **Surface the photography dependency early.** This is the most common blocker for streetwear brand sites.
3. **Distinguish between what the brand wants to say and what visitors need to find.** JTBD questions bridge this gap.
4. **Name a primary audience.** A website designed for everyone is designed for no one.
5. **Produce assertions, not notes.** The output should make specific, opinionated recommendations.
6. **Flag content dependencies as blockers.** Design cannot proceed until dependencies are resolved.
7. **Capture visual references and anti-references.** These do more work for a designer than verbal descriptions.

### 8. Fashion E-Commerce UX Patterns (2024–2026)

Context for the consultation agent when advising on e-commerce decisions.

#### Mobile-First Is Non-Negotiable

Over 60% of fashion e-commerce traffic is mobile. Key mobile patterns:
- Persistent add-to-cart visible while scrolling
- Swipe galleries for product photography
- Edge-to-edge product images filling the screen
- Accelerated checkout (Shop Pay achieves 4x faster checkout)
- Performance floor: ≤200ms INP; a 1-second delay causes 7% conversion drop

#### Product Detail Page Requirements

For fashion PDPs that convert:
- HD imagery zoomable without pixellation (fabric texture matters at streetwear price points)
- Whether items run true to size, model measurements
- Fabric behavior: weight, stretch, drape, hand-feel
- Real inventory availability, not false scarcity
- Size guide above the fold (80%+ of apparel sites fail this per Baymard)
- User-generated content showing product on different body types

#### Digital Lookbooks

The most structurally important content type for fashion brands that want to increase AOV. Outfits presented as complete looks with tappable hotspots that add items to cart. Brands report 39% AOV increases from this approach.

Two failure modes:
1. Lookbook siloed in a "Journal" section users never visit
2. Lookbook designed for desktop that breaks on mobile

Best practice: embed lookbook content within product pages ("Complete the look"), not in separate editorial sections.

#### The Platform Decision

Shopify powers most notable streetwear brands (Kith, Supreme). The risk is not Shopify itself — it's the failure to invest beyond a stock theme.

- **Stock theme**: Early stage, testing viability. Acceptable.
- **Custom Shopify Plus**: Brand has established identity, needs unique experience. This is where most successful brands land.
- **Headless / fully custom**: Brands doing $20M+ DTC where 1% conversion improvement has meaningful dollar value.

Drop mechanics (password gates, countdown timers, RSVP flows, queue mechanics, regional staggering) are not edge cases for streetwear — they are core commerce flows. Standard Shopify requires apps or custom development for all of these.

---

## Sources

### Discovery & Strategy Frameworks
- Nielsen Norman Group — Discovery: Definition, Stakeholder Interviews 101, Problem Statements in UX Discovery, Audience-Based Navigation
- EightShapes — Documenting Design Discovery (Dan Brown), Tokens in Design Systems, Typography in Design Systems
- A List Apart — Practical Design Discovery, Style Tiles and How They Work
- Design Council — The Double Diamond
- Interaction Design Foundation — Design Thinking, Lean UX, Personas
- UX Design Institute — Content-First Design Guide
- Smart Insights — Web Design Personas
- User Interviews — Jobs to Be Done in UX Research

### Streetwear Web Design
- Growthcurve — Corteiz Growth Playbook
- The Page Edit — How ALD Revived Storytelling
- Mensweird (Substack) — The ALD Aesthetic
- Avex Designs — Kith eCommerce Redesign
- OPUMO Magazine — Corteiz: Streetwear's Second Coming
- Appnova — Streetwear Marketing Strategy
- Shopify — Fashion CRO Guide, Fashion Brand Storytelling, Streetwear Marketing

### Design Specification & AI Tooling
- Addy Osmani — How to Write a Good Spec for AI Agents
- Vercel — How to Prompt v0, Maximizing Outputs with v0
- Jane Street — I Design with Claude More Than Figma Now
- W3C Design Tokens Community Group — Design Tokens Specification (2025.10)
- Imperavi — Designing Semantic Colors for Your System
- Penpot — Design Tokens for Designers
- Samantha Warren — Style Tiles (styletil.es)

### Terminology & Methodology
- Figma — Wireframe vs. Mockup, UI vs. UX, Information Architecture
- UXPin — Double Diamond Design Process, Prototypes vs. Wireframes vs. Mockups
- CareerFoundry — UX vs. UI Design
- Sketch Blog — Wireframe vs. Mockup vs. Prototype
