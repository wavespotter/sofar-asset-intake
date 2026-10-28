---
name: intake-asset
description: >
  This skill should be used when someone shares a marketing asset — a URL, pasted text,
  or an uploaded file (case study, blog, webinar, one-pager, press release, customer
  story, spec sheet, tool/demo, internal tool, podcast, slide deck, custom deck or
  one-pager made for one customer or meeting, rep-made asset, savings report, etc.) — and wants it filed into Sofar Ocean's Notion databases.
  Trigger on phrases like "add this to the resource library", "catalogue this asset",
  "log this resource", "intake this asset", "add to Notion", "add this case study",
  "capture this testimonial/quote", or "add this stat". The skill catalogues the asset in
  the Resource Library, extracts customer quotes into the Customer Testimonials
  Repository (after confirmation), and surfaces genuinely new featureable statistics into
  the Statistics Repository (conservatively, after confirmation, always under review).
metadata:
  version: "0.11.0"
  author: "Sofar Ocean Marketing"
---

# Sofar Asset Intake

Take one marketing asset and file it into the right Sofar Notion databases:

1. **Resource Library** — always: create one catalogue entry. (Created directly.)
2. **Customer Testimonials Repository** — when the asset has genuine customer quotes:
   extract them, **confirm with the user**, then create one row per approved quote.
3. **Statistics Repository** — only when the asset has a genuinely new, featureable
   statistic: draft a candidate, **confirm with the user**, then create it **as
   "Under review – do not share"**. Conservative by default — most assets add nothing here.
4. **Case Study Coverage Map** (conditional): only for Spotter customer stories. If the case
   study is not already mapped, draft a row, **confirm with the user** (especially Depth and
   Geography), then add it. Dedupe first; most published case studies are already there.

**Prevent duplicates.** Before creating anything in any database, check whether it already
exists and **warn and ask** on a likely match (update / add anyway / skip) — never silently
create over a probable duplicate. The same asset often appears under different URLs (blog,
PDF, Drive link) and the same quote can appear in multiple resources, so matching must be
URL-normalized and fuzzy. Follow `references/deduplication.md` at every write step.

Each database has its own schema and rules. Read the relevant reference file before
classifying:

- `references/deduplication.md` — duplicate detection (applies to all steps below).
- `references/resource-library-schema.md`
- `references/testimonials-repository-schema.md`
- `references/statistics-repository-schema.md`
- `references/coverage-map-schema.md` — Case Study Coverage Map (Spotter customer stories only).

## Step 1 — Load the Notion tools

The Notion connector's tool names carry an instance-specific prefix that differs per
user, so do not hardcode them. Load them by capability with ToolSearch:

```
ToolSearch: "notion fetch query data sources create pages update page"
```

Load at least: a Notion **fetch**, **query-data-sources**, **create-pages**, and
**update-page** tool. If none are found, stop and tell the user the Notion connector must
be connected first (Settings → Connectors).

## Step 2 — Read the asset

- **URL**: fetch and read it. If the page is client-rendered and the fetch returns a
  shell, escalate to the Claude in Chrome tools to get the real text.
- **Pasted text**: use it directly. Ask for the canonical Link if none is given.
- **Uploaded file**: read it from the uploads folder.

Capture the asset's real title, body, author, publication date, and source URL.

## Step 3 — Resource Library entry (dedupe, then create)

Fetch the Resource Library database to confirm the live data-source id and current
options (`https://www.notion.so/sofarocean/1ac8ff95945081eda6d6d0538f2eed87`,
data source `collection://1ac8ff95-9450-815b-b8b4-000b7de5b0a3`).

