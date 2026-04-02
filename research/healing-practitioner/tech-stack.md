# Tech Stack for Healing Practitioner Websites

The ideal tech stack for a healing practitioner website balances five concerns: code-first design freedom, easy content management for the practitioner, seamless scheduling with integrated payments, automated communication (email newsletters, feedback collection, booking confirmations), and minimal ongoing cost. This report evaluates the leading options and recommends a specific stack.

---

## Context

The brand development pipeline produces a complete HTML/Tailwind mock-up at `brands/<brand>/mock-up/`. The final build phase must translate this mock-up into a production website that:

1. Preserves the design exactly (code-first — no visual editor adaptation)
2. Lets the practitioner publish blog posts and update product gallery without a developer and without triggering a rebuild/redeploy
3. Integrates scheduling with payment collection at time of booking
4. Sends automated emails — newsletter on blog publish, feedback requests after sessions, booking confirmations
5. Costs as little as possible to host and maintain ($0/month target)
6. Minimizes technical debt (fewer moving pieces, less maintenance)
7. Hosts on Cloudflare (existing account, DNS already managed there)

Prior experience: Astro (static mode) + Koalendar integration was unsatisfactory — the scheduling embed felt foreign and poorly integrated, and content changes required a rebuild/redeploy cycle.

---

## The Recommended Stack

### Astro SSR (hybrid) + Cloudflare Pages/Workers + Sanity CMS + Cal.com + Loops + Stripe

| Component | Role | Monthly Cost |
|---|---|---|
| **Astro (hybrid mode)** | Site framework — static pages + server-rendered dynamic pages | Free (open source) |
| **Cloudflare Pages** | Hosting — global CDN, auto-deploys from git | Free tier |
| **Cloudflare Workers** | Serverless functions — webhook handlers, automation | Free tier |
| **Sanity CMS** | Content management — blog posts, product gallery, editable copy | Free tier |
| **Cal.com** | Scheduling — embedded booking with payment integration | Free tier |
| **Loops** | Email — newsletters, feedback forms, transactional emails | Free tier |
| **Mux** | Video streaming — introductory video on homepage | Usage-based (near-zero) |
| **Stripe** | Payments — charged at time of booking via Cal.com | Per-transaction only |
| **Total fixed cost** | | **$0/month** |

**Variable costs:**
- **Stripe:** 2.9% + $0.30 per transaction. For a $150 session, that's ~$4.65. At 10 sessions/week, approximately $46.50/week in processing fees. Industry-standard and unavoidable with any payment processor.
- **Mux:** Usage-based pricing with no monthly minimum. Encoding ~$0.015/min (one-time per video), delivery ~$0.00075/min viewed. For a 90-second intro video at ~1,000 views/month, cost is approximately $1/month. Negligible at solo practitioner traffic levels.

---

## Free Tier Capacity vs. Actual Usage

Every service in this stack offers a free tier that far exceeds a solo practitioner's needs.

| Service | Free Tier Limit | Estimated Monthly Usage | Headroom |
|---|---|---|---|
| **Cloudflare Pages** | 500 builds/month, unlimited bandwidth | 5–10 builds (design changes only) | ~50x |
| **Cloudflare Workers** | 100K requests/day, 5 cron triggers | ~100–1,000 requests/day | ~100x |
| **Sanity CMS** | 1M CDN requests, 250K API requests, 10K documents, 100GB storage, 2 webhooks | ~50–100 documents, minimal API traffic | ~100x |
| **Cal.com** | Unlimited bookings, calendar sync, Stripe integration, embeds | ~40 bookings/month | Unlimited |
| **Loops** | 1K contacts, 2K sends/month, forms, transactional emails, API access | ~50–200 contacts, ~200–500 sends | ~4–10x |
| **Mux** | No monthly minimum, usage-based | 1 video, ~1K views/month (~$1/mo) | N/A (pay-per-use) |
| **Stripe** | No monthly fee | ~40 transactions/month | Unlimited |

**When would free tiers become insufficient?**

