---
name: email-campaign-ideas
description: Generate a strategic email campaign calendar grounded in brain knowledge. Use when the user wants email campaign ideas, a monthly email plan, campaign calendar, or email strategy. Triggers on "email campaign", "email ideas", "email plan", "email calendar", "campaign ideas", "what emails should we send", or any request for email marketing concepts.
---

# Email Campaign Ideas Generator

Builds a strategic email campaign calendar for ecommerce brands. Think Common Thread Collective or Homestead Studios approach: data-informed, segment-aware, strategically sequenced. Not a list of random email ideas, but a cohesive plan with reasoning behind every send.

Default: 8 campaigns over 30 days. That's the optimal cadence before hitting diminishing returns.

## Phase 1: Brain Loading

### Step 1: Read the Index
Read `brain/index.md` to understand what knowledge exists.

### Step 2: Load Relevant Pages
Load everything that informs email strategy:
- **Segment pages** -- audience language, objections, triggers, purchase behavior
- **Product pages** -- what messaging works, best sellers, new arrivals, seasonal relevance
- **Channel pages** (especially `channel-email.md`) -- past email performance data, open rates, click rates, what's been tested, send frequency patterns
- **Campaign pages** -- any campaigns run in the last 60 days (to avoid repetition)
- **Concept pages** -- brand voice, customer journey mechanics, positioning

### Step 3: Check Briefs
Scan `brain/briefs/` for the last 5 session briefs. Look for:
- Previous email campaigns that were generated
- Notes about what worked or needed rework
- Performance feedback on past campaigns

## Phase 2: Gather Inputs

Confirm the following with the user. If not provided, use the defaults:

1. **Campaign goal** -- What's the business objective? (e.g., drive revenue, reduce churn, increase repeat purchases, launch a new product, grow the list, build brand affinity). No default -- always ask.
2. **Date range** -- What period are we planning for? Default: next 30 days from today.
3. **Number of campaigns** -- How many emails in the plan? Default: 8 over the 30-day period.
4. **Constraints** -- Any constraints? (e.g., "no discounting," "we have a product launch on the 15th," "avoid Mondays," "SMS + email combo"). Default: none.

## Phase 3: Analyze

Before generating any campaign ideas, do this analysis. This is what separates a strategic plan from a list of email types.

### 3a: Performance Review

Pull any past email performance data from the brain (channel-email page, campaign pages, product pages with email-specific metrics). Look for:

- Which campaign types drove the highest revenue per send?
- Which subject line patterns had the best open rates?
- Which segments had the highest engagement?
- Which sends underperformed and why?
- What day of week and time of day patterns show up?

If no performance data exists in the brain, note this explicitly in the output. Tell the user: "No past email performance data found in the brain. Add your email/campaign analytics to `raw/` and run brain-ingest to make future plans data-driven."

### 3b: Recent Campaign Deduplication

Check all campaign pages from the last 60 days. List out what was sent, to which segments, and what angle was used. Do NOT propose campaigns that are similar to anything sent in this window. If you're drawing from the same campaign type (e.g., "testimonial spotlight"), it must use a different angle, segment, or product than the recent version.

### 3c: Segment Assessment

Identify the segments available in the brain. For each, note:
- Last time they were emailed (if known)
- Engagement level (if known)
- Where they sit in the customer journey
- Which campaign types are most relevant to them

If no segment pages exist in the brain, use these standard ecommerce segments as a starting framework. But flag this clearly: "No segment data found in the brain. Using default ecommerce segments. Add your ICP details to `raw/templates/icp-details.md` and ingest to make segment targeting specific to your brand."

Default ecommerce segments:
- **Engaged subscribers** -- On the list, opening emails, haven't purchased yet
- **First-time buyers** -- Purchased once in the last 30 days
- **Repeat customers** -- 2+ purchases
- **VIPs** -- Top 10% by revenue or frequency
- **At-risk** -- Previously active, no engagement in 30-60 days
- **Lapsed** -- No purchase or engagement in 60+ days

### 3d: Strategic Mix

Plan the 8 campaigns (or however many were requested) as a balanced mix across these dimensions:

**Campaign type variety** -- Don't stack 4 product pushes in a row. Alternate between value-driven, social proof, product, and brand-building sends. Use this palette of campaign types (not exhaustive -- combine and adapt):

