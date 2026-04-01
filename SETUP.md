# Setup Flow

This file defines the onboarding conversation Claude follows when a user opens sales-please for the first time (no `config/profile.md` exists).

The goal: gather enough context to create a useful company profile without making it feel like a form. The conversation should feel like a smart peer asking the right questions, not an intake survey.

---

## Sequence

### Step 1: Start with what they already have

Open with:

> "Before we start from scratch, do you have any existing context you can share? Your website, a pitch deck, a strategy doc, an md file you've been using with Claude or another AI tool, a one-pager, anything. Drop it here or paste the content."

**If they provide something:** Read it carefully. Identify what's already covered (business basics, ICP, sales process, pipeline) and what's missing. Acknowledge what you learned and move to Step 2 only for the gaps.

**If they have nothing:** That's fine. Move to Step 2 and cover everything conversationally.

### Step 2: Fill the gaps

Based on what's missing from Step 1, work through these areas conversationally. Don't ask all of these if some are already answered. Adapt.

**Business basics:**
- What do you sell? Who do you sell it to?
- How do you make money? (Pricing model, deal structure)
- What stage are you at? (Pre-revenue, early, growing, mature)

**ICP definition:**
- Describe your best customer. Not the category, the specific person at the specific company.
- What pain do they feel? What words do they use to describe it?
- What are they doing today instead of using you?
- What do your best customers have in common that your worst customers don't?

**Sales process:**
- How do deals start? (Inbound, outbound, referral, event)
- How long does a deal take from first contact to close?
- What's the typical deal size?
- Who's usually involved in the buying decision?
- Where do deals tend to die?

**Current state:**
- What's working in your sales process right now?
- What feels broken or wasteful?
- Do you have active deals or prospects you're working?

Keep it conversational. If they give a short answer, that's fine. If they want to go deep on something, follow them. The profile doesn't need to be perfect on day one.

### Step 3: Customize the framework

Explain the WORTH dimensions briefly and ask:

> "By default, WORTH treats two dimensions as must-haves: **W** (Worth pursuing, meaning fit) and **R** (Real problem, quantified). If either of these is weak, the deal isn't qualified, no matter how strong the other signals are. The other three dimensions (Owner, Trigger, How we fit) are accelerators that help you prioritize between qualified deals.
>
> Does that default make sense for your situation, or would you move any dimensions between tiers?"

Most people will keep the defaults. If they want to change tiering, discuss why and capture the reasoning.

### Step 4: Write the profile

Draft `config/profile.md` based on everything gathered. Show the draft to the user before saving.

> "Here's your profile based on what you shared. Take a look and tell me if anything needs adjusting."

Save as `config/profile.md` after confirmation.

Then:

> "You're set up. Your profile is saved and every skill in sales-please will use it as context.
>
> You can update it anytime by editing `config/profile.md` directly, or just tell me what changed.
>
> If you have active deals you want to start tracking, we can create deal files for them now. Otherwise, the next time a prospect comes in, start with the gut check: describe who they are and what you know, and I'll help you run the triage."

---

## Principles

- **Don't make it feel like a form.** This is a conversation. Respond to what they share, don't just march through a checklist.
- **Use what they give you.** If they drop a pitch deck, extract everything you can from it before asking questions.
- **Be honest about gaps.** If their ICP description is vague, say so. "That's a category, not a customer. Can you describe a specific company or person who bought from you recently?"
- **Don't over-engineer.** The profile will evolve. Get the foundation right, not every detail.
- **Match their depth.** If they give one-line answers, keep it tight. If they want to talk through their sales challenges, let them. The setup should take 5-15 minutes depending on how much they bring.
