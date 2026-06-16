---
name: brain-lint
description: Health-check the brand brain for staleness, contradictions, orphan pages, missing cross-references, and data gaps. Use when the user wants to audit brain quality, asks "what's missing", "what needs updating", "is the brain healthy", or on a periodic schedule to maintain brain integrity. Triggers on "lint", "audit", "health check", "what's stale", "what's missing", or any request to review brain quality.
---

# Brain Lint

Audit the brand brain for quality issues and suggest improvements. A healthy brain compounds value. A neglected brain decays. This skill catches decay early.

## When to Use

- Periodically (suggest monthly, or after a burst of new ingests)
- User asks about brain health, staleness, gaps
- Before a major planning session (ensure the brain is current first)

## Lint Workflow

### 1. Load Everything
Read:
- `CLAUDE.md` -- conventions to check against
- `brain/index.md` -- full page catalog
- `brain/log.md` -- activity timeline
- All brain pages (scan frontmatter and content)

### 2. Check for Issues

Run these checks and categorize findings:

**Staleness**
- Pages not updated in 90+ days (check `updated` field in frontmatter)
- "What's Working" sections with entries older than 90 days and no recent confirmation
- Flag severity: 90 days = warning, 180 days = stale, 365+ days = potentially obsolete

**Contradictions**
- Claims on one page that conflict with claims on another
- Existing `[!contradiction]` callouts that haven't been resolved
- Performance claims that conflict with more recent campaign data

**Orphans and Missing Links**
- Pages with no inbound `[[wikilinks]]` from other pages
- Entities mentioned in page text but lacking their own page
- Products referenced in campaign pages that don't have a product page
- Segments referenced but lacking a segment page

**Missing Cross-References**
- Campaign pages that reference products/segments/channels but don't link to their brain pages
- Product pages that don't link to their relevant segment pages
- Channel pages that don't link to recent campaign pages

**Data Gaps**
- Product pages with no campaign data
- Segment pages with no "what's working" entries
- Channel pages with no recent (last 90 days) campaign results
- Competitors mentioned but lacking their own page

**Structural Issues**
- Pages missing required frontmatter fields
- Pages not listed in index.md
- Naming convention violations
- Missing "What's Working" / "What's Not Working" sections on products, segments, channels

### 3. Report

Present findings as a prioritized list:

**Critical** (fix now): Active contradictions, badly stale pages for active products/channels
**Important** (fix soon): Missing pages for referenced entities, orphan pages, data gaps
**Maintenance** (fix when convenient): Missing cross-references, frontmatter issues, index gaps

### 4. Fix Mechanical Issues

Offer to automatically fix:
- Missing cross-references (add wikilinks)
- Index gaps (add missing pages to index.md)
- Frontmatter issues (add missing fields)
- Orphan page linking

Do NOT automatically fix:
- Contradictions (human decision)
- Stale content (needs new raw sources)
- Data gaps (needs new raw sources)

### 5. Suggest Next Steps

Based on gaps found, suggest:
- Specific raw sources the user should gather ("we need recent Meta campaign data for Product X")
- Pages that need human review ("the brand voice concept page hasn't been updated since the rebrand")
- Questions to investigate ("three campaigns show conflicting results about Segment Y's price sensitivity")

### 6. Log It
Append to `brain/log.md`:
```
## [YYYY-MM-DD] lint | Brain health check
- Pages checked: [count]
- Critical issues: [count]
- Important issues: [count]
- Maintenance issues: [count]
- Auto-fixed: [list or "none"]
```
