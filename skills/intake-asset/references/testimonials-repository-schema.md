# Customer Testimonials Repository — schema & extraction rules

**Database:** ⭐ Customer Testimonials Repository — `https://app.notion.com/p/2858ff959450802d90ecf81e6d53db47`
**Data source (parent for new pages):** `collection://2858ff95-9450-8149-b7c6-000b876715dd`

This is a **quote-level** database: each row is a single customer quote with attribution.
One asset (e.g. a case study) usually yields one or two rows. Confirm the live option
lists by fetching the database before tagging.

## When to extract

Extract only **genuine, attributable customer quotes** — direct statements from a named
(or clearly identifiable) customer/partner about Sofar, Spotter, Wayfinder, or related
offerings. Found in case studies, customer stories, press releases, webinars, etc.
Sofar's own marketing copy, employee quotes, and paraphrases are **not** testimonials.
If the asset has no such quotes, skip testimonial creation entirely.

## Always confirm first

Before writing any rows, present the drafted quotes to the user as a numbered list
(customer, person + title, the verbatim quote, and proposed Product/Vertical tags) and ask
them to approve, edit, or drop any. Only create rows for approved quotes.

## Properties to fill

| Property | Type | Notes |
|---|---|---|
| Customer | title | The customer org/company being quoted. |
| Name | rich_text | The person quoted. |
| Title | rich_text | That person's job title/role. |
| Quotation | rich_text | The quote **verbatim**, preserving wording and quotation marks. |
| Testimonial Summary | rich_text | One short line capturing the gist. |
| Product | multi_select | See taxonomy below (distinct from Resource Library). |
| Vertical | multi_select | See taxonomy below (distinct from Use Case Category). |
| Source | url | Where the quote was published. |
| Publication Date | date | Use `date:Publication Date:start`. |

Leave **"Where is it used?"** empty (it has no defined options).

## Write format

- Title field is `Customer`: `"Customer": "Port of Lyttelton"`.
- Multi-selects are JSON-array strings: `"Product": "[\"Spotter\"]"`, `"Vertical": "[\"Ports\"]"`.
- Date: `"date:Publication Date:start": "2021-06-15"`.

## Product (multi_select) — testimonials taxonomy

Options: **Spotter**, **Wayfinder**, **Data / Open Access**, **Bristlemouth**,
**Sofar Ocean (General)**, **Weather**, **Do Not Use**.
- Map the quote to the offering it praises. Use **Sofar Ocean (General)** for company-level
  quotes, **Weather** for forecasting/weather-data quotes, **Data / Open Access** for open
  data programs, **Bristlemouth** for the open standard.
- **Never auto-apply "Do Not Use".** That tag is reserved for former customers or retracted
  quotes and is a human governance decision. If the source suggests the customer may no
  longer be active, flag it to the user instead of tagging it.

## Vertical (multi_select) — testimonials taxonomy

Options: Government, Offshore Wind, Defense, Academia / Research, Ports,
Coastal Resilience, Aquaculture, Maritime Shipping, Extreme Weather,
Indigenous Communities, Marine Renewables, Marine Protected Areas (MPA),
Weather Forecasting.

Pick 1–3 that fit the quote's context. Rough bridge from Resource Library Use Case
Category (not 1:1 — choose the closest):
- Shipping & Logistics → Maritime Shipping
- Government & Defense → Government and/or Defense
- Offshore Renewables → Offshore Wind and/or Marine Renewables
- Ocean Science & Research → Academia / Research
- Conservation & Marine Protection → Coastal Resilience or Marine Protected Areas (MPA)
- Ports & Harbors → Ports
- Coastal Management → Coastal Resilience
- Aquaculture & Fisheries → Aquaculture
- Weather-forecasting context → Weather Forecasting and/or Extreme Weather
- Indigenous/community deployments → Indigenous Communities

## Example row

- Customer: Port of Lyttelton
- Name: Neil McLennan
- Title: Engineering Adviser
- Quotation: "The purchase and operating cost of the Spotter is much lower than the large
  buoy so we are now using it as our primary offshore wave data source…"
- Testimonial Summary: Spotter replaced large buoy as main wave data source; affordable and reliable
- Product: ["Spotter"]
- Vertical: ["Ports"]
- Source: https://www.sofarocean.com/posts/port-of-lyttelton-sofar-ocean-spotter-as-primary-offshore-wave-buoy
- Publication Date: 2021-06-15
