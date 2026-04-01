# Integrations

sales-please works without a CRM. Your `deals/` directory is your pipeline. Claude is your interface. That's the whole system.

But if you already use a CRM, or if your pipeline grows to the point where you want one, these guides show you how to bridge WORTH into your existing tools without creating a second source of truth.

---

## Philosophy

**CRM integration is a bridge, not a dependency.** sales-please never requires an external tool. The integration layer connects your deal files to a CRM so you can keep both in sync, but the framework, the scoring, and the qualification logic all live here.

**Light-touch mapping.** You're mapping five dimensions and a score into CRM properties. That's it. Don't try to replicate the entire deal file in your CRM. The CRM holds the summary; the deal file holds the detail.

**Claude reads and writes via MCP.** If your CRM has an MCP server (or you build one), Claude can read deal data from the CRM and write WORTH scores back. This is the ideal setup: qualify in conversation, sync to the CRM automatically.

**"Here's what to set up" over automated provisioning.** These guides tell you which properties to create and how to map them. They don't run scripts against your CRM or auto-create fields. You set it up once, and then the mapping just works.

---

## What to map

Every CRM integration maps the same core data:

| WORTH concept | CRM field type | What it captures |
|---------------|---------------|-----------------|
| WORTH score | Number (0-12) | Overall deal quality |
| Must-have status | Number (0-2) | Whether W and R are strong |
| Quality tier | Dropdown (High/Medium/Low/Not qualified) | Scoring threshold result |
| Stage | Dropdown | discovery / evaluation / negotiation / closed-won / closed-lost |
| Next action | Text | The single most important next step |
| Last WORTH update | Date | When the deal was last scored |

That's six fields. Some CRMs let you add per-dimension scores (W, O, R, T, H individually), which is useful for filtering and reporting. The per-CRM guides below cover this.

---

## What not to map

- **Evidence and reasoning.** The "why" behind each score lives in the deal file. Don't try to cram it into CRM notes fields.
- **Stakeholder details.** CRM contact records handle people. The deal file's stakeholder section captures decision-role context that most CRMs don't model well. Keep it in the deal file.
- **Meeting notes.** Your CRM might have an activity log. Use it for logging that a meeting happened. The substance goes in the deal file's notes section.

---

## Available guides

| CRM | Guide | Status |
|-----|-------|--------|
| HubSpot | [hubspot.md](hubspot.md) | Ready |
| Attio | [attio.md](attio.md) | Ready |
| Any CRM | [generic-crm.md](generic-crm.md) | Ready |

If your CRM isn't listed, start with the generic guide. The principles are the same everywhere.

---

## MCP setup (general)

MCP (Model Context Protocol) lets Claude read from and write to external tools. If your CRM has an MCP server, Claude can:

1. **Read:** Pull deal data from the CRM when qualifying or reviewing deals.
2. **Write:** Push WORTH scores and stage updates back to the CRM after qualification.
3. **Sync:** Keep deal files and CRM records in sync without manual data entry.

The per-CRM guides include MCP configuration where available. If your CRM doesn't have an MCP server yet, you can still use sales-please fully. Just update your CRM manually after qualification sessions, or build a simple MCP server that bridges the gap.
