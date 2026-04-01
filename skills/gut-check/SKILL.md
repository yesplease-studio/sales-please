---
name: gut-check
description: >
  Fast triage before booking a call or investing time in a prospect. Trigger when
  the user mentions a new prospect, asks "should I take this call?", "is this worth
  pursuing?", "someone reached out", or describes an inbound lead. Also trigger when
  the user pastes a LinkedIn message, email, or referral intro. Input: prospect
  name/company + whatever context is available. Output: go/no-go recommendation
  with reasoning mapped to WORTH dimensions.
---

# Gut Check Skill

You help the user decide whether a prospect is worth their time before they invest in a discovery call. The output is a fast, honest go/no-go recommendation.

---

## Step 0: Load context

1. Read `config/profile.md` for the user's business context, ICP, and WORTH customization.
2. Read `framework/GUT-CHECK.md` for the five triage questions.
3. Read `framework/SYSTEM.md` for WORTH dimension definitions (reference, not full output).

If `config/profile.md` doesn't exist, stop and run the setup flow (`SETUP.md`) first.

---

## Step 1: Gather input

The user may provide anything from a name and company to a full email thread. Work with what you get.

**Minimum needed:** A company name or a person's name and role. You can work with less, but flag that the triage is low-confidence.

**If context is thin**, ask one focused question:

> "What do you know about them? Even one sentence helps: what they do, how they found you, what they want."

Don't ask multiple questions. One is enough to get started.

---

## Step 2: Research (if possible)

If the user has provided a company name or website:
- Look up what the company does, size, stage, and industry
- Check if the contact person's role suggests decision-making authority
- Look for any obvious fit or misfit signals

If no web research is available, work with what the user gave you. Don't stall.

---

## Step 3: Run the gut check

Answer each of the five questions from `framework/GUT-CHECK.md`, mapping to the user's ICP and WORTH dimensions:

1. **Does this company look like someone I can actually help?** (maps to W)
2. **Is there a real problem I can see from the outside?** (maps to R)
3. **Is there a person with authority driving this?** (maps to O)
4. **Is there any urgency?** (maps to T)
5. **Can I articulate, in one sentence, why I'm the right fit?** (maps to H)

For each question, give a **Yes**, **No**, or **Unknown** with a one-sentence reason.

---

## Step 4: Deliver the verdict

### Output format

---

#### GUT CHECK: [Company name]

**Contact:** [Name, title if known]
**Source:** [How they came in: inbound, referral, outbound, event, unknown]

| # | Question | Answer | Reasoning |
|---|----------|--------|-----------|
| 1 | Audience fit | Yes/No/Unknown | [one sentence] |
| 2 | Visible problem | Yes/No/Unknown | [one sentence] |
| 3 | Authority | Yes/No/Unknown | [one sentence] |
| 4 | Urgency | Yes/No/Unknown | [one sentence] |
| 5 | Clear fit statement | Yes/No/Unknown | [one sentence] |

**Score:** [X/5 yes answers]

**Verdict:** [Book the call / Book but stay sharp / Nurture only / Move on]

**Reasoning:** [2-3 sentences explaining the verdict. Be specific about what makes this a yes or a no. If it's borderline, say what one piece of information would tip it.]

**If booking:** [One sentence on what to focus on in the call, based on which questions were weak.]

---

## Self-check

Before delivering the verdict:
1. Am I being honest, or am I inflating the score because the prospect seems "interesting"?
2. Did I distinguish between what I know and what I'm assuming?
3. If this is a "no," did I say so clearly instead of hedging?
4. Is the reasoning specific to this prospect, or could it apply to anyone?
