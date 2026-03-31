Discover, capture, and discuss competitor and inspiration websites to build a visual reference board before mock-up.

## Instructions

Follow the protocol defined in `.claude/skills/reference-gathering.md`:

1. **Identify brand** — determine which brand this session is for by checking `brands/`. Never assume.
2. **Verify prerequisites** — web design strategy must exist at `brands/<brand>/web-design-strategy.md`. Brand DNA must exist at `brands/<brand>/brand-dna.md`. Copy should ideally exist at `brands/<brand>/copy.md`.
3. **Load context** — read the brand's DNA (competitors, visual codes, positioning), web design strategy (archetype, reference sites, tokens, design rules), and industry research (`research/<industry>/web-design.md`) for case studies and archetype patterns.
4. **Seed the search** — ask the client about competitors, sites they admire, and sites they dislike. Combine with references already in DNA and strategy docs.
5. **Dispatch discovery subagent** — send a background subagent to search for sites, capture screenshots (Playwright CLI), and fetch page content (WebFetch). The subagent saves all files to `brands/<brand>/references/` and writes a summary to `capture-notes.md`. Continue conversing with the client while it runs.
6. **Present one at a time** — when the subagent completes, display viewport screenshots to the client one site at a time using the Read tool. Only load the full-page screenshot if the client wants to go deeper. This preserves context window for phases that follow.
7. **Guide discussion** — for each site, ask for gut reaction, specific element reactions, and comparison to Brand DNA. Capture the client's own words. If they name additional sites, dispatch a quick capture subagent for those URLs.
8. **Clone closest reference (optional)** — if one site emerges as structurally closest to the client's vision, offer to clone its front-end as a mock-up starting point. Dispatch a clone subagent to extract rendered HTML/CSS via Playwright, saving to `brands/<brand>/references/<domain>/`. The clone preserves layout structure, spacing, and section flow while stripping JavaScript and third-party embeds. This gives the mock-up phase an editable structural reference instead of a blank page.
9. **Synthesize** — identify patterns, name the visual territory, extract adopt/avoid elements, reconcile with strategy.
10. **Record** — write the reference board to `brands/<brand>/references.md` using the format from the skill. The `mock_up_guidance` section is the most important output — it translates reactions into direct mock-up instructions. If a clone was produced, include the `cloned_reference` section mapping the clone's structure to the web design strategy.

**Context window discipline:** The heavy I/O (searching, fetching, screenshotting) happens in subagents. The main thread only sees: the client's words, one screenshot at a time, and the synthesis. This keeps the consultant's context available for the mock-up phase.

This is a visual conversation. Show, don't tell. Let the client react to real examples rather than describing sites in words.
