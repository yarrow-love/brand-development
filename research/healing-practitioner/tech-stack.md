# Tech Stack for Healing Practitioner Websites

The ideal tech stack for a healing practitioner website balances four competing concerns: code-first design freedom, easy content management for the practitioner, seamless scheduling with integrated payments, and minimal ongoing cost and technical debt. This report evaluates the leading options and recommends a specific stack based on research into Squarespace, Cal.com, Astro, Cloudflare Pages, and Decap CMS.

---

## Context

The brand development pipeline produces a complete HTML/Tailwind mock-up at `brands/<brand>/mock-up/`. The final build phase must translate this mock-up into a production website that:

1. Preserves the design exactly (code-first — no visual editor adaptation)
2. Lets the practitioner edit copy without a developer (content management)
3. Integrates scheduling with payment collection at time of booking
4. Costs as little as possible to host and maintain
5. Avoids re-deploys where possible (or makes them invisible)
6. Minimizes technical debt (fewer moving pieces, less maintenance)

Prior experience: Astro + Koalendar integration was unsatisfactory — the scheduling embed felt foreign and poorly integrated. This research seeks a better solution.

Relevant existing docs:
- Mock-up skill: `.claude/skills/mockup.md`
- Web design research: `research/healing-practitioner/web-design.md`
- Cal.com payment research: `research/healing-practitioner/cal-com-payment-integration.md`

---

## Findings

### 1. Platforms Evaluated and Eliminated

#### Squarespace — Not Viable for Code-First

Squarespace's Developer Mode is locked to the legacy v7.0 architecture. All new sites since 2020 use v7.1, which has no code access. Even on v7.0, developers write in JSON-T (a proprietary templating language), not real HTML. There is no CLI deployment, no REST API for code, no staging environment, and no way to deploy an HTML/Tailwind codebase to Squarespace.

**Verdict:** Architecturally incompatible with a code-first workflow. Eliminated.

#### WordPress — Too Much Maintenance

WordPress can handle everything (content, booking, payments) but carries significant technical debt: security updates, plugin conflicts, PHP hosting, database management. For a 4–6 page practitioner site, this is overengineered.

**Verdict:** Viable but wrong trade-off for this use case. Eliminated.

#### Wix — Same Problems as Squarespace

Visual-editor-first platform with limited code access. No way to deploy custom HTML/Tailwind.

**Verdict:** Eliminated for the same reasons as Squarespace.

### 2. The Recommended Stack

#### Astro + Cloudflare Pages + Cal.com + Decap CMS

| Component | Role | Cost |
|---|---|---|
| **Astro** | Static site generator — transforms our mock-up into a production build | Free (open source) |
| **Cloudflare Pages** | Hosting — fast, global CDN, auto-deploys from git | Free (already have account) |
| **Cal.com** | Scheduling + payments — embedded booking with Stripe integration | Free (individual plan) |
| **Decap CMS** | Content management — web-based editor for the practitioner | Free (open source) |
| **Total** | | **$0/month** |

### 3. Component Deep Dive

#### Astro — Site Generator

Astro is the right generator for this use case because:

- **HTML-first** — our Tailwind mock-up translates directly. Astro components are essentially HTML files with optional frontmatter
- **Zero JavaScript by default** — the output is static HTML/CSS. No client-side framework shipped to the browser unless explicitly needed
- **Content Collections** — Astro's content layer reads markdown/YAML files and makes them available to templates. Copy changes happen in content files, not in component markup
- **Fast builds** — a 4–6 page site builds in seconds on Cloudflare Pages
- **Island architecture** — if Cal.com's embed needs client-side JavaScript, it loads only in that component, not site-wide

The mock-up-to-Astro conversion:
```
brands/<brand>/mock-up/index.html    →  src/pages/index.astro
brands/<brand>/mock-up/about.html    →  src/pages/about.astro
brands/<brand>/mock-up/css/style.css →  src/styles/global.css
brands/<brand>/copy.md               →  src/content/copy.yaml (structured)
Tailwind CDN                         →  @astrojs/tailwind integration
```

#### Cloudflare Pages — Hosting

- **Free tier** — unlimited sites, unlimited bandwidth, 500 builds/month
- **Auto-deploy from git** — push to main, site rebuilds in ~30 seconds
- **Global CDN** — fast load times everywhere
- **Custom domains** — free SSL, DNS already managed in Cloudflare
- **Preview deployments** — every branch gets a preview URL for client review before merging

