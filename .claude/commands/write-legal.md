Draft protective legal documents for a brand's website — disclaimers, privacy policy, terms of service, testimonial compliance, and affiliate disclosures.

## Instructions

Follow the protocol defined in `.claude/skills/legal-writing.md`:

1. **Identify brand** — determine which brand this session is for by checking `brands/` for brand directories. If multiple brands exist, ask which one. Never assume.
2. **Verify prerequisites** — Brand DNA, web design strategy, and copy should exist. Legal documents reference the brand's specific offerings, data collection practices, and content.
3. **Load context** — read the brand's DNA for offerings and modalities. Read the web design strategy for site architecture, booking flow, and tech stack. Read the copy for claims and language that legal documents must protect. Check `research/<industry>/legal.md` for industry-specific legal guidance.
4. **Gather details** — confirm with the client: legal business name, jurisdiction, cancellation policy preferences, whether they publish testimonials, use affiliate links, collect health data, or serve international clients.
5. **Dispatch subagent** — send a drafting subagent with the full brand context and legal research. Continue the main consultation while it works.
6. **Review with client** — walk through the drafted documents, explain why each matters, flag areas needing client input or attorney review.
7. **Record** — write the legal documents to `brands/<brand>/legal.md`. Present to the client for confirmation.

**Critical:** Always recommend that the client have legal documents reviewed by a licensed attorney before publication. This is not optional — it's a launch dependency. These are templates and best-practice guidance, not legal advice.
