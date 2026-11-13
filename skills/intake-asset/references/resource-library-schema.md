# Resource Library — schema & classification rules

**Database:** 📚 Resource Library — `https://www.notion.so/sofarocean/1ac8ff95945081eda6d6d0538f2eed87`
**Data source (parent for new pages):** `collection://1ac8ff95-9450-815b-b8b4-000b7de5b0a3`

Always confirm the live option lists by fetching the database first; the values below are
the intended set, but the live schema wins if they differ.

## Properties to fill

| Property | Type | Notes |
|---|---|---|
| Title | title | The asset's real headline. |
| Summary | rich_text | One short, factual sentence in house style. Required for a Tool (shown on its tile); see "Internal tools". |
| Product | multi_select | Spotter and/or Wayfinder. |
| Content Type | select | Exactly one of the 14 values below. |
| Smart Mooring Sensor(s) | multi_select | Sensors named; see rule. |
| Use Case Category | multi_select | Up to 5, only for buyers the asset speaks to directly, or empty for horizontal assets. |
| Topic | multi_select | Up to 3 main subjects, or empty. See "Topic". |
| Website status | select | Only Not on hub, and only in the cases listed under "Website status". Otherwise leave blank. |
| Third-Party? | select | "Yes" or "No" — classify by publication venue; see rule. |
| Source | rich_text | Publication/outlet/journal name when Third-Party? = Yes; see rule. |
| Origin | select | "Official" (default) or "Custom"; see "Origin and Customer / Prospect". |
| Customer / Prospect | rich_text | Account name. Only for Custom assets made for a specific customer or prospect. |
| Sofar Reference | select | Research papers only: Central, Passing or None. See "Sofar Reference". Leave blank for every other Content Type. |
| Link | url | Canonical URL. For a Custom asset, its shareable Slides/Docs/Drive URL; for a Tool, its web address (required). |
| Last Updated | date | Publication date for dated assets; intake date for living docs. See "Last Updated rule". |
| Detailed description (for AI parsing) | rich_text | Structured block (see format). |
| Tutorial Videos | rich_text | Optional. Training, demo or tutorial videos for the asset (e.g. Loom links). One video: just the link. Several: one per line as `Title: link`. Fill it whenever the user gives any; for a Tool, ask (see "Internal tools"). Never invent or search for one. The old `Tutorial Video` (url) property is retired: never write to it. |

Do **not** set: `Partners Only?` (checkbox, governance), `Publicly Shareable?`,
`New Hire?`, `Partner`, `Featured On`, `Stage in Buyer's Journey`, `Spotter Solution`,
`Drive Link`, `Webflow item ID` — unless the user explicitly asks. These are managed by people/other flows.
The one exception is a research PDF saved to the Research papers folder: then set Drive
Link (and Link, when the paper has no public link), per `research-pdfs.md`. A paywalled
paper does not change Publicly Shareable?: customers often have their own access.
Setting Drive Link never replaces Link: the library opens Link when someone clicks a card,
and Drive Link only powers the Download button. For Custom assets in particular, leave
`Publicly Shareable?` empty unless the user explicitly says the asset can go to customers.
`Created time` is system-managed by Notion (auto-filled on creation) and cannot be written.

## Write format

- Multi-selects are JSON-array strings, e.g. `"Product": "[\"Spotter\"]"`,
  `"Use Case Category": "[\"Offshore Renewables\",\"Coastal Management\"]"`.
- Select is a plain string, e.g. `"Content Type": "Customer stories"`, `"Origin": "Custom"`.
- Text is a plain string, e.g. `"Customer / Prospect": "Acme Offshore Wind"`.
- Date uses the expanded key: `"date:Last Updated:start": "2026-06-17"`.

## Product (multi_select)

Options: **Spotter**, **Wayfinder**.
- **Spotter** = ocean sensing, buoys, Smart Mooring, subsurface/metocean data. Smart
  Mooring and Bristlemouth content roll up under Spotter.
- **Wayfinder** = voyage optimization, routing, fuel savings, shipping operations.
- Can be both, or neither (some brand/company assets have no product).

