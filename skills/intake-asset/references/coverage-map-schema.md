# Case Study Coverage Map — schema & rules (conditional, dedupe-first, confirm-first)

**Database:** Case Study Coverage Map (embedded in the "Spotter Case Study Program" page)
`https://app.notion.com/p/da05048bc0ea4505a133ed3f2ff741d4`
**Data source (parent for new pages):** `collection://4b61d3e0-2975-4334-aed4-7366a5dd5b7f`

This database is a sales-readiness map of Spotter **case studies** (deep customer stories),
categorized by Use Case, Geography, and Depth, and tracked through a pipeline
(Nominated, Survey Sent, Interview Scheduled, In Progress, Customer Review, Published).
It is narrower than the Resource Library: it is only for customer case studies, not every
asset. Always confirm the live option lists by fetching the database first.

## When to act

Only consider this database when the asset is a **Spotter customer story / case study**,
i.e. the Resource Library classification was Product = Spotter and Content Type =
"Customer Story". For anything else (Wayfinder content, articles, brand assets, webinars,
tools), do nothing here.

Most published case studies are already in this map (it was seeded with the existing
library), so expect the dedupe step to find a match more often than not.

## Step order

Run this for every Spotter customer story so the map stays current, whether or not the case
study is already listed.

1. **Dedupe first (per `references/deduplication.md`).** Query the Coverage Map data source
   for an existing row by normalized URL against the `URL` property, and as a backup by
   `Organization` and by fuzzy `Case Study` title.
2. **If no row exists, draft one and confirm before creating.** Depth and Geography are
   judgment calls, so always show the drafted values and let the user adjust before writing.
   Reuse the Resource Library classification where it lines up (Use Case Category).
3. **If a row already exists, supplement it rather than duplicate.** Compare the existing row
   against what the asset provides and look for properties that are empty or could be improved
   (for example a blank `URL`, `Geography`, `Depth`, `Published` date, or `Organization`).
   Propose the specific field updates, and on the user's confirmation update that row. If it
   is already complete and accurate, report that it is already mapped and change nothing.
   Never overwrite an existing human-set value without showing the before/after and getting
   approval; prefer filling blanks over changing populated fields.

## Properties to fill

| Property | Type | Notes |
|---|---|---|
| Case Study | title | Short label, e.g. "HIMB Coral Nursery". |
| Organization | text | The customer org. |
| Use Case Category | select (single) | One primary category (see options). Reuse the Resource Library primary. |
| Geography | select (single) | Infer from the story (see options). |
| Depth | select (single) | Deep / Moderate / Light (see definitions). Confirm with the user. |
| Status | select (single) | For an already-published story, use "Published". |
| Published | date | Publication date. Use `date:Published:start`. |
| URL | url | Canonical URL. Write with the `userDefined:URL` key. |
| Notes | text | Optional one-line context. |

Do **not** set: `Marketing Project` (relation) or `Nominated by` (person). Those are managed
by the case study program owners.

## Write format

- Title field is `Case Study`: `"Case Study": "HIMB Coral Nursery"`.
- Single selects are plain strings (not JSON arrays): `"Geography": "North America"`,
  `"Use Case Category": "Ocean Science & Research"`, `"Depth": "Deep"`, `"Status": "Published"`.
- URL is a reserved name, so write it as `"userDefined:URL": "https://..."`.
- Date: `"date:Published:start": "2026-06-09"`.

## Option lists

- **Use Case Category:** Aquaculture & Fisheries, Coastal Management, Conservation & Marine
  Protection, Government & Defense, Marine Construction, Maritime Tourism & Recreation,
  Ocean Science & Research, Offshore Renewables, Oil & Gas, Ports & Harbors,
  Shipping & Logistics.
- **Geography:** Australia & New Zealand, Europe, North America, South America, Asia,
  Pacific Islands, Africa, Middle East, Global.
- **Depth:** Deep, Moderate, Light.
- **Status:** Nominated, Survey Sent, Interview Scheduled, In Progress, Customer Review,
  Published.

## Depth definitions (from the program page)

- **Deep:** Narrative-driven, multiple customer quotes, tells a full story. Can stand alone
  as a sales asset.
- **Moderate:** Has some customer perspective and useful detail, but does not tell a
  complete story. Useful as supporting material.
- **Light:** Mostly product-focused or announcement-style. Minimal customer voice. Not
  really usable as a sales tool today.

Propose a Depth based on these definitions, but treat it as a suggestion for the user to
confirm. It is a subjective sales-readiness judgment.