| Trigger | Service | Action | Cost |
|---|---|---|---|
| Newsletter exceeds 1K subscribers | Loops | Upgrade to paid plan | ~$49/month |
| Practice grows to multiple practitioners | Cal.com | Teams plan | $12/user/month |
| Need session packages, memberships, gift certificates | Cal.com | Switch to Acuity Scheduling | ~$20/month |
| Heavy CMS API usage (very unlikely) | Sanity | Upgrade to Growth plan | $15/month |

For a solo practitioner doing ~10 sessions/week, these triggers are years away — if ever.

**Cal.com caveat:** The pricing page advertises unlimited event types on the free plan, but some UI text suggests a limit of one active event type. Verify at signup. If limited to one, sessions can be structured under a single event type with variants, or the Starter plan ($12/month) removes the restriction. This is the one item to confirm before committing.

---

## Component Deep Dive

### 1. Astro (Hybrid Mode) — Site Framework

Astro in hybrid rendering mode solves the rebuild problem that made the previous static-only approach frustrating.

**How hybrid mode works:**
- **Static pages** (Home, About, Offerings, Testimonials, Contact) are pre-built at deploy time. Fastest possible page loads — pure HTML served from CDN edge.
- **Server-rendered pages** (Blog, Product Gallery) are rendered on each request by a Cloudflare Worker that fetches content from Sanity's API. New blog posts and products appear immediately — no rebuild, no redeploy.

**Why Astro over TanStack Start:**
TanStack Start (the full-stack framework built around TanStack Router) can do runtime routing, but it's React-based and ships the React runtime to the browser. For a content-heavy, low-interactivity healing practitioner site, this is unnecessary weight. Astro's island architecture ships zero JavaScript by default and loads interactive components (like the Cal.com embed) only where needed.

TanStack Router's "runtime routes" are standard dynamic routing — a route like `/blog/[slug]` that resolves at request time. Every SSR framework does this. Astro in hybrid mode gives the same capability with less client-side JavaScript.

**The mock-up-to-production conversion:**
```
brands/<brand>/mock-up/index.html    →  src/pages/index.astro        (static)
brands/<brand>/mock-up/about.html    →  src/pages/about.astro        (static)
brands/<brand>/mock-up/offerings.html→  src/pages/offerings.astro    (static)
brands/<brand>/mock-up/blog.html     →  src/pages/blog/index.astro   (SSR)
brands/<brand>/mock-up/blog-post.html→  src/pages/blog/[slug].astro  (SSR)
brands/<brand>/mock-up/products.html →  src/pages/products.astro     (SSR)
brands/<brand>/mock-up/contact.html  →  src/pages/contact.astro      (static)
Tailwind CDN                         →  @astrojs/tailwind integration
```

**Deployment:** `@astrojs/cloudflare` adapter. Static pages serve from Cloudflare's CDN. SSR pages execute as Cloudflare Pages Functions (Workers).

### 2. Sanity CMS — Content Management

Sanity replaces Decap CMS from the previous recommendation. The key reason: Sanity provides a real-time API that Astro's SSR pages can query at request time, eliminating the need for rebuilds on content changes. Sanity's webhooks also enable the entire automation chain (newsletter, feedback, social media).

**What the practitioner sees:**
Sanity Studio — a customizable web-based editing interface hosted on the site's domain (e.g., `studio.cheriekalisa.com` or `cheriekalisa.com/studio`). The studio is a React app that can be tailored to show exactly the fields the practitioner needs:

- **Blog editor:** Title, body (rich text with Portable Text), featured image, excerpt, tags/categories, publish toggle
- **Product gallery:** Product name, image, description, affiliate link, category
- **Editable site copy:** Testimonials, hero text, any copy the practitioner should be able to update

**Content flow (no rebuild):**
1. Cherie opens Sanity Studio
2. Writes a blog post, adds a product, or edits copy
3. Clicks "Publish"
4. Content is immediately available via Sanity's GROQ API
5. Next visitor to the blog/product page sees the new content (server-rendered from API)

**Webhooks (automation triggers):**
Sanity fires webhooks on content events. The free tier includes 2 GROQ-powered webhooks — enough for:
1. Blog publish → triggers newsletter + optional social media post
2. Product publish → could trigger a notification or update

