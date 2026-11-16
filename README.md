# StudyDeck

A lightweight, local-first flashcard study app inspired by the core flashcard workflow in Quizlet. StudyDeck runs as a standalone HTML page without an account, server, build tools, or an API key. It organizes cards into class folders and decks, remembers which cards you know, and can make editable flashcard drafts from lecture notes, screenshots, and textbook pages.

![StudyDeck Generate Cards screen](assets/studydeck-generate-preview.png)

## Features

- **Class folders and decks:** keep subjects and study sets separate.
- **Flashcard reviews:** flip each card, then choose **Know it** or **Still learning**. Missed cards repeat within the current study session, and all cards retain their review history for future sessions.
- **Review scheduling:** known cards return after increasing day-based intervals; missed cards are due again sooner.
- **Automatic draft generation:** create questions and answers from pasted notes, `.txt`, `.md`, `.csv`, `.docx`, `.pdf`, and image files (such as screenshots or textbook photos). Preview and edit drafts before saving to the current deck.
- **Manual editing and importing:** enter cards yourself, import structured question/answer text, edit or delete existing cards, and attach images to cards.
- **Local data and backups:** saved cards use IndexedDB where available, with a localStorage fallback. Export and restore a JSON backup.

## Run locally

1. Download or clone this repository.
2. Open [`index.html`](index.html) in a recent browser. You can also open the standalone [`studydeck_auto_generate.html`](studydeck_auto_generate.html); both contain the same app.
3. Create a class folder, then a deck.
4. Use **Add cards** for manual entry or **Generate cards** to import notes and build drafts.
5. Review drafts, save the selected ones, and start studying.

No package installation, build step, or login is required.

> **Back up your cards.** Saved cards belong to the browser and site origin that created them. Opening the local file, another browser, or the GitHub Pages version can produce separate libraries. Export a JSON backup from the original location and restore it in the new one.

## Generate cards from files

In a deck, open **Generate cards** and drop files, choose files, or paste notes. StudyDeck extracts readable text, proposes question/answer pairs using local rules, and shows editable drafts. You can select which drafts to keep. New cards are inserted into the selected deck without resetting existing cards' review history.

| File type | Extraction path |
| --- | --- |
| TXT / Markdown / CSV | Browser text reader |
| DOCX | Mammoth.js text extraction |
| PDF with selectable text | PDF.js text extraction |
| Scanned PDF / PNG / JPG / WEBP images | Tesseract.js OCR |

The generation step is **rule-based, not a hosted AI model**. Output quality varies. Always proofread the extracted text, questions, and answers, especially after OCR.

To keep memory use manageable, the importer limits files to **12 per batch**, **18 MB each**, and **the first 16 pages per PDF**. The generation selector offers 10, 30, or 60 draft cards. Source text may be truncated on very large inputs.

PDF/DOCX/OCR features load their libraries on demand from external CDNs and may require internet access on first use. The current app does not intentionally upload your notes or flashcards to an AI service. CDN requests still contact third-party hosts to fetch library code and OCR language resources.

## Review behavior

- **Know it:** increases the review streak and schedules the card after 1, 3, 7, 14, 30, 60, or 120 days, depending on streak.
- **Still learning:** resets the streak, schedules a new due time about 10 minutes later, and puts the same card back into the current study session queue.
- **Study modes:** due cards, all cards, or still-learning cards.

This is a simple spaced-review heuristic, not a validated memory-learning algorithm.

## Deploy on GitHub Pages

The site is static. With the files committed to your repository:

1. Open repository **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Select the default branch (usually `main`) and **/(root)**, then save.
4. Open the GitHub Pages URL shown in the Pages settings once publishing completes.

GitHub Pages hosts the app itself. It does **not** store or sync the cards saved in each visitor's browser.

## Documentation

- [User guide](docs/USER_GUIDE.md): using decks, imports, reviews, and backups.
- [Technical notes](docs/TECHNICAL_NOTES.md): structure, dependencies, data model, and limitations.

## Privacy, reliability, and limitations

- Browser data may be lost when clearing site data, using private browsing, encountering storage limits, or switching devices. Export backups regularly.
- PDF/image text extraction is imperfect, particularly for diagrams, dense tables, handwriting, small fonts, or blurry photos.
- No account, cloud sync, multi-user access, or server-side storage is included.
- Automatic drafts may be incomplete or misleading; verify them against the source notes before study.
- The app is an early standalone version. PDF, DOCX, and OCR integration paths were tested with simulated readers, but live third-party library loading was not fully verified.
- This repository does not declare a software license; add one if you want to grant reuse or contribution rights.

## Project files

```text
index.html                          GitHub Pages entry point
studydeck_auto_generate.html       Original standalone app file
docs/USER_GUIDE.md                 End-user instructions
docs/TECHNICAL_NOTES.md            Implementation and limitations
assets/studydeck-generate-preview.png  Screenshot
```

---

coded by chatgpt 6-astra