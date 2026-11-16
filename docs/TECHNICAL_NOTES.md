# Technical notes

## Architecture

StudyDeck is a single-page web app with HTML, CSS, and JavaScript in one file. `index.html` and `studydeck_auto_generate.html` are identical standalone entry points. There is no build pipeline, service worker, server, authentication, cloud database, or paid AI API.

Core functionality includes class/deck navigation, card editing, study queue management, due scheduling, text/image import, browser storage, and JSON backup/restore.

## Persistence

The app stores a versioned top-level state object containing `classes[]`, each with `decks[]`, each with `cards[]`. Cards have an ID, front, back, optional image data, and review metadata such as `seen`, `streak`, `misses`, `status`, `due`, and `interval`.

Storage prefers IndexedDB (`StudyDeckDatabase` with the `state` object store) and falls back to localStorage when necessary. If both fail, the UI warns that saving is unavailable. This is **per-browser/per-origin persistence**, not synchronization.

Images attached to cards are resized/compressed before being stored. Large backups or too many attached images can still approach browser quota limits.

## Review algorithm

- Known streaks map to due intervals `[1, 3, 7, 14, 30, 60, 120]` days, capped at the last entry.
- Missed cards have their streak reset, are marked `learning`, are due after approximately 10 minutes, and are appended to the current active queue.
- Starting a due review selects cards with no due date or a due date in the past. Other modes select all or learning cards.

This is intentionally simple: there is no FSRS/SM-2 parameter estimation or performance analysis.

## Import and generation pipeline

1. File selection or drag/drop triggers a client-side extractor.
2. TXT/MD/CSV uses native file text reading.
3. DOCX uses Mammoth.js.
4. PDF uses PDF.js. The first 16 pages are read; pages with insufficient embedded text are rendered and passed through OCR.
5. Images use Tesseract.js OCR in English.
6. Extracted text is presented for revision, then parsed into `term: definition`, `question | answer`, and other recognizable structures. Sentence-pattern and cloze rules propose additional Q/A drafts.
7. The user can edit, select, and save drafts, with duplicate filtering against the chosen deck.

On-demand scripts currently load from:

- PDF.js 3.11.174: https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/
- Tesseract.js 6: https://cdn.jsdelivr.net/npm/tesseract.js@6/dist/tesseract.min.js
- Mammoth 1.13.0: https://cdn.jsdelivr.net/npm/mammoth@1.13.0/mammoth.browser.min.js

The code is not bundled, so availability and behavior of those third-party CDNs is outside this repository's control. Live OCR/PDF/DOCX loading was not fully end-to-end verified in the initial version; test on intended browsers before depending on it for coursework.

## Security and privacy considerations

- User-entered flashcard content persists locally in the selected browser profile, unless the user exports it.
- The app does not intentionally send uploaded notes to a model/API, but third-party scripts and OCR language resources are downloaded over the network.
- GitHub Pages deployment publishes the **code**, not the user's locally stored cards or notes.
- Backups contain the user's study content and may include image data. Handle backup files accordingly.
- Like any site, browser storage can be cleared and is not a substitute for backups.

## Suggested future improvements

- Replace the rule-based Q/A generator with an optional, opt-in AI provider, with clear handling of costs and content privacy.
- Add an in-app migration/export format validator and merge-import mode.
- Add automated tests for extraction, due scheduling, and restore behavior.
- Add optional cloud sync/account storage only with explicit user consent.
- Consider bundling and pinning dependencies, a CSP, and offline-first caching for a reproducible deployment.

## Maintaining the repository

When editing the application, update **both** `index.html` and `studydeck_auto_generate.html` or remove the duplicate standalone file as part of an intentional migration. The original file is preserved so that earlier shared links and downloads remain easy to identify.