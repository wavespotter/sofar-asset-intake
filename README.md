# Sofar Asset Intake plugin

Drop in a marketing asset — a URL, pasted text, or an uploaded file — and Sofar Asset
Intake files it into the right Sofar Ocean Notion databases, with the right level of
confirmation for each.

## What it does

Give Claude an asset and say something like "add this to the resource library" or "intake
this asset." The skill will:

1. **Catalogue it in the Resource Library** (directly) — Title, Summary, Product, Content
   Type, Smart Mooring Sensor(s), Use Case Category, Link, Last Updated, and the AI
   detailed-description field.
2. **Capture customer testimonials** — if the asset contains genuine customer quotes, it
   drafts a row per quote and **shows them to you for approval** before adding them to the
   Customer Testimonials Repository.
3. **Surface new statistics** — only when the asset introduces a genuinely new, featureable
   figure, it drafts a candidate, **dedupe-checks** the Statistics Repository, **confirms
   with you**, and creates the row **as "Under review – do not share."** It never approves a
   stat — that stays a human governance decision. Most assets add nothing here.
4. **Map Spotter case studies** — for every Spotter customer story, it dedupe-checks the
   Case Study Coverage Map. If the story is not there yet, it drafts a row and **confirms
   with you** (especially Depth and Geography) before adding it. If it is already mapped, it
   looks for empty or improvable fields and **proposes filling those in** (never overwriting
   a human-set value without asking).

## Components

| Component | Purpose |
|---|---|
| Skill: `intake-asset` | End-to-end intake workflow plus four reference schemas (Resource Library, Testimonials, Statistics, Case Study Coverage Map). |

No bundled MCP server — the skill uses your connected **Notion** connector.

## Setup

- Connect the **Notion** connector (Settings → Connectors) with access to the Sofar
  workspace. The skill loads Notion tools dynamically, so it works regardless of which
  Notion account each teammate connects, as long as it can reach:
  - 📚 Resource Library
  - ⭐ Customer Testimonials Repository
  - 📈 Sofar Ocean Statistics Repository
  - 🗺️ Case Study Coverage Map (in the Spotter Case Study Program page; Spotter customer stories only)

## Usage

Trigger phrases include: "add this to the resource library", "intake this asset",
"catalogue this asset", "add this case study", "capture this quote", "add this stat".
Provide a URL, paste the text, or upload the file.

Confidence levels by destination:
- **Resource Library** — dedupe-checked, then created.
- **Testimonials** — always shown for your approval first; "Do Not Use" never auto-applied.
- **Statistics** — conservative, confirmed first, always created **under review** (never approved).
- **Case Study Coverage Map** — Spotter customer stories only; dedupe-checked, then confirmed before adding.

**Duplicate prevention (all three).** Before any write, the skill checks for an existing
match and **warns and asks** (update / add anyway / skip) rather than silently duplicating.
Matching is URL-normalized (strips tracking params; checks both Link and Drive Link), fuzzy
on titles, and based on verbatim quote text for testimonials — so the same asset under a
different URL, or the same quote from a different resource, is still caught. See
`references/deduplication.md`.

## Notes

- All classification rules and the three database schemas live in the skill's `references/`
  files.
- The skill confirms each live database schema at runtime, so it stays correct if options
  change.
- Replaces the earlier `sofar-resource-library` plugin (renamed to reflect that it now feeds
  multiple Notion databases).