The user already has a Cloudflare account. No new service to set up.

#### Cal.com — Scheduling + Payments

Cal.com resolves the Koalendar frustration with better embed quality and payment integration on the free tier.

**Payment capabilities (free plan):**

| Feature | Supported |
|---|---|
| Charge at booking | Yes |
| Authorization hold (no-show deterrence) | Yes |
| Configurable no-show fees | Yes |
| Stripe (cards, Apple Pay, Google Pay) | Yes |
| PayPal | Yes |
| Embedded checkout (no redirect) | Yes |
| Custom embed styling | Yes |

**What Cal.com cannot do:**
- True deposits (partial payment, collect remainder later)
- Session packages or bundles ("5 sessions for $X")
- Recurring billing / subscriptions / memberships
- Gift certificates
- Invoicing
- Coupon / discount codes

**Embed integration:**
Cal.com offers three embed modes — inline, pop-up, and floating button. The full booking + payment flow happens within the embed without redirecting. The embed can be styled to match the site's design tokens ("make your embed look like an indiscernible part of your website"). Implementation is a copy-paste code snippet or React component.

**Upgrade path:** If the practitioner eventually needs packages, memberships, or gift certificates, Acuity Scheduling (~$20/month, owned by Squarespace) is the natural upgrade. Acuity supports all of those features and embeds well into custom sites.

#### Decap CMS — Content Management

Decap CMS (formerly Netlify CMS) provides a web-based content editor at `/admin` that commits changes to git — triggering an automatic rebuild on Cloudflare Pages.

**How it works:**
1. Practitioner navigates to `their-site.com/admin`
2. Logs in (GitHub/GitLab OAuth or Cloudflare Access)
3. Sees an editor interface with their pages and content fields
4. Edits copy, clicks "Publish"
5. Decap commits the change to the git repo
6. Cloudflare Pages auto-rebuilds (~30 seconds)
7. Site is live with new content

**Pros:**
- No database — content lives in git (Markdown/YAML files)
- No server — the admin UI is a static single-page app
- Free — open source, no hosted service needed
- Structured editing — the practitioner edits defined fields, not raw code
- Version history — every change is a git commit, fully reversible

**Cons:**
- Not WYSIWYG — the editor shows form fields, not the live page
- ~30 second delay between "Publish" and live site (auto-rebuild)
- Initial setup requires defining a config file mapping content fields to data files
- Authentication setup adds a one-time configuration step

**Alternative: Tina CMS** — provides visual/contextual editing (closer to WYSIWYG) with a free tier. More polished editing experience but slightly more complex setup and a hosted service dependency. Worth considering if the practitioner finds Decap's form-based editing too abstract.

### 4. The Re-Deploy Question

The user expressed a preference for avoiding re-deploys. With this stack:

- **Content edits** trigger an auto-rebuild (~30 seconds). The practitioner clicks "Publish" in Decap and the site is live shortly after. This is technically a re-deploy, but it's invisible — no developer needed, no terminal, no manual step.
- **Scheduling changes** happen in Cal.com's dashboard — no site rebuild needed. The embed loads the current schedule dynamically.
- **Design changes** require a developer to edit Astro components and push to git. This is a true re-deploy, but design changes are infrequent after launch.

For a practitioner's needs, this is effectively "no re-deploys" — copy edits are self-service with invisible rebuilds, and scheduling is fully dynamic.

### 5. Architecture Overview

```
┌─────────────────────────────────────────────────┐
│                  Practitioner                    │
│                                                 │
│  Edits copy via          Manages schedule via    │
│  site.com/admin          cal.com dashboard       │
│       │                        │                 │
│       ▼                        ▼                 │
│  Decap CMS ──commits──> Git repo    Cal.com API  │
│                            │              │      │
│                            ▼              │      │
│                     Cloudflare Pages      │      │
│                     (auto-rebuild)        │      │
│                            │              │      │
│                            ▼              │      │
│                     Static site ◄─embed───┘      │
│                     (Astro + Tailwind)           │
│                                                 │
│                  Visitor sees:                   │
│                  Fast static pages +             │
│                  embedded Cal.com booking        │
└─────────────────────────────────────────────────┘
```

