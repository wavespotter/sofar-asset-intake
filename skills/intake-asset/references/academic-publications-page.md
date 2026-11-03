# Academic publications page: rules (conditional, dedupe-first, automatic)

**Page:** 📚 Academic publications featuring Sofar / Spotter
`https://app.notion.com/p/af13290265a04c7095f9934ad5eb4dbc`

This is an internal page that lists third-party research featuring or mentioning Sofar or
Spotter, by year and then by publication. The Resource Library is the source of truth.
This page is kept in sync with it until it is retired. It is a regular Notion page, not a
database, so every write is a targeted edit to its content.

**The golden rule: match the page exactly. Never add anything new.** No new heading
styles, sections, labels, colors, callouts, dividers, emoji, properties or notes the page
does not already use. Copy the formatting of the entries next to where you are writing.
If an asset doesn't fit the page's existing patterns, skip it and say why, rather than
inventing a new pattern.

## When to act

Only when the Resource Library entry just created (or the existing entry the user chose to
update) has **Content Type = "Whitepaper / Research" and Third-Party? = "Yes"**. That
covers journal papers, conference proceedings, preprints, theses and dissertations, and
technical or government reports. Skip it for everything else, including Sofar blog posts
and Sofar's own white papers (Third-Party? = No), datasets, talks and slides, articles,
and anything Custom. A paper written by Sofar staff but published in a journal is
Third-Party? = Yes, so it is in scope.

The page step needs a link. If the asset is only an uploaded file with no public link,
skip the page and say so in the report.

## Step order

1. **Fetch the page** with the Notion fetch tool. It is long (about 70,000 characters), so
   if the result is saved to a file, read all of it. Check `truncated`. Never write based
   on a partial read.
2. **Dedupe (per `deduplication.md`).** Compare the asset against every entry on the page:
   - Normalized URL match against every link on the page. Also compare DOIs: a
     `doi.org/10.x/...` link and a publisher link with the same DOI string are the same
     paper.
   - Fuzzy title match (case-insensitive, ignoring punctuation). Many older entries are
     PDF attachments with no link, so also compare the title against attachment file names
     (`name=...pdf`), where underscores stand for spaces.
   - A preprint and its published version count as the same paper.
   If any likely match exists, **do not write**. Report "Already on the Academic
   publications page" in the summary. Do not ask, and do not update the existing entry.
3. **Find the year.** Use the publication year (the same date used for the Resource Library
   Last Updated). Year sections are level 1 headings in descending order, newest first,
   formatted exactly as `# <span color="blue">2026</span>`. If the year has no section yet,
   create one in that exact format, placed above the next older year. The
   "Links to private/purchase only publications" section at the bottom is not a year:
   never write there.
4. **Find the publication heading** within that year. Publication headings are level 3
   headings (`### Name`) naming the journal, conference, publisher, institution or
   category. Search only between this year's heading and the next level 1 or level 2
   heading. Some years repeat the same journal heading more than once, and the same
   journal appears in many years, so never match on the first heading found on the page.
   - If the year already has a heading for this publication, add the entry at the end of
     that heading's block (after its last entry and any toggle or file under it), not as
     a new heading.
   - Otherwise add a new `### Name` heading in alphabetical order by publication name
     within the year (ignore a leading "The" and any bold markup when sorting). Insert it
     directly before the first existing heading that sorts after it. If none does, put it
     at the end of the year's section. Write it as plain `### Name`, without bold.
   - Name the publication the way the page already does when it appears elsewhere on the
     page (for example "Geophysical Research Letters", "Journal of Atmospheric and Oceanic
     Technology", "Ocean Engineering"). Otherwise use the journal or venue's full name, the
     same value as the Resource Library Source property.
   - Categories the page already uses: `Preprint` for preprints, the university name for
     theses (for example `### Oregon State University`, with the Master’s thesis note
     below, or `### Oregon State University (Doctoral Dissertation)` for a dissertation),
     and `Project Report` for unreviewed project reports.
5. **Write the entry** in the page's existing format:
   - The title as a link on its own line: `[Title](URL)`. Use the asset's real title and
     the canonical link (the DOI link when there is one, otherwise the publisher page).
   - Optional bracketed notes on the same line, after a space, only in forms the page
     already uses: `\[<b>paywalled</b>\]`, `\[<i>not peer reviewed</i>\]`,
     `\[Master’s thesis\]`. Add one only when it is true.
   - **Toggle, only when the year's section already uses them.** Check the existing
     entries in the target year's section. The 2026 section puts a toggle under each entry
     and the older years don't. If the section's entries carry toggles, add one directly
     under the link, matching them exactly:

     ```
     <toggle>
     <b>AI Summary</b>

     <2 to 4 sentences: what the study does, and how Sofar, Spotter or Smart Mooring
     appears in it (or that it is only mentioned in passing)>
     </toggle>
     ```

     Use `<b>Abstract</b>` with the abstract copied word for word instead, only when you
     have the full abstract text. If the section's entries carry no toggles, add none.
   - Leave a blank line between blocks, as the page does.
   - Never attach files, add comments or mentions, or change any existing entry, heading
     or the page's intro text.
6. **Insert with a targeted edit.** Use the update-page tool's `update_content` command
   with an `old_str` that uniquely anchors the insertion point, for example the full line
   of the next heading in the year (`### Ocean Dynamics`) plus enough of the following
   entry's link to be unique. Replace it with the new block followed by the original
   text, unchanged. Never use `replace_content` on this page. If no unique anchor can be
   built, skip the write and report it, rather than guessing.
7. **Verify.** Fetch the page again and confirm the new entry appears once, under the right
   year and heading, and that nothing else changed. If the edit landed in the wrong place,
   tell the user what happened, and don't attempt more edits without asking.

## Example

A 2026 paper in "Coastal Engineering", where the 2026 section already has
`### Coastal Dynamics 2025 Volume 2 (book / conference)` and
`### Coastal Engineering Journal`, but no `### Coastal Engineering` heading. By
alphabetical order the new heading goes after "Coastal Dynamics..." and before "Coastal
Engineering Journal", so insert directly before `### Coastal Engineering Journal`:

```
### Coastal Engineering

[Spectral and time-domain comparison of GNSS and accelerometer wave buoys](https://doi.org/10.1016/j.coastaleng.2026.105049)

<toggle>
<b>AI Summary</b>

<summary>
</toggle>

### Coastal Engineering Journal
```

## Report line

In the final report, say one of:
- "Added to the Academic publications page under <year> / <publication>: <page link>".
- "Already on the Academic publications page (matched <the existing entry's title>)."
- "Skipped the Academic publications page: <reason>" (out of scope, no link, no unique
  anchor, or the page couldn't be read in full).
