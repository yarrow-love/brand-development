# Protective Legal Documents for Web Design Company Websites

Web design companies occupy a uniquely exposed legal position: they build the digital infrastructure where legal compliance happens for other businesses, which means their own website is held to a higher standard by clients, competitors, and regulators alike. A web design agency whose own site lacks a proper privacy policy, fails accessibility standards, or displays client work without proper authorization faces not just legal liability but credibility destruction -- the digital equivalent of a plumber with leaking pipes. The liability surface is broader than most agency owners realize. It spans intellectual property disputes over who owns delivered work, professional liability for recommendations that lead to client losses, portfolio display rights that implicate trademark law, accessibility compliance that carries federal penalty exposure, and privacy obligations multiplied by the number of third-party tools embedded in the tech stack. This report covers every protective legal document a web design company's website needs, with specific attention to how the recommended tech stack creates data handling obligations and how the unique nature of selling design services creates legal requirements that don't apply to most other service businesses.

**This report is research, not legal advice.** Every web design company should have its legal documents reviewed by a business attorney who understands technology services, intellectual property, and internet law. State requirements vary, international exposure through serving clients in other jurisdictions adds complexity, and the regulatory landscape -- particularly around accessibility and data privacy -- is shifting rapidly.

---

## Context

This research supports the brand development and web design pipeline for web design company brands. Legal documents directly shape website design: cookie consent banners affect first-visit UX, disclaimer placement determines footer layout, portfolio display restrictions constrain case study page design, and accessibility compliance dictates the entire front-end development approach.

The recommended tech stack (Astro SSR + Sanity + Cal.com + Loops + Cloudflare + Stripe) creates specific legal obligations. Cal.com collects booking data from prospective clients. Stripe processes payments and requires PCI-DSS disclosure. Loops stores email addresses and behavioral data subject to CAN-SPAM and GDPR. Cloudflare logs visitor data and may set cookies depending on the services enabled. Sanity stores content including potentially client testimonials and portfolio assets. Each service requires disclosure in the privacy policy.

```
BRAND DNA -> WEB DESIGN STRATEGY -> COPYWRITING -> LEGAL DOCUMENTS -> MOCK-UP -> FINAL BUILD
```

This report should be read alongside brand-dna.md (for positioning and messaging that affects legal claims) and web-design.md (for how legal documents integrate into site architecture and UX).

---

## Findings

### 1. The Web Design Company Legal Landscape

Web design agencies face a liability profile that differs from most service businesses in several critical ways.

#### Primary Liability Exposures

| Exposure Area | Description | Severity |
|---|---|---|
| **Professional liability** | Errors in delivered work causing client losses (broken functionality, security vulnerabilities, poor SEO implementation) | High |
| **IP ownership disputes** | Disagreements over who owns designs, code, and content after project completion | High |
| **Scope creep and change orders** | Client claims that agreed scope included work the agency considers out-of-scope | Medium-High |
| **Portfolio display** | Using client work, logos, or confidential information without proper authorization | Medium |
| **Warranty and guarantee** | Client claims that post-launch bugs or issues should be fixed indefinitely at no cost | Medium |
| **Hosting and maintenance** | Liability for downtime, data loss, or security breaches on sites the agency hosts or maintains | Medium-High |
| **Accessibility** | ADA/WCAG non-compliance on the agency's own site or on client sites the agency built | High |
| **Third-party tool failures** | Liability when a recommended platform (CMS, hosting, plugin) fails or is discontinued | Medium |
| **Content advice** | Blog posts or resources that constitute professional advice leading to client losses | Low-Medium |

#### Insurance Context

Professional liability insurance (errors and omissions / E&O) is the foundational protection. According to Insureon, the average E&O policy for web designers costs approximately $68/month with $1M per-occurrence and $1M aggregate limits and a $2,500 deductible. Technology E&O bundles professional liability with cyber liability coverage, addressing both dissatisfied-client claims and data breach exposure. General liability insurance covers bodily injury and property damage (relevant for in-person client meetings). The website's legal documents work in concert with insurance -- disclaimers and limitation of liability clauses reduce exposure, while insurance covers what remains.

---

### 2. Website Terms of Service

A web design company's Terms of Service (ToS) governs the relationship between the company and visitors to its website. This is distinct from client contracts (MSAs, SOWs) -- the ToS covers what happens when someone visits the website itself.

#### Essential Provisions

**Intellectual property notice.** The agency's website is itself a demonstration of its work. The ToS must assert copyright over all original content: page designs, layouts, copy, blog posts, graphics, icons, and code. This is both a legal protection and a market signal -- a web design company that doesn't protect its own IP cannot credibly promise to protect a client's.

Key language should cover:
- All website content is the property of the company or its licensors
- No content may be reproduced, distributed, or used without written permission
- The website design itself is proprietary and may not be copied or used as a template
- Screenshots of the site may not be used in competitor marketing

