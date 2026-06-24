# Statistics Repository — schema & rules (conservative, confirm-first)

**Database:** 📈 Sofar Ocean Statistics Repository — `https://app.notion.com/p/24e8ff95945080878aceeed4acac388e`
**Data source (parent for new pages):** `collection://24e8ff95-9450-8003-8e88-000bf69d7ba6`

This is a **tightly governed, curated** database of company/product metrics. Statistics
are reused across many assets; they require human calculation and approval. **Default to
adding nothing.** Only act when an asset introduces a genuinely new, featureable,
quantified statistic — and even then, draft conservatively, confirm, and never approve.

## Hard rules (do not violate)

1. **Never set an "Approved" status.** New rows are **always** `Status = "Under review – do
   not share"`. Approval for public/internal use is a separate human governance step.
2. **Dedupe before creating.** Query the data source for existing rows with a similar
   `Statistic` title or `Externally Shareable Description`. If a comparable stat exists, do
   **not** create a duplicate — tell the user it already exists and offer to update that row
   instead. (Many near-identical Wayfinder savings rows already exist.)
3. **Confirm with the user** before writing anything.
4. **Leave calculation rigor to a human.** Do not invent methodology. Record the asset as
   provenance and note that the figure still needs verification.
5. Be **conservative**: most assets reference existing stats rather than introduce new ones.
   When unsure, surface the candidate to the user as a suggestion rather than creating a row.

## When a statistic qualifies

A featureable statistic is a quantified, reusable company/product metric — e.g. a
cumulative savings figure ($/MT/CO2), a network metric (buoys, observations, ocean hours),
a fuel-savings percentage, a funding/scale figure. A one-off number specific to a single
customer's voyage is usually **not** repository-worthy on its own (it belongs in the
Resource Library entry / testimonial).

## Properties

| Property | Type | Notes |
|---|---|---|
| Statistic | title | Short internal label for the metric (e.g. "Average fuel (%) saved per voyage using Wayfinder (2025)"). |
| Category | multi_select | See options below. |
| Status | status | **Always "Under review – do not share"** for new rows. |
| Externally Shareable Description | rich_text | Proposed polished, share-ready phrasing. |
| [internal only] How Was This Calculated? | rich_text | Record provenance: the asset URL + "needs human verification". |
| [internal only] Additional Notes | rich_text | Any caveats / context. |

### Category options

`Company`, `Spotter Network`, `Spotter (Customers)`, `Wayfinder`, `Emissions Equivalency`,
`Ocean Intelligence`, `Retired - Do Not Use`. (Do not use "Retired - Do Not Use" for new
entries.)

### Status options (for reference — only ever set the first for new rows)

- `Under review - do not share`  ← **set this for all new entries**
- `Approved for public use` (human-only)
- `Approved for internal use only)` (human-only; note the literal trailing parenthesis in the option name)
- `Retired - do not use` (human-only)

## Write format

- Title field is `Statistic`: `"Statistic": "..."`.
- `"Category": "[\"Wayfinder\"]"` (JSON-array string).
- `"Status": "Under review - do not share"` (exact option string).
- Text fields are plain strings.

## Workflow

1. Identify at most a few candidate statistics from the asset.
2. For each, query existing rows to check for duplicates; if found, recommend updating
   rather than creating.
3. Draft Statistic + Externally Shareable Description + Category; put the asset URL and a
   "needs verification" note in "[internal only] How Was This Calculated?".
4. Present the candidate(s) to the user and get explicit approval.
5. Create approved rows with `Status = "Under review - do not share"`.
6. Tell the user the row was created under review and still needs calculation/approval.
