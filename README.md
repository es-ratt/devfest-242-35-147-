# TenderFlow — Tender Document Package Builder

## 5-line plan
1. Load and validate any tender `requirements.json` without hardcoded tender data.
2. Add files locally, reject invalid/damaged PDFs, count pages, and detect SHA-256 duplicates.
3. Match each file to one requirement and collect expiry dates where required.
4. Recompute exact blocking statuses after every change and keep Generate disabled until ready.
5. Build and download one ordered PDF with an English cover and a split footer.

## Files

- `index.html` — semantic app shell and workflow layout.
- `style.css` — responsive TenderFlow-inspired light/dark visual system.
- `i18n.js` — complete English/Bangla UI copy plus persistent theme and language settings.
- `app.js` — validation, matching, hashing, statuses, and pdf-lib package generation.

## How to run

Open `index.html` in the latest Google Chrome, or serve this folder with any static file server. The only external script is pdf-lib 1.17.1 from cdnjs, as specified by the contest prompt.

Use the header toggle to switch between Light and Dark mode. The preference is saved in `localStorage` and restored on refresh.

## PDF footer

The generated package keeps the tender ID on the left side of the footer and shows only the current page number on the right side, for example:

```text
TEST-2026-001                                      Page 1
```

## How to test

- Load a valid `requirements.json` and verify numeric order and tender details.
- Load malformed JSON or missing fields and verify a bilingual error.
- Upload an expired document, a document expiring exactly on the deadline, and a missing mandatory document.
- Leave an optional document without a file and verify `Not provided` is non-blocking.
- Upload duplicate files with different names and verify the duplicate label and one-match restriction.
- Upload a PNG or a renamed non-PDF and verify it is rejected by extension and `%PDF-` header.
- Try a damaged/password-protected PDF and verify the app does not crash.
- Switch between বাংলা and English and verify the entire UI changes; reload and verify persistence.
- Switch Light/Dark mode and reload to verify theme persistence.
- Generate a package and check cover metadata, document order, split footer, page count, and footer separation from source content.
