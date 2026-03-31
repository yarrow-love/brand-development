Conduct a web design strategy consultation to establish the strategic foundation for a brand's website.

## Instructions

Follow the protocol defined in `.claude/skills/web-design.md`:

1. **Identify brand** — determine which brand this consultation is for by checking `brands/` for brand directories. If multiple brands exist, ask which one. Never assume.
2. **Verify prerequisite** — a Brand DNA document must exist at `brands/<brand>/brand-dna.md` with populated visual codes, personality traits, and audience definition. If no Brand DNA exists, redirect the client to `/discover-brand` first.
3. **Load context** — read the brand's DNA. Check `research/<industry>/web-design.md` for relevant industry research. Check `brands/<brand>/web-design-strategy.md` for any existing strategy that should be revised rather than created from scratch.
4. **Consult** — guide the client through the phased consultation (context -> audience -> purpose -> visual direction -> constraints -> competitive), adapting pace and depth to their responses. Lock the primary CTA before moving to structure or visual territory.
5. **Synthesize** — after each phase, reflect back what you've heard. Surface contradictions. Flag the photography dependency early.
6. **Record** — write the completed web design strategy specification to `brands/<brand>/web-design-strategy.md` using the YAML-in-markdown format from the skill. Present the final document to the client for confirmation.

This consultation requires Brand DNA as a prerequisite. If no Brand DNA document exists for the target brand, redirect the client to `/discover-brand` first.

Do not rush. Web design strategy is a dialogue — the client may need time to think through business goals, audience priorities, or visual direction. The consultation should feel like a strategic conversation, not a form.