### 6. Cost Comparison

| Stack | Monthly Cost | Content Editing | Scheduling Quality | Technical Debt |
|---|---|---|---|---|
| **Astro + Cloudflare + Cal.com + Decap** | **$0** | Form-based CMS | Good (styled embed) | Low |
| Astro + Cloudflare + Acuity | ~$20 | Needs CMS addition | Excellent (more features) | Low |
| Squarespace + Acuity | ~$33–49 | Visual WYSIWYG | Best (native integration) | Zero |
| WordPress + Amelia | ~$10–20 | WordPress admin | Good (plugin) | High |
| Astro + Cloudflare + Koalendar | ~$97 | Needs CMS addition | Poor (embed quality) | Low |

---

## Trade-offs & Recommendations

### Primary Recommendation

**Astro + Cloudflare Pages + Cal.com + Decap CMS** — $0/month, code-first, good scheduling integration, practitioner can edit copy.

This stack:
- Preserves full design freedom (our mock-up becomes production code)
- Costs nothing to run
- Gives the practitioner self-service content editing
- Integrates scheduling with payments via a styleable embedded widget
- Has a clear upgrade path (Cal.com → Acuity if the practice grows)

### Key Trade-offs to Accept

| Trade-off | What You Give Up | What You Get |
|---|---|---|
| Content editing is form-based, not WYSIWYG | Practitioner sees fields, not the live page | $0/month, no hosted service dependency |
| ~30 second rebuild on content edit | Not instant publish | Free hosting, git-based version history |
| Cal.com lacks packages/subscriptions | Can't sell session bundles natively | Free scheduling with payments |
| Cal.com embed is styled but not native | Slight visual difference from rest of site | $0 vs $20-97/month for native solutions |

### When to Upgrade

| Trigger | Action |
|---|---|
| Practice needs session packages, memberships, or gift certificates | Replace Cal.com with Acuity (~$20/month) |
| Practitioner finds Decap CMS too confusing | Switch to Tina CMS (free tier, more visual) |
| Practice grows to multiple practitioners | Cal.com Teams plan ($12/user/month) or Acuity |
| Practitioner wants WYSIWYG editing and is willing to pay | Consider managed platform migration |

### What This Means for the Build Skill

The `/build-mockup` output at `brands/<brand>/mock-up/` becomes the direct input for the final build:

1. Convert mock-up HTML files to Astro components
2. Extract copy into structured content files (YAML/Markdown)
3. Configure Tailwind as an Astro integration (replace CDN link)
4. Add Cal.com embed to booking/contact page
5. Configure Decap CMS with content field definitions
6. Deploy to Cloudflare Pages
7. Set up practitioner authentication for `/admin`

---

## Sources

### Squarespace Developer Workflows
- Squarespace Developer Documentation — Developer Mode (v7.0 only, no v7.1 support)
- Squarespace Help — Differences between 7.0 and 7.1
- Community reports on Developer Mode limitations and JSON-T templating

### Cal.com Payment Integration
- Cal.com Features — Payments (https://cal.com/features/payments)
- Cal.com Help — Paid Bookings (https://cal.com/help/bookings/paid-bookings)
- Cal.com Help — How to Receive Payments (https://cal.com/help/event-types/how-to-receive-payments)
- Cal.com Blog — Apple and Google Pay Support (https://cal.com/blog/apple-and-google-pay-support)
- Cal.com Blog — Time-Based Cancellation Fees (https://cal.com/blog/time-based-cancellation-fees-for-no-show)
- Cal.com Pricing (https://cal.com/pricing)
- Cal.com Features — Embed (https://cal.com/features/embed)

### Scheduling Platform Comparisons
- Koalendar — Booking Payment System (https://koalendar.com/features/booking-payment-system)
- Koalendar Pricing (https://koalendar.com/pricing)
- Acuity Scheduling — Payments (https://acuityscheduling.com/features/payments)
- Acuity Help — Packages, Gift Certificates, Subscriptions (https://help.acuityscheduling.com/hc/en-us/articles/16676947677325)

### Hosting & CMS
- Cloudflare Pages Documentation (https://developers.cloudflare.com/pages/)
- Astro Documentation (https://docs.astro.build)
- Decap CMS Documentation (https://decapcms.org/docs/)
- Tina CMS Documentation (https://tina.io/docs/)