## Content Type (select), 14 values + disambiguation

Nine website types (a row reaches the public resources hub only when a person sets Website
status to On hub, never because of its Content Type):

- **Customer stories**: how a real customer used Spotter or Wayfinder (case studies,
  customer success stories). One customer's story, in any format except a webinar.
- **Research papers**: published in a journal, at a conference or as a preprint, by anyone,
  including Sofar staff. Also theses, technical or government reports, and datasets and
  supporting materials that go with research (including third-party data archives).
- **Webinars and events**: webinar recordings and event pages.
- **Videos and podcasts**: videos and podcasts that show the product in use or how to use
  it (how-tos, demos, field footage, customer stories on video, Sofar's own podcast),
  whoever made them. Videos come first.
- **Tools and demos**: customer-facing tools, dashboards, demos, configurators, calculators,
  scenario builders and live dashboards. These stay in the main library.
- **Spec sheets**: product and sensor spec sheets, product booklets and product one-pagers.
- **Product updates**: what is new only: Sofar launches, new features, releases and what's
  new roundups.
- **Guides and reports**: in-depth Sofar content that explains a subject or shares
  analysis: explainers, how-to guides, how the product works, how we built it, test
  results, Sofar blog posts that summarize a paper, white papers, and reports such as
  savings reports and fuel savings snapshots. Articles and downloadable documents both
  belong here.
- **News and press**: press releases, partnerships, funding, team stories (including team
  Q&As), and articles, interviews and news segments published by outside outlets,
  including pieces Sofar wrote for an outside publication.

Five internal-only types (never on the hub):

- **Presentation**: slide decks, including custom decks made for one customer. Custom
  assets use the same Content Types as Official ones; Origin never changes the Content
  Type, so never invent a "Custom" Content Type.
- **Enablement**: internal or partner enablement, sales training and onboarding material.
- **Creative / Brand Asset**: logos, photo and video directories, brand books, media kits,
  renderings and design files.
- **Webpage / FAQ**: product webpages, site pages and FAQs.
- **Internal tool**: internal web utilities that Sofar staff open and use rather than share,
  e.g. an email signature generator or a quote calculator. These appear on the internal
  library's Tools page. See "Internal tools (Content Type = Internal tool)".

There is no Other option. If nothing fits, ask the user.

**Tie-breakers:**
- Published in a journal, conference proceedings or as a preprint is a Research paper,
  whoever wrote it. Published by Sofar, as an article or a downloadable document, is a Guide
  or report. A post on our site that gives a paper's authors and abstract is the Research
  paper itself.
- Ask whether it announces something new. A launch, a new feature, a release or a what's
  new roundup is a Product update. Everything else Sofar writes is a Guide or report,
  including how the product works, how we built it and test results.
- Where an article is published decides its type. An article on another site is News and
  press, whatever its subject, including pieces Sofar wrote for an outside publication. A
  post on our site that mainly points to it (In the News category, a publisher logo, a link
  to the full article) is News and press too.
- One customer's story is a Customer story. A report that pools results across customers,
  like a savings report, is a Guide or report.
- A product launch or new feature is a Product update. Anything about the company, a
  partnership, funding, the team, or coverage written by someone else is News and press.
- A webinar recording stays Webinars and events, so the series lives in one place.
- A customer story told on video is Videos and podcasts. A written customer story is
  Customer stories.
- For videos and podcasts, what is in it decides. One that shows the product in use or how
  to use it is Videos and podcasts, whoever made it (Sofar's own podcast, or a customer or
  program video such as Backyard Buoys). An interview or news segment about Sofar by an
  outside outlet is News and press.

**Internal tool vs. Tools and demos:** ask who uses it. Internal staff utility → Internal
tool. Something customers see or use (demo, configurator, dashboard) → Tools and demos. If
a link could be either, ask the user whether it's an internal tool or something customers
see.

**During the switch (old option names).** The options were renamed on 13 November 2026.
The fetch in Step 1 shows the live names. If the live Content Type options still use the
old names, use the old name that matches and never create a new option by writing an
unknown value: Customer Story (Customer stories), Whitepaper / Research (Research papers),
Webinar / Video (Webinars and events, Videos and podcasts), Interactive Tool / Demo (Tools
and demos), Sales Collateral (Spec sheets), Article (Product updates, Guides and reports,
News and press), Tool (Internal tool). Every rule in these references that names a new
type applies to its old name in the same way. Do the same for Topic and Website status:
fill them only when the property exists.

## Origin (select) and Customer / Prospect (rich_text)

**Origin** options: Official, Custom. Always set one. Origin is about what the asset is for,
not what format it is. (Before v0.9.0 the second option was called "Field-Created".)
- **Official** (the default): reusable assets marketing made or approved for general use.
  This covers almost everything, including third-party articles and research that marketing
  has curated.
- **Custom**: either a one-off made for a specific customer, prospect, meeting or deal,
  whoever made it (marketing included), or anything a rep, the field team, or anyone outside
  marketing made that marketing hasn't reviewed. It can be any format: a deck, a one-pager,
  a proposal, a custom savings report, a demo video, a spreadsheet, a tool. Signs: a company
  name in the title or file name, "for [Company]" or "prepared for [Company]", a named
  meeting, "my deck" or "a one-pager I made", or the user saying a rep made it.
- Use judgment from those signs. Ask the user only when the asset could plausibly be either
  and nothing points one way, or when it's clearly for one account but you can't tell which.

When Origin = Custom:
- **Customer / Prospect**: fill with the account name (e.g. "Acme Offshore Wind") whenever
  the asset was made for a specific customer or prospect. Leave it blank for a general asset
  a rep made for reuse, and always blank for Official assets.
- **Content Type**: the kind of asset it is, using the same rules as for Official assets
  (Presentation for a deck, Spec sheets for a product one-pager or spec sheet, Videos and
  podcasts for a recording, and so on). Never invent a "Custom" Content Type.
- **Link**: always the asset's shareable URL (e.g. the Google Slides, Docs or Drive link),
  not only Drive Link. The library opens Link when someone clicks the card; Drive Link only
  powers the Download button.
- **Publicly Shareable?**: leave empty unless the user explicitly says the asset can go to
  customers. The library treats Custom assets as internal-only unless it's Yes.
- **Third-Party?**: No (the asset is Sofar-produced).
- **Last Updated**: today's date (treat it as a living document).
- Skip Testimonials, Statistics and the Coverage Map (SKILL.md Steps 4, 5 and 6): the content
  is one-off or hasn't been reviewed by marketing.

## Internal tools (Content Type = Internal tool)

| Field | Rule |
|---|---|
| Link | **Required.** The tool's web address. |
| Summary | **Required.** One or two plain sentences saying what the tool does; it's the description shown on the tool's tile. |
| Product, Smart Mooring Sensor(s), Use Case Category, Stage in Buyer's Journey | Optional; usually blank. Fill only when clearly applicable (Stage in Buyer's Journey only if the user asks, as for any asset). |
| Third-Party? | No. |
| Origin | Official, unless someone outside marketing built it and marketing hasn't reviewed it (then Custom). |
| Last Updated | Today's date (living document). |
| Tutorial Videos | Optional. Training, demo or tutorial videos (Loom, YouTube, Vimeo or any other link). One video: just the link. A series: one per line as `Title: link`, in viewing order, using the titles the user or source gives (e.g. `Pt 2: How to Share: https://...`). The tile shows "Watch tutorial" for one video and a "Tutorials (N)" menu for several; Loom, YouTube and Vimeo play in a pop-up and other links open in a new tab. If the user didn't include any, ask once whether there are tutorial videos; if not, leave it blank. |
| Page icon | Optional. Set the Notion page icon to one fitting emoji (e.g. 🧮 for a cost calculator, ✍️ for a signature generator); the tile shows it. Skip it if nothing fits. |

