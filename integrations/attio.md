# Attio Integration

How to map WORTH into Attio so your deal scores and pipeline are visible alongside your relationship data.

Attio's flexible data model makes this straightforward. You're adding attributes to your Deals object (or whatever you've named your pipeline object).

---

## Attributes to create

Add these as attributes on your **Deals** object (or create a Deals object if you don't have one).

| Attribute name | Type | Options / format |
|---------------|------|-----------------|
| WORTH Score | Number | 0-12 |
| Must-Have Status | Number | 0-2 |
| WORTH Quality | Status | High, Medium, Low, Not qualified |
| WORTH Next Action | Text | Free text |
| WORTH Last Updated | Date | Date |
| W - Worth Pursuing | Number | 0-3 |
| O - Owner | Number | 0-3 |
| R - Real Problem | Number | 0-2 |
| T - Trigger | Number | 0-2 |
| H - How We Fit | Number | 0-2 |

**Tip:** Attio lets you group attributes. Create a "WORTH" group to keep these together in the record view.

---

## Stage mapping

Map sales-please stages to your Attio pipeline stages:

| sales-please stage | Attio stage |
|-------------------|-------------|
| discovery | Discovery |
| evaluation | Evaluation |
| negotiation | Negotiation |
| closed-won | Won |
| closed-lost | Lost |

Attio pipelines are flexible. Name the stages whatever makes sense. Just keep the mapping consistent between your deal files and Attio.

---

## Record layout

Customize your deal record layout to surface WORTH data:

1. Open any deal record
2. Click "Customize layout"
3. Add a section called "WORTH Qualification"
4. Add: WORTH Score, WORTH Quality, Must-Have Status, WORTH Next Action
5. Position it prominently so you see it when opening any deal

---

## MCP setup

Attio has an official API and community MCP servers are available. To connect Claude:

### 1. Get an Attio API key

- Go to Settings > Developers > API keys
- Create a new key with read/write access to your workspace
- Copy the key

### 2. Configure the MCP server

Add the Attio MCP server to your Claude Code configuration:

```json
{
  "mcpServers": {
    "attio": {
      "command": "npx",
      "args": ["-y", "@attio/mcp-server"],
      "env": {
        "ATTIO_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

Check the MCP server's documentation for the latest installation method. The Attio API is well-documented and most MCP implementations support reading and writing records, lists, and attributes.

### 3. What Claude can do with Attio MCP

Once connected:
- Search for companies and deals
- Read WORTH attributes from existing deal records
- Update scores and quality tiers after qualification
- Create new deal records when a prospect qualifies
- Pull relationship data (people, companies, interactions) for context

### 4. Workflow

Same as any CRM integration:
1. Qualify or debrief a deal using the sales-please skills
2. Claude writes the updated WORTH data back to Attio
3. Your Attio pipeline view stays current without manual entry

---

## Views to create

**Pipeline by WORTH quality:**
- Filter: Stage is not Won or Lost
- Sort by: WORTH Quality, then WORTH Score
- Columns: Company, WORTH Score, Quality, Must-Haves, Next Action, Last Updated

**Needs attention:**
- Filter: WORTH Last Updated is more than 14 days ago AND stage is active
- Sort by: WORTH Last Updated ascending
- Surfaces stale deals that need a debrief or disqualification

**Unqualified pipeline:**
- Filter: Must-Have Status < 2 AND stage is active
- These deals have open must-have gaps. Either close the gaps or move them out.

---

## What stays in the deal file

Attio holds the scores and stage. The deal file holds:
- Evidence behind each checklist item
- Stakeholder roles and decision dynamics
- Detailed notes and conversation history
- Score change history across debriefs
- The full 12-item checklist

The CRM is where you glance at the pipeline. The deal file is where you think about the deal.
