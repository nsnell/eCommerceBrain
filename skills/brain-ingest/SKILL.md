---
name: brain-ingest
description: Ingest raw source material into the brand brain. Use when the user drops a new file into raw/ and wants it processed, or when they paste content and say to "ingest this", "add this to the brain", "process this source", "file this". Also use after completing any other task (ad creation, email campaign, etc.) where the results should be captured in the brain. Triggers on any mention of ingesting, adding sources, updating the brain with new information, or processing new material.
---

# Brain Ingest

Process raw source material into the brand brain. This is the core operation that makes the brain compound over time.

## When to Use

- User drops a file into `raw/` and asks you to process it
- User pastes content directly and says to add it to the brain
- After running another skill (email campaign, ad copy, etc.) where the output and learnings should be captured
- User says "ingest", "add this", "file this", "process this"
- User fills out one of the starter templates in `raw/templates/` and wants it broken into brain pages

## Ingest Workflow

### 1. Load Context
Read these files first:
- `CLAUDE.md` -- the schema and conventions
- `brain/index.md` -- what pages already exist
- `brain/log.md` (last 10 entries) -- what's been done recently

### 2. Read the Source
Read the new raw source. If it's a file in `raw/`, read it. If the user pasted content, work from that.

Identify:
- What type of source is this? (campaign results, customer research, competitor analysis, brand context, call transcript, ad performance data, starter template, etc.)
- What entities does it reference? (products, segments, channels, competitors)
- What are the key takeaways?
- Does anything here contradict existing brain knowledge?

### 3. Discuss with the User
Before updating the brain, briefly share:
- What you found in the source
- Which existing brain pages you plan to update
- Whether any new pages need to be created
- Any contradictions with existing knowledge

Keep this concise. The user should confirm or redirect before you start writing.

### 4. Update the Brain

For each affected brain page:
1. Read the current page
2. Add new information with dates and source attribution
3. Update "What's Working" / "What's Not Working" sections if relevant
4. Add new cross-references (`[[page-name]]` wikilinks)
5. Update frontmatter: `updated` date, add to `sources` list, update `related` list

For new pages:
1. Create with proper frontmatter (category, created date, sources, related)
2. Follow the naming convention from CLAUDE.md (`product-[name].md`, `segment-[name].md`, etc.)
3. Include "What's Working" and "What's Not Working" sections for products, segments, and channels

### 5. Write Source Summary
Create `brain/source-[YYYY-MM-DD]-[short-name].md` with:
- What the source is
- Key takeaways
- Which brain pages were updated or created

### 6. Update Index and Log
- Add any new pages to `brain/index.md` with one-line summaries
- Append to `brain/log.md`:
  ```
  ## [YYYY-MM-DD] ingest | [Source description]
  - Source: [filename or description]
  - Pages created: [list]
  - Pages updated: [list]
  - Contradictions flagged: [list or "none"]
  ```

### 7. Report
Tell the user:
- What was ingested
- Pages created and updated (with counts)
- Any contradictions flagged
- Any gaps identified ("we have campaign data for this product but no segment page for the audience it targeted")

## Template Ingestion

When the source is one of the starter templates from `raw/templates/`, the ingest is different from a normal raw source. Templates are broad documents covering audience, style, positioning, or journey -- they need to be decomposed.

**ICP Details template** breaks into:
- One or more `segment-[name].md` pages (from the demographics and vocabulary sections)
- Updates to relevant `product-[name].md` pages (from emotional triggers and frustrations)

**Brand Style template** breaks into:
- `concept-brand-voice.md` (the core voice patterns, comparison tests, and channel calibration)
- Updates to `channel-[name].md` pages (from the per-channel tone calibration section)

**Market Positioning template** breaks into:
- `competitor-[name].md` pages (one per competitor in the snapshot section)
- `concept-positioning.md` (owned/contested/ceded territory, white space, anti-patterns)

**Customer Journey template** breaks into:
- Updates to `segment-[name].md` pages (discovery paths, evaluation questions, churn reasons)
- Updates to `channel-[name].md` pages (from discovery paths and conversion data)
- `concept-customer-journey.md` (the overall journey mechanics, stall points, expansion patterns)
- Updates to `product-[name].md` pages (entry point SKUs, product pairings)

If a template still has `[FILL IN]` placeholders, skip those sections and note them in the report as gaps.

## Source Types and What to Extract

**Starter templates:** Decompose into brain pages per the mapping above. These are the richest initial sources.

**Campaign results/recaps:** Performance metrics, what creative ran, what targeting was used, what worked and what didn't, lessons learned. Update product, segment, channel, and campaign pages.

**Customer research (surveys, calls, reviews):** Feedback themes, objections, language customers use, what they value, pain points. Update segment and product pages.

**Competitor intelligence:** Positioning, pricing, messaging, creative approaches, gaps. Update competitor pages and relevant product pages.

**Brand context (guidelines, positioning docs, strategy docs):** Voice rules, positioning statements, values, do/don't rules. Update or create concept pages.

**Ad performance data:** Which angles, hooks, formats, and targeting combinations performed. Update channel, product, and segment pages with specific data points.

**Email performance data:** Subject line performance, content types that drive clicks, segment-specific engagement patterns. Update channel and segment pages.

## Batch Ingest

If the user drops multiple files at once, process them one at a time. After each, update the relevant pages before moving to the next. This ensures cross-references build correctly. Report a summary at the end covering all sources.
