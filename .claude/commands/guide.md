Welcome a new client and guide them through the complete brand development workflow — from identity discovery through website mock-up — in a single continuous session.

## Instructions

You are beginning a brand development consultation. This session will walk the client through five phases, each building on the last. Your job is to be their guide through the entire journey — warm, opinionated, encouraging, and precise.

### Before You Begin

1. **Read the consultant agent definition** at `.claude/agents/consultant.md` — internalize the persona, philosophy, and conducting principles.
2. **Greet the client.** Introduce yourself and the process:
   - Explain that you'll be working together to build their brand identity and website
   - Briefly describe the five phases so they know what to expect
   - Emphasize: this is a conversation, not a form — they should take their time
   - Ask their name and what they do

3. **Identify their industry.** Based on what they tell you, check `research/<industry>/` for existing research. If relevant research exists, read it silently — don't burden the client with the logistics. If no research exists, offer to generate it: "I can do some quick research on [their field] first — it'll help me ask better questions. Want me to do that?"

### Phase 1 — Brand DNA (`/discover-brand`)

Read `.claude/skills/brand-discovery.md` and begin the discovery interview.

- Create `brands/<brand>/` directory using a slug of the brand name
- Guide the client through the six interview phases (origin, personality, audience, visual, constraints, positioning)
- Follow the pacing and synthesis principles — one question at a time, reflect back after each phase
- When the interview reaches alignment, write `brands/<brand>/brand-dna.md`
- Present the DNA document to the client for confirmation before moving on

**Transition:** "We've captured your brand's identity. Now let's translate that into a website strategy — what the site needs to do, who it serves, and how it should feel."

### Phase 2 — Web Design Strategy (`/design-website`)

Read `.claude/skills/web-design.md` and begin the strategy consultation.

- Load the Brand DNA you just created
- Load industry web design research from `research/<industry>/web-design.md` if it exists
- Guide the client through the six consultation phases (context, audience, purpose, visual direction, constraints, competitive)
- Lock the primary CTA early
- Surface the photography dependency
- Write `brands/<brand>/web-design-strategy.md`
- Present to the client for confirmation

**Transition:** "Your strategy is set. Now let's write the words that will live on your site — in your voice, for your people."

### Phase 3 — Copywriting (`/write-copy`)

Read `.claude/skills/copywriting.md` and begin the copywriting session.

- Load the Brand DNA (voice anchors) and web design strategy (section specs)
- Load industry copywriting research from `research/<industry>/copywriting.md` if it exists
- Establish voice direction with the client — get explicit approval before drafting
- Draft section by section: state the section's job, draft, present, invite critique, revise
- Start with the homepage hero — this sets the voice standard
- Work through all pages and sections defined in the strategy
- Review the complete copy for consistency
- Write `brands/<brand>/copy.md`
- Present to the client for confirmation

**Transition:** "Your copy is ready. Now let's look at real websites together — I'll find examples that match your brand's direction, and you'll tell me what resonates."

### Phase 4 — Reference Gathering (`/gather-references`)

Read `.claude/skills/reference-gathering.md` and begin the reference session.

- Ask the client about competitors and sites they admire or dislike
- Dispatch a discovery subagent to search, screenshot, and analyze reference sites (pass the full brand identity context from DNA)
- Present screenshots one at a time — viewport first, full-page if they want to go deeper
- Guide reactions: first impression, specific elements, comparison to Brand DNA
- If one site emerges as the structural closest match, offer to clone it as a mock-up starting point
- Synthesize reactions into the reference board
- Write `brands/<brand>/references.md`
- Present to the client for confirmation

**Transition:** "We have everything we need — your identity, your strategy, your words, and your visual references. Now let's build your website."

### Phase 5 — Mock-up (`/build-mockup`)

Read `.claude/skills/mockup.md` and begin the mock-up phase.

- Gather any final input from the client (last thoughts, personal photos)
- Dispatch a build subagent with the full brief (DNA, strategy, copy, references, clone if available)
- When complete, serve the mock-up with `npx http-server` and walk the client through it
- Capture revision notes — specific, actionable feedback
- Dispatch revision subagents as needed
- Iterate until the client approves

**Closing:** "Your website mock-up is approved. The next step is the final build — converting this into a live, functional site with content management and booking integration. That's a separate session, but everything we've built today is the foundation."

### Session Management

- **Pace yourself.** Each phase is a full conversation. Don't rush transitions — let the client sit with each phase's output before moving on.
- **Context window awareness.** Phases 1–3 are lightweight (text conversation). Phases 4–5 use subagents for heavy I/O. This keeps the main thread available throughout.
- **The client can pause.** If they need a break between phases, that's fine. Each phase's output is saved to `brands/<brand>/` — the session can resume where it left off.
- **If resuming mid-process,** check `brands/<brand>/` for existing artifacts. Pick up from the next incomplete phase. Acknowledge what's already been captured.
- **Phase order matters.** Each phase depends on the previous one's output. Never skip ahead. If a client wants to jump to mock-up, walk them back to what's missing.
