# Self Improving AI Brain for your DTC brand

A knowledge system for ecommerce marketing that compounds over time. You feed it raw information about your brand, customers, and competitors. It organizes that into structured pages. Skills read those pages before producing any output, so everything they create is grounded in what you actually know -- not generic best practices.

The system also tracks what you do across sessions and proposes new skills based on patterns it spots. The more you use it, the smarter it gets.

## What's in the box

```
raw/templates/          4 starter templates you fill out with real brand data
brain/                  Where structured knowledge lives (empty until you ingest)
brain/briefs/    Session logs that feed the learning loop
skills/                 6 skills that read the brain and do work
CLAUDE.md               The instruction file that governs how everything works
```

## Getting started

### 1. Fill out your first template

Open any file in `raw/templates/`. Each one is a fillable document with `[FILL IN]` placeholders and examples showing what kind of data goes in each section.

Pick whichever one you have the best data for. You don't need to do all four before you start.

**icp-details.md** -- Your customer's vocabulary, emotional triggers, frustrations, and where they hang out. This is the most impactful template to fill first. Pull from customer reviews, Reddit threads, support tickets, and social comments. The key insight: capture how your customers actually talk, not how your marketing team talks about them.

**brand-style.md** -- How your brand sounds when the content is working. Not aspirational adjectives like "warm and empowering," but actual patterns: sentence rhythm, how you open and close pieces, what sounds like you vs. what doesn't. Build this from your 10 best-performing pieces of content.

**market-positioning.md** -- What competitive territory you own, what's contested (everyone claims it so nobody owns it), and what you've deliberately ceded. Plus competitor snapshots. Build this from competitor homepages, review sites, and your win/loss data.

**customer-journey.md** -- How people actually find you, what questions they ask while evaluating, what closes the sale, where they stall after buying, what brings them back, and what makes them leave. Build this from analytics, sales call recordings, and post-purchase surveys.

### 2. Ingest it

Tell the agent "ingest icp-details" (or whichever template you filled out). The brain-ingest skill reads the template, breaks it apart into structured brain pages, and updates `brain/index.md`.

For example, the ICP details template gets decomposed into segment pages (one per customer segment you described) and updates to any product pages with relevant emotional triggers. The brand style template becomes `concept-brand-voice.md` with your actual voice patterns.

After ingesting, the brain has real knowledge. Before ingesting, skills are working blind.

### 3. Use a skill

Try "give me 3 email campaign ideas for lapsed customers." The email-campaign-ideas skill will read `brain/index.md`, find relevant segment and product pages, load the brand voice concept page, and produce campaigns grounded in your actual brand data.

If the brain is sparse, the skill will tell you which templates to fill out next to improve its output.

### 4. End your session

Tell the agent to run captains-log. It reviews what happened during the session -- what skills ran, what worked, what didn't, what felt manual -- and saves a structured brief to `brain/briefs/`.

### 5. Level up weekly

Run the level-up skill. It reads all unreviewed session briefs, looks for patterns (things you did more than once, tasks that needed rework, repeated friction), and proposes new skills with draft instruction files. It checks existing skills first so it doesn't propose duplicates.

## How the brain works

The brain is a folder of `.md` files, each one covering a single entity or concept. Pages are organized by category:

- **Products** (`product-[name].md`) -- What messaging works for this product, which segments it resonates with, performance history
- **Segments** (`segment-[name].md`) -- Who they are, their vocabulary, what channels work, what objections they raise
- **Channels** (`channel-[name].md`) -- What's working on this channel right now, creative format learnings, targeting approaches tested
- **Competitors** (`competitor-[name].md`) -- Their positioning, where they're strong, where they're weak, gaps they leave
- **Campaigns** (`campaign-[YYYY-MM]-[name].md`) -- What ran, what happened, why it worked or didn't
- **Concepts** (`concept-[name].md`) -- Reusable strategic knowledge like brand voice, pricing strategy, seasonal patterns
- **Sources** (`source-[YYYY-MM-DD]-[name].md`) -- Summary of each raw source that was ingested

`brain/index.md` is the table of contents. Every skill reads it first to figure out which pages are relevant to its task, then loads only those pages. An email skill loads segments, products, and brand voice. A competitive landing page skill loads competitors and positioning. Selective loading, not everything at once.

## How skills use the brain

Every skill follows the same pattern:

**Before running:** Read `brain/index.md`, identify relevant pages, load them. This is how a skill knows your customers say "treat myself" instead of "make a purchase," or that your lapsed buyers respond to urgency better than curiosity.

**After running:** If the work revealed something new (a messaging angle, a segment insight, a channel learning), the skill tells you what it learned and asks before writing it to the brain. You confirm, it updates the page. You decline, it moves on. The brain never gets written to without your approval.

This means the brain grows in two ways: deliberately through ingests (you drop a file in raw/ and say "ingest this"), and organically through skill write-backs (a skill notices something worth capturing during normal work).

## What each skill does

**brain-ingest** -- Processes raw source material into brain pages. Use when you drop a new file in `raw/` or paste content you want the brain to learn. Handles templates, campaign reports, customer research, competitor intel, ad performance data.

**brain-query** -- Answers questions from brain knowledge. "What do we know about our lapsed segment?" or "Brief me on what's working on email." Synthesizes across multiple brain pages and cites its sources.

**brain-lint** -- Health-checks the brain. Finds stale pages, unresolved contradictions, orphan pages with no links, missing cross-references, and data gaps. Run monthly or after a burst of ingests.

**email-campaign-ideas** -- Generates email campaign concepts with strategic angles, subject lines, sequence outlines, and success metrics. Everything grounded in brain knowledge.

**captains-log** -- Writes a structured brief at end of session. Captures what skills ran, what worked, what needed rework, what felt manual, and flags potential new skills.

**level-up** -- Reviews session briefs and proposes new skills based on patterns. Checks for duplicates against existing skills. Run weekly.

## Adding more knowledge over time

The templates are just the starting point. As your brand generates new data, drop it into `raw/` and ingest it:

- Campaign performance reports
- Customer survey results
- Sales call transcripts
- Competitor homepage screenshots or positioning changes
- Ad performance exports
- Email engagement data
- Customer reviews and social comments

Each ingest updates existing brain pages and creates new ones as needed. The brain gets richer over time, and every skill benefits.

## Building new skills

When level-up proposes a skill (or you want to build one yourself), every skill follows the same template:

1. **Brain loading block** -- Read `brain/index.md`, load relevant pages
2. **Inputs** -- What the skill needs from the user
3. **Steps** -- The actual work
4. **Output format** -- What gets produced
5. **Quality checks** -- How to verify the output
6. **Post-run** -- Surface learnings, ask before writing to brain, log to captains brief

Save new skills to `skills/[name]/SKILL.md` and add them to the Skills Registry in `CLAUDE.md`.

## The flywheel

Fill templates with real data. Ingest them. Run skills that use brain context. Captains-log captures what happened. Level-up spots patterns and proposes new skills. New skills make future sessions faster. New ingests make the brain richer. Each cycle compounds on the last.