Skip SKILL.md Steps 4, 5 and 6 (Testimonials, Statistics, Coverage Map) for tools.

When a tool has both an internal version and a public, customer-facing version, catalogue them
as two separate entries: the internal one as an Internal tool (Tools page) and the public one
as Tools and demos (main library), each with its own Link. Mention the other version in
each entry's Detailed description.

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
- **Buyer before activity.** Tag the categories whose buyers the asset is for, judged
  against the company definitions, not every category whose activity it mentions. A
  hurricane paper for researchers is Ocean Science & Research even though it mentions
  coastal flooding.
- **Maximum 5**, and only categories whose buyer or specific problem the asset names,
  never every category it could apply to. Broad product content can carry several (a
  Spotter Sound post that names MPA monitoring, pile-driving compliance, port monitoring,
  harbor security and soundscape research carries all five). Most assets carry 1 or 2.
- Customer stories always carry the customer's category.
- **Horizontal assets → leave empty**: general platform/company overviews, brand assets,
  internal tools/demos/configurators/repositories not tied to a specific industry. (For
  Content Type = Internal tool, this field is optional and usually blank.)
- Wayfinder / voyage / fuel / routing content → **Shipping & Logistics**.
- Customer stories and research papers almost always map to at least one category.
- Disambiguation: research/academic/data/climate/oceanography → **Ocean Science &
  Research**; habitat/MPA/biodiversity/coral/species → **Conservation & Marine
  Protection**; storm surge / sea level / shoreline / flood / coastal engineering →
  **Coastal Management**.

