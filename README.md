# B2B Lead Qualification & Routing Workflow

An N8N automation that researches inbound B2B leads, scores them against a fit model, and routes them to the right person by market — built to remove manual research and triage work from the top of the sales funnel.

## What it does

1. **Trigger** — new lead submission lands in a Google Sheet (via a lead capture form).
2. **Research** — an AI-powered search step pulls open, public information about the company (industry, size, recent activity).
3. **Scoring** — an LLM scores the lead from 0–100 based on four weighted factors:
   - Company size fit — up to 30 points
   - Industry fit — up to 20 points
   - Growth / funding signals — up to 25 points
   - Revenue signals — up to 25 points
4. **Segmentation** — leads are categorized based on total score:
   - 70+ → **Hot**
   - 40–69 → **Warm**
   - Below 40 → **Cold**
5. **Routing** — each lead is logged to a tracking sheet and a notification is sent to the relevant person, based on category and market.

## Why I built this

Sales and RevOps teams often lose time doing manual background research on every inbound lead before deciding whether it's worth a response — and high-intent leads can sit in a queue behind low-relevance ones simply because nobody has triaged the list yet. This workflow automates that first pass, so a human only spends time on leads that have already been qualified, and hot leads get flagged for action immediately rather than waiting in a shared inbox.

## Current integrations

- **Google Sheets** — lead intake and score tracking
- **Gmail** — notification on new hot/warm/cold leads
- **Tavily** — web search for company research
- **Google Gemini** — LLM for research synthesis and scoring

## Possible extensions

- Swap the notification step for a direct **HubSpot** (or other CRM) integration, so qualified leads land straight into a rep's pipeline as a new deal instead of an email notification.
- Add a "request urgency" field to the lead capture form itself, and factor it into scoring — so leads that explicitly indicate urgency aren't buried under a larger volume of lower-priority submissions.
- Add deduplication logic to avoid re-scoring a lead that's already been researched.

## Setup

1. Import `b2b-lead-qualification-workflow.json` into your N8N instance.
2. Replace the placeholder values (`YOUR_CREDENTIAL_ID`, `YOUR_GOOGLE_SHEET_ID`, `your-email@example.com`) with your own credentials, sheet, and notification address.
3. Connect your own Google Sheets, Gmail, Tavily, and Gemini credentials in N8N.
4. Adjust the scoring prompt in the "Basic LLM Chain" node to match your own product/ICP fit criteria.

## Tech stack

N8N · Google Gemini (LLM) · Tavily (web search) · Google Sheets · Gmail

---

Built by [Fluwormie](https://github.com/weiying1014) — e-commerce operations professional exploring automation and RevOps workflows.
