---
name: find-resource
description: "Use when anyone at Sofar asks whether Sofar already has material on a topic, or wants something to cite or send: research papers, validations, case studies, customer quotes, statistics, spec sheets, decks, webinars, one-pagers, demos or tools. Trigger on questions like \"do we have any papers on Spotter's SST accuracy\", \"is there a case study for ports in Europe\", \"what can I send a customer about Smart Mooring\", \"find me a quote from an offshore wind customer\", \"do we have a stat on Wayfinder fuel savings\" or \"where's the deck for...\", even when no database is named. Searches Sofar's Resource Library first, then the Statistics, Testimonials and Case Study Coverage Map databases, then wider Notion and Drive, then the web, and labels every result for whether it can go to customers. Read-only. To file a new asset use intake-asset; for deal coaching use what-would-jarrah-do."
metadata:
  version: "0.17.0"
  author: "Sofar Ocean Marketing"
---

# Find a Sofar resource

Answer "do we have anything on X?" from Sofar's own curated material first, and tell the
person exactly what each result can and can't be used for. Anyone at Sofar may ask: sales,
customer success, science, engineering, marketing. What they find often ends up in front of
a customer, so the labels matter as much as the search.

**This skill is read-only.** It never creates, edits or deletes anything in Notion or Drive.
When it finds something worth filing, it offers the intake-asset skill and does nothing
unless the person says yes.

Read `references/sources-and-labels.md` before searching. It has the database addresses,
the fields that decide what is shareable, and the label rules.

## Step 1: Load the tools

Tool names carry a per-user prefix, so load them by capability with ToolSearch:

```
ToolSearch: "notion search fetch query data sources"
ToolSearch: "google drive search files"
```

You need a Notion **search** and **fetch** tool, and a **query-data-sources** tool if one
exists. Drive search and web search are optional. If no Notion tools load, say that the
Resource Library needs the Notion connector (Settings, Connectors) and continue with Drive
and the web, saying clearly that Sofar's curated library was not checked.

## Step 2: Pin down the question

Work out, without asking unless it is truly ambiguous:

- **The subject and the claim.** "Spotter SST accuracy" is about the hull sea surface
  temperature sensor, which is not the same as the Smart Mooring temperature sensors.
  Note the exact product, sensor, metric and conditions, because results are judged
  against them in Step 4.
- **The kind of material wanted:** research or validation, statistic, customer quote,
  case study, collateral, deck, video, tool. "Proof" or "evidence" questions want research,
  stats, quotes and case studies.
- **Who it is for.** If the person says it is for a customer or prospect, put shareable
  items first and say plainly which results must not be sent.

Write two to four search phrasings with the obvious synonyms (for example SST, sea surface
temperature, water temperature; barometer, barometric pressure, atmospheric pressure, sea
level pressure; validation, accuracy, comparison, intercomparison).

## Step 3: Search in tiers

Go down the tiers in order. Stop widening once the question is answered well, except for
technical accuracy, specification or calibration questions, where you always run Tier 3
too, because Sofar's engineering and science teams keep internal analyses that the library
does not hold.

**Tier 1: Resource Library (always first).** Run the Notion search with `data_source_url`
set to the Resource Library data source, once per phrasing. Then fetch the most promising
hits (usually up to five) to read their properties and the "Detailed description (for AI
parsing)" field, which holds the summary, the numbers and any "Caveat for reps" line. If
search is thin and a query-data-sources tool is available, also filter by Content Type and
Product. Skip any page the fetch marks as deleted or in the trash.

**Tier 2: the governed repositories,** when the question is about numbers, quotes, customer
stories or proof. Search the Statistics Repository, the Customer Testimonials Repository
and the Case Study Coverage Map the same way (scoped search, then fetch).

**Tier 3: wider Sofar sources.** Search Notion without a data source scope, and Google
Drive. Useful places include the Spotter Team Porthole (technical support, known issues,
manufacturing tests), the Weather Team and Ocean Science Team pages, and the Research
papers folder in Drive. For research questions only, and only when the library came up
short, check the Academic publications page (see the reference file for how); the library
is the source of truth and that page is being retired. Everything found in this tier is
internal unless it is clearly a published asset.

**Tier 4: the web,** last. Look for published papers, reports or articles that are not in
the library yet, preferring the publisher or DOI page. These are public but have not been
reviewed by marketing.

## Step 4: Judge each result against the question

Read enough of each result to know what it actually shows. Check the product, sensor,
metric, conditions and method against what was asked, and say so when they differ. A tank
test of Smart Mooring temperature sensors is not evidence about the hull SST sensor. A
pressure comparison the authors call "not an accuracy estimate" is not an accuracy number.
Never stretch a result to fit the question, and never call something peer reviewed unless
the source, the library entry or the paper says so.

## Step 5: Label every result

Apply the rules in `references/sources-and-labels.md`. Each result gets one sharing label:

- **OK to share with customers**
- **Share the public link only** (for example a paywalled paper: link the publisher page,
  never send the PDF)
- **Partners only**
- **Internal only** (with the reason, such as "made for Acme" or "engineering analysis")
- **Do not use** (retired, "Do Not Use" quotes, stats still under review)

Add whatever else the person needs to use it safely: peer reviewed or not, Sofar Reference
for research (only Central counts as product evidence), any "Caveat for reps" line in close
paraphrase, the date, and a note when a living document looks out of date.

## Step 6: Answer

Lead with the direct answer in one or two sentences: yes, no, or partly, and the single
best item. Then list results grouped by where they came from:

1. **In the Resource Library** (and the other governed databases)
2. **Other Sofar sources (internal)**
3. **Outside sources**

For each result: the linked title, one line on what it shows (with the key numbers), and
its label line. Keep it tight. Leave out weak or off-topic hits rather than padding the list.

Then:

- **Gaps.** Say plainly what was not found, for example "No independent validation of the
  hull SST sensor turned up." This is useful information, not a failure.
- **Filing offer.** If a useful item came from Tier 3 or Tier 4 and is not in the Resource
  Library, offer in one line to file it with intake-asset. Do nothing unless they say yes.
- **Access note.** If a known database or page could not be opened, say the person may not
  have access and that the marketing team can help, instead of concluding nothing exists.
- **Sources.** End with a "Sources:" list of links to everything cited.

If the person then asks for a customer-facing draft (an email, a slide), use only items
labeled OK to share or Share the public link only, and say which results you left out and
why.

## Never

- Write to any Notion database or page, or to Drive.
- Present a statistic that is under review, internal only or retired as shareable, or use
  a quote tagged "Do Not Use".
- Present a Passing or None research paper as evidence about a Sofar product.
- Send or suggest sending a paywalled PDF, a Custom asset made for another account, or an
  internal analysis to a customer.
- Invent results, numbers, peer-review status or links. If you didn't open it, don't
  describe what it shows.
