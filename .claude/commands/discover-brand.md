Conduct a brand DNA discovery interview to establish foundational brand identity.

## Instructions

Follow the protocol defined in `.claude/skills/brand-discovery.md`:

1. **Identify brand** — ask the client for their brand name. Check `brands/` for an existing directory. If one exists with a populated `brand-dna.md`, confirm whether this is a revision session.
2. **Load industry context** — ask what the client does (their trade, industry, or modality). Check `research/<industry>/brand-dna.md` for relevant research. If none exists, recommend generating it via `/research` — the industry context will produce a better interview.
3. **Load existing DNA** — if `brands/<brand>/brand-dna.md` exists, read it and acknowledge what's already captured.
4. **Interview** — guide the client through the phased interview structure (origin -> personality -> audience -> visual -> constraints -> positioning), adapting pace and depth to their responses. One question at a time.
5. **Synthesize** — after each phase, reflect back what you've heard. Surface contradictions gently. Push for specificity in visual language.
6. **Record** — write the completed Brand DNA specification to `brands/<brand>/brand-dna.md` using the YAML-in-markdown format from the skill. Present the final document to the client for confirmation.

Do not rush. Brand DNA discovery is a dialogue — the client may need time to think through answers, revisit earlier questions, or explore contradictions. The interview should feel like a design conversation, not a form.
