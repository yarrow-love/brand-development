# Legal Writing

Structured workflow for drafting protective legal documents for a brand's website — disclaimers, privacy policy, terms of service, and informed consent language. Conducted by a subagent using industry research and the brand's accumulated artifacts, then reviewed with the client in the main thread.

## When to Use

- After copywriting is complete and before or alongside mock-up
- The brand's website will collect personal data, offer services, or publish testimonials
- The client needs disclaimers, privacy policy, terms of service, or informed consent language
- Especially critical for healing practitioners, wellness providers, and anyone operating near the boundary of medical claims

## Prerequisites

**Brand DNA, web design strategy, and copy should exist.** Legal documents need to reference the brand's specific offerings, data collection practices, and content to be accurate.

Before starting, verify:
1. Brand DNA exists at `brands/<brand>/brand-dna.md` — provides offerings, modalities, and values
2. Web design strategy exists at `brands/<brand>/web-design-strategy.md` — provides site architecture, booking flow, and tech stack context
3. Copy exists at `brands/<brand>/copy.md` — provides the actual claims and language used on the site that legal documents must protect

## Context

**Industry research:** Read `research/<industry>/legal.md` for industry-specific legal guidance — regulatory landscape, disclaimer requirements, compliance considerations, and template language. If no legal research exists, recommend generating it via `/research` before proceeding.

**Tech stack:** If known, identify which third-party services process personal data (booking systems, payment processors, email services, analytics, CDN, video hosting). Each must be disclosed in the privacy policy.

## Context Window Strategy

Legal document drafting is research-heavy and template-driven — ideal for subagent delegation. The main thread stays focused on client review and approval.

```
Main thread (consultant + client):     Subagent (drafts):
┌─────────────────────────────┐        ┌──────────────────────────┐
│ Explain what's needed & why │───────>│ Read brand artifacts     │
│ Get client input on details │        │ Read legal research      │
│ Wait for drafts             │<───────│ Draft all legal docs     │
│ Review with client          │        │ Write to brands/<brand>/ │
│ Adjust as needed            │        └──────────────────────────┘
└─────────────────────────────┘
```

### Subagent Dispatch Pattern

```
Dispatch a subagent with this prompt:

"Draft protective legal documents for the [brand name] website.

Read these files for context:
- Brand DNA: brands/<brand>/brand-dna.md
- Web design strategy: brands/<brand>/web-design-strategy.md
- Website copy: brands/<brand>/copy.md
- Legal research: research/<industry>/legal.md

Brand-specific details:
- Business name: [legal entity name]
- Practitioner name: [name]
- Location/jurisdiction: [state/country]
- Modalities offered: [list]
- Data collection points: [booking system, payment, email signup, contact forms, analytics, video]
- Tech stack (if known): [services used]
- Testimonials: [will the site publish client testimonials?]
- Affiliate links: [does the site include affiliate product links?]
- Health information collection: [does the booking/intake process collect health data?]

Draft the following documents to brands/<brand>/legal.md:

1. **Medical/Healing Disclaimer**
   - Medical non-substitution statement
   - Results disclaimer (individual results vary)
   - Risk assumption language for physical modalities (acupuncture, bodywork)
   - Scope of practice statement
   - Language should be clear and warm, not cold legalese — consistent with the brand voice while remaining legally protective

2. **Privacy Policy**
   - What data is collected and by which services
   - How data is used
   - Third-party processors with links to their privacy policies
   - Cookie/tracking disclosure
   - User rights (access, correction, deletion)
   - GDPR considerations (if serving international clients)
   - CCPA/state privacy law considerations
   - Health information handling (if applicable)
   - Contact information for privacy inquiries

3. **Terms of Service**
   - Scope of services and limitations
   - Booking and cancellation policy framework
   - Payment terms
   - Intellectual property (website content)
   - Limitation of liability
   - Dispute resolution
   - Governing law

4. **Testimonial Disclaimer**
   - Individual results statement
   - FTC compliance language
   - Placed inline near testimonials and on the legal page

5. **Affiliate Disclosure** (if applicable)
   - FTC-required disclosure for affiliate links
   - Clear statement that the practitioner may receive compensation
   - Placed on product gallery page and in the legal page

6. **Inline Disclaimers**
   - Abbreviated footer disclaimer (1-2 sentences for every-page footer)
   - Offerings page inline disclaimer
   - Blog post disclaimer template

Format: Use pure markdown, no YAML. Organize under clear headings. Include placement notes indicating where each piece of text should appear on the website.

Important: Include a prominent note at the top that these documents should be reviewed by a licensed attorney before publication. This is template language, not legal advice."
```

