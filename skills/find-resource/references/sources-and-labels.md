# Sources and sharing labels

Where to search, in what order, and how to label what you find. The live database wins if
any option name here has drifted: match options by meaning, and fetch the data source when
in doubt.

## Tier 1: Resource Library (always first)

- **Database:** 📚 Resource Library, `https://www.notion.so/sofarocean/1ac8ff95945081eda6d6d0538f2eed87`
- **Data source (use as `data_source_url`):** `collection://1ac8ff95-9450-815b-b8b4-000b7de5b0a3`

The catalogue of every marketing asset, including third-party research. It is the source
of truth. Fields that matter for finding and labeling:

| Field | What it tells you |
|---|---|
| Title, Summary | What the asset is. |
| Detailed description (for AI parsing) | The fullest account: authors, numbers, method, and any line starting `- Caveat for reps:`. Always read it before describing a result. |
| Content Type | Article, Customer Story, Webinar / Video, Sales Collateral, Whitepaper / Research, Webpage / FAQ, Interactive Tool / Demo, Presentation, Enablement, Creative / Brand Asset, Tool, Other. |
| Product | Spotter and/or Wayfinder. |
| Smart Mooring Sensor(s), Spotter Solution, Use Case Category | Topic filters. |
| Third-Party?, Source | Yes plus the venue when published outside Sofar (journal, outlet, institute). |
| Sofar Reference | Research only. Central, Passing or None. Only Central is evidence about Sofar's products. |
| Origin, Customer / Prospect | Official (general use) or Custom (made for one account, or made outside marketing and not reviewed). |
| Publicly Shareable? | Yes, No, or blank. |
| Partners Only? | Checkbox. |
| Link, Drive Link | Link is the canonical URL. Drive Link is a stored PDF or file. |
| Last Updated | Publication date for dated assets; last refresh for living documents. |

## Tier 2: governed repositories

**Statistics Repository**
- Data source: `collection://24e8ff95-9450-8003-8e88-000bf69d7ba6`
- Fields: Statistic (title), Externally Shareable Description, Category, Status,
  "[internal only] How Was This Calculated?", "[internal only] Additional Notes".
- Status options: Approved for public use; Approved for internal use only (the live
  option name ends with a stray ")"); Under review - do not share; Retired - do not use.
  A Category of "Retired - Do Not Use" also means do not use.

**Customer Testimonials Repository**
- Data source: `collection://2858ff95-9450-8149-b7c6-000b876715dd`
- Fields: Customer (title), Name, Title, Quotation (verbatim), Testimonial Summary,
  Product, Vertical, Source (URL), Publication Date.
- A Product tag of "Do Not Use" marks a former customer or retracted quote.

**Case Study Coverage Map** (Spotter customer stories)
- Data source: `collection://4b61d3e0-2975-4334-aed4-7366a5dd5b7f`
- Fields: Case Study (title), Organization, Use Case Category, Geography, Depth (Deep,
  Moderate, Light), Status (Nominated, Survey Sent, Interview Scheduled, In Progress,
  Customer Review, Published), Published, URL, Notes.
- Useful for "do we have a case study for <industry> in <region>?". Only Published stories
  exist as assets; the rest are in the pipeline.

## Tier 3: wider Sofar sources (internal)

- **Notion, unscoped search.** Engineering and science material lives mainly in the Spotter
  Team Porthole (technical support, known issues, firmware releases, manufacturing tests),
  the Weather Team pages and the Ocean Science Team pages. These are internal analyses:
  useful for answering colleagues, not for sending to customers.
- **Google Drive.** The Research papers folder (Sofar Marketing shared drive, Resource
  Library, Research papers):
  `https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2`.
  Search Drive by full text for the topic as well.
- **Academic publications page** (fallback for research only):
  `https://app.notion.com/p/af13290265a04c7095f9934ad5eb4dbc`. A search scoped with
  `page_url` only returns the page itself with one matching snippet, so to find entries,
  fetch the page (about 70,000 characters; the result is usually saved to a file) and
  search that text for your keywords. Entries marked "[not peer reviewed]" are not peer
  reviewed. Anything useful found here but missing from the library is worth the filing offer.

## Tier 4: the web

Public papers, reports and articles. Prefer the publisher or DOI page. Treat as "public,
not reviewed by marketing" and offer to file anything useful with intake-asset.

## Sharing labels

Apply the first rule that matches, top to bottom.

**Resource Library entries**

1. The page is deleted or in the trash: skip it.
2. Origin = Custom and Publicly Shareable? is not Yes: **Internal only**, "made for
   <Customer / Prospect>" (or "rep-made, not reviewed by marketing" when that field is blank).
3. Partners Only? is checked: **Partners only**.
4. Content Type = Tool or Enablement: **Internal only** (staff tool or training material).
5. Publicly Shareable? = No: if the Link is a public publisher or DOI page, **Share the
   public link only** (do not send the stored PDF); otherwise **Internal only**.
6. Everything else (Official, with a public Link such as sofarocean.com, a journal, or a
   public report): **OK to share with customers**. If the only link is a Drive file and
   Publicly Shareable? is blank, say "check with marketing before sending the file".

Then add, where they apply:
- **Research:** the venue (Source); "peer reviewed" only when the venue is a peer-reviewed
  journal or the entry says so, "not peer reviewed" when the entry, page or paper says so,
  otherwise state the type (preprint, technical report, conference paper, thesis) without
  guessing. Sofar Reference: say "not product evidence" for Passing or None.
- **Caveat for reps:** always pass it on, closely paraphrased, with what not to claim.
- **Age:** for living documents (decks, one-pagers, spec sheets, FAQs, webpages) last
  updated more than about 18 months ago, note that figures may be out of date.

**Statistics**
- Approved for public use: **OK to share with customers.** Use the Externally Shareable
  Description wording.
- Approved for internal use only: **Internal only.**
- Under review - do not share: **Do not use** (not approved yet).
- Retired - do not use, or Category "Retired - Do Not Use": **Do not use.**
- Never quote the "[internal only]" fields to a customer.
- Some rows are templates with placeholders ("an average of X%", "$ on fuel"). Report
  those as "no approved figure yet", never as a number.
- When several rows cover the same metric (Wayfinder savings has many), lead with the
  approved one and mention the others only if they add something.

**Testimonials**
- Product includes "Do Not Use": **Do not use.**
- Otherwise: **OK to share with customers**, quoted verbatim with the person's name, title
  and company, and the publication date. Flag quotes more than about three years old.

**Case Study Coverage Map**
- Status = Published, with a URL: **OK to share with customers** (link the story).
- Any other status: **Internal only** (in the pipeline, not published).

**Tier 3 results:** **Internal only**, unless the item is plainly a published public asset
(then treat it as a web result and offer to file it).

**Tier 4 results:** public. Label "public, not reviewed by marketing", and still apply the
research checks above (venue, peer review, whether it is really about a Sofar product).
