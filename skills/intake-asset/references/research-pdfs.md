# Research PDFs: one copy in Drive, linked from Notion (Whitepaper / Research only)

**Folder:** Sofar Marketing shared drive / Resource Library / Research papers
**Folder link:** https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2
**Folder id:** `1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2` (shared drive id `1TLcetYMT79Gi2mNF05HOi8-6eWoqv9JqVOo`)

When someone gives you a research paper as a PDF, it gets one home: a file in the
Research papers folder. Notion links to it in two places, and nothing is attached in
Notion:
- **Resource Library entry:** **Drive Link** (powers the Download button), and **Link** too
  when the paper has no public page.
- **Academic publications page** (third-party research): the title links to the Drive file
  when there is no public page; otherwise the title links to the public page and a
  `[PDF]` link to the Drive file goes at the end of the line (see
  `academic-publications-page.md`).

The person filing should never need to know any of this. At most they do one small step
(drag the PDF into a folder and click Done), and only when the file is too big to upload
from the session.

## When this applies

Only for Content Type "Whitepaper / Research", and only when one of these is true:
- The user provided the paper as a PDF (uploaded or attached).
- The paper exists only as a PDF, with no public web page or DOI to link to.

Don't go looking for a PDF when the paper has a public link, and don't download one from a
publisher site. A link alone is a complete entry. If the user gives both a link and a PDF,
save the PDF and keep the public link in Link.

Paywalled or gated papers are filed the same way. Don't set Publicly Shareable? because a
paper is paywalled: customers often have their own access. Leave it to people, as for every
asset.

## File name

`<year> - <title>.pdf`, for example
`2025 - Observations and Simulations of the Effects of Infragravity Wave Reflection on Runup at a Rock-Reef-Fronted Dissipative Beach.pdf`.

- The year is the publication year (the same date as Last Updated).
- Use the paper's real title, from the PDF itself if the file name doesn't give it.
- Remove characters file systems reject (`/ \ : * ? " < > |`), collapse repeated spaces,
  and keep the whole name under 180 characters.
- Before saving, search the folder (Google Drive connector, `parentId =
  '1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2'`, title contains a distinctive title word) for a file
  with the same name or title. If one is there, don't save a second copy. Use the existing
  file's link.

You name the file. Never ask the user to rename anything.

## Saving to Drive

Note the time (`date -u +%Y-%m-%dT%H:%M:%SZ`) before you start, for finding the file later.
Check the size (`stat -c %s`), then use the first path that applies.

**Path A: upload it for them (PDFs up to 3,000,000 bytes).** Connector calls can carry
files up to about 3.1 MB, so never try this for a bigger file. Load the Google Drive
connector's create-file tool (ToolSearch "google drive create file") and upload the PDF
straight into the folder:
- `title`: the file name above
- `parentId`: `1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2`
- `contentMimeType`: `application/pdf`, and `disableConversionToGoogleType`: true
- `base64Content`: a file reference, not typed base64. Copy the PDF to a path with a plain
  name in the scratchpad, compute its SHA-256 (`sha256sum`), and pass
  `sha256:<64 lowercase hex>:<absolute path>`. The app fills in the content when the user
  approves the call. Say in one line, before the call, that they'll be asked to approve an
  upload to the Research papers folder.
Use the returned file's view link. If the call fails (no access, too big, any error), go to
Path C. Don't retry and don't try other ways.

**Path B: an already connected folder.** Only when the Research papers folder is already
one of the session's connected folders on the user's computer (`$HOME/mnt/Research
papers` in the device shell). Copy the PDF in with `cp -n` under the file name above,
then find it in Drive with the search above (a new file usually appears within a minute or
two). Don't request folder access for this; if it isn't connected already, use Path C.

**Path C: one guided step (everything else).** File everything else first, then end with
the short report (SKILL.md Step 7), whose last line is the one step:

> **One last step:** drag the PDF into [the Research papers folder](https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2), then click **Done**.

Then ask with buttons (the AskUserQuestion tool when it's available). Make the question
self-contained, because the user may see only the dialog:
- Question: "Drag the PDF into the Research papers folder in Drive
  (https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2), then choose
  Done. I'll name it and link it in Notion."
- Options: **Done** ("It's in the folder") and **Do it later** ("Leave it marked as
  pending").
Without a button tool, ask them to reply "done" instead. Never ask them to rename the file,
copy a link or paste anything. If they paste a link anyway, use it.

**After Done:**
1. Find the file: search the folder for PDFs created since the time you noted
   (`parentId = '1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2' and mimeType = 'application/pdf' and
   createdTime > '<time>'`). If several match, pick the one whose title or size matches
   the PDF you were given (`fileSize` equals the local file's size).
2. If nothing is there yet, wait about 30 seconds and search once more. If it's still
   missing, say so in one line, give the folder link again, and ask with the same buttons.
3. Rename it to the file name above with the Drive update-file tool if it differs (people
   often leave the original name, or end up with ".pdf.pdf").
4. Fill in Drive Link (and Link, when the paper has no public page), add the `[PDF]` link
   or the Drive title link on the Academic publications page, and remove the pending line.
5. Reply in one line, for example: "All set: the PDF is in Drive and linked from
   [the entry](link)."

**After Do it later:** leave the pending line, and reply in one line that they can say
"the PDF is in Drive" any time and you'll link it.

## Never leave a paper half-filed

Every other step runs while the Drive copy is waiting. Until it's done:
- **In the entry.** Add a line at the end of the Introduction in the Detailed description:
  `PDF pending: not in the Research papers folder yet.` Remove it once the file is linked.
- **On the Academic publications page.** A paper with no public link still gets its entry,
  as a bold title with no link (see `academic-publications-page.md`), swapped for the Drive
  link later.

If the user comes back later in the same chat (or says "the PDF is in Drive"), run "After
Done" from step 1.

## PDFs attached in Notion only

When the only copy of a paper is a PDF already attached in Notion, it still needs a Drive
copy. Notion file links point to Notion's file storage, which the session's network
usually can't reach. Ask the user to download the PDF from Notion and attach it to the
chat, then save it as above.
