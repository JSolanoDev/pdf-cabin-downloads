# Desktop and online document tools

The editions share the document workspace and tool implementations. Original
text/image edits use PDFium 156.0.8076.0: a local authenticated Python service on
desktop, and a bundled WebAssembly engine in a browser worker online. PDF bytes
are not uploaded to a remote editing service. The engine and its notices are
included in the offline web-app cache and Android assets.

Both support original text replacement, on-page typing, font/size/color controls,
image replacement/resizing, drag movement, deletion, grouped text runs and history.
They also share creation/import/merge, page organization/extraction, forms,
comments/highlights, stamps, signatures, OCR, exports, search and text comparison.

Platform integration differs. Browser Save to file uses the File System Access
API where available and otherwise downloads a copy. Android uses its Save As
picker. Desktop has native menus; online uses toolbar controls and shortcuts.
Printing follows the browser/OS (native mobile exports to the device's file app).
These are platform interfaces, not claims of access to browser-restricted OS APIs.

The same editing limits apply: 30 MB direct-edit input, top-level text/images,
single text runs, supported glyphs and no automatic paragraph reflow. Nested form
XObjects and scanned text replacement remain unsupported. Platform substitutes
for non-embedded fonts can have different ink bounds; original glyph support and
device memory vary. This is feature coverage, not universal PDF fidelity.

The WASM archive is checksum-pinned in legal/browser-engine.json. Build preparation
fails on a changed archive or missing notices. Original runtime source, PDFium and
component notices, provenance, and loader adaptation details ship with the app.