**Limitation of liability.** The ToS should limit the company's liability for information provided on the website. This is particularly important for web design companies that publish blog posts with technical advice, platform recommendations, or design guidance. Standard language limits liability to the amount paid for services (which, for website visitors who haven't purchased anything, is zero).

**User-generated content.** If the site accepts comments on blog posts, project inquiry forms, or any other user-submitted content, the ToS should address IP ownership of submissions and the company's right to use, edit, or remove them.

**Third-party links.** Web design agency sites frequently link to tools, platforms, and resources. The ToS should disclaim responsibility for third-party content and services.

**Governing law and dispute resolution.** Specify the jurisdiction whose laws govern the ToS and whether disputes will be resolved through arbitration, mediation, or litigation. Many agencies include mandatory arbitration clauses.

---

### 3. Privacy Policy

A privacy policy is legally required for any website that collects personal information. For a web design company using the recommended tech stack, the data collection footprint is substantial.

#### Data Collection Map (Stack-Specific)

| Data Source | Data Collected | Legal Basis | Disclosure Required |
|---|---|---|---|
| **Contact/inquiry forms** (Astro + Cloudflare Workers) | Name, email, phone, company name, project description, budget range | Consent (form submission) | Yes -- categories of data, purpose, retention |
| **Cal.com** (consultation booking) | Name, email, phone, appointment details, answers to intake questions, timezone | Contract performance | Yes -- Cal.com shares data with Twilio (SMS), Intercom (support), daily.co (video) |
| **Stripe** (payments/deposits) | Payment card details (processed by Stripe, not stored on-site), billing address, transaction history | Contract performance | Yes -- PCI-DSS compliance, Stripe as processor |
| **Loops** (email marketing) | Email address, name, subscription preferences, open/click behavior, device info | Consent (signup) | Yes -- behavioral tracking, CAN-SPAM compliance |
| **Cloudflare** (hosting/CDN) | IP addresses, browser fingerprint, pages visited, access timestamps, security tokens | Legitimate interest | Yes -- Cloudflare cookies, DPA required |
| **Cloudflare Web Analytics** (if enabled) | Page views, referrers, device type, country | Legitimate interest | Yes -- though cookie-free, still collects visitor data |
| **Sanity** (CMS) | Content data including any client info in testimonials or case studies | Legitimate interest / Consent | Yes if storing personal data |

#### Jurisdiction-Specific Requirements

**GDPR (EU/EEA visitors).** Even if a web design agency is US-based, serving clients in Europe or having European visitors triggers GDPR obligations. Requirements include: lawful basis for processing, explicit consent for non-essential data collection, right to access/rectify/delete data, data processing agreements with all third-party processors, Data Protection Officer designation if processing at scale, and 72-hour breach notification.

**CCPA/CPRA (California).** Applies to businesses meeting revenue or data volume thresholds. Requirements include: disclosure of categories of personal information collected and purposes, "Do Not Sell or Share My Personal Information" link, right to know, delete, and opt out, and privacy policy updates at least annually.

**State privacy laws proliferation.** By 2026, more than 20 US states have comprehensive privacy laws. Indiana, Kentucky, and Rhode Island joined the expanding list. A web design agency serving clients nationally should draft its privacy policy to the highest common standard.

**Cal.com-specific disclosure.** Cal.com's booking pages display "By proceeding, you agree to our Terms and Privacy Policy" -- linking to Cal.com's own policies, not the agency's. The agency's privacy policy should explicitly disclose that booking data is processed through Cal.com and list Cal.com's sub-processors (Twilio, Intercom, daily.co).

**Stripe-specific disclosure.** Per Stripe's Services Agreement, merchants must inform customers that Stripe processes transactions on their behalf. The privacy policy must disclose Stripe as a payment processor, note that payment card details are processed but not stored by the agency, and reference PCI-DSS compliance. The August 2025 Stripe update added AI training rights for transaction data (Section 6.2) -- agencies should be aware of this when drafting disclosures about data sharing.

---

### 4. Cookie Policy

Cookie requirements depend on what services are active and which jurisdictions the agency's visitors come from.

#### Cookie Inventory for the Recommended Stack

| Cookie Source | Cookie Type | Purpose | Consent Required? |
|---|---|---|---|
| **Cloudflare** | Functional / Security | Bot detection (`__cf_bm`), security challenge (`cf_clearance`) | EU: Debatable (strictly necessary exemption may apply). US: No |
| **Cloudflare Web Analytics** | None | Privacy-first analytics, no client-side cookies | No |
| **Cal.com embed** | Functional | Session management for booking widget | EU: Yes if non-essential. US: No |
| **Stripe** | Functional | Fraud detection, payment session | EU: Strictly necessary exemption likely applies. US: No |
| **Loops** | Tracking | Email campaign attribution, UTM tracking | EU: Yes (marketing). US: California opt-out required |
| **Google Analytics** (if used) | Tracking | Visitor behavior, demographics | EU: Yes (prior opt-in). US: California opt-out required |
| **Embedded content** (YouTube, Vimeo, social) | Third-party tracking | Video playback sets third-party cookies | EU: Yes. US: Varies |