**Why not Decap CMS:**
Decap is git-based — it commits markdown files to the repo, which triggers a Cloudflare Pages rebuild. This creates the rebuild-on-every-edit pattern we want to eliminate. Decap also has no API for SSR to query. It's a good tool for static sites, but the move to hybrid SSR makes an API-based CMS essential.

**Why Sanity over Contentful/Storyblok:**
- **Contentful:** Larger free tier (1M API calls, 5 users) but less customizable editing experience and the content model can feel rigid. Good alternative if Sanity's free tier ever becomes limiting.
- **Storyblok:** Best visual editing (closest to WYSIWYG) but limited to 1 user on free tier. Worth considering if the practitioner finds Sanity Studio too abstract.
- **Sanity wins** because webhooks + customizable studio + GROQ API + generous free tier = the best fit for this automation-focused architecture.

### 3. Cal.com — Scheduling + Payments

Cal.com resolves the Koalendar frustration with better embed quality and native payment integration.

**Embed integration:**
Cal.com offers three embed modes — inline, popup, and floating button. The inline embed renders within the page (not a generic iframe) and accepts CSS styling to match the site's design tokens. The full booking + payment flow happens within the embed without redirecting.

For deeper visual integration, Cal.com's API allows building a fully custom booking UI in Astro components — the site's own date picker, time slots, and payment form, with Cal.com as the backend. More development work, but completely seamless. Decision to make after seeing the embed in the mock-up.

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
- Session packages or bundles ("5 sessions for $X")
- Recurring billing / subscriptions / memberships
- Gift certificates
- Invoicing or coupon/discount codes

**Calendar sync:**
Bidirectional sync with Google Calendar, Apple Calendar (CalDAV), and Outlook. Sessions booked on the website appear on Cherie's iPhone calendar. Her personal events automatically block booking slots.

**Client self-service:**
Cherie manages everything in Cal.com's dashboard — availability, pricing, event types, time-off — without touching the website or calling the developer.

**Upgrade path:**
If the practice grows to need session packages, memberships, or gift certificates, Acuity Scheduling (~$20/month, owned by Squarespace) is the natural upgrade. Acuity supports all of those features and embeds well into custom sites.

### 4. Loops — Email + Forms + Automation

Loops handles all email communication in one platform: marketing newsletters, transactional emails (booking confirmations, feedback requests), and form-based data collection.

**Why Loops over Kit (ConvertKit) or Buttondown:**

| Concern | Kit | Buttondown | Loops |
|---|---|---|---|
| **Complexity** | Feature-heavy — built for content creators whose business IS email. Course funnels, automation trees, commerce. Cherie would navigate past features she'll never use. | Very minimal — great for devs, light on features | Clean, minimal UI. Enough features without overwhelm. |
| **Transactional + marketing** | Separate tools needed | Newsletter only | Both in one platform |
| **Forms** | Landing pages (heavy) | No | Yes — embedded forms for feedback, signup |
| **Free tier** | 10K subscribers (generous) | 100 subscribers (tight) | 1K contacts, 2K sends/month (right-sized) |
| **API** | Good | Good | Good |
| **Aesthetic** | Cluttered dashboard | Developer-oriented | Minimal, clean — matches brand values |

**Three roles Loops plays:**

**A. Newsletter on blog publish:**
```
Cherie publishes blog post in Sanity
  → Sanity webhook fires
    → Cloudflare Worker receives webhook
      → Fetches new post content from Sanity API
      → Calls Loops API to send newsletter to subscriber list
        → Subscribers receive email with post excerpt + link
```

**B. Post-consultation feedback collection (testimonial pipeline):**
```
Client completes session (Cal.com booking marked complete)
  → Cal.com webhook fires
    → Cloudflare Worker calculates follow-up date (e.g., 2 days post-session)
    → Cloudflare cron trigger checks daily for pending follow-ups
      → Loops API sends feedback form email
        → Client fills out form
          → Responses collected in Loops
            → Cherie reviews, curates best responses as testimonials (with consent)
```

This directly solves the open item in the web design strategy: *"Testimonials — Need to gather from existing clients with permission."* Instead of Cherie remembering to ask, the system asks for her.