## Topic (multi_select), 11 values

`Waves`, `Currents`, `Water temperature`, `Water level`, `Water quality`,
`Underwater sound`, `Weather and forecasts`, `Storms and extreme events`,
`Vessel performance`, `Emissions and regulation`, `Accuracy and validation`.

Topic answers "what is this asset about?" across products and industries.

- **Waves**: wave height, period, direction and spectra, plus the surface data Spotter
  reports alongside them (barometric pressure, estimated wind). Observations, not forecasts.
- **Currents**: surface and subsurface currents and drift.
- **Water temperature**: temperature through the water column (stratification, profiling).
  Surface temperature alone does not qualify.
- **Water level**: tides, surge and water level measurement.
- **Water quality**: dissolved oxygen, salinity, pH, turbidity, chlorophyll, eDNA and the
  temperature measured alongside them.
- **Underwater sound**: acoustics, hydrophones, marine mammals and underwater noise.
- **Weather and forecasts**: how marine forecasts are made, how ocean data improves them,
  and how they are used to make decisions.
- **Storms and extreme events**: hurricanes, typhoons, El Niño and other extremes, and how
  people measured or coped with them.
- **Vessel performance**: speed and fuel models, hull fouling, wind-assisted propulsion.
- **Emissions and regulation**: CII, EU ETS and decarbonization rules for shipping.
- **Accuracy and validation**: tests how accurate Sofar's data or forecasts are, compares
  them with other systems, or uses Spotter as the trusted reference to check something else.

Rules:
- Tag a topic only when it is a main subject, meaning the asset would be a good answer to
  "show me resources about this." **Maximum 3.** Empty is fine.
- Tag both Weather and forecasts and Storms and extreme events only when the asset is about
  forecasting a specific extreme event.
- Tag Accuracy and validation only when testing or comparing accuracy is the point of the
  asset, never because it calls something accurate.
- Never invent a topic. New topics are added through review, not during intake.
- Internal tools, brand assets, decks and enablement material usually get none.

Write format: `"Topic": "[\"Storms and extreme events\",\"Waves\"]"`.

## Website status (select) and Webflow item ID (rich_text)

**Website status** options: On hub, Not on hub, Retired. It is the only gate for the
public resources hub on sofarocean.com, and blank never reaches the website. A person in
marketing decides On hub and Retired, never intake.

- Set **Not on hub** when the asset clearly cannot go on the public hub: any internal-only
  Content Type (Presentation, Enablement, Creative / Brand Asset, Webpage / FAQ, Internal
  tool), Origin = Custom, Partners Only? checked, or the user says it must not be shared.
- Otherwise leave it **blank** for marketing to review.
- Never set On hub or Retired, and never change an existing value.

