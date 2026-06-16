# Brand Brain

This file governs how the agent operates in this project. Read it at the start of every session.

## System Overview

Brand Brain is a compounding knowledge system for ecommerce marketing. Raw sources go in, the brain grows, skills get smarter, and the system learns what to automate.

The human curates sources, directs work, and asks questions. The agent maintains the brain, runs skills, and captures learnings -- but never writes to the brain without confirmation.

## Directory Structure

```
raw/                    # Immutable source material. Never modify files here.
  templates/            # Starter templates to fill out and ingest first.
brain/                  # Agent-maintained knowledge pages.
  index.md              # Catalog of all pages. Skills read this first.
  log.md                # Chronological record of all operations.
  [pages].md            # Entity, concept, and source pages.
brain/           # Session intelligence layer.
  briefs/               # Captains-log session briefs.
    reviewed.md         # Tracks which briefs level-up has analyzed.
skills/                 # Reusable skills. Each has its own folder + SKILL.md.
```

## The Flow

```
raw/ --> brain-ingest --> brain/ --> skills read brain/index.md --> captains-log --> level-up
```

1. User drops source material into `raw/` (or fills out a starter template in `raw/templates/`)
2. **brain-ingest** processes it into structured brain pages
3. Skills read `brain/index.md` to find and load relevant pages before executing
4. After a skill runs, it surfaces any new learnings and asks before writing to the brain
5. **captains-log** captures what happened at end of session
6. **level-up** reviews briefs weekly and proposes new skills

---

## Agent Rules

### Always do at session start
- Read this file
- Read `brain/index.md` to know what knowledge exists

### Before any content task
- Read `brain/index.md` and load the brain pages relevant to the task
- Don't start from a blank brief when the brain has accumulated knowledge

### After any skill produces output
- Assess whether the work revealed something new: a messaging angle that works, a segment insight, a channel learning, a competitive data point
- If yes, **tell the user what you learned and ask before writing it to the brain**. Example: "This campaign concept relies on urgency-based subject lines for lapsed buyers. Want me to add that as a tested angle to [[segment-lapsed-buyers]]?"
- If the user approves, update the relevant brain page(s) and append to `brain/log.md`
- If no new learnings, move on
- This is NOT the same as running brain-ingest. Ingest is for processing raw sources. This is a lightweight "I noticed something worth capturing" that happens during normal work.

### At end of every session
- Run the captains-log skill to capture what happened

### Never do
- Write to the brain without the user's confirmation
- Modify files in `raw/` (they're immutable source material)
- Overwrite existing brain claims silently (use contradiction handling instead)

---

## Brain Conventions

### Page Categories

**Products** -- `product-[name].md` -- One per product or product line. Positioning, target segments, key claims, performance history, customer feedback themes, what messaging works and doesn't.

**Segments** -- `segment-[name].md` -- One per customer segment. Who they are, what channels they respond to, what language works, objections and how to handle them, which products resonate.

**Channels** -- `channel-[name].md` -- One per marketing channel. Current strategy, what's working/not working (with dates), targeting approaches tested, creative format learnings, best-performing campaigns.

**Competitors** -- `competitor-[name].md` -- One per competitor. Positioning, pricing, messaging angles they own, gaps they leave, where we win and lose.

**Campaigns** -- `campaign-[YYYY-MM]-[name].md` -- One per significant campaign or test. What ran, goals, results, why it worked or didn't, cross-references to product/segment/channel pages.

**Concepts** -- `concept-[name].md` -- Reusable strategic knowledge. Brand voice, pricing strategy, creative frameworks, seasonal patterns. These emerge from patterns across campaigns and segments.

**Sources** -- `source-[YYYY-MM-DD]-[short-name].md` -- One summary per ingested raw source. What it was, key takeaways, which pages were updated.

### Frontmatter

Every brain page has YAML frontmatter:

```yaml
---
category: product | segment | channel | competitor | campaign | concept | source
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [list of raw source filenames that informed this page]
related: [list of brain page filenames this cross-references]
---
```

### Cross-references
Use `[[page-name]]` wikilink syntax. When updating a page, check whether new cross-references are needed.

### Evidence dating
Always include dates with performance data and learnings. "UGC outperforms polished creative" is less useful than "UGC outperformed polished creative in Q1 2026 on Meta for the 25-34 segment (CTR +40%, CPA -22%)."

### Contradiction handling
When new information contradicts an existing brain claim:
1. Keep the old claim with its date
2. Add the new data with its date
3. Add a `> [!contradiction]` callout explaining the conflict
4. Let the human decide how to resolve it

### What's working / What's not
Every product, segment, and channel page should have these sections. They're the most actionable parts of the brain. Update on every relevant change. Date every entry.

---

## Starter Templates

The `raw/templates/` folder has four fillable documents to bootstrap the brain:

- `icp-details.md` -- Customer profile, vocabulary, emotional triggers, frustrations
- `brand-style.md` -- Brand voice patterns, tone calibration, comparison tests
- `market-positioning.md` -- Competitive territory, owned/contested/ceded positions
- `customer-journey.md` -- Discovery, evaluation, purchase, retention, churn mechanics

When ingested via brain-ingest, each template gets decomposed into proper brain pages (segment pages, concept pages, competitor pages, etc.). The templates are the starting point. The brain is the living system.

---

## Skills Registry

Skills live in `skills/[name]/SKILL.md`. Each skill's SKILL.md contains its full instructions. Read the relevant SKILL.md before running a skill.

### Core skills (always available)

| Skill | What it does | When to use |
|-------|-------------|-------------|
| `brain-ingest` | Processes raw sources into brain pages | User drops a file in raw/ or says "ingest this" |
| `brain-query` | Answers questions from brain knowledge | User asks about brand, products, segments, channels |
| `brain-lint` | Health-checks the brain | Monthly, or after a burst of ingests |
| `captains-log` | Writes end-of-session brief | End of every session |
| `level-up` | Reviews briefs, proposes new skills | Weekly |

### Content skills

| Skill | What it does | When to use |
|-------|-------------|-------------|
| `email-campaign-ideas` | Generates email campaign concepts | User wants email strategy or campaign ideas |

### Adding new skills

When building a new skill, follow this pattern in its SKILL.md:

1. **Brain loading block** -- Read `brain/index.md`, load relevant pages for the task
2. **Inputs** -- What the skill needs from the user
3. **Steps** -- The actual work
4. **Output format** -- What gets produced
5. **Quality checks** -- How to verify the output is good
6. **Post-run** -- Surface learnings, ask before writing to brain, log to captains brief

Add the new skill to the Skills Registry table above so this file stays current.

---

## Evolution

This file should evolve. When you discover conventions that aren't working, patterns that should be captured, or structural changes that would help -- update this file. The system should reflect how it's actually used, not how it was originally imagined.