**C. Booking confirmations:**
Cal.com handles booking confirmation emails natively — no Loops integration needed for this. However, Loops can send branded follow-up emails (session preparation instructions, what to expect) that match the site's design, supplementing Cal.com's functional confirmations.

### 5. Mux — Video Streaming

The homepage features a 60–90 second introductory video of Cherie speaking about her work. Mux provides adaptive bitrate streaming — the video quality adjusts to the viewer's connection speed, ensuring smooth playback without buffering.

**Why Mux over self-hosted video or YouTube:**
- **Self-hosted (MP4 in Cloudflare):** No adaptive bitrate. A single fixed-quality file means either poor quality on slow connections or huge file sizes. No analytics.
- **YouTube/Vimeo embed:** Branding overlays, related video suggestions, ads (YouTube). Breaks the immersive sanctuary feel of the site.
- **Mux:** Clean player with no third-party branding, adaptive streaming, usage-based pricing with no monthly minimum, simple API.

**Integration:**
Mux provides a `<mux-player>` web component that drops into an Astro component. Supports customizable controls, poster images, and responsive sizing. The player loads as an Astro island — JavaScript only loads for this component, not site-wide.

```astro
<mux-player
  playback-id="VIDEO_PLAYBACK_ID"
  metadata-video-title="Meet Cherie Kalisa"
  accent-color="#7dd3fc"
  poster="path/to/poster.jpg"
/>
```

**Cost for this use case:**
- Encoding: ~$0.02 one-time (90 seconds × $0.015/min)
- Delivery: ~$0.001 per view (90 seconds × $0.00075/min)
- At ~1,000 views/month: approximately $1/month
- Effectively free at solo practitioner traffic levels

### 6. Stripe — Payments

No monthly fee. Per-transaction pricing only:
- **US cards:** 2.9% + $0.30 per transaction
- **International cards:** +1.5%
- **Apple Pay / Google Pay:** Same as card rates

Integrated via Cal.com — Cherie connects her Stripe account in Cal.com's dashboard once and never interacts with Stripe directly. Payments appear in her Stripe account and transfer to her bank automatically.

### 7. Cloudflare — DNS + Hosting + Serverless

Cloudflare serves triple duty:

**DNS:** Already managing the domain. No change needed.

**Pages (hosting):** Astro's build output deploys to Cloudflare Pages. Static pages cached at CDN edge (300+ global locations). SSR pages run as Pages Functions.

**Workers (automation):** Lightweight serverless functions handle:
- Sanity webhook receiver → triggers newsletter send via Loops
- Cal.com webhook receiver → schedules feedback follow-up via Loops
- Cron trigger → checks for pending feedback follow-ups daily
- Optional: Facebook Graph API post on blog publish

All on the free tier: 100K requests/day, 5 cron triggers.

---

## Architecture Overview

```
┌──────────────────────────────────────────────────────────────────┐
│                          Cherie                                  │
│                                                                  │
│  Publishes content         Manages schedule        Reviews       │
│  via Sanity Studio         via Cal.com dashboard   feedback      │
│       │                         │                  in Loops      │
│       │                         │                                │
│       ▼                         ▼                                │
│  Sanity CMS               Cal.com                                │
│  ├─ GROQ API ──────────→ Astro SSR pages (blog, products)       │
│  └─ Webhook ──────────→ Cloudflare Worker                        │
│                           ├─→ Loops API (send newsletter)        │
│                           └─→ Facebook Graph API (optional)      │
│                                                                  │
│                         Cal.com                                  │
│                         ├─ Embed ──→ Site booking page            │
│                         ├─ Stripe ──→ Payment at booking          │
│                         ├─ Calendar sync ──→ iPhone / Google      │
│                         ├─ Confirmation emails (built-in)         │
│                         └─ Webhook ──→ Cloudflare Worker          │
│                                        └─→ Loops (feedback form, │
│                                             timed follow-up)     │
│                                                                  │
│  Mux ──→ Adaptive video streaming (homepage intro video)         │
│          └─ <mux-player> web component (Astro island)            │
│                                                                  │
│  Astro (hybrid) on Cloudflare Pages                              │
│  ├─ Static: Home, About, Offerings, Testimonials, Contact        │
│  └─ SSR:   Blog listing, Blog posts, Product Gallery             │
│            (fetched from Sanity API at request time)              │
│                                                                  │
│  Visitor experience:                                             │
│  Fast static pages + dynamic content + embedded booking          │
│  + adaptive video streaming                                      │
│  Zero JS shipped except where interactive (Cal.com, Mux player)  │
│                                                                  │
│  Monthly cost: $0  (Stripe per-transaction fees only)            │
└──────────────────────────────────────────────────────────────────┘
```

