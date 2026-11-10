# Research PDFs: Drive copy plus a Notion attachment (Whitepaper / Research only)

**Folder:** Sofar Marketing shared drive / Resource Library / Research papers
**Folder link:** https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2
**Folder id:** `1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2` (shared drive id `1TLcetYMT79Gi2mNF05HOi8-6eWoqv9JqVOo`)

When someone gives you a research paper as a PDF, it ends up in two places:
1. **Drive (the master copy).** One file in the Research papers folder. The Resource
   Library entry's **Drive Link** points to it, which powers the library's Download button.
2. **Notion (an attached copy).** The same PDF attached in one place, so people can open
   it without leaving Notion and Notion search and AI can read it:
   - under the paper's entry on the Academic publications page, when the paper goes on
     that page (third-party research), or
   - at the top of the Resource Library entry's page body, when it doesn't (for example a
     Sofar white paper).
   One attachment per paper, so if it has to be done by hand it is a single step.

The person filing should never have to know any of this. Do the steps, and only ask them
to act when a step can't be done from the session, with exact, short instructions.

## When this applies

Only for Content Type "Whitepaper / Research", and only when one of these is true:
- The user provided the paper as a PDF (uploaded or attached).
- The paper exists only as a PDF, with no public web page or DOI to link to.

Don't go looking for a PDF when the paper has a public link, and don't download one from a
publisher site. A link alone is a complete entry. If the user gives both a link and a PDF,
do both steps below and keep the public link in Link.

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
  file's link and say so.

Use the same file name for the Notion attachment.

## Step 1: save to Drive

Try these in order and use the first that works.

**Path A: the Google Drive connector (PDFs up to about 3 MB).** Connector calls can carry
files up to about 3.1 MB, so check the size first (`stat -c %s`). If the PDF is over
3,000,000 bytes, skip straight to Path B or C without trying. Otherwise load the Drive
connector's create-file tool (ToolSearch "google drive create file") and upload the PDF
straight into the folder:
- `title`: the file name above
- `parentId`: `1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2`
- `contentMimeType`: `application/pdf`, and `disableConversionToGoogleType`: true
- `base64Content`: a file reference, not typed base64. Copy the PDF to a path with a plain
  name in the scratchpad, compute its SHA-256 (`sha256sum`), and pass
  `sha256:<64 lowercase hex>:<absolute path>`. The app fills in the content when the user
  approves the call, so tell them in one line that they'll be asked to approve an upload
  to the Research papers folder.
Use the returned file's view link as Drive Link. If the call fails because the user can't
write to the folder, say so plainly and go to Path C (they may need to be added to the
Sofar Marketing shared drive).

**Path B: the synced folder.** Use this when Path A isn't possible (no Drive connector,
or the PDF is over 3 MB) and the session has a shell on the user's computer with Google
Drive for desktop. Otherwise go straight to Path C. If "Research papers" is already a connected folder, it is at
`$HOME/mnt/Research papers` in the device shell. Otherwise it is usually at
`~/Library/CloudStorage/GoogleDrive-<their work email>/Shared drives/Sofar Marketing/Resource Library/Research papers`
on a Mac, or `G:\Shared drives\Sofar Marketing\Resource Library\Research papers` on
Windows. Confirm it exists, request access to that exact folder once, then write the file
with the device commit-files tool (or `cp -n` in the device shell, never plain `cp` or
`mv`). Find it in Drive with the search above; a new file usually appears within a minute
or two. If access is declined or the file never appears, go to Path C.

**Path C: the user uploads it.** Give these steps, word for word apart from the file name:

> Please upload the PDF to our Research papers folder in Google Drive:
> 1. Open https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2
> 2. Click **New**, then **File upload**, and choose the PDF. (Or drag the file into the
>    folder window.)
> 3. Rename it (right-click, **Rename**), select the whole name including ".pdf", and
>    paste: `<the file name>`
> 4. Reply here when it's uploaded, or paste its link (right-click the file, then
>    **Share**, then **Copy link**).
>
> If the link says you don't have access, ask the marketing team to add you to the Sofar
> Marketing shared drive.

