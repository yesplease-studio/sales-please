---
name: deal-debrief
description: >
  Post-meeting deal update. Trigger when the user has already qualified a deal and
  comes back with new information from a follow-up meeting, call, or email exchange.
  Also trigger when the user says "update the deal", "debrief", "just had a call with X",
  "here's what happened", or pastes notes for a deal that already has a file. Input:
  existing deal file + meeting notes or transcript. Output: updated deal file with
  re-scored checklist, changes highlighted, and next actions redefined.
---

# Deal Debrief Skill

You update an existing deal after new information comes in. The output highlights what changed, what improved, what got worse, and what to do next.

---

## Step 0: Load context

1. Read `config/profile.md` for the user's business context and WORTH customization.
2. Read `framework/SCORECARD.md` for the checklist and thresholds.
3. Read `framework/SYSTEM.md` for dimension definitions and red flags.
4. Read the existing deal file at `deals/[company-name].md`. This is required. If no deal file exists, redirect to the `deal-qualify` skill instead.

---

## Step 1: Gather input

The user provides new information about an existing deal:
- Meeting notes or transcript from a follow-up call
- An email exchange
- A verbal update ("talked to their CEO, she's on board but wants to see a proposal first")
- Any new context about the deal

If the user just says "I had a call with [company]" without details, ask:

> "What happened? Give me the highlights, or paste the notes."

One question only. Don't interview them.

---

## Step 2: Compare old and new

Read the existing deal file carefully. For each WORTH dimension:

1. **What was checked before?** Note the previous score and evidence.
2. **What does the new information change?** Did any unchecked items get confirmed? Did any checked items get undermined?
3. **What's genuinely new?** New stakeholders, new objections, new timeline information, shifts in sentiment.

Be precise about what actually changed versus what was restated.

---

## Step 3: Re-score

Score all 12 checklist items against the combined evidence (old + new). An item stays checked if the original evidence still holds. An item gets unchecked only if new evidence contradicts it.

Calculate:
- **New score:** X/12
- **Previous score:** X/12
- **Delta:** +/- X
- **Must-haves:** X/2
- **Quality tier:** High / Medium / Low / Not qualified

---

## Step 4: Update stakeholders

From the new information:
- Add any new people mentioned
- Update sentiment, role, or context for existing stakeholders
- Note last contact date
- Flag any changes in the decision-making dynamic (new blocker, champion lost enthusiasm, economic buyer engaged directly)

---

## Step 5: Redefine next actions

Based on the updated score and what happened in the meeting:
- What WORTH gaps remain?
- What's the single most important thing to do next?
- Are any previous next actions now irrelevant?
- Should the deal stage change? (discovery to evaluation, evaluation to negotiation, or any stage to closed-lost)

If the deal has deteriorated below threshold, say so. "This deal was medium quality and it's now low. The must-have gap in [dimension] didn't close after two conversations. Consider deprioritizing."

---

## Step 6: Deliver the debrief and update the file

### Output format

Present the debrief summary before updating the file:

---

#### DEAL DEBRIEF: [Company name]

**Score:** [X/12] (was [Y/12], [+/-Z]) | **Must-haves:** [X/2] | **Quality:** [tier]
**Stage:** [current, flag if changed]

**What changed:**
- [+] [Item that got checked, with evidence]
- [-] [Item that got unchecked, with reason]
- [~] [Item where evidence shifted but didn't flip]

**New information:**
- [Anything significant that doesn't map to a checklist item: new stakeholder, objection surfaced, pricing discussed, competitor mentioned]

**Stakeholder updates:**
- [Name]: [what changed about their role, sentiment, or context]

**Next actions:**
1. [Most important action, targeting the biggest gap]
2. [Supporting action]

**Overall trajectory:** [Improving / Stable / Deteriorating / Stalled]

---

Then update the deal file at `deals/[company-name].md`:
- Re-check/uncheck items with updated evidence
- Update frontmatter (score, stage, last_updated, next_action)
- Add/update stakeholder entries
- Add a dated note to the Notes section

Preserve all previous notes and evidence. New evidence goes alongside old evidence, not replacing it.

---

## Self-check

Before delivering the debrief:
1. Did I distinguish between what actually changed and what was merely restated?
2. Is every score change backed by specific new evidence?
3. Am I being honest about trajectory, or am I preserving optimism from the previous score?
4. If this deal is stalling, did I name it? Deals that stay at the same score for multiple debriefs are stalling.
5. Are the next actions different from last time, or am I recommending the same thing again? (If the same gap persists, the approach needs to change, not just repeat.)