#### Consent Requirements by Jurisdiction

| Jurisdiction | Model | Requirements |
|---|---|---|
| **EU/EEA** (GDPR + ePrivacy) | Opt-in | Prior explicit consent for all non-essential cookies. Must offer granular category toggles. "Reject All" must be as prominent as "Accept All." Fines up to 4% of global revenue or EUR 20M. |
| **UK** (UK GDPR + PECR) | Opt-in | Similar to EU. The Data Use and Access Act (June 2025) introduced five narrow exemptions for low-risk cookies, but analytics and marketing cookies still require prior consent. |
| **California** (CCPA/CPRA) | Opt-out | Disclose cookie usage. Provide "Do Not Sell or Share My Personal Information" link. Opt-in required for sale/sharing under CPRA definitions. |
| **Other US states** | Varies | 20+ states now have privacy laws. Most follow opt-out model. No federal cookie law exists. |
| **Canada** (PIPEDA) | Implied consent for non-sensitive | Disclose cookies and purposes. Opt-out mechanism required. |
| **Brazil** (LGPD) | Opt-in | Consent required. Portuguese-language notice if targeting Brazilian users. |

**Practical recommendation for web design agencies:** If the agency serves or may serve international clients, implement an opt-in cookie consent banner that meets EU standards. This satisfies the strictest jurisdiction and avoids maintaining multiple consent mechanisms. Cloudflare Web Analytics is specifically designed to work without cookies and can be used as the primary analytics tool to minimize consent friction.

---

### 5. Portfolio and Case Study Legal Considerations

This is the single most web-design-specific legal issue and the one most agencies get wrong. Displaying client work on a portfolio is not an automatic right -- it requires explicit authorization.

#### The Trademark Problem

Client logos are trademarks owned by the client. Displaying them on the agency's website without permission constitutes trademark infringement, even if the agency designed the logo. As trademark attorney Peter J. Lamont has written, "using or displaying someone's trademark without their permission is considered trademark infringement" regardless of the business relationship. The "nominative fair use" defense -- using a trademark to refer to the trademark holder -- has narrow application and does not cleanly cover portfolio marketing use.

#### Portfolio Rights Framework

| Approach | Description | Risk Level |
|---|---|---|
| **Contract clause (recommended)** | Include portfolio rights in every MSA/SOW: "Agency retains the right to display deliverables, including screenshots and client name/logo, in its portfolio, website, and marketing materials" | Lowest |
| **Post-project written permission** | Send a specific written request after project completion detailing what will be displayed | Low |
| **Verbal permission only** | Client says "sure, go ahead" without written record | High -- unenforceable if disputed |
| **No permission obtained** | Agency displays work without asking | Highest -- trademark infringement, breach of implied confidentiality |

#### NDA-Protected Work

Many enterprise and regulated-industry clients require NDAs that explicitly prohibit displaying project work. Options include:

- **Anonymized case studies:** Remove client name, logo, and identifying details. Describe the industry, challenges, and outcomes without attribution. Replace distinctive brand colors and elements with generic alternatives.
- **Process-focused case studies:** Describe the methodology, technical challenges solved, and approach taken without showing the final deliverable.
- **Redacted screenshots:** Show layout and design decisions with client branding obscured.
- **Written NDA carve-outs:** Negotiate portfolio display rights as an exception within the NDA. Many clients will agree to limited display rights when asked directly.

#### Case Study Content Risks

Beyond trademark and NDA issues, case studies can create liability through:

- **Confidential business information:** Revealing a client's revenue, conversion rates, traffic numbers, or business strategy without permission.
- **Results claims:** Stating "we increased Client X's revenue by 300%" creates an implied guarantee to prospective clients and may trigger FTC scrutiny as an endorsement.
- **Before/after screenshots:** "Before" screenshots showing a competitor agency's work could constitute disparagement if presented negatively. The previous agency may also assert copyright over their design.
- **Client approval of final text:** Even with portfolio rights, the specific language and framing of a case study should be approved by the client to avoid misrepresentation claims.

---

### 6. Intellectual Property Protection

A web design agency's website is both a marketing tool and a portfolio of protectable IP. Protecting it requires a multi-layered approach.

#### What's Protectable

| Element | Protection Type | Notes |
|---|---|---|
| **Website copy** | Copyright (automatic) | Protected upon creation. Registration provides additional enforcement benefits. |
| **Original graphics and illustrations** | Copyright (automatic) | Includes custom icons, illustrations, infographics. Stock imagery is licensed, not owned. |
| **Page layouts and design compositions** | Copyright (limited) | The specific creative expression is protectable; general layout patterns (hero + features + testimonials) are not. |
| **Source code** | Copyright (automatic) | HTML, CSS, JavaScript. Open-source components retain their original licenses. |
| **Blog content** | Copyright (automatic) | Articles, tutorials, guides. |
| **Company name and logo** | Trademark | Requires registration for strongest protection. |
| **Typography** | Not copyrightable | Typeface designs cannot be copyrighted in the US (font software can be). |
| **Color schemes** | Generally not protectable | Individual colors and basic palettes are not copyrightable or trademarkable (narrow exceptions exist for single-color marks with secondary meaning, e.g., Tiffany blue). |

