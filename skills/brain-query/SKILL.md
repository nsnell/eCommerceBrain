---
name: brain-query
description: Query the brand brain to answer questions, build briefs, or synthesize knowledge across pages. Use when the user asks questions about their brand, products, customers, competitors, or channels and wants answers grounded in accumulated brain knowledge. Also use when preparing briefs before creating ads, emails, or campaigns. Triggers on "what do we know about", "brief me on", "pull together", "what's working", "what's not working", "summarize our knowledge on", or any question that should draw on the brain.
---

# Brain Query

Answer questions and build briefs by synthesizing knowledge from the brand brain. The brain contains accumulated, cross-referenced knowledge that's richer than any single source.

## When to Use

- User asks a question about their brand, products, segments, channels, or competitors
- User wants a brief before writing ads, emails, or launching a campaign
- User asks "what do we know about X"
- User asks "what's working" or "what's not working" for a product, segment, or channel
- Before running email-campaign-ideas, ad-copywriting, or similar skills -- pull brain context first

## Query Workflow

### 1. Load Context
Read:
- `CLAUDE.md` -- conventions
- `brain/index.md` -- find relevant pages

### 2. Identify Relevant Pages
From the index, determine which pages are relevant to the query. A question about "email performance for Product X" might need:
- `channel-email.md`
- `product-x.md`
- Recent campaign pages that ran Product X via email
- Relevant segment pages
- `concept-brand-voice.md` (if the question involves messaging)

Read all relevant pages.

### 3. Synthesize
Answer the question by pulling together information across pages. Always:
- Reference which brain pages the information comes from
- Note the dates of the evidence (how recent is this knowledge?)
- Flag any contradictions between pages
- Distinguish between well-supported claims (multiple sources, recent data) and thin claims (single source, old data)

### 4. Output Formats

**Quick answer:** For simple factual questions, give a direct answer with page references.

**Brief:** For pre-campaign briefs, structure as:
- Target segment: who, what they respond to, what doesn't work
- Product positioning: what messaging works, competitive angle
- Channel context: what's working on this channel, recent learnings
- Creative direction: angles that have evidence behind them
- Risks/gaps: what we don't know, contradictions to be aware of

**Deep dive:** For research questions, produce a thorough synthesis. Offer to file it as a new concept page if it's reusable.

### 5. File Back (Optional)
If the query produced a valuable synthesis -- a comparison, a strategic analysis, a connection between previously unlinked knowledge -- offer to save it as a new brain page (usually a concept page). This is how explorations compound back into the brain.

If filing back:
- Create the page with proper frontmatter
- Update index.md
- Append to log.md with `query` operation type

## Pre-Task Briefing

When another skill is about to run (email-campaign-ideas, ad copy, etc.), this skill can be used first to pull relevant brain context. The pattern:

1. User says "write an email campaign for Product X targeting Segment Y"
2. Before writing, query the brain for Product X, Segment Y, and the email channel
3. Feed the accumulated knowledge into the creative task
4. This makes every output informed by everything you've learned, not just the immediate brief
