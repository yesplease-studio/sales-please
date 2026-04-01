---
name: meeting-prep
description: >
  Pre-meeting brief for an upcoming prospect conversation. Trigger when the
  user says "I have a call with X", "prep me for the meeting", "meeting with
  X tomorrow", "what should I focus on with X?", or mentions an upcoming
  conversation with a company that has a deal file. Input: deal file + optional
  agenda + who's in the room. Output: WORTH gaps to close, per-person approach
  from stakeholder map, recommended questions, and anticipated objections.
---

# Meeting Prep Skill

You prepare the user for a prospect meeting by turning their deal file into a focused game plan. The output tells them exactly what to listen for, who to address, and which WORTH gaps to close in this conversation.

---

## Step 0: Load context

1. Read `config/profile.md` for the user's business context, ICP, and offering.
2. Read `framework/SYSTEM.md` for WORTH dimension definitions and red flags.
3. Read `framework/SCORECARD.md` for the checklist items.
4. Read the deal file at `deals/[company-name].md`. This is required. If no deal file exists, offer to create one first using `deal-qualify`, or at minimum run a `gut-check`.

---

## Step 1: Gather input

The user should provide:
- **Which company** (so you can find the deal file)
- **Who's in the room** (if known, and if different from existing stakeholder map)
- **Meeting type** (discovery follow-up, demo, proposal review, negotiation, check-in)
- **Anything specific** they want to address

If the user just says "I have a call with [company]," that's enough. Pull the rest from the deal file.

---

## Step 2: Analyze the deal state

From the deal file, identify:

### WORTH gaps to close
Which checklist items are unchecked? Rank them by impact:
1. **Must-have gaps first.** If W or R items are unchecked, those are the priority. The deal isn't qualified until these are resolved.
2. **Accelerator gaps that could move this week.** Which unchecked items could realistically be addressed in this conversation?
3. **Items that need more time.** Some gaps (like "champion emerged") take multiple conversations. Note them but don't make them the focus.

### Stakeholder analysis
From the stakeholder section of the deal file:
- Who's in this meeting and what's their role in the decision?
- What does each person care about? What are they measured on?
- What's their current sentiment?
- Who's missing from the room that should be there?

### Deal trajectory
- Is this deal improving, stable, stalling, or deteriorating?
- How many conversations have you had? What's changed between them?
- What was the previous next action, and was it completed?

---

## Step 3: Produce the meeting brief

### Output format

---

#### MEETING PREP: [Company name]

**Meeting:** [Type] with [who's in the room]
**Deal state:** [Score X/12] | [Quality tier] | [Stage]
**Last updated:** [date] ([X days ago])

---

##### Objective

One sentence: what success looks like for this meeting. Tied to the most important WORTH gap.

> Example: "Confirm that the CTO is the economic buyer and get direct access, moving O from 1/3 to 3/3."

---

##### WORTH gaps to close in this meeting

| Priority | Dimension | Gap | How to close it |
|----------|-----------|-----|-----------------|
| 1 | [W/O/R/T/H] | [Unchecked item] | [Specific question or approach] |
| 2 | [W/O/R/T/H] | [Unchecked item] | [Specific question or approach] |
| 3 | [W/O/R/T/H] | [Unchecked item] | [Specific question or approach] |

Don't list more than 3. A meeting that tries to close 5 gaps closes none.

---

##### People in the room

For each person attending (from stakeholder map + any new names):

**[Name] — [Title] — [Role: Champion / Economic Buyer / Evaluator / Blocker]**
- **Cares about:** [their pain, their metrics, what they're measured on]
- **Sentiment:** [Positive / Neutral / Skeptical / Unknown]
- **Approach:** [How to engage this person specifically. What to say, what to ask, what to avoid.]

If someone is attending who isn't in the stakeholder map yet, flag it:
> "[Name] is new. Priority: figure out their role in the decision and what they care about."

---

##### Questions to ask

5 questions maximum, ordered by priority. Each targets a specific WORTH gap or stakeholder insight.

1. **[Question]** — targets [dimension/gap]. Listen for: [what a good answer sounds like vs. a red flag].
2. **[Question]** — targets [dimension/gap]. Listen for: [what to watch for].
3. **[Question]** — targets [dimension/gap]. Listen for: [signal vs. noise].

Draw from the red flags in `framework/SYSTEM.md`. If a question could surface a red flag, name it.

---

##### Anticipated objections

Based on the deal state, stakeholder sentiment, and common patterns from `config/profile.md`:

1. **[Objection]** — [How to address it. Be specific to this deal, not generic.]
2. **[Objection]** — [Response approach.]

If no objections are likely (early discovery, relationship is strong), skip this section.

---

##### Don't forget

- [Any logistics: proposal to send beforehand, demo to prepare, reference to mention]
- [Follow-up from last conversation that was promised but might be forgotten]
- [Stakeholder who should be in the room but isn't, and how to ask for the introduction]

---

## Self-check

Before delivering the brief:
1. Is the objective specific and measurable, or is it vague ("learn more about their needs")?
2. Are the questions targeting actual WORTH gaps, or are they generic discovery questions?
3. Did I use the stakeholder map to tailor the approach, or am I treating everyone the same?
4. Am I being honest about the deal state, or am I preparing the user for a meeting that shouldn't happen?
5. Can the user read this brief in 5 minutes before walking into the meeting?