*Social proof & trust:* Testimonial Spotlight, Press Mention / Media Feature, Publication Highlight, Research Highlight, Myths Debunked

*Product & commerce:* Trending Products, Best Sellers, New Arrivals, Staff Picks, Back In Stock, Bundles, Essentials, Gift Guide

*Education & value:* Blog/Article Highlight, FAQ, How To Use, Tips & Tricks, How It's Made

*Brand & story:* Behind The Scenes, Brand USPs, Brand Story, Founder Story, Meet The Team, Recent Developments, Sneak Peek

*Conversion-focused:* Feature Highlight, Benefit Highlight, Us vs. Them, Problem to Solution, Before and After, About Yourself (quiz/personalization)

**Segment rotation** -- Spread sends across segments. Don't email the same segment 4 times in a row while ignoring others.

**Journey stage coverage** -- Make sure the plan covers multiple journey stages (awareness, consideration, purchase, retention, win-back) rather than clustering at one stage.

**Timing** -- Space sends 3-4 days apart minimum. Consider day-of-week patterns from performance data if available. Avoid stacking heavy promotional sends back to back.

## Phase 4: Build the Plan

### Output: Campaign Calendar

Present the plan as a calendar with this structure:

---

**Data Analysis Summary**

Before listing campaigns, present a brief summary of what informed the plan:
- Performance insights used (or "No performance data available -- recommend adding to raw/")
- Campaigns from the last 60 days that were avoided (or "No recent campaigns found in the brain")
- Segments targeted and why
- Any data gaps that limited the plan's precision

---

**Campaign Calendar: [Date Range]**

For each campaign:

**[#]. [Campaign Title]**
- **Brief:** [Two sentences on the creative idea behind this campaign. What's the hook? Why will this land?]
- **Type:** [From the campaign type palette above]
- **Segment:** [Which segment and why this campaign is right for them at this point]
- **Send date:** [Specific date]
- **Journey stage:** [Where this hits in the customer lifecycle]
- **Data reasoning:** [What brain data informed this choice -- past performance, segment behavior, timing pattern. If no data, say "Based on ecommerce best practices -- add performance data to improve targeting."]

---

**Gaps & Recommendations**

After the calendar, list:
- What data would make the next plan better (be specific: "Add your last 90 days of Klaviyo campaign performance to raw/")
- Which segments are underserved and need more data
- Any brain pages that should be created or updated

## Quality Checks

Before presenting the plan, verify:

- [ ] No campaign is similar to anything sent in the last 60 days
- [ ] Campaign types are varied (no more than 2 of the same type in the plan)
- [ ] Segments are rotated (no segment gets more than 3 sends unless the plan is segment-specific)
- [ ] Sends are spaced at least 3 days apart
- [ ] Every campaign has a clear segment and journey stage, not "everyone"
- [ ] Audience language matches vocabulary from segment pages (their words, not yours)
- [ ] Subject line patterns match brand voice from `concept-brand-voice.md` (if it exists)
- [ ] Data reasoning is present for every campaign (even if it's "no data available")
- [ ] The plan includes a Gaps & Recommendations section

## Post-Run

After completing this skill:

1. **Log to captains brief:** Note what was produced, which brain pages were loaded, data gaps identified, and how many campaigns were planned.
2. **Offer to file back:** Ask if the user wants to save this plan as a brain page (`campaign-[YYYY-MM]-email-plan.md`) so future runs can reference what was planned.
3. **Surface learnings:** If the planning process revealed something new about segments, timing, or campaign type effectiveness, tell the user and ask before writing to the brain.

## Notes

- If the brain is empty, the skill still works -- it uses default segments and ecommerce best practices. But it should be clear about what's assumption vs. what's data. The output should push the user toward filling the brain so the next plan is better.
- 8 campaigns over 30 days is the default, not a rule. If the user asks for more or fewer, adjust. But if they ask for significantly more than 8, flag that frequency above ~2-3x/week tends to hit diminishing returns for most ecommerce brands unless they have strong engagement data supporting higher frequency.
- The campaign type palette is inspiration, not a checklist. Campaigns can combine types (e.g., "Founder Story + New Arrival" or "Testimonial + Problem to Solution"). The best campaigns usually blend 2-3 types.
- Always explain the reasoning. A campaign plan without reasoning is just a list of email types on a calendar. The value is in the "why" -- why this type, why this segment, why this timing, why this sequence.
