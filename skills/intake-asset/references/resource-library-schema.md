# Resource Library — schema & classification rules

**Database:** 📚 Resource Library — `https://www.notion.so/sofarocean/1ac8ff95945081eda6d6d0538f2eed87`
**Data source (parent for new pages):** `collection://1ac8ff95-9450-815b-b8b4-000b7de5b0a3`

Always confirm the live option lists by fetching the database first; the values below are
the intended set, but the live schema wins if they differ.

## Properties to fill

| Property | Type | Notes |
|---|---|---|
| Title | title | The asset's real headline. |
| Summary | rich_text | One short, factual sentence in house style. |
| Product | multi_select | Spotter and/or Wayfinder. |
| Content Type | select | Exactly one of the 11 values below. |
| Smart Mooring Sensor(s) | multi_select | Sensors named; see rule. |
| Use Case Category | multi_select | 1–3 primary, or empty for horizontal assets. |
| Third-Party? | select | "Yes" or "No" — classify by publication venue; see rule. |
| Source | rich_text | Publication/outlet/journal name when Third-Party? = Yes; see rule. |
| Link | url | Canonical URL. |
| Last Updated | date | Today's date (`date +%F`), set `date:Last Updated:start`. |
| Detailed description (for AI parsing) | rich_text | Structured block (see format). |

Do **not** set: `Partners Only?` (checkbox, governance), `Publicly Shareable?`,
`New Hire?`, `Partner`, `Featured On`, `Stage in Buyer's Journey`, `Spotter Solution`,
`Drive Link` — unless the user explicitly asks. These are managed by people/other flows.

## Write format

- Multi-selects are JSON-array strings, e.g. `"Product": "[\"Spotter\"]"`,
  `"Use Case Category": "[\"Offshore Renewables\",\"Coastal Management\"]"`.
- Select is a plain string, e.g. `"Content Type": "Customer Story"`.
- Date uses the expanded key: `"date:Last Updated:start": "2026-06-17"`.

## Product (multi_select)

Options: **Spotter**, **Wayfinder**.
- **Spotter** = ocean sensing, buoys, Smart Mooring, subsurface/metocean data. Smart
  Mooring and Bristlemouth content roll up under Spotter.
- **Wayfinder** = voyage optimization, routing, fuel savings, shipping operations.
- Can be both, or neither (some brand/company assets have no product).

## Content Type (select) — 11 values + disambiguation

`Article`, `Customer Story`, `Webinar / Video`, `Sales Collateral`,
`Whitepaper / Research`, `Webpage / FAQ`, `Interactive Tool / Demo`, `Presentation`,
`Enablement`, `Creative / Brand Asset`, `Other`.

- **Article** — blog posts, news, press releases, announcements.
- **Customer Story** — case studies / customer success stories.
- **Webinar / Video** — webinars, recorded talks, videos, podcasts.
- **Sales Collateral** — one-pagers, spec sheets, booklets, media kits.
- **Whitepaper / Research** — academic papers, scientific studies, technical evaluations.
- **Webpage / FAQ** — product webpages, FAQs, guides.
- **Interactive Tool / Demo** — tools, dashboards, demos, configurators, calculators,
  scenario builders, web apps, live dashboards, data archives/repositories.
- **Presentation** — slide decks.
- **Enablement** — internal or partner enablement / sales-training / onboarding material.
- **Creative / Brand Asset** — photo/video directories, logos, brand books, renderings,
  design files.
- **Other** — only when nothing above fits.

## Smart Mooring Sensor(s) (multi_select)

Options: Dissolved Oxygen, Current, Hydrophone, Pressure, Temperature, None,
Bristlemouth (custom), Salinity, pH.

Rules:
- Tag the sensors the content actually discusses (e.g. a current meter → Current; a
  custom integrated payload like an oil-spill monitor → Bristlemouth (custom)).
- Surface waves/wind are **not** Smart Mooring sensors — do not tag a sensor for those alone.
- Mentioning a *future*/planned sensor is not the same as the asset being about it — tag
  only sensors the asset is actually about.
- **Leave blank** when the asset has nothing to do with subsurface sensing (Wayfinder /
  shipping content, brand assets).
- Use **"None"** only when the asset *is* Spotter/Smart Mooring content but deliberately
  covers no subsurface sensor (e.g. surface-only wave data). Blank = not applicable;
  "None" = considered, genuinely no sensor.

## Use Case Category (multi_select) — 11 categories

`Aquaculture & Fisheries`, `Coastal Management`, `Conservation & Marine Protection`,
`Government & Defense`, `Marine Construction`, `Maritime Tourism & Recreation`,
`Ocean Science & Research`, `Offshore Renewables`, `Oil & Gas`, `Ports & Harbors`,
`Shipping & Logistics`.

Rules:
- Pick **1–3 genuinely primary** categories (max 4). Quality over quantity.
- **Horizontal assets → leave empty**: general platform/company overviews, brand assets,
  internal tools/demos/configurators/repositories not tied to a specific industry.
- Wayfinder / voyage / fuel / routing content → **Shipping & Logistics**.
- Customer stories and research papers almost always map to at least one category.
- Disambiguation: research/academic/data/climate/oceanography → **Ocean Science &
  Research**; habitat/MPA/biodiversity/coral/species → **Conservation & Marine
  Protection**; storm surge / sea level / shoreline / flood / coastal engineering →
  **Coastal Management**.

## Third-Party? (select) and Source (rich_text)

Third-Party? options: **Yes**, **No**. Classify by **where the asset is published**, not
who it is about:

- **Yes** — published somewhere other than Sofar Ocean's own properties: third-party
  publications and media articles, blog posts on websites that are not Sofar Ocean's, and
  research papers / scientific-journal articles not published by Sofar.
- **No** — published by Sofar Ocean itself: sofarocean.com pages and blog posts,
  Sofar-produced collateral, webinars, presentations, tools, and brand assets.
- Always set one of the two. If the venue is genuinely unclear (e.g. an uploaded file with
  no provenance), ask the user instead of guessing.

Source:

- When Third-Party? = **Yes**, set Source to the name of the publication, media outlet, or
  journal — the venue, not the author (e.g. "ECO Magazine", "Nature Communications",
  "gCaptain").
- When Third-Party? = **No**, leave Source blank.

Write format: both are plain strings, e.g. `"Third-Party?": "Yes"`,
`"Source": "ECO Magazine"`.

## Summary (style)

One factual sentence, kept slightly on the short side. Example:
"Customer story on how Chile's Skyring Marine scaled from one Spotter to a six-buoy fleet
delivering real-time wave and current data for tanker mooring decisions at exposed oil
terminals."

## Detailed description (for AI parsing) — format

```
### Extended Description of Content

Introduction
<1–3 sentences framing the asset, with author/date if known>

Key Themes
- <Theme>: <short explanation>
- ...

Detailed Analysis
- <Point>: <detail>
- ...

Conclusion
<1–2 sentence wrap-up of significance>
```