## The Legal Writing Process

### Step 1 — Gather Details (Main Thread)

Before dispatching the subagent, confirm with the client:

- Legal business name and jurisdiction
- Whether they collect health information through booking/intake forms
- Their cancellation policy preferences (timeframe, fees)
- Whether they publish client testimonials
- Whether they use affiliate links
- Whether they serve clients internationally (GDPR relevance)
- Any existing legal documents they want to incorporate or replace

### Step 2 — Dispatch Subagent

Send the subagent with the full context. Continue the main consultation while it drafts.

### Step 3 — Review with Client (Main Thread)

When the subagent completes:

1. Summarize what was drafted and why each document matters
2. Walk through key decisions that need the client's input (cancellation timeframe, dispute resolution approach, etc.)
3. Flag any areas where state-specific legal review is especially important
4. Confirm placement: where each disclaimer appears on the site

### Step 4 — Recommend Legal Review

Explicitly recommend that the client have the documents reviewed by an attorney before publication. Name this as a dependency for launch, not an optional nice-to-have.

## Output Format

Write the legal documents to `brands/<brand>/legal.md` using pure markdown:

```markdown
---
title: Legal Documents
tags: [legal, compliance, policy]
last_updated: YYYY-MM-DD
brand: {brand-name}
status: DRAFT — requires attorney review before publication
---

# Legal Documents — {Brand Name}

> **Important:** These documents are templates drafted from industry research and best practices. They are not legal advice. Have all legal documents reviewed by a licensed attorney in your jurisdiction before publishing on your website.

---

## Medical / Healing Disclaimer

**Placement:** Dedicated `/legal` page, abbreviated version in site footer, inline on offerings pages and health-related blog posts.

{Disclaimer text}

---

## Privacy Policy

**Placement:** Dedicated `/legal` or `/privacy` page, linked from site footer.

{Privacy policy text with sections for each required element}

---

## Terms of Service

**Placement:** Dedicated `/legal` or `/terms` page, linked from site footer.

{Terms text}

---

## Testimonial Disclaimer

**Placement:** On testimonials page (above or below testimonials), on `/legal` page, inline wherever testimonials appear on other pages.

{Testimonial disclaimer text}

---

## Affiliate Disclosure

**Placement:** On product gallery page (visible before affiliate links), on `/legal` page.

{Affiliate disclosure text}

---

## Inline Disclaimers

### Footer Disclaimer
**Placement:** Every page footer, abbreviated.

{1-2 sentence footer disclaimer}

### Offerings Page Disclaimer
**Placement:** Bottom of offerings/services page.

{Inline disclaimer for service descriptions}

### Blog Post Disclaimer
**Placement:** Bottom of health-related blog posts.

{Blog disclaimer template}
```

### Writing Guidelines

- **Warm but protective.** Legal documents can be clear and human without sacrificing legal strength. Avoid unnecessarily cold legalese, but don't sacrifice precision for warmth.
- **Pure markdown, no YAML.** Consistent with all other brand artifacts.
- **Placement notes are critical.** The mock-up agent needs to know where each piece of legal text appears in the site layout.
- **Industry-specific.** Reference the legal research for the client's industry. Healing practitioners have different requirements than e-commerce or SaaS.
- **Flag uncertainties.** If a legal question depends on state law or the client's specific circumstances, say so explicitly rather than guessing.
- **Include the attorney review caveat prominently.** This is not optional.

## Integration with Other Phases

- **Mock-up:** The mock-up agent reads `legal.md` for footer disclaimer text, placement of disclaimer links, and any inline disclaimers that need to appear on specific pages.
- **Final build:** Legal pages become part of the site architecture. Cookie consent banners (if needed) are implemented based on the privacy policy's cookie disclosure.
- **Copywriting:** The copy should already follow FTC-safe language patterns (experience language, not outcome claims). Legal documents formalize this protection.

The legal documents at `brands/<brand>/legal.md` should be read alongside the web design strategy when producing mock-ups, to ensure all required legal text is placed correctly.
```

