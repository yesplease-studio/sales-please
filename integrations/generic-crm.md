# Generic CRM Integration

Principles for mapping WORTH to any CRM. If your CRM isn't HubSpot or Attio, this guide covers what to set up, what to track, and what to skip.

---

## The six fields that matter

Every CRM integration needs these six custom fields on your deal/opportunity object:

| Field | Type | Values |
|-------|------|--------|
| **WORTH Score** | Number | 0-12 |
| **Must-Have Status** | Number | 0-2 |
| **Quality Tier** | Picklist / dropdown | High, Medium, Low, Not qualified |
| **Next Action** | Text | Free text, one sentence |
| **Stage** | Picklist / dropdown | discovery, evaluation, negotiation, closed-won, closed-lost |
| **Last WORTH Update** | Date | When the deal was last scored |

That's the minimum. If your CRM supports it, add per-dimension scores:

| Field | Type | Values |
|-------|------|--------|
| W - Worth Pursuing | Number | 0-3 |
| O - Owner | Number | 0-3 |
| R - Real Problem | Number | 0-2 |
| T - Trigger | Number | 0-2 |
| H - How We Fit | Number | 0-2 |

Per-dimension scores let you filter your pipeline by specific gaps (e.g., "show me all deals where O is 0" to find deals with no identified decision-maker).

---

## What to track in the CRM

**Track:**
- WORTH scores and quality tier (the summary)
- Deal stage
- Next action (so it shows up in your CRM task list or dashboard)
- Last update date (so you can spot stale deals)
- Company and contact associations (your CRM already does this)

**Don't track:**
- Evidence or reasoning behind scores. That's in the deal file.
- Stakeholder decision-role mapping. Most CRMs model contacts by job title, not by buying role. The deal file handles this better.
- Meeting notes substance. Log that a meeting happened; keep the content in the deal file.
- Score change history. The deal file's notes section captures this chronologically.

The rule: if you'd need to read it to make a qualification decision, it belongs in the deal file. If you'd need to see it on a dashboard, it belongs in the CRM.

---

## Stage mapping

Map the five sales-please stages to your CRM's pipeline stages. Most CRMs let you customize stages. Create a clean mapping:

| sales-please | Your CRM equivalent |
|-------------|---------------------|
| discovery | Your first active stage |
| evaluation | Mid-pipeline (prospect is actively comparing options) |
| negotiation | Late-stage (terms, pricing, contracts) |
| closed-won | Won |
| closed-lost | Lost |

If your CRM has more stages (like "Appointment Scheduled" or "Proposal Sent"), decide which sales-please stage each maps to. Keep it simple. More stages doesn't mean more clarity.

---

## Connecting Claude via MCP

If your CRM has an API, you can connect it to Claude via MCP (Model Context Protocol). This lets Claude read deal data from the CRM and write WORTH scores back after qualification.

### What you need

1. **API access** to your CRM with read/write permissions on deals/opportunities and contacts
2. **An MCP server** that wraps your CRM's API. Check if one exists for your CRM, or build a simple one using the MCP SDK.
3. **Claude Code MCP configuration** pointing to the server

### If no MCP server exists for your CRM

You have two options:

**Option A: Manual sync.** Run qualification in Claude, update the CRM yourself. This works fine for small pipelines (under 20 active deals). The deal file is the source of truth; the CRM is updated when you have a moment.

**Option B: Build a simple MCP server.** If your CRM has a REST API, an MCP server that supports `search_deals`, `read_deal`, `update_deal`, and `create_deal` operations covers everything sales-please needs. The MCP SDK makes this straightforward.

Don't over-invest here. The integration is a convenience, not a requirement.

---

## Views to create

Regardless of CRM, set up these three views:

### 1. Active pipeline by quality
- Filter: Stage is active (not closed)
- Sort: Quality tier descending, then WORTH score descending
- Shows your best deals at the top

### 2. Stale deals
- Filter: Last WORTH update > 14 days ago AND stage is active
- Sort: Last WORTH update ascending
- Surfaces deals that need a debrief or a disqualification decision

### 3. Must-have gaps
- Filter: Must-Have Status < 2 AND stage is active
- Sort: WORTH Score descending
- These deals score well on accelerators but aren't truly qualified. Either close the must-have gaps or move on.

---

## Common CRM-specific notes

**Salesforce:** Use custom fields on the Opportunity object. Consider a custom "WORTH" field set for organization. The Salesforce MCP ecosystem is relatively mature.

**Pipedrive:** Custom fields on Deals. Pipedrive's API is straightforward and community MCP servers exist.

**Close:** Custom fields on Opportunities. Close's API is clean and well-documented.

**Notion databases:** If you're using Notion as a lightweight CRM, add WORTH properties to your deals database. Notion has MCP server support.

**Spreadsheets:** If your "CRM" is a Google Sheet or Airtable, add WORTH columns. This works. Don't overthink it.

---

## The honest version

If you have fewer than 20 active deals at any time, you probably don't need a CRM integration. Your `deals/` directory and Claude are enough. Add a CRM when:

- You have multiple people who need to see the pipeline
- You need reporting that goes beyond "read the deal files"
- You're integrating with other tools (email sequences, call logging) that feed into the CRM
- Your deal volume makes manual sync genuinely painful

Until then, keep it simple.
