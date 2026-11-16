# StudyDeck user guide

## 1. Start a class and deck

Open \`index.html\` or the published GitHub Pages site. Use **New class folder** in the left sidebar for a subject such as Biology, then **New deck name** beneath that class for a topic such as Cell Biology. Select the deck to study or modify it.

## 2. Add cards manually

Select **Add cards** and enter a front (prompt) and back (answer). You can attach an image or enter multiple structured pairs. The text importer recognizes formats such as:

\`\`\`text
Mitosis: Division of a cell into two daughter cells.
What does ATP stand for? | Adenosine triphosphate
Photosynthesis :: The process of converting light energy into chemical energy.
\`\`\`

The manual file importer accepts \`.txt\`, \`.md\`, and \`.csv\` for card pairs. Uploading an image in **Add cards** creates an image prompt to edit manually; to **read text from a picture**, use **Generate cards** instead.

## 3. Generate cards automatically

1. Open the desired deck and select **Generate cards**.
2. Paste lecture notes or upload supported files: PDF, DOCX, TXT, MD, CSV, or images including PNG/JPG/WEBP.
3. The app extracts text. Check and correct the extracted text in the text area.
4. Choose a maximum draft count (10, 30, or 60) and click **Generate drafts** if necessary.
5. Inspect the proposed front and back of each draft. Edit inaccurate wording and deselect unwanted drafts.
6. Click **Save selected cards to deck** (the button displays the selected count).

The card generator is rule-based and may produce few or imperfect cards from disconnected notes, complex formulas, charts, and drawings. For best results, provide complete factual sentences or clear \`term: definition\` pairs. OCR requires legible images; scanned PDF pages may be slower.

Limits: up to 12 uploaded files per batch, 18 MB per file, and the first 16 pages of each PDF. Only English OCR is configured. Internet access is needed to load document/OCR readers when they are not already available.

## 4. Study and repeat

Use **Study** for a deck and choose:

- **Study due cards** to focus on cards scheduled for review.
- **Study all** to review the complete deck regardless of due date.
- **Still learning only** to practice cards previously missed.

Read the question, click to flip, and choose **Know it** or **Still learning**. Missed cards rejoin your active queue. Known cards stay in the deck and return on future days as scheduled.

## 5. Manage a deck

Open **All cards** to search, edit, or delete cards. Deleting a card permanently removes its saved review history. Generated cards are regular deck cards; they do not depend on the uploaded source file after saving.

## 6. Export, restore, and change devices

Use **Export** to download a JSON backup of your classes, decks, and review history. Use **Restore** to load a backup, but be aware that restore **replaces the current library** rather than merging it. Export the current library before restoring another backup.

A downloaded HTML file, a GitHub Pages deployment, and different browsers generally use separate storage. To migrate, export from the old location, open the new location, then restore.

## 7. Troubleshooting

- **Nothing saved after refreshing:** browser storage may be disabled; export frequently and try a normal browser window.
- **Image has no text:** use a clear, uncropped image with high contrast and readable text.
- **PDF or DOCX import fails:** confirm internet access for on-demand libraries; try a TXT version of the notes.
- **OCR takes a while:** scanned pages must be rendered and read as images; use fewer or smaller pages.
- **Generated card is incorrect:** edit the draft or remove it before saving. This app does not check factual correctness.
- **No drafts appear:** try clear definitions, complete factual sentences, or \`question | answer\` pairs.