**Dedupe first (per `references/deduplication.md`).** Query for an existing entry by
normalized URL against both `Link` and `Drive Link`, and by fuzzy `Title` match. If a likely
match exists, **warn and ask** (update existing / add anyway / skip) before doing anything —
do not create blindly. (A title match often catches a duplicate a URL check misses, e.g. when
the asset's PDF is stored under `Drive Link` and the blog URL under `Link`.)

If it's not a duplicate, then following `references/resource-library-schema.md`, fill Title,
Summary, Product, Content Type, Smart Mooring Sensor(s), Use Case Category, Third-Party?
(Yes when the asset is published outside Sofar Ocean's own properties — third-party media,
external blogs, research journals — else No), Source (the publication/outlet/journal name
when Third-Party? = Yes; blank otherwise), Origin, Customer / Prospect (Custom assets
made for a specific account), Link, Last Updated (today, via bash `date +%F`),
the Detailed description (for AI parsing), and Tutorial Videos (only when video links are
given; see the Tool rules below). Create
the entry with the create-pages tool, parent = the Resource Library `data_source_id`.

Before filling the fields, settle two classifications (full rules in
`references/resource-library-schema.md`):

**Origin: Official or Custom.** Origin is about what the asset is for, not what format it is.
Official is the default: reusable assets marketing made or approved for general use. Set
Origin = "Custom" when either is true:
- It is a one-off made for a specific customer, prospect, meeting or deal, **whoever made
  it, marketing included** (e.g. a deck prepared for one prospect meeting).
- A rep, the field team, or anyone outside marketing made it and marketing hasn't reviewed
  it, even if it's meant for reuse.

It can be any format: a deck, a one-pager, a proposal, a custom savings report, a demo
video, a spreadsheet, and so on. Signs include a company name in the title or file name,
"for [Company]" or "prepared for [Company]", a named meeting, "my deck" or "a one-pager I
made", or the user saying a rep made it. For a Custom asset:
- Fill **Customer / Prospect** with the account name whenever it was made for a specific
  customer or prospect. Leave it blank only when it's a general asset the rep made for
  reuse (e.g. a rep's own version of a pitch deck).
- Set **Content Type** to the kind of asset it is, exactly as for an Official one
  (Presentation for a deck, Sales Collateral for a one-pager or spec sheet, Webinar / Video
  for a recording, and so on). Origin never changes the Content Type; there is no "Custom" Content Type.
- Always put the asset's shareable URL (e.g. the Google Slides, Docs or Drive link) in
  **Link**, not only in Drive Link. The library opens Link when someone clicks the card;
  Drive Link only powers the Download button.
- Leave **Publicly Shareable?** empty unless the user explicitly says the asset can go to
  customers. The library treats Custom assets as internal-only unless it's Yes.
- Skip Steps 4, 5 and 6 (Testimonials, Statistics, Coverage Map). The content is one-off or
  hasn't been reviewed by marketing.

Use judgment from the signs above. Ask the user only when the asset could plausibly be
either and nothing points one way, or when it's clearly for one account but you can't tell
which.

**Tool or Interactive Tool / Demo.** Use Content Type "Tool" for internal web utilities that
Sofar staff open and use rather than share (e.g. an email signature generator or a quote
calculator); Tools appear on a separate Tools tab. Use "Interactive Tool / Demo" only for
customer-facing demos, configurators, dashboards and datasets, which stay in the main library.
If a link could be either, ask the user whether it's an internal tool or something customers
see. For a Tool:
- **Link** (the tool's web address) is required.
- **Summary** is required: one or two plain sentences saying what the tool does, because it's
  the description shown on the tool's tile.
- Product, Smart Mooring Sensor(s), Use Case Category and Stage in Buyer's Journey are
  optional. Third-Party? = No.
- **Tutorial Videos** is optional: the training, demo or tutorial videos (e.g. Loom). For one
  video, put just the link. For several, put one per line as `Title: link` (e.g.
  `Pt 1: How to Create: https://www.loom.com/share/...`). The card shows "Watch tutorial" for
  one video and a "Tutorials" menu for several. If the user didn't include any, ask once
  whether there are any. Never invent or search for a video.
- Optionally set the page icon to one fitting emoji; the tile shows it.
- If the tool also has a public, customer-facing version, file that as a separate
  Interactive Tool / Demo entry with its own Link rather than combining them.
- Skip Steps 4, 5 and 6.

## Step 4 — Customer Testimonials (conditional, confirm first)

Skip this step for Custom assets and for Tools.

Per `references/testimonials-repository-schema.md`, decide whether the asset contains
**genuine, attributable customer quotes**. If yes, draft a row per quote (Customer, Name,
Title, verbatim Quotation, Testimonial Summary, Product, Vertical, Source, Publication
Date). **Dedupe each quote first (per `references/deduplication.md`)** — query by a
distinctive verbatim substring of the quote and by Name + Customer; a quote already captured
from a *different* source is still a duplicate. **Present the drafts (and flag any likely
duplicates) for the user's approval**, and only then create the approved, non-duplicate rows
(parent = Testimonials `data_source_id`). Never auto-apply "Do Not Use".

## Step 5 — Statistics (conditional, conservative, confirm first)

Skip this step for Custom assets and for Tools.

Per `references/statistics-repository-schema.md`, decide whether the asset introduces a
**genuinely new, featureable, quantified company/product statistic** (e.g. a cumulative
savings figure, a network metric, a new fuel-savings result). Most assets do not — when
in doubt, add nothing.

If one exists:
1. **Dedupe first.** Query the Statistics data source for similar existing entries
   (by Statistic title and Externally Shareable Description). If a match exists, do **not**
   create a duplicate — tell the user it already exists and offer to update that row instead.
2. Draft a candidate: Statistic (short label), a proposed Externally Shareable Description,
   and Category. Record the asset as the provenance in the
   "[internal only] How Was This Calculated?" field (note that the figure still needs human
   verification).
3. **Confirm with the user**, then create the row **with Status = "Under review – do not
   share"** (parent = Statistics `data_source_id`). **Never** set an "Approved" status —
   approval is a separate human/governance step. Leave internal calculation rigor to a person.

## Step 6 — Case Study Coverage Map (conditional, Spotter customer stories, confirm first)

Only when the Resource Library classification was **Product = Spotter** and **Content Type =
"Customer Story"**. Otherwise skip this step entirely (it never runs for Tools or
Custom assets).

Run it for **every** Spotter customer story so the Coverage Map always reflects the case
study, whether or not it is already listed. Per `references/coverage-map-schema.md`:
1. **Dedupe first.** Query the Coverage Map data source
   (`collection://4b61d3e0-2975-4334-aed4-7366a5dd5b7f`) for an existing row by normalized
   `URL`, and as a backup by `Organization` and fuzzy `Case Study` title.
2. **If no row exists, draft one** (Case Study label, Organization, Use Case Category,
   Geography, Depth, Status, Published date, URL), reusing the Resource Library
   classification where it lines up. **Confirm with the user before creating**, especially
   Depth and Geography, which are judgment calls. Do not set the Marketing Project relation
   or Nominated by.
3. **If a row already exists, do not duplicate. Look for gaps to supplement.** Compare the
   existing row against what the asset provides and find properties that are empty or could
   be improved (for example a missing `URL`, `Geography`, `Depth`, `Published` date, or
   `Organization`). If you find any, propose the specific field updates and, on the user's
   confirmation, update that row. If the row is already complete and accurate, report that
   it is already mapped and make no changes. Never overwrite a human-set value without
   showing the before/after and getting approval.

## Step 7 — Report

Give the user links to everything created: the Resource Library entry, any testimonial
rows, any statistic candidate (noting it's under review), and any Case Study Coverage Map
row (or a note that the case study was already mapped). Add a one-line note on how each was
classified so the user can correct anything. For the Resource Library entry, always say how
Origin was set (Official, or Custom and for which Customer / Prospect, and why), and,
for any tool or demo, whether it was filed as "Tool" (internal) or "Interactive Tool / Demo"
(customer-facing) and why. If later steps were skipped because the asset is Custom or
a Tool, say so.

## Notes

- Databases are referenced by URL/ID (workspace-global, identical for all teammates); only
  the Notion tool names are instance-specific, which is why Step 1 loads them dynamically.
- If a property's options have changed since the reference files were written, trust the
  live schema from the fetch.
- Order of confidence: Resource Library is direct; Testimonials, Statistics, and the Case
  Study Coverage Map are always confirm-first; Statistics is additionally conservative,
  dedupe-aware, and never approved. The Coverage Map step runs only for Spotter customer
  stories, and most published case studies are already mapped.