---

## Automation Chains

### Chain 1: Blog Publish → Newsletter

```
Sanity: blog post published
  → Sanity GROQ webhook fires (filtered to blog documents)
    → POST to Cloudflare Worker endpoint
      → Worker fetches full post from Sanity API (title, excerpt, slug)
      → Worker composes email (post title, excerpt, link to full post)
      → Worker calls Loops API: send to newsletter segment
        → Subscribers receive branded email with blog excerpt + "Read more" link
```

### Chain 2: Session Complete → Feedback Request → Testimonial Pipeline

```
Cal.com: booking created (includes session date/time)
  → Cal.com webhook fires
    → POST to Cloudflare Worker endpoint
      → Worker stores booking info in Cloudflare KV (client email, session date)

Cloudflare cron trigger (runs daily):
  → Worker checks KV for sessions completed 2 days ago
    → For each, calls Loops API: send feedback form email
      → Client receives email with embedded Loops form
        → Client submits feedback (rating, experience description, permission to share)
          → Response stored in Loops
            → Cherie reviews in Loops dashboard
              → Best responses curated as website testimonials (with consent)
```

### Chain 3: Blog Publish → Social Media Post (Optional)

```
Sanity: blog post published
  → Same webhook as Chain 1 (Cloudflare Worker handles both)
    → Worker composes social post (title + excerpt + link)
    → Worker calls Facebook Graph API: publish to business page
      → Post appears on Facebook page
```

**Alternative (no-code):** Use Zapier/Make.com as middleware instead of a custom Worker. Sanity webhook → Zapier → Facebook post. No code to maintain. Zapier free tier (100 tasks/month) covers typical blog post frequency.

---

## Platforms Evaluated and Eliminated

### Squarespace — Not Viable for Code-First

Squarespace's Developer Mode is locked to legacy v7.0. All new sites since 2020 use v7.1, which has no code access. Even on v7.0, developers write in JSON-T (proprietary templating), not real HTML. No CLI deployment, no REST API for code, no way to deploy an HTML/Tailwind codebase.

**Verdict:** Architecturally incompatible. Eliminated.

### WordPress — Too Much Maintenance

Can handle everything but carries significant technical debt: security updates, plugin conflicts, PHP hosting, database management. Overengineered for a 4–6 page practitioner site.

**Verdict:** Wrong trade-off for this use case. Eliminated.

### Wix — Same Problems as Squarespace

Visual-editor-first platform with limited code access. No way to deploy custom HTML/Tailwind.

**Verdict:** Eliminated.

### Decap CMS — Superseded by Sanity

Git-based CMS that commits content files to the repo, triggering rebuilds. No API for SSR. Previously recommended in the static-only architecture, but the move to hybrid SSR makes an API-based CMS essential. Decap remains a good choice for purely static sites.

**Verdict:** Replaced by Sanity in this architecture.

### TanStack Start — Viable but Heavier

Full-stack React framework with runtime routing. Solves the same rebuild problem as Astro hybrid mode but ships the React runtime to the browser. More JavaScript than this content-heavy site needs. Younger ecosystem, less battle-tested for content sites.

**Verdict:** Viable alternative if React ecosystem access is needed. Not recommended for this use case.

### Kit (ConvertKit) — Too Much for This Use Case

Powerful email platform built for content creators whose business centers on email (course sellers, YouTubers, newsletter writers). Feature-rich to the point of complexity — automation trees, commerce, subscriber tagging workflows. The client would navigate past features she'll never use. 10K subscriber free tier is generous but the UX trade-off isn't worth it.

