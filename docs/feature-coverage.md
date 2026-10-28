# PDF Cabin feature coverage

Reference inventory: Adobe's current feature overview,
https://www.adobe.com/acrobat/features and desktop overview,
https://helpx.adobe.com/acrobat/desktop/get-started/learn-the-basics/overview.html
(consulted 2026-10-26). Categories below are an implementation roadmap, not a
claim of exhaustive equivalence across Adobe plans, platforms or integrations.

| Category | PDF Cabin status | Remaining work |
| --- | --- | --- |
| View / navigate / zoom | Selectable text, tabs with close/dirty prompts, page navigation/thumbnails, fit width, shortcuts, themes, existing bookmarks/links | Persistent sessions, more reading modes, accessibility |
| Find / export text | Text PDF export/search and English OCR text export | Layout-preserving exports, OCR search integration |
| Organize pages | Thumbnail organizer with drag reorder, hover delete, select/rotate/duplicate/open; insert, merge, extract ranges | Bulk selection, split into multiple files, page labels |
| Create PDF | Blank white documents, PNG/JPEG conversion, and combining PDF/image files | Office, HTML, scanner integrations |
| Edit content | Actual top-level text/image object replacement, double-click on-page text editing with live preview, font size/color, movement, deletion, image resize; added text/images | Paragraph reflow, nested form XObjects, universal font matching, scanned text replacement, link authoring |
| Crop | Crop box editing | Interactive crop handles; cropping does not erase content |
| Stamps | Watermarks, headers, footers, prefix + sequential numbering | Alignment, font/style controls, full Bates options |
| Forms | Inline text/checkbox/dropdown filling; dialog filling; create text fields/checkboxes/dropdowns; flatten | Radio authoring, validation, calculations, XFA |
| Export | Current page PNG/JPEG, document plain text, PDF | JPEG batches, Word/Excel/PowerPoint, PDF/A |
| Properties | Title, author, subject | Full metadata inspection and sanitization |
| History / save | Per-tab 15-edit undo/redo, downloads, browser Save-to-file API | Persistent sessions, large-document memory optimization |
| Review | Native PDF Text comments and Highlight annotations; list/remove; flattened visual highlights | Change existing comments, replies, review stamps, measurements |
| OCR / scans | English local OCR to text, current/all pages | More languages, deskew, searchable PDF layer |
| Compare | Page-aligned text comparison | Layout/image comparison engine |
| Redact / sanitize | Not implemented | Actual object/pixel removal and hidden-data verification |
| Protect | Not implemented | Encryption, permissions, password workflows |
| Sign | Drawn signature images | Cryptographic signatures, validation, timestamps |
| Compress | Not implemented | Image downsampling, resource deduplication, optimization controls |
| Accessibility / prepress | Not implemented | Tags, reading order, validation, print production |
| Print | All-page raster print preview (108 DPI) | Vector printing, paper-size controls |
| Cloud collaboration / signature requests | Not implemented | Backend, accounts, storage, sharing, audit trails |
| AI assistant / document spaces | Not implemented | Retrieval, model integrations, consent and document permissions |
| Desktop / mobile / integrations | Windows/Linux/macOS Electron packages with bundled engine, signed Android APK and offline Home Screen web app for iOS/Android | Trusted Windows signing, macOS notarization, app-store publication, auto-update, file associations and third-party integrations |

Use `node --test tests/tools.test.js` for transformation tests and `npm run build`
for production compilation. These checks do not establish comprehensive PDF
fidelity or Acrobat parity. Test representative documents before relying on edits.
All content placement uses unrotated PDF coordinates in points. Standard Latin
fonts are supported for added text. Signed originals should be retained.

The online and desktop editions now share these document tools, including
original-content editing. See [edition parity](edition-parity.md) for the local
WASM/native engines, browser/OS integration differences and common limitations.

## Additional implemented tools

- Text comparison: page-aligned extracted text, whitespace normalization,
  changed/added/removed page statuses, and downloadable JSON report. Does not
  inspect visual differences or make scanned pages searchable.
- Signature drawing: transparent PNG placement with user-selected position/width.
  Not cryptographic signing or identity verification.
- Form authoring: checkboxes and dropdowns, removal of named fields, JSON export
  of supported field values. Other form gaps in the table still apply.
- Navigation/export: direct page jump, reverse page order, current-page JPEG.
