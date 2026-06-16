---
name: level-up
description: Review captains log session briefs to surface patterns worth turning into new skills. Use weekly or when the user wants to find automation opportunities. Triggers on "level up", "find skills", "what should be a skill", "what am I repeating", "automation opportunities", or any request to analyze session patterns for skill candidates.
---

# Level Up

Review session briefs to surface patterns worth turning into reusable skills. The idea: if you keep doing the same thing manually, it should be a skill.

## When to Use

- Weekly cadence (suggest running every Friday or Monday)
- After a productive stretch of sessions where lots of work happened
- When the user says "what should be a skill?" or "what am I repeating?"

## Workflow

### 1. Load Review State

Read `brain/briefs/reviewed.md` to get the list of already-reviewed briefs. If the file doesn't exist, create it with:

```markdown
# Reviewed Briefs

Briefs that have already been analyzed by level-up. Prevents re-reviewing the same sessions.

## Reviewed
<!-- One filename per line -->
```

### 2. Find Unreviewed Briefs

Scan `brain/briefs/` for any `.md` files not listed in `reviewed.md` (excluding `reviewed.md` itself). If there are no unreviewed briefs, tell the user and stop.

### 3. Analyze Each Brief

For each unreviewed brief, extract:

- **Repeated prompts** -- Any prompt or task marked as repeated (strongest signal)
- **Multi-attempt tasks** -- Any task that required multiple attempts or rework
- **Manual reformatting** -- Any output that was manually adjusted after saving
- **Friction points** -- Anything flagged as slow, annoying, or manual
- **Existing skill candidates** -- Anything the captains-log already flagged as a skill candidate

### 4. Cross-Brief Pattern Matching

This is where the value is. Look across ALL unreviewed briefs (and optionally recent reviewed ones for context) for:

- Tasks that appear in more than one session (strongest candidate)
- Similar friction points across sessions
- Related skill candidates that could be one unified skill
- Workflows that always happen in sequence (could be one compound skill)

### 5. Check for Duplicates

Before proposing any new skill, check:
- Read all existing `skills/*/SKILL.md` files
- Does a skill already exist that covers this task?
- Would this be better as an improvement to an existing skill rather than a new one?
- Is this too similar to another candidate in this batch?

If a skill already exists that partially covers the candidate, recommend extending that skill instead of creating a new one.

### 6. Build Candidates

For each genuine candidate skill (not a duplicate, supported by evidence from briefs):

**Name:** A clear, action-oriented name (e.g., `weekly-metrics-report`, `product-launch-checklist`)

**Evidence:** Which briefs and what specific entries support this candidate

**Draft SKILL.md:** Write a first-draft skill file including:
- Description and trigger conditions
- Step-by-step workflow
- Inputs needed from the user
- Output format
- Which brain pages the skill should load (using the brain-query pattern)
- Post-run captains-log entry

**Time estimate:** How much time this would save per week based on the brief data

### 7. Present to User

For each candidate, present:
1. The skill name and what it does
2. The evidence (which sessions, how many times)
3. Estimated weekly time saved
4. The draft SKILL.md (so they can review and approve)

Ask the user which candidates to keep. For approved candidates, save the SKILL.md files to `skills/[name]/SKILL.md`.

### 8. Update Reviewed List

Append all analyzed brief filenames to `brain/briefs/reviewed.md` under the `## Reviewed` heading, regardless of whether any skills were created. This prevents re-analyzing the same briefs next time.

## What Makes a Good Skill Candidate

**Strong signals:**
- Same task done 3+ times across sessions
- A multi-step workflow that always follows the same sequence
- Something the user explicitly said "I wish this was automated"
- A task that always loads the same brain pages

**Weak signals (probably not a skill yet):**
- Done once, even if it was complex
- Something that changes significantly each time
- A task that's more about judgment than process

**Not a skill:**
- One-off tasks
- Tasks that are already covered by an existing skill
- Pure research/exploration with no repeatable pattern
