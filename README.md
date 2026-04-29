<img width="1584" height="396" alt="Github-sales-please" src="https://github.com/user-attachments/assets/4f031495-9a63-464b-9a85-b1d25805f7cd" />

# sales-please

A lightweight, AI-native sales qualification framework for founders and small teams. Built on **WORTH**, a five-dimension alternative to MEDDPICC designed for people who sell but don't have a sales background.

## What this is

sales-please gives you a structured way to decide which deals deserve your time. You fork this repo, open Claude Code, and start qualifying deals immediately. No CRM required. No sales methodology certification. No pipeline dashboards.

Your deal files are your CRM. The WORTH framework is your thinking tool. Claude is your qualification partner.

## Who this is for

- Founders doing their own sales
- Small teams without a dedicated sales function
- Anyone who has more prospects than hours and needs a system for prioritizing

If you have a VP of Sales and 20 AEs, this isn't for you. Use MEDDPICC.

## The WORTH framework

Five dimensions, two tiers:

| Dimension | Question | Default tier |
|-----------|----------|-------------|
| **W** — Worth pursuing | Does this prospect fit your ICP? | Must-have |
| **O** — Owner of the decision | Do you know who decides, and can you reach them? | Accelerator |
| **R** — Real problem, quantified | Can they describe the pain and its cost? | Must-have |
| **T** — Trigger and timeline | Is something forcing a decision? | Accelerator |
| **H** — How we fit | Does your solution match their specific problem? | Accelerator |

Deals are scored against a 12-item checklist. Must-haves gate qualification. Accelerators help you prioritize between qualified deals.

Full framework definition: [`framework/SYSTEM.md`](framework/SYSTEM.md)

## Quickstart

1. **Fork this repo** (or clone it)
2. **Open Claude Code** in the repo directory
3. **Start talking.** Claude will detect that you haven't set up yet and walk you through a short onboarding conversation to create your company profile.
4. **Qualify your first deal.** Describe a prospect or paste meeting notes, and Claude will run the WORTH qualification.

That's it. No configuration files to edit manually, no dependencies to install.

## Structure

```
sales-please/
├── CLAUDE.md              # Operating instructions for Claude
├── SETUP.md               # Onboarding flow definition
├── framework/
│   ├── SYSTEM.md          # WORTH framework (dimensions, tiering, philosophy)
│   ├── SCORECARD.md       # Deal Quality Checklist (12 items, thresholds)
│   └── GUT-CHECK.md       # 30-second pre-call triage
├── skills/
│   ├── gut-check/         # Pre-call triage (go/no-go)
│   ├── deal-qualify/      # Post-discovery scoring and deal file creation
│   ├── deal-debrief/      # Post-meeting deal update and re-scoring
│   ├── pipeline-review/   # Weekly pipeline review and prioritization
│   └── meeting-prep/      # Pre-meeting brief with WORTH gap analysis
├── deals/
│   └── _template.md       # Deal file template
├── config/
│   └── _template.md       # Company profile template (setup creates profile.md)
└── integrations/
    ├── GUIDE.md            # Integration philosophy and options
    ├── hubspot.md          # HubSpot property mapping + MCP setup
    ├── attio.md            # Attio property mapping + MCP setup
    └── generic-crm.md     # Principles for mapping WORTH to any CRM
```

## Three speeds

| Speed | When | Time |
|-------|------|------|
| **Gut Check** | Before booking a call | 30 seconds |
| **Deal Qualification** | After a discovery call | 5-10 minutes |
| **Pipeline Review** | Weekly | 15-20 minutes |

## The "-please" family

Open-source, AI-native tools for strategic and product work by [Yes Please Studio](https://yesplease.studio):

| Tool | What it does |
|------|-------------|
| **[strategy-please](https://github.com/yesplease-studio/strategy-please)** | Maps challenges to the right workshop using a strategic maturity framework |
| **[prd-please](https://github.com/yesplease-studio/prd-please)** | Structured methodology for AI-native product requirements |
| **sales-please** (this repo) | Lightweight deal qualification framework built on WORTH |
| **[voice-please](https://github.com/yesplease-studio/voice-please)** | Defines, encodes, and maintains a company's voice and language system |
| **[design-please](https://github.com/yesplease-studio/design-please)** | Scopes design direction and encodes it for Claude Design or designer handoff |
| **[name-please](https://github.com/yesplease-studio/name-please)** | Validates and generates company and product names grounded in ICP and voice context |
| **[messaging-please](https://github.com/yesplease-studio/messaging-please)** | Builds messaging architecture -- purpose, positioning, and per-audience message matrix |

Each tool works standalone. Fork it, open Claude Code, start working.

## License

Apache 2.0