Don't wait for the reply: finish every other step now and mark the Drive copy as pending
(see "Never leave a paper half-filed"). When the user replies, find the file (Drive
get-file-metadata on the pasted link's id, or the folder search), check it's in the
Research papers folder, and fix the name with the Drive update-file tool if it differs
(for example a doubled ".pdf.pdf"). Then fill in Drive Link (and Link, if the paper has no
public link) and update the pending note.

## Step 2: attach it in Notion

Do this after the Resource Library entry exists and, for third-party research, after the
Academic publications page entry is written, so you know exactly where the file goes.

1. Create an upload with the Notion create-file-upload tool (ToolSearch "notion file
   upload"), using the file name above and `application/pdf`.
2. Send the PDF to the returned `upload_url` in one multipart POST from the session's
   shell: `curl -sS -X POST "<upload_url>" -H "authorization: <value from upload_headers>"
   -F "file=@<path>;type=application/pdf"`. Include every header the tool returned.
   Never print or repeat the authorization value to the user.
   - If the cloud shell can't reach the upload URL (a proxy 403, a connection refused or a
     "not allowed" network error), and the PDF is in a folder connected to the user's
     computer, try the same command once in the device shell.
   - Don't try anything else (no other hosts, no public file links). If neither shell can
     send it, go to the drag-in fallback below.
3. Place the file with a targeted edit, using the `markdown_source` the upload returns:
   - **Academic publications page:** a file block on its own line directly under the
     entry's title line, before its AI Summary toggle, the same way existing entries with
     PDFs look:
     ```
     [Title](URL) \[<i>not peer reviewed</i>\]

     <file source="file-upload://..." />

     <toggle>
     ...
     ```
   - **Resource Library entry:** the file block as the first block of the entry's page
     body.
4. Fetch once to confirm the file block is there.

**Drag-in fallback.** When the upload can't be sent, tell the user in one short paragraph,
with a link to the exact place:

> I couldn't attach the PDF in Notion from this session, so it needs one quick drag:
> open <link to the Academic publications page or the Resource Library entry>, find
> "<paper title>" under <year> / <heading>, and drag the PDF onto the empty line just
> below the title (above "AI Summary").

Use the Resource Library wording ("drag the PDF onto the top of the page") when the
attachment belongs there. Then mark it as pending (below).

## Never leave a paper half-filed

Every step still runs when another one is waiting on the user. Anything not finished is
recorded in two places until it is done:
- **In the entry.** Add a line at the end of the Introduction in the Detailed description:
  `PDF pending: <what's missing, e.g. "Drive copy not uploaded yet" or "not attached on the
  Academic publications page yet">.` Remove the line once it's done.
- **In the report.** End with a short "Still to do" list, one line per pending item, each
  with the exact step and the link. Leave the list out when nothing is pending.

When the user later says it's done (or pastes the Drive link), check it (search Drive, or
fetch the page for the file block), fill in any field that was waiting, and remove the
pending line.

## PDFs attached in Notion only

When the only copy of a paper is a PDF already attached in Notion, it still needs a Drive
copy. Notion file links point to Notion's file storage, which the session's network
usually can't reach. The built-in browser on the user's computer can:

1. Get a fresh signed link with the Notion get-file-download-urls tool (links expire after
   about five minutes).
2. Open it in the built-in browser and trigger a download to the user's Downloads folder
   (fetch the file in the page, then click a temporary download link with the original
   file name).
3. With the user's permission for Downloads access and for removing files there, copy the
   file into the Research papers folder under the new name, check the copy matches
   (`cmp`), then remove the copy in Downloads.

Ask before downloading, and say which files and roughly how large they are. Never remove
anything else from Downloads. If that isn't possible, ask the user to download the PDF
from Notion and attach it to the chat, then save it as in Step 1.

## Report lines

For the Drive copy, say one of:
- "Saved the PDF to Research papers as `<file name>`: <link>".
- "Used the PDF already in Research papers (`<file name>`): <link>".
- "Drive copy pending: upload steps above."

For the Notion attachment, say one of:
- "Attached the PDF on <the Academic publications page / the Resource Library entry>".
- "PDF attachment pending: one drag-in step above."

When no PDF was involved, say nothing about PDFs.
