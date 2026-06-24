# Deduplication — check before every write

Before creating anything in any of the three databases, check whether it already exists.
On a likely match, **warn and ask** — show the existing item and let the user choose to
**update it, add anyway, or skip**. Never silently create over a probable duplicate.
Prefer recall: when unsure, surface the near-match and let the human decide.

## Why this matters

The same asset often appears under **different URLs** — a blog post, a hosted PDF, and a
Google Drive link can all be the same thing. URLs also carry tracking junk
(`?__hstc=…`, `__hssc`, `__hsfp`, `utm_*`, `submissionGuid`, `source`, `pvs`). And the same
**quote** can appear in multiple resources. Exact-string checks miss all of these.

## URL normalization (do this before comparing any URLs)

1. Lowercase.
2. Drop the scheme (`http://`, `https://`) and a leading `www.`.
3. Remove the query string (everything after `?`) and fragment (everything after `#`).
4. Strip a trailing slash.

Compare the normalized form. Treat the blog URL, the PDF, and the Drive link as possibly
the **same asset** — so check the candidate against **both** the `Link` and `Drive Link`
columns, and compare the normalized incoming URL against normalized stored URLs.

## Resource Library dedupe (Step 3)

Before creating, query the Resource Library data source for a likely existing entry:
- Normalized URL match against `Link` **or** `Drive Link`, OR
- Title match — case-insensitive, ignoring punctuation and minor year/wording differences.
  Use `LIKE` on the distinctive title tokens (e.g. `%Wayfinder%Savings Report%`).

If a candidate matches, **stop and ask**: show the existing entry's title + link and offer
to (a) update it, (b) add as new anyway, or (c) skip. Note: a title match can catch a
duplicate that a URL check misses (e.g. the asset's PDF is stored under `Drive Link` while
`Link` holds the blog post) — run both checks.

## Testimonials dedupe (Step 4)

Before writing each quote, query the Testimonials data source for:
- A distinctive verbatim substring of the `Quotation` (`LIKE '%<distinctive phrase>%'`), OR
- The same `Name` + `Customer`.

A quote already captured from a *different* source asset is still a duplicate — match on the
quote text itself, not the source. On a match, warn and ask (skip by default for an exact
quote match unless the user wants it re-added).

## Statistics dedupe (Step 5)

Already conservative. Match on `Statistic` title tokens and/or `Externally Shareable
Description`. On a match, do not create — offer to update the existing row instead.

## Matching technique

SQL has no fuzzy operator here, so:
- Build `LIKE` patterns from normalized distinctive tokens (title keywords, a unique quote
  phrase, a normalized URL stem).
- Run a few targeted queries rather than one exact-equality query.
- When results are ambiguous, list the near-matches to the user instead of guessing.

## Warn-and-ask format

> Possible duplicate — "<title or quote>" already exists: <link>.
> Want me to (a) update the existing one, (b) add this as a new entry anyway, or (c) skip it?

Wait for the user's choice before writing.
