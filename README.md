# Sofar Asset Intake plugin

Drop in a marketing asset — a URL, pasted text, or an uploaded file — and Sofar Asset
Intake files it into the right Sofar Ocean Notion databases, with the right level of
confirmation for each.

## What it does

Give Claude an asset and say something like "add this to the resource library" or "intake
this asset." The skill will:

1. **Catalogue it in the Resource Library** (directly) — Title, Summary, Product, Content
   Type, Smart Mooring Sensor(s), Use Case Category, Link, Last Updated, and the AI
   detailed-description field. It also sets **Origin**: Official for anything marketing
   made or approved for general use, or Custom (with the Customer / Prospect) for one-off
   assets made for a specific customer or meeting, and for anything a rep made on their own.
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
5. **List third-party research on the Academic publications page.** For research papers
   published outside Sofar (Content Type Whitepaper / Research, Third-Party? = Yes), it
   checks the "Academic publications featuring Sofar / Spotter" page and, if the paper isn't
   already listed, adds it under the right year and publication in the page's existing
   format. It never edits existing entries. Research entries also get a **Sofar Reference**
   tag (Central, Passing or None) saying how much the paper references Sofar's products.
6. **Save research PDFs to Drive.** When a research paper comes as a PDF, or exists only as
   a PDF, it saves the file to Sofar Marketing / Resource Library / Research papers in
   Google Drive (through your synced Drive folder when it can reach your computer, or with
   step-by-step upload instructions when it can't) and links it from the library entry.

## Finding assets (find-resource)

Ask Claude something like "do we have any papers on Spotter's barometer accuracy?",
"is there a case study for ports in Europe?" or "what can I send a customer about Smart
Mooring?" The `find-resource` skill:

1. Searches the **Resource Library first**, then the Statistics, Testimonials and Case
   Study Coverage Map databases, then wider Notion and Drive, then the web.
2. Checks each result against the actual question (right product, sensor, metric) and
   says so when it only partly fits.
3. **Labels every result:** OK to share with customers, share the public link only,
   partners only, internal only, or do not use. Research also shows the venue, whether
   it is peer reviewed, its Sofar Reference, and any caveat for reps.
4. Says plainly what was not found, and offers to file anything useful that isn't in the
   library yet (through intake, only if you say yes).

It is read-only: it never changes Notion or Drive. Results depend on your own Notion and
Drive access.

## Components

| Component | Purpose |
|---|---|
| Skill: `intake-asset` | End-to-end intake workflow plus reference files for the Resource Library, Testimonials, Statistics, the Case Study Coverage Map, the Academic publications page, and research PDFs in Drive. |
| Skill: `find-resource` | Read-only search across the Resource Library, governed repositories, wider Notion and Drive, and the web, with a sharing label on every result. Reference: `sources-and-labels.md`. |

No bundled MCP server — the skill uses your connected **Notion** connector.

## Setup

- Connect the **Notion** connector (Settings → Connectors) with access to the Sofar
  workspace. The skill loads Notion tools dynamically, so it works regardless of which
  Notion account each teammate connects, as long as it can reach:
  - 📚 Resource Library
  - ⭐ Customer Testimonials Repository
  - 📈 Sofar Ocean Statistics Repository
  - 🗺️ Case Study Coverage Map (in the Spotter Case Study Program page; Spotter customer stories only)
  - 📚 Academic publications featuring Sofar / Spotter (a page in Marketing Team; third-party research only)
- For research PDFs: the **Google Drive** connector, and ideally Google Drive for desktop
  signed in with your Sofar account so the Sofar Marketing shared drive syncs to your
  computer. Without it, the skill gives you the folder link and upload steps instead:
  https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2

## Usage

Trigger phrases include: "add this to the resource library", "intake this asset",
"catalogue this asset", "add this case study", "capture this quote", "add this stat".
Provide a URL, paste the text, or upload the file.

Confidence levels by destination:
- **Resource Library** — dedupe-checked, then created.
- **Testimonials** — always shown for your approval first; "Do Not Use" never auto-applied.
- **Statistics** — conservative, confirmed first, always created **under review** (never approved).
- **Case Study Coverage Map** — Spotter customer stories only; dedupe-checked, then confirmed before adding.
- **Academic publications page:** third-party research only; dedupe-checked, then added directly if not already listed.
- **Research PDFs:** saved to the Research papers folder only when you provide a PDF or the paper has no public link.

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