#### Copyright Registration Benefits

While copyright protection is automatic upon creation, registration with the US Copyright Office provides critical enforcement advantages:

- Ability to file infringement lawsuits in federal court
- Eligibility for statutory damages (up to $150,000 per willful infringement) and attorney's fees
- Public record establishing ownership and creation date
- Registration must occur within three months of publication or before infringement to qualify for statutory damages

**For web design agencies specifically:** Registering the website as a whole (or key portfolio pieces) is advisable because the agency's own site is the primary target for competitor copying. A competitor who lifts an agency's layout, copy structure, or design approach is committing infringement -- but enforcement is dramatically easier with registration.

#### Practical IP Protection Measures

- Display a copyright notice in the website footer: "(c) [Year] [Company Name]. All rights reserved."
- Include IP protection language in the Terms of Service
- Use DMCA takedown procedures for infringing content (register a DMCA agent with the Copyright Office)
- Monitor for design theft using reverse image search and visual similarity tools
- Watermark portfolio images where appropriate (though this can detract from presentation quality)

---

### 7. Testimonial Disclaimers

The FTC's updated Endorsement Guides (2023) and the Consumer Reviews and Testimonials Rule (effective October 21, 2024) set clear requirements for how businesses display testimonials.

#### FTC Requirements for Web Design Agency Testimonials

**Truthfulness.** All testimonials must reflect the honest opinions and genuine experiences of the endorser. Testimonials cannot be fabricated, and endorsements must reflect the endorser's actual views.

**Material connection disclosure.** If the testimonial provider received any compensation, discount, free services, or other benefit, that connection must be disclosed clearly and conspicuously near the testimonial. For web design agencies, this includes:

- Clients who received a discount in exchange for a testimonial
- Clients who are personal friends or family members of the agency owner
- Partners or vendors who provide reciprocal testimonials
- Employees or contractors posting reviews

**Results claims.** This is where web design agency testimonials create the most risk. A testimonial stating "My website traffic tripled after working with [Agency]" implies that similar results are typical. Under the 2023 Endorsement Guides, the "results not typical" disclaimer is no longer sufficient. The FTC now requires either:

1. That the advertiser have adequate substantiation that the endorser's experience is representative of what consumers will generally achieve, or
2. A clear and conspicuous disclosure of the generally expected results

**Review management.** The 2024 Consumer Reviews and Testimonials Rule prohibits:

- Creating or buying fake reviews
- Suppressing negative reviews selectively (cherry-picking only positive ones)
- Using AI-generated reviews
- Insider reviews without disclosure
- Intimidating or threatening customers to prevent negative reviews

**Intermediary liability.** The FTC has expressly included "intermediaries" -- including advertising agencies and marketing firms -- within its definition of "advertisers." A web design agency that also handles marketing for clients could face FTC liability for testimonials on client websites it builds and manages.

#### Recommended Testimonial Disclaimer Language

A general disclaimer should accompany the testimonials section:

"Client testimonials reflect individual experiences and results. Your results may vary based on your project scope, industry, goals, and other factors. Testimonials are not guarantees of future performance or outcomes."

For testimonials that include specific metrics or results claims, add:

"Results described are specific to this client's project and circumstances and should not be interpreted as typical or guaranteed outcomes."

---

### 8. Disclaimer Needs

Web design agencies need several specific disclaimers beyond the standard business website requirements.

#### Project Timeline Disclaimers

Web design projects are notorious for timeline disputes. The website should include clear language that:

- Estimated timelines are not guaranteed delivery dates
- Timelines depend on timely client feedback and content delivery
- Projects delayed more than a specified period (common: 12 months) due to client inaction may be considered complete, with remaining balance invoiced
- Rush projects may incur additional fees

#### Results Disclaimers

Any claims about business outcomes from web design services need qualification:

- "A professionally designed website is one component of business success. We do not guarantee specific business outcomes including but not limited to increased revenue, traffic, leads, or conversions."
- "Past project results shown in our portfolio are specific to those clients' circumstances and should not be interpreted as typical or guaranteed."

#### Third-Party Platform Disclaimers

Web design agencies recommend and implement numerous third-party tools. The website should disclaim responsibility for:

- Third-party platform functionality, uptime, pricing changes, or discontinuation
- WordPress plugin conflicts, CMS updates that break functionality, or hosting provider failures
- Changes to platform terms of service that affect client websites
- Third-party security breaches or data handling practices

