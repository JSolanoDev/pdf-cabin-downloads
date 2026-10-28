# PDF Cabin user guide

[Back to the project](../README.md)

## Online edition

Choose **Use online** on the [website](https://pdf-cabin.pages.dev/)
to work in your browser without installation. Adding text/images, page tools,
forms, comments, visual signatures, exports, and English OCR run on your device.
The online edition does not upload documents or contact a PDF editing server.
The **Edit** tool also replaces original PDF text and images locally through
PDFium WebAssembly. Double-click or double-tap text to type on the page; Enter
applies, Escape cancels. Images can be replaced, resized, moved and deleted.
The side panel provides font, size and color controls. Save your files
before closing or refreshing the browser tab; recent files last for the session.

## Home and creation

Home opens by default with recent session documents, stars, file search, and
recommended tools. Recent documents are kept in memory for this browser session;
refreshing the app does not restore them. Choose **Create → Blank canvas** for a
white PDF page, or **Select Files** to combine PNG, JPEG, and PDF files.

In the page organizer, drag thumbnails to reorder and use the corner trash icon
to delete. The organizer remains open for these operations. Form-aware copying
preserves fillable fields; imported field names are renamed when they collide.

## Theme and visual editing

Use the upper-right Dark mode / Light mode button on Home or in the document
workspace to change themes. Both controls stay synchronized. The preference
is saved in this browser; the initial theme follows the operating system.
PDF pages keep their original colors in either theme.

Choose **Edit a PDF** or the top **Edit** workspace. Click an outlined existing
text/image object, change it in the left inspector, and choose **Apply changes**.
Nearby horizontal text fragments with matching style and baseline are grouped
into editable lines, including PDFs that store separate objects for each letter.
Use **Edit individual text fragments** to select the original runs when needed.
Grouping keeps widely separated columns and differently styled text separate;
it is geometric inference and does not provide paragraph reflow.

Drag existing text/images to preview their position; releasing applies the move.
Delete or the selection trash icon removes the selected object. Other inspector
changes use **Apply changes**. Undo restores applied changes.

Text replacement, size, color, font choice, movement, deletion, and image
replacement/resizing modify the actual PDF page objects. The original text object
is changed or replaced, not hidden under a white rectangle or another text layer.
Existing fonts are kept by default; explicit standard-font substitutions are
available when the original font cannot encode the requested text.

Use **Add text & images** under View more for the separate staged content-adding
canvas. It supports placement, drag movement, text size/color, images and deletion
before applying additions. Added text there uses standard Latin Helvetica.

Direct editing currently handles top-level text runs and images in PDFs up to
30 MB. It does not reflow paragraphs, edit nested form XObjects, replace scanned
image text, or guarantee arbitrary embedded/subset font support. Unsupported
font encoding is rejected when the engine detects a text mismatch. Keep the
original or select a supported replacement font. Object deletion is not secure
redaction or hidden-data sanitization.

Browser checks verified theme persistence, visual text placement and formatting,
text export from the edited PDF, and undo. Image/rotated-page fidelity still needs
broader representative-document testing.

## Scan and reading tools

**Scan & OCR** recognizes English text on the current page or every page and
downloads a text file with confidence scores. Recognition runs locally using
Tesseract.js (Apache-2.0). It does not create a searchable PDF layer or edit scan
content. Review OCR accuracy, especially on handwriting or complex layouts.

The first `npm run dev` or `npm run build` prepares bundled worker/WASM assets and
downloads the English language model from tessdata.projectnaptha.com. Thereafter
the app serves OCR assets locally. The production browser test recognized text
from an image-only PDF with no external network requests. Engine assets are
generated under ignored `public/ocr/`; they retain their own license notices.

Use **Organize pages** to select, rotate, duplicate, delete, reorder or open a
page using thumbnails; **Fit page width** sizes the page. **Find text or tools**
filters the available tools, and Enter opens text search with the query filled.
Existing safe web/mail links and internal PDF destinations are clickable, and
Bookmarks lists existing document outlines. Arrow keys navigate, Ctrl/Cmd+F opens
document search, and Ctrl/Cmd+S downloads a copy outside editable inputs/dialogs.

Run `npm test` for transformation checks. With Playwright and Chrome available,
serve the production build on port 5174 and run `node tests/browser-ocr.cjs`.
Set PLAYWRIGHT_MODULE to an absolute Playwright package path if needed.

## Renaming documents

Double-click a document tab name or a recent-file name on Home to rename it.
Home renaming stays on the dashboard, including for closed recent documents.
Names receive a `.pdf` extension automatically. Enter opens a focused recent
file; F2 opens its rename dialog. Renaming participates in document Undo/Redo.
Saving a renamed document uses the new name and asks for a new file target;
this does not rename the original disk file in place.

## Tabs and saving

Opening or creating a PDF adds a separate document tab. Tabs retain their own
document, selected page, zoom and undo/redo history. Close buttons work on active
and inactive tabs. Dirty documents show a dot and offer Save a copy and close,
Close without saving, or Cancel. Reloading with unsaved work invokes the browser's
standard leave-page confirmation. Sessions are in memory, not persisted across a
reload.

**Save a copy** downloads the edited bytes. **Save to file** (also the disk icon)
uses the browser's File System Access API to choose a target, which can be the
original PDF. After permission is granted, subsequent saves in that tab write to
the chosen handle. Browsers without that API fall back to a download. Native file
chooser/overwrite prompts are controlled by the browser and require the user.

Hold **Ctrl** and scroll up/down to zoom the PDF while keeping the app interface
at its normal size. Scrolling without Ctrl scrolls normally.

## Undo and Redo

Use the visible **Undo** / **Redo** buttons in the top bar. Undo uses Ctrl+Z;
Redo uses Ctrl+Y or Ctrl+Shift+Z (Command+Z / Command+Shift+Z on macOS).
Each document has its own last 15 applied changes. A new edit clears its Redo
history. Text inputs keep their native typing shortcuts; unapplied inspector
values are protected separately when navigating away.