**Webflow item ID**: leave blank. It is filled when the asset's page is created in Webflow.

## Third-Party? (select) and Source (rich_text)

**Third-Party?** options: Yes, No. Classify by **where the asset is published**, not who
it is about:
- **Yes** — published somewhere other than Sofar Ocean's own properties: third-party
  publications and media articles, blog posts on websites that are not Sofar Ocean's,
  and research papers / scientific-journal articles not published by Sofar.
- **No** — published by Sofar Ocean itself: sofarocean.com pages and blog posts,
  Sofar-produced collateral, webinars, presentations, tools, and brand assets.
- Always set one of the two. If the venue is genuinely unclear (e.g. an uploaded file
  with no provenance), ask the user instead of guessing.

**Source:**
- When Third-Party? = Yes, set Source to the name of the publication, media outlet, or
  journal — the venue, not the author (e.g. "ECO Magazine", "Nature Communications",
  "gCaptain").
- When Third-Party? = No, leave Source blank.

Write format: both are plain strings, e.g. `"Third-Party?": "Yes"`,
`"Source": "ECO Magazine"`.

## Sofar Reference (select), Research papers only

Options: **Central**, **Passing**, **None**. Set it on every Research papers entry,
including papers by Sofar staff. Leave it blank for every other Content Type, including
Guides and reports (Sofar's own white papers and reports). It works the same for every product (Product says which one), so it records only how
much the paper references Sofar.

- **Central:** Sofar's products, data or forecasts are a real part of the study:
  Spotter or Smart Mooring validations and comparisons, studies that use Spotter, Smart
  Mooring, Bristlemouth, Wayfinder or Sofar data, and Sofar-authored papers about them.
- **Passing:** Sofar is cited or mentioned, but it isn't what the paper is about (for
  example a single sentence naming Spotter in a literature review, or a citation of a Sofar
  blog post).
- **None:** no reference to Sofar's products or data. Typically a paper by Sofar staff
  that is kept for credibility, where Sofar appears only in the author affiliation.

Rules:
- Judge it from the paper itself (methods, data, figures and acknowledgments), not from
  who wrote it. A Sofar author doesn't make a paper Central.
- Only products Sofar sells today count toward Central. A paper whose only Sofar link is a
  discontinued product (for example the Trident ROV or other OpenROV products) is Passing.
- Only Central is evidence about our products. Passing and None should never be presented
  to a customer as product proof.
- If you can't tell (the full text is paywalled or can't be fetched and the abstract
  doesn't say), ask the user rather than guessing.

**Caveat for reps.** Whenever the paper mentions a Sofar product, also read its
limitations, discussion and conclusion for criticism of that product: data or processing
problems, poor performance in some conditions, or a recommendation to use other
instruments. If there is any, add a line to the Detailed description starting
`- Caveat for reps:` that paraphrases it closely, gives the page (the printed page number
when there is one), and says what not to claim from this paper. Mention it in the report.
Sofar Reference stays as judged above: a Central paper with a caveat is still Central. A
note on the Academic publications page (for example "negative product feedback on page
56") is a strong hint to look.

Write format: plain string, e.g. `"Sofar Reference": "Central"`.

## Last Updated rule

Set `date:Last Updated:start` based on the kind of asset:

- **Assets with a true, fixed publication date** — news articles, press releases, blog
  posts, published papers, podcast/video episodes: use the **publication date**
  (`YYYY-MM-DD`). When only month/year is known, use the first of the month; year only,
  use January 1. Note the precision in the Detailed description if not exact.
- **Living documents** — sales decks, one-pagers, FAQs, tools/demos, webpages,
  enablement material, brand assets: use **today's date** (`date +%F`), i.e. the intake
  date, since Last Updated signals content freshness for these.
- **Publication date should exist but cannot be determined** (gated/paywalled article,
  undated page): use today's date and add this note to the Detailed description:
  "Publication date unknown; Last Updated reflects intake date."

Rationale: intake time is captured automatically by Notion's built-in Created time
property, so nothing is lost. For dated assets, sorting and filtering on Last Updated
should reflect when the piece was published.

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