**Specific to the recommended stack:** "Our websites are built on third-party platforms and services including but not limited to Astro, Sanity, Cloudflare, Cal.com, Loops, and Stripe. We are not responsible for changes to, outages of, or discontinuation of these services. We recommend reviewing each service's terms and privacy policies."

#### Hosting and Maintenance Disclaimers

If the agency provides hosting or maintenance services:

- No guarantee of 100% uptime (industry standard is 99.9%, which still allows approximately 8.7 hours of downtime per year)
- Not responsible for data loss due to client actions, third-party breaches, or force majeure events
- Maintenance plans cover specified services only; out-of-scope requests are billable
- The agency is not responsible for client-initiated changes that break functionality

#### Blog and Resource Disclaimers

Web design agency blogs often contain technical recommendations, platform comparisons, and strategic advice. This content needs an informational disclaimer:

"The content on this website, including blog posts, guides, and resources, is provided for informational and educational purposes only. It does not constitute professional advice. Specific technology decisions should be made based on your unique business requirements, and we recommend consulting with qualified professionals for your particular situation."

This disclaimer should appear:
- On a dedicated disclaimer page linked from the footer
- Inline at the top or bottom of blog posts containing recommendations
- On any page offering free resources, guides, or tools

---

### 9. Professional Liability

Professional liability -- also known as errors and omissions (E&O) -- is the risk that the agency's professional work or advice causes a client financial harm. For a web design company, this extends beyond delivered project work to content published on the company's own website.

#### Scope of Professional Advice on the Website

| Content Type | Liability Risk | Example |
|---|---|---|
| **Blog posts with platform recommendations** | Medium | "WordPress is the best CMS for small businesses" -- if a client relies on this and WordPress is wrong for their use case |
| **Pricing guidance** | Medium | "A typical website costs $5,000-$15,000" -- client may claim reliance on estimate |
| **Technical tutorials** | Low-Medium | Step-by-step guides that, if followed incorrectly, could break a client's existing site |
| **SEO advice** | Medium | SEO recommendations that conflict with current algorithm updates |
| **Security recommendations** | High | Security advice that proves inadequate, leading to a breach |
| **Plugin/tool recommendations** | Medium | Recommending a tool that later has a security vulnerability or is discontinued |

#### Limiting Professional Liability Through Website Documents

1. **Terms of Service:** Include language that website content is informational only, not professional advice, and that reliance on website content is at the visitor's own risk.
2. **Blog disclaimers:** Add disclaimers to blog posts and resource pages clarifying that content does not create a professional relationship.
3. **No professional relationship language:** Clearly state that visiting the website or consuming content does not create a client-agency relationship.
4. **Limitation of liability:** Cap any potential liability at the amount paid for services (which is zero for website visitors).
5. **E&O insurance:** Maintain professional liability insurance. Average cost for web designers is approximately $816/year ($68/month) for $1M coverage through providers like Hiscox, Insureon, or Embroker.

#### Warranty Period Considerations

Industry standard for post-launch warranty periods:

| Duration | Coverage | Common Practice |
|---|---|---|
| **30 days** | Bug fixes for issues within original scope | Minimum standard |
| **60 days** | Bug fixes, minor adjustments | Common |
| **90 days** | Bug fixes, browser compatibility, performance issues | Best practice |
| **Beyond 90 days** | Requires maintenance agreement | Standard |

A "bug" should be defined clearly -- typically as any feature that no longer functions as it did during the User Acceptance Testing (UAT) phase. Warranty should explicitly exclude: new feature requests, design changes, content updates, third-party CMS or plugin issues, and problems caused by client modifications.

---

### 10. Accessibility Compliance

Accessibility is the area where a web design agency faces the most unique reputational and legal exposure. A web design company whose own website fails WCAG standards is the digital equivalent of a dentist with bad teeth -- it undermines the entire business proposition.

#### The Legal Landscape (2025-2026)

**ADA Title III (private businesses).** 5,114 ADA digital accessibility lawsuits were filed in 2025, a 37% year-over-year increase. eCommerce sites account for 70% of cases, but service businesses including agencies are increasingly targeted. New York, Florida, and California account for over 74% of filings, with Illinois emerging as a growing jurisdiction (237 lawsuits in H1 2025 alone). Federal pro se ADA Title III lawsuits increased 40% in 2025, driven in part by AI tools enabling individuals to draft and file complaints without legal representation.

**ADA Title II (government entities).** The DOJ's final rule under Title II requires state and local government websites to conform to WCAG 2.1 Level AA. The compliance deadline for entities with populations of 50,000+ is **April 24, 2026**. Smaller entities and special districts have until April 2027. This is directly relevant to web design agencies because agencies that build government websites will face contractual liability if those sites don't meet the new standard.

**European Accessibility Act (EAA).** Takes effect June 28, 2025, requiring private-sector digital products and services sold in the EU to meet accessibility standards. Agencies serving European clients or building products for the EU market need to account for this.

#### WCAG 2.1 AA: The Standard

