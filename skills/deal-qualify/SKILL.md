---
name: deal-qualify
description: >
  Score a deal against the WORTH framework after a discovery call or meeting.
  Trigger when the user pastes meeting notes, a transcript, or describes a
  conversation with a prospect and wants to evaluate the deal. Also trigger
  when the user asks "how does this deal look?", "score this", "qualify this",
  or "create a deal file for X". Input: meeting notes or transcript, plus
  the existing deal file if one exists. Output: a new or updated deal file
  with WORTH scores, evidence, stakeholder updates, and next actions.
---

# Deal Qualify Skill

You score a deal against the WORTH checklist and produce a deal file that captures everything the user knows. The output is honest, evidence-based, and actionable.

---

## Step 0: Load context

1. Read `config/profile.md` for the user's business context, ICP, and WORTH customization.
2. Read `framework/SCORECARD.md` for the 12-item checklist and scoring thresholds.
3. Read `framework/SYSTEM.md` for WORTH dimension definitions and red flags.
4. Check if `deals/[company-name].md` exists. If it does, read it. You're updating, not starting fresh.

If `config/profile.md` doesn't exist, stop and run the setup flow (`SETUP.md`) first.

---

## Step 1: Gather input

The user should provide one of:
- Meeting notes (structured or unstructured)
- A call transcript
- A verbal summary of a conversation

**If no deal file exists yet**, also ask for:
- Company name
- Contact name and role
- How the deal started (inbound, outbound, referral)

If the user drops raw notes or a transcript, don't ask for more. Extract what you can and flag what's missing.

---

## Step 2: Extract WORTH signals

Go through the input and pull out every piece of evidence relevant to the 12 checklist items. Be specific. Quote the prospect's words where possible.

For each WORTH dimension, identify:
- **What's confirmed:** Evidence that checks a box.
- **What's missing:** Items with no evidence either way.
- **Red flags:** Signals that suggest a problem (reference the red flags in `framework/SYSTEM.md`).

---

## Step 3: Score the deal

Check each of the 12 items based on evidence only. If you don't have evidence, the item is unchecked. Don't infer.

Calculate:
- **Score:** X/12
- **Must-haves:** X/2 (W and R by default, or whatever the user configured)
- **Quality tier:** High / Medium / Low / Not qualified (per `framework/SCORECARD.md` thresholds)

---

## Step 4: Identify stakeholders

From the meeting notes or transcript, extract any people mentioned:
- Name and title
- Role in the decision (champion, economic buyer, evaluator, user, blocker)
- What they care about (pain, metrics, priorities)
- Sentiment toward your solution
- Reporting relationship if mentioned

If updating an existing deal file, merge new stakeholder info with existing entries. Don't overwrite previous context unless it's been explicitly corrected.

---

## Step 5: Define next actions

Based on the unchecked items and the current deal stage, recommend 1-3 specific next actions. Each action should:
- Target a specific WORTH gap
- Name what to do, who to contact, and what to ask or send
- Be completable in the next 1-2 weeks

If the deal doesn't qualify, the next action might be "deprioritize" or "disqualify." Say so.

---

## Step 6: Produce the deal file

### If creating a new deal file:

Copy the structure from `deals/_template.md` and fill in everything from Steps 2-5.

### If updating an existing deal file:

Update the existing file:
- Re-score all checklist items (some may change)
- Update the frontmatter (score, stage, last_updated, next_action)
- Add new evidence under each dimension
- Update stakeholder entries
- Add a dated note to the Notes section summarizing what changed

### Output format

Before writing the file, present a summary:

---

#### DEAL QUALIFICATION: [Company name]

**Score:** [X/12] | **Must-haves:** [X/2] | **Quality:** [High/Medium/Low/Not qualified]
**Stage:** [discovery/evaluation/negotiation]

**What's strong:**
- [Dimension]: [one sentence on what's confirmed]

**What's missing:**
- [Dimension]: [one sentence on the gap and what would fill it]

**Red flags:**
- [Any red flags from the evidence]

**Next actions:**
1. [Specific action targeting a specific gap]
2. [Specific action]
3. [Specific action]

**Changes from last score:** [If updating: what moved, what's new, what got worse]

---

Then write or update the deal file at `deals/[company-name].md`.

---

## Self-check

Before delivering the qualification:
1. Is every checked item backed by evidence from the conversation, not my assumption?
2. Am I being honest about must-have gaps, or am I giving the deal the benefit of the doubt?
3. Are the next actions specific enough that the user knows exactly what to do?
4. If this deal is below threshold, did I say "deprioritize" clearly instead of suggesting more discovery?
5. Did I capture stakeholder information accurately, or am I guessing at roles and sentiment?
