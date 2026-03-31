Draft website copy through a conversational process — section by section, in the brand's voice, guided by the web design strategy structure.

## Instructions

Follow the protocol defined in `.claude/skills/copywriting.md`:

1. **Identify brand** — determine which brand this session is for by checking `brands/` for brand directories. If multiple brands exist, ask which one. Never assume.
2. **Verify prerequisites** — both Brand DNA (`brands/<brand>/brand-dna.md`) and web design strategy (`brands/<brand>/web-design-strategy.md`) must exist. If either is missing, redirect the client to `/discover-brand` or `/design-website` first.
3. **Load context** — read the brand's DNA for voice anchors (personality, values, essence, audience). Read the web design strategy for page specifications, section purposes, and CTAs. Check `research/<industry>/copywriting.md` for industry-specific copywriting guidance. Check `brands/<brand>/copy.md` for any existing copy that should be revised.
4. **Establish voice** — propose a voice direction based on Brand DNA personality. Give a concrete example. Get explicit client approval before drafting any sections.
5. **Draft section by section** — work through the site in strategy spec order. For each section: state its job, draft the copy, present it, invite critique, revise until approved. One section at a time.
6. **Review for consistency** — after all sections are drafted, read the complete document for voice consistency, message hierarchy, CTA flow, and accuracy.
7. **Record** — write the completed copy to `brands/<brand>/copy.md` using the YAML-in-markdown format from the skill. Present the final document to the client for confirmation.

The three non-negotiables: accuracy (flag anything you're inferring for client verification), priorities (the client's most important messages get the most prominent placement), and voice (every sentence should pass the "does this sound like the brand?" test).

Do not rush. Copy is the client's voice on the page. They may need to sit with a draft, try different angles, or revisit their Brand DNA to clarify what they mean. The process should feel like co-writing, not filling in blanks.