WCAG 2.1 AA is the de facto compliance standard referenced by ADA litigation, the DOJ's Title II rule, and most accessibility statutes worldwide. Key principles:

- **Perceivable:** Content is presented in ways all users can perceive (alt text, captions, contrast ratios)
- **Operable:** Interface components are operable by all users (keyboard navigation, no seizure triggers, sufficient time limits)
- **Understandable:** Information and UI operation are understandable (readable text, predictable navigation, input assistance)
- **Robust:** Content is robust enough to be interpreted by assistive technologies (valid markup, ARIA attributes)

#### Accessibility Overlays Are Not a Solution

The FTC's $1 million settlement with accessiBe (January 2025, finalized April 2025) confirmed what accessibility professionals have argued for years: automated overlay widgets do not make websites WCAG-compliant. The FTC found that accessiBe's claims that its "one line of code" could achieve full WCAG compliance were "false, misleading, or unsubstantiated." The settlement also revealed that accessiBe had deceptively formatted third-party articles to appear as independent reviews.

For web design agencies, the implications are clear:

- Do not use accessibility overlays on the agency's own website
- Do not recommend overlays to clients as a compliance solution
- If asked about overlays, advise clients that they do not satisfy ADA requirements and cite the FTC enforcement action
- Build accessibility into the development process from the start using semantic HTML, proper ARIA implementation, and manual testing with assistive technologies

#### VPAT Considerations

A Voluntary Product Accessibility Template (VPAT) is a self-disclosure document that evaluates a product's conformance with accessibility standards (Section 508, WCAG 2.1, EN 301 549). While primarily used for products sold to government agencies, a VPAT can differentiate a web design agency:

- Agencies bidding on government contracts will increasingly need to provide VPATs for their deliverables
- Creating a VPAT for the agency's own website demonstrates accessibility competence
- The ITI VPAT 2.5 template has four editions: 508 (US federal), EU (EN 301 549), WCAG, and INT (all three combined)

#### The Agency's Own Site as a Standard

A web design agency's website should meet or exceed WCAG 2.1 AA as a baseline. This means:

- All images have descriptive alt text
- Color contrast ratios meet minimum thresholds (4.5:1 for normal text, 3:1 for large text)
- Full keyboard navigability with visible focus indicators
- Proper heading hierarchy and semantic HTML
- Form labels properly associated with inputs
- Skip navigation links
- Responsive design that works with screen magnification
- No content that relies solely on color to convey meaning
- Video content has captions and transcripts

---

### 11. Contract Considerations on the Website

While the primary focus of this report is the agency's website legal documents (not client contracts), the website should properly reference and make available the agency's contractual framework.

#### How the Website Should Reference Contracts

**MSA (Master Service Agreement).** The MSA governs the overall client-agency relationship and typically covers: intellectual property ownership and transfer terms, confidentiality and NDA provisions, limitation of liability (commonly capped at fees paid under the relevant SOW, or 6-12 months of retainer fees), indemnification, termination provisions, governing law, and dispute resolution (mediation or arbitration before litigation).

The website does not need to publish the full MSA, but should reference its existence on the engagement process or "how we work" page, and make clear that all projects are governed by a formal agreement.

**SOW (Statement of Work).** Each project gets its own SOW defining scope, deliverables, timeline, milestones, payment schedule, and change order procedures. The website should explain the SOW process on the services or process page so prospective clients understand that scope will be formally documented before work begins.

**Payment terms.** The website should disclose general payment structure (deposit required, milestone billing, payment upon completion) without necessarily specifying exact amounts. Stripe integration means the agency must comply with Stripe's Services Agreement, which requires disclosing that Stripe processes payments and that card details are handled by Stripe, not stored by the agency.

#### Key Contract Clauses to Reference on the Website

| Clause | Website Reference |
|---|---|
| **Scope definition and change orders** | Process page: "All projects begin with a detailed scope document. Changes to scope require a written change order with revised timeline and cost." |
| **IP transfer** | Services or FAQ page: "Upon final payment, you own your website. We retain the right to display completed work in our portfolio." |
| **Portfolio rights** | Built into IP transfer language or as a separate clause visible on the website |
| **Payment terms** | Pricing or process page: "Projects require a deposit to begin. We invoice at milestones. Final payment is due before launch." |
| **Warranty period** | Services or FAQ page: "All projects include a [30/60/90]-day warranty period for bug fixes after launch." |
| **Termination** | Can be referenced in FAQ: "Either party may terminate with [30] days written notice. Client pays for all work completed to date." |

---

## Trade-offs & Recommendations

### Key Trade-offs