**Verdict:** Viable but unnecessarily complex. Loops is a better fit.

### Buttondown — Too Limited

Clean, developer-friendly newsletter service. But 100-subscriber free tier is restrictive, no forms, no transactional emails. Better suited for developers who want a simple API.

**Verdict:** Free tier too limited. Loops offers more.

---

## Cost Comparison

| Stack | Monthly Cost | Content Editing | Scheduling | Email Automation | Rebuild on Content? |
|---|---|---|---|---|---|
| **Astro SSR + Cloudflare + Sanity + Cal.com + Loops** | **$0** | API-based CMS | Styled embed + payments | Full (newsletter, feedback, transactional) | **No** |
| Astro static + Cloudflare + Decap + Cal.com | $0 | Git-based CMS | Styled embed + payments | None | Yes (~30s) |
| Astro static + Cloudflare + Sanity + Cal.com | $0 | API-based CMS (overkill for static) | Styled embed + payments | Webhook triggers only | Yes (~30s) |
| Astro + Cloudflare + Acuity | ~$20 | Needs CMS addition | More features (packages, etc.) | Needs email addition | Depends on mode |
| Squarespace + Acuity | ~$33–49 | Visual WYSIWYG | Best (native) | Basic | No |
| WordPress + Amelia | ~$10–20 | WordPress admin | Good (plugin) | Plugin-dependent | No |

---

## What This Means for the Build Phase

The `/build-mockup` output at `brands/<brand>/mock-up/` becomes the direct input for production:

1. Convert mock-up HTML files to Astro components (static + SSR as mapped above)
2. Install `@astrojs/cloudflare` adapter, configure hybrid output mode
3. Extract copy into Sanity content schemas (blog, products, editable site copy)
4. Configure Sanity Studio with editing interfaces tailored to the practitioner
5. Set up Tailwind as an Astro integration (replace CDN link)
6. Add Cal.com embed to booking/contact page with site-matched styling
7. Upload introductory video to Mux, integrate `<mux-player>` on homepage as Astro island
8. Create Cloudflare Workers for webhook handlers (newsletter, feedback, optional social)
9. Configure Sanity webhooks → Worker endpoints
10. Configure Cal.com webhooks → Worker endpoints
11. Set up Loops account with newsletter segment, feedback form, and email templates
12. Deploy to Cloudflare Pages
13. Connect custom domain (DNS already in Cloudflare)

---

## Sources

### Frameworks
- Astro Documentation — Hybrid Rendering (https://docs.astro.build)
- Astro Cloudflare Adapter (https://docs.astro.build/en/guides/integrations-guide/cloudflare/)
- TanStack Start Documentation (https://tanstack.com/start)

### CMS
- Sanity Documentation (https://www.sanity.io/docs)
- Sanity Pricing / Free Tier (https://www.sanity.io/pricing)
- Sanity Webhooks (https://www.sanity.io/docs/webhooks)
- Contentful Documentation (https://www.contentful.com/developers/docs/)
- Storyblok Documentation (https://www.storyblok.com/docs)
- Decap CMS Documentation (https://decapcms.org/docs/)

### Scheduling + Payments
- Cal.com Features — Payments (https://cal.com/features/payments)
- Cal.com Features — Embed (https://cal.com/features/embed)
- Cal.com Pricing (https://cal.com/pricing)
- Cal.com API Documentation (https://cal.com/docs/api)
- Acuity Scheduling (https://acuityscheduling.com)
- Stripe Pricing (https://stripe.com/pricing)

### Email
- Loops Documentation (https://loops.so/docs)
- Loops Pricing (https://loops.so/pricing)
- Kit (ConvertKit) (https://kit.com)
- Buttondown (https://buttondown.com)

### Video Streaming
- Mux Documentation (https://docs.mux.com)
- Mux Pricing (https://www.mux.com/pricing)
- Mux Player Web Component (https://docs.mux.com/guides/mux-player-web)

### Hosting
- Cloudflare Pages Documentation (https://developers.cloudflare.com/pages/)
- Cloudflare Workers Documentation (https://developers.cloudflare.com/workers/)
- Cloudflare Workers KV (https://developers.cloudflare.com/kv/)
