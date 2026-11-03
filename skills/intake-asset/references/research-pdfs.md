# Research PDFs: saving them to Drive (Whitepaper / Research only)

**Folder:** Sofar Marketing shared drive / Resource Library / Research papers
**Folder link:** https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2
**Folder id:** `1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2` (shared drive id `1TLcetYMT79Gi2mNF05HOi8-6eWoqv9JqVOo`)

Every research PDF the library holds lives in this one folder, and the Resource Library
entry points to it through **Drive Link**. That keeps the file somewhere the whole company
can open it, instead of in a chat upload or a Notion attachment.

## When to save a PDF

Only for Content Type "Whitepaper / Research", and only when one of these is true:
- The user provided the paper as a PDF (uploaded or attached).
- The paper exists only as a PDF, with no public web page or DOI to link to.

Don't go looking for a PDF when the paper has a public link, and don't download one from a
publisher site. A link alone is a complete entry. If the user gives both a link and a PDF,
save the PDF and keep the link in Link.

## Field rules

| Field | Rule |
|---|---|
| Drive Link | The Drive file's view link (`https://drive.google.com/file/d/<id>/view`). |
| Link | The paper's public link (DOI link first, otherwise the publisher page). If it has none, put the Drive link here too, because the library opens Link when someone clicks the card. |
| Publicly Shareable? | Set "No" when the paper is paywalled (the saved PDF is a licensed copy that can't go to customers). Otherwise leave it empty, as for every asset. |

This is the one case where the skill sets Drive Link and Publicly Shareable? without being
asked.

## File name

`<year> - <title>.pdf`, for example
`2025 - Observations and Simulations of the Effects of Infragravity Wave Reflection on Runup at a Rock-Reef-Fronted Dissipative Beach.pdf`.

- The year is the publication year (the same date as Last Updated).
- Use the paper's real title, from the PDF itself if the file name doesn't give it.
- Remove characters file systems reject (`/ \ : * ? " < > |`), collapse repeated spaces,
  and keep the whole name under 180 characters.
- Before saving, check the folder for a file with the same name or the same title. If one
  is there, don't save a second copy. Use the existing file's link and say so.

## Path A: the synced folder (preferred)

Use this when the session has a shell on the user's computer (the remote device tools:
load them with ToolSearch "device bash list dir request folder access") and the user has
Google Drive for desktop with the Sofar Marketing shared drive.

1. **Find the folder.** Check the session's connected folders (the device info tool). If
   "Research papers" is already connected, it is mounted in the device shell at
   `$HOME/mnt/Research papers`. If not, look for it on the user's computer:
   - Mac: `~/Library/CloudStorage/GoogleDrive-<their work email>/Shared drives/Sofar Marketing/Resource Library/Research papers`
   - Windows: usually `G:\Shared drives\Sofar Marketing\Resource Library\Research papers`
     (the drive letter can differ).
   Confirm it exists with the device list-dir tool, then request access to that exact
   folder once, with a one-line reason. If it doesn't exist, use Path B.
2. **Get the PDF onto the computer.**
   - A file the user uploaded to the chat sits in the cloud workspace. Send it with the
     send-file tool, then write it into the folder with the device commit-files tool,
     under the file name above.
   - A file already in another connected folder on the computer: copy it in the device
     shell with `cp -n` (never plain `cp` or `mv`, which can overwrite).
   - A PDF that is only attached in Notion: see "PDFs attached in Notion" below.
3. **Find it in Drive.** Load the Google Drive connector (ToolSearch "google drive search
   files") and search `parentId = '1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2'`. A new file
   usually appears within a minute or two (large files take longer). Wait and search again
   a few times before giving up. Use the result's `viewUrl` as Drive Link.
4. If the file never appears (Drive for desktop paused or signed out), finish the entry
   without Drive Link and tell the user the file is in their synced folder but hasn't
   uploaded yet. Offer to fill Drive Link once it has.

## Path B: manual upload (no synced folder)

Use this when there's no shell on the user's computer, the folder isn't on their computer,
or they'd rather upload it themselves. Give them these steps, word for word apart from the
file name:

> Please upload the PDF to our Research papers folder in Google Drive:
> 1. Open https://drive.google.com/drive/folders/1Na-_eW7X415pCbLRkVHvx2Hv6BXthTG2
> 2. Click **New**, then **File upload**, and choose the PDF. (Or drag the file into the
>    folder window.)
> 3. Rename it to: `<the file name>`
> 4. Reply here when it's uploaded, or paste its link (right-click the file, then
>    **Share**, then **Copy link**).
>
> If the link says you don't have access, ask the marketing team to add you to the Sofar
> Marketing shared drive.

Then file the Resource Library entry right away rather than waiting. When the user
replies, find the file with the Google Drive search above (or use the link they pasted)
and update the entry's Drive Link, and Link too if the paper has no public link.

If they'd like the folder on their computer for next time: in Google Drive for desktop,
sign in with their Sofar Google account (Settings, then **Add another account** if a
personal account is already signed in). Shared drives then appear in Finder or File
Explorer under Google Drive, in **Shared drives**. A personal account only shows My Drive.

## PDFs attached in Notion

Notion file links point to Notion's file storage on Amazon S3, which the session's network
proxy blocks from both the cloud workspace and the device shell. The built-in browser on
the user's computer can reach it, so:

1. Get a fresh signed link with the Notion get-file-download-urls tool (links expire after
   about five minutes).
2. Open it in the built-in browser and trigger a download to the user's Downloads folder
   (fetch the file in the page, then click a temporary download link with the original
   file name).
3. With the user's permission for Downloads access and for removing files there, copy the
   file into the Research papers folder under the new name, check the copy matches
   (`cmp`), then remove the copy in Downloads.

Ask before downloading, and say which files and roughly how large they are. Never remove
anything else from Downloads.

## Report line

Say one of:
- "Saved the PDF to Research papers as `<file name>` and set Drive Link: <link>".
- "Used the PDF already in Research papers (`<file name>`): <link>".
- "Waiting on the PDF upload: Drive Link is empty until it's in Research papers."

When no PDF was involved, say nothing about PDFs.