| Decision | Option A | Option B | Recommendation |
|---|---|---|---|
| **Cookie consent approach** | Minimal compliance (US-only opt-out) | Full GDPR-compliant opt-in banner | **Option B** -- higher standard protects against international exposure and signals professionalism |
| **Privacy policy scope** | Single-jurisdiction focus | Multi-jurisdiction comprehensive policy | **Option B** -- web design agencies serve clients who may be in any jurisdiction |
| **Accessibility standard** | WCAG 2.0 A (minimum) | WCAG 2.1 AA (recommended standard) | **Option B** -- a web design agency must exceed minimum standards for credibility |
| **Portfolio display approach** | Display all work freely | Formal written permission for every piece | **Option B** -- build portfolio rights into contracts going forward; retroactively obtain written permission for existing work |
| **Legal document display** | Minimal footer links | Comprehensive legal center with all documents | **Option B** -- a web design agency's own legal setup is a sales tool |
| **Blog disclaimers** | None or minimal | Inline disclaimers on technical content | **Option B** -- professional advice liability is real, and disclaimers are cheap insurance |
| **Accessibility overlay** | Use an overlay for quick compliance | Manual WCAG implementation | **Manual implementation** -- overlays are discredited (FTC action), and a web design agency using one is a reputational liability |

### Priority Document List

Create these documents in this order:

1. **Privacy Policy** -- legally required, covers the broadest liability surface, and must be in place before collecting any data through forms, analytics, or email signups
2. **Terms of Service** -- establishes IP protection, limitation of liability, and governs all website interactions
3. **Cookie Policy** -- required if any non-essential cookies are set; can be integrated into the privacy policy or stand alone
4. **Portfolio Display Agreement** -- template clause for contracts and retroactive permission requests for existing portfolio items
5. **Accessibility Statement** -- declares the agency's commitment to WCAG 2.1 AA compliance, provides feedback mechanism, and documents known issues and remediation timeline
6. **Blog/Content Disclaimer** -- covers professional advice liability for published content
7. **Testimonial Disclaimer** -- FTC-compliant disclosure language for client testimonials
8. **MSA/SOW Templates** -- while not website legal docs per se, these should be updated to include portfolio rights, IP transfer language, warranty terms, and accessibility responsibility clauses

### Implementation Notes

- All legal documents should be accessible from the website footer
- Cookie consent should load before any non-essential scripts fire
- The privacy policy must be updated whenever a new third-party service is added to the stack
- Testimonials should be reviewed for FTC compliance before publishing
- Portfolio work should be audited for proper authorization
- The agency's own website should pass a WCAG 2.1 AA audit before launch -- this is both a legal requirement and a business-critical credibility signal
- Consider using Termageddon or a similar legal policy management service to auto-update policies when laws change

---

## Sources

