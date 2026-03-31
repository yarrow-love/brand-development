Build a static HTML/Tailwind website mock-up from the brand's accumulated assets — strategy spec, approved copy, reference board, and stock imagery.

## Instructions

Follow the protocol defined in `.claude/skills/mockup.md`:

1. **Identify brand** — determine which brand this session is for by checking `brands/`. Never assume.
2. **Verify prerequisites** — Brand DNA, web design strategy, and copy must exist. Reference board is recommended. Check whether a cloned reference exists at `brands/<brand>/references/<domain>/` — this determines the build path.
3. **Prepare the brief** — ask the client for any final input before building: last thoughts on feel, any personal photos to include, CTA confirmation. Save any client-provided images to `brands/<brand>/mock-up/images/client/`.
4. **Dispatch build subagent** — send a subagent with the full build brief. The subagent reads all brand assets, sources stock imagery (Unsplash/Pexels), and builds the complete HTML/Tailwind mock-up to `brands/<brand>/mock-up/`. If a clone exists, it starts from the clone and transforms it. If not, it builds from scratch following the strategy spec.
5. **Serve and review** — when the build completes, serve the mock-up locally with `npx http-server brands/<brand>/mock-up/ -p 8080`. Walk through each page with the client. Capture screenshots with Playwright if the client can't view the browser directly. Discuss page by page: does it feel like the brand? Does the flow work? Does the imagery set the right tone?
6. **Iterate** — compile revision notes from the client (3-5 changes per round). Dispatch a revision subagent with specific instructions. Review the updated mock-up. Repeat until the client approves.

**Context window discipline:** All HTML generation and image sourcing happens in subagents. The main thread only handles: the client conversation, one or two review screenshots at a time, and revision notes. This preserves context for iteration.

The mock-up uses approved copy from `/write-copy` — no lorem ipsum. It uses design tokens from the strategy spec — no invented colors or fonts. Every image is sourced to match the Brand DNA visual codes and attributed in `images/attribution.md`.
