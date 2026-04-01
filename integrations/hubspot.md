# HubSpot Integration

How to map WORTH into HubSpot so your deal scores, stages, and next actions are visible in your CRM without duplicating work.

---

## Custom properties to create

Create these as **Deal properties** in HubSpot (Settings > Properties > Deal properties > Create property).

| Property name | Internal name | Type | Options / format |
|--------------|---------------|------|-----------------|
| WORTH Score | `worth_score` | Number | 0-12 |
| Must-Have Status | `worth_must_haves` | Number | 0-2 |
| WORTH Quality | `worth_quality` | Dropdown | High, Medium, Low, Not qualified |
| WORTH Next Action | `worth_next_action` | Single-line text | Free text |
| WORTH Last Updated | `worth_last_updated` | Date picker | Date |
| W - Worth Pursuing | `worth_w` | Number | 0-3 |
| O - Owner | `worth_o` | Number | 0-3 |
| R - Real Problem | `worth_r` | Number | 0-2 |
| T - Trigger | `worth_t` | Number | 0-2 |
| H - How We Fit | `worth_h` | Number | 0-2 |

**Property group:** Create a group called "WORTH Qualification" and put all properties there. Keeps them organized in the deal sidebar.

---

## Deal stage mapping

Map sales-please stages to your HubSpot pipeline stages. If you're using the default HubSpot pipeline, a reasonable mapping:

| sales-please stage | HubSpot stage |
|-------------------|---------------|
| discovery | Qualified to Buy (or create "Discovery") |
| evaluation | Presentation Scheduled |
| negotiation | Decision Maker Bought-In |
| closed-won | Closed Won |
| closed-lost | Closed Lost |

If your pipeline stages don't match, create custom stages. The names don't matter as long as the mapping is consistent.

---

## Setting up the deal card

Customize your deal card to show WORTH data at a glance:

1. Go to Settings > Objects > Deals > Record customization
2. Add a card section called "WORTH"
3. Add: WORTH Score, WORTH Quality, Must-Have Status, WORTH Next Action
4. Move it near the top so it's visible without scrolling

---

## MCP setup

HubSpot has community-built MCP servers that let Claude read and write deal data. To set this up:

### 1. Get a HubSpot private app token

- Go to Settings > Integrations > Private apps
- Create a new app with these scopes:
  - `crm.objects.deals.read`
  - `crm.objects.deals.write`
  - `crm.objects.contacts.read`
- Copy the access token

### 2. Configure the MCP server

Add the HubSpot MCP server to your Claude Code configuration. The exact setup depends on which MCP server implementation you use. A typical configuration in your Claude Code MCP settings:

```json
{
  "mcpServers": {
    "hubspot": {
      "command": "npx",
      "args": ["-y", "@hubspot/mcp-server"],
      "env": {
        "HUBSPOT_ACCESS_TOKEN": "your-token-here"
      }
    }
  }
}
```

Check the MCP server's documentation for the latest installation method and available tools.

### 3. What Claude can do with HubSpot MCP

Once connected, Claude can:
- Search for deals by company name
- Read WORTH properties from existing deals
- Update WORTH scores after qualification
- Create new deals when a gut check passes
- Pull contact information for stakeholder mapping

### 4. Workflow

The ideal flow:
1. User says "qualify this deal" or "update the deal for [company]"
2. Claude runs the qualification skill using the deal file
3. After scoring, Claude writes the WORTH properties back to HubSpot
4. The CRM stays in sync without manual data entry

---

## Views and reports

Once your properties are set up, create these HubSpot views:

**Active pipeline by WORTH quality:**
- Filter: Deal stage is not closed-won or closed-lost
- Sort by: WORTH Quality (descending), then WORTH Score (descending)
- Columns: Deal name, WORTH Score, Quality, Must-Haves, Next Action, Last Updated

**Stale deals:**
- Filter: WORTH Last Updated is more than 14 days ago AND deal stage is not closed
- Sort by: WORTH Last Updated (ascending)
- This surfaces deals that need attention or disqualification

**Must-have gaps:**
- Filter: Must-Have Status is less than 2 AND deal stage is not closed
- Sort by: WORTH Score (descending)
- These deals have potential but aren't qualified yet

---

## What stays in the deal file

HubSpot holds the summary. The deal file holds everything else:
- Evidence and reasoning behind each score
- Stakeholder decision-role context
- Detailed meeting notes
- Score change history
- The full WORTH checklist with per-item status

Don't try to replicate the deal file in HubSpot. The CRM is the view layer; the deal file is the source of truth.