1. [Hiscox -- Web Designer Insurance](https://www.hiscox.com/small-business-insurance/professional-business-insurance/web-design-insurance) -- Professional liability and E&O insurance specifics for web designers
2. [Insureon -- Web and UX/UI Designer Business Insurance](https://www.insureon.com/technology-business-insurance/web-designers) -- Insurance cost benchmarks and coverage details
3. [Embroker -- Insurance for Website Designers](https://www.embroker.com/blog/insurance-for-website-designers/) -- Technology E&O and cyber liability coverage explanations
4. [Termageddon -- How Agencies Can Protect Themselves](https://termageddon.com/how-agencies-can-protect-themselves-and-limit-their-own-liability-when-building-websites-for-clients/) -- Agency-specific liability limitation strategies
5. [Matchstick Legal -- Limitation of Liability Clauses for Creative Agencies](https://matchstick.legal/blog/limitation-liability-clause-agency-service-agreements) -- LOL clause types and recommended caps
6. [LegalGPS -- Client vs. Agency IP Rights](https://www.legalgps.com/creative-services-agreement/client-vs-agency-intellectual-property-rights-ownership) -- IP ownership in creative services agreements
7. [Phil Nicolosi Law -- Using Clients' Logos on Website and Marketing Materials](https://www.pjlesq.com/post/using-your-clients-logos-on-website-and-marketing-materials) -- Trademark implications of portfolio display
8. [Owen, Wickersham & Erickson -- Portfolio Rights](https://www.owe.com/resources/legalities/19-portfolio-rights/) -- Legal framework for designer portfolio display rights
9. [Interaction Design Foundation -- How to Handle NDAs in Case Studies](https://www.interaction-design.org/literature/article/how-to-handle-non-disclosure-agreements-ndas-when-you-write-your-ux-case-study) -- Practical guidance on NDA-compliant portfolio work
10. [FTC -- Endorsement Guides (16 CFR Part 255)](https://www.ftc.gov/legal-library/browse/federal-register-notices/16-cfr-part-255-guides-concerning-use-endorsements-testimonials-advertising) -- Updated 2023 endorsement and testimonial requirements
11. [FTC -- Consumer Reviews and Testimonials Rule](https://www.ftc.gov/business-guidance/advertising-marketing/endorsements-influencers-reviews) -- 2024 rule on review management and fake reviews
12. [Share.One -- FTC Testimonial Guidelines 2026](https://www.share.one/ftc-testimonial-guidelines-2026/) -- Current state of FTC enforcement
13. [Accessible.org -- 2026 ADA Website Compliance Predictions](https://accessible.org/2026-ada-website-compliance-lawsuits-ai/) -- Lawsuit trends and AI-driven filing increases
14. [DarrowEverett LLP -- The Rising Tide of ADA Website Accessibility Litigation](https://darroweverett.com/ada-website-accessibility-litigation-insights-legal-analysis/) -- 2025 litigation analysis and trends
15. [ADA.gov -- First Steps Toward Web Accessibility Compliance](https://www.ada.gov/resources/web-rule-first-steps/) -- DOJ Title II requirements and compliance timeline
16. [ArcStone -- The April 2026 Web Accessibility Deadline](https://www.arcstone.com/the-april-2026-web-accessibility-deadline-what-your-organization-needs-to-know/) -- Title II deadline details for public entities
17. [FTC -- accessiBe $1 Million Settlement](https://www.ftc.gov/news-events/news/press-releases/2025/01/ftc-order-requires-online-marketer-pay-1-million-deceptive-claims-its-ai-product-could-make-websites) -- Enforcement action against accessibility overlay provider
18. [Lainey Feingold Law -- FTC accessiBe Fine](https://www.lflegal.com/2025/01/ftc-accessibe-million-dollar-fine/) -- Analysis of the overlay enforcement action
19. [CookieYes -- Cookie Consent Trends by Country 2026](https://www.cookieyes.com/blog/cookie-consent-trends/) -- Global cookie consent requirements
20. [Termly -- Cookie Law Guide](https://termly.io/resources/articles/cookie-law/) -- EU, US, and UK cookie consent comparison
21. [Gerrish Legal -- Cookie Compliance in 2026](https://www.gerrishlegal.com/blog/cookie-compliance-in-2026-where-gdpr-enforcement-stands-now) -- Current GDPR enforcement posture on cookies
22. [Cal.com -- Privacy Policy](https://cal.com/privacy) -- Cal.com data collection and third-party sharing disclosures
23. [Stripe -- Services Agreement](https://stripe.com/legal/ssa) -- Merchant disclosure and PCI-DSS compliance requirements
24. [Stripe -- Data Processing Agreement](https://stripe.com/legal/dpa) -- GDPR data processing requirements for Stripe merchants
25. [FTC -- CAN-SPAM Act Compliance Guide](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business) -- Email marketing legal requirements
26. [Loops -- Privacy Policy](https://loops.so/privacy) -- Loops data handling and scanning practices
27. [Cloudflare -- Cookie Documentation](https://developers.cloudflare.com/fundamentals/reference/policies-compliances/cloudflare-cookies/) -- Cloudflare cookie types and disclosure requirements
28. [Cloudflare -- GDPR Compliance](https://www.cloudflare.com/trust-hub/gdpr/) -- Cloudflare's GDPR compliance framework
29. [Daniel Ross Law -- Can I Copyright My Website Design?](https://danielrosslawfirm.com/2024/01/13/can-i-copyright-my-website-design-insights-from-daniel-ross-and-associates/) -- Copyright protection scope for web designs
30. [Pinsent Masons -- IP in Websites: Ownership and Protection](https://www.pinsentmasons.com/out-law/guides/intellectual-property-in-websites-ownership-and-protection) -- Comprehensive IP ownership framework for websites
31. [Terms.Law -- Change Management Contracts](https://terms.law/Software-Dev-Contracts/change-management-contracts.html) -- Scope creep and change order contract provisions
32. [US Law Explained -- Scope Creep: The Ultimate Legal Guide](https://uslawexplained.com/scope_creep) -- Legal framework for scope disputes
33. [WebDesignLaw.com -- Full Terms and Conditions](http://webdesignlaw.com/contracts/full-terms-and-conditions.html) -- Comprehensive web design contract terms reference
34. [Section508.gov -- VPAT FAQ](https://www.section508.gov/sell/acr-vpat-faq/) -- Voluntary Product Accessibility Template guidance
35. [ITIC -- VPAT](https://www.itic.org/policy/accessibility/vpat) -- Official VPAT template and editions
36. [EcomBack -- 2025 Mid-Year ADA Website Accessibility Lawsuit Report](https://www.ecomback.com/ada-website-lawsuits-recap-report/2025-mid-year-ada-website-lawsuit-report) -- Detailed lawsuit statistics and trends
37. [The CEO Legal Loft -- Website Disclaimer Examples 2026](https://theceolegalloft.com/examples-of-disclaimers/) -- Current disclaimer examples and best practices
38. [TermsFeed -- Blog Disclaimers](https://www.termsfeed.com/blog/blog-disclaimer/) -- Professional advice disclaimer guidance for blogs
39. [Termly -- CCPA Privacy Policy Requirements](https://termly.io/resources/articles/ccpa-privacy-policy/) -- California privacy policy compliance guide
40. [SecurePrivacy -- CCPA Privacy Policy Requirements 2025](https://secureprivacy.ai/blog/ccpa-privacy-policy-requirements-2025) -- Updated CCPA compliance requirements
