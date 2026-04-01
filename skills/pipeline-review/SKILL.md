---
name: pipeline-review
description: >
  Weekly review of all active deals. Trigger when the user asks "how's my
  pipeline?", "what should I focus on this week?", "review my deals", "pipeline
  check", "what's stale?", or any variation of wanting to see the full picture
  across all active opportunities. Also trigger at the start of the week if the
  user asks for a plan or priorities. Input: all deal files in deals/. Output:
  ranked list by quality and staleness, focus recommendations, disqualification
  calls, and gap analysis.
---

# Pipeline Review Skill

You give the user a clear, honest view of their entire pipeline and tell them where to spend their time this week. The output is a prioritized action plan, not a dashboard.

---

## Step 0: Load context

1. Read `config/profile.md` for the user's business context and WORTH customization.
2. Read `framework/SCORECARD.md` for scoring thresholds.
3. Read every `.md` file in `deals/` (except `_template.md`). These are the active deals.

If `deals/` is empty or contains only the template, say so:

> "No active deals to review. When you have a prospect, start with a gut check or qualify a deal, and it'll show up here."

---

## Step 1: Assess each deal

For each deal file, extract:

- **Company name** (from frontmatter or filename)
- **Stage** (discovery / evaluation / negotiation / closed-won / closed-lost)
- **WORTH score** (X/12)
- **Must-have status** (X/2)
- **Quality tier** (High / Medium / Low / Not qualified)
- **Last updated** (from frontmatter)
- **Days since last update** (calculate from today)
- **Next action** (from frontmatter)
- **Key gaps** (unchecked must-have items, or the weakest accelerator dimension)

Skip closed-won and closed-lost deals unless the user asks to include them.

---

## Step 2: Rank and flag

### Sort active deals into three buckets:

**Work this week:** High-quality deals, or medium deals with a clear next action that's overdue. These get your time first.

**Watch list:** Medium deals where the next action isn't urgent, or deals waiting on the prospect. Check in if stale, but don't over-invest.

**Disqualify or deprioritize:** Low-quality deals, deals missing must-haves after multiple conversations, or deals that have been stale for more than 3 weeks with no movement.

### Flag staleness:

| Days since update | Status |
|-------------------|--------|
| 0-7 | Active |
| 8-14 | Getting stale |
| 15-21 | Stale |
| 22+ | Dead unless proven otherwise |

### Flag patterns:

- Deals stuck at the same score across multiple debriefs
- Must-have gaps that haven't closed after two or more conversations
- Deals where the next action hasn't changed in two weeks
- Deals with no stakeholder information (you're selling to a company, not a person)

---

## Step 3: Produce the review

### Output format

---

#### PIPELINE REVIEW

**Date:** [today]
**Active deals:** [count] | **Total pipeline score:** [sum of all scores] / [max possible]

---

##### Work this week

| Deal | Score | Must-haves | Quality | Last updated | Days stale | Priority action |
|------|-------|-----------|---------|-------------|------------|----------------|
| [Company] | X/12 | X/2 | High/Med | YYYY-MM-DD | X | [one-line action] |

For each deal in this bucket, add a 2-3 sentence note:
- Why it's a priority this week
- What specific WORTH gap to close
- What question to ask or action to take

---

##### Watch list

| Deal | Score | Must-haves | Quality | Last updated | Days stale | Status |
|------|-------|-----------|---------|-------------|------------|--------|
| [Company] | X/12 | X/2 | Med | YYYY-MM-DD | X | [waiting on X / nurture / check in] |

Brief note per deal: what you're waiting on and when to re-engage.

---

##### Disqualify or deprioritize

| Deal | Score | Must-haves | Last updated | Days stale | Reason |
|------|-------|-----------|-------------|------------|--------|
| [Company] | X/12 | X/2 | YYYY-MM-DD | X | [why this should go] |

Be direct. "This deal has been at 4/12 for three weeks with no must-have progress. Your time is better spent elsewhere."

---

##### Pipeline health

**Strengths:**
- [What's working: strong deals, good momentum, clear next actions]

**Risks:**
- [What's concerning: too many stale deals, pipeline concentrated in one stage, must-have gaps across the board]

**Recommendations:**
- [1-2 strategic suggestions: "You need more top-of-funnel activity" or "Three deals are stuck in discovery, push for next steps this week"]

---

## Self-check

Before delivering the review:
1. Am I being honest about which deals should be disqualified, or am I keeping them alive to make the pipeline look fuller?
2. Is each "work this week" item actionable within the next 5 business days?
3. Did I flag staleness accurately, or am I giving old deals the benefit of the doubt?
4. Are my recommendations specific to this pipeline, or could they apply to any pipeline? (If generic, sharpen them.)
5. Did I account for the user's capacity? Five "work this week" items for a solo founder might be too many. Prioritize ruthlessly.
