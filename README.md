# Batch PDF Scaler & A4 Resizer

A zero-backend, client-side web utility for standardizing mixed-size documents, irregular scans, and Letter-formatted PDFs into uniform A4 sheets or unified page widths. 

Runs 100% inside your browser using WebAssembly and JavaScript - no files are ever uploaded to a remote server.

Live Demo: [nekonyan.fun/PDF-Resizer](https://nekonyan.fun/PDF-Resizer)

---

## Why This Exists

1. **Broken Online Converters:** Standard web utilities attempt to deconstruct PDFs into HTML DOM nodes and reflow them. This causes character drift, overlapping text, missing font subsets, and displaced clipping masks.
2. **Slow Virtual Printers:** Tools like *Microsoft Print to PDF* or *Adobe PDF* freeze the machine on bulk tasks, require manual interaction per file, and spawn a viewer window for every single output.
3. **Paper Standard Mismatches:** Office workflows frequently mix Letter, legal documents, irregular scanner cuts, and receipts.

This tool embeds original pages as immutable vector objects (`/XObject`) and applies uniform affine transformations. The internal text layers, vector curves, and OCR scan masks scale together without distortion or font substitution.

---

## Key Features

- **Mode 1  -  Fit to A4 Canvas:** Centers each page inside a standard A4 canvas (210 × 297 mm) with user-defined margins and automatic portrait/landscape orientation matching.
- **Mode 2  -  Unify Width to A4:** Locks the width of all pages to 210 mm while calculating page heights proportionally to match each original page's aspect ratio.
- **Reorderable Queue:** Drag-and-drop handles (`☰`) to rearrange document sequence before merging or exporting.
- **Batch Export Options:**
  - **View in New Tab (`👁️`):** Instant in-memory blob preview in browser reader.
  - **Individual Download (`⬇️`):** Staggered downloads to avoid browser spam throttles.
  - **Download Combined PDF (`📑`):** Sequentially merges all processed PDFs into a single file.
  - **Download as ZIP (`📦`):** Bundles all converted outputs into an uncompressed archive.
- **Deep Directory & Archive Ingestion:** Drag and drop folders, loose PDFs, or `.zip` archives directly into the interface.

---

## Repository Structure

```text
PDF-Resizer/
├── index.html          # Standalone web application
├── pdf-lib.min.js      # Core PDF transformation engine (offline)
├── jszip.min.js        # Archive extraction engine (offline)
└── CNAME               # Custom domain configuration (if needed)

```

---

## Setup & Offline Dependencies

To make the app run 100% offline without CDN reliance:

### Windows (PowerShell)

```powershell
Invoke-WebRequest -Uri "[https://unpkg.com/pdf-lib/dist/pdf-lib.min.js](https://unpkg.com/pdf-lib/dist/pdf-lib.min.js)" -OutFile "pdf-lib.min.js"
Invoke-WebRequest -Uri "[https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js](https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js)" -OutFile "jszip.min.js"

```

### macOS / Linux (curl)

```bash
curl -L "[https://unpkg.com/pdf-lib/dist/pdf-lib.min.js](https://unpkg.com/pdf-lib/dist/pdf-lib.min.js)" -o pdf-lib.min.js
curl -L "[https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js](https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js)" -o jszip.min.js

```

---

## Local Development

Browsers apply security restrictions to directory drag-and-drop operations on `file:///` URLs. Run a local HTTP server for full folder-traversal capabilities:

```bash
# Python 3
python -m http.server 8000

```

Open your browser to `http://localhost:8000`.

---

## Deployment (GitHub Pages)

1. Push this repository to GitHub.
2. Go to **Settings** > **Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch` and select `main` / `/(root)`.
4. If using a custom domain, add your domain to the **Custom domain** field (or maintain a `CNAME` file in the root).

---

## Related Tools

* **[Anything to PDF](https://nekonyan.fun/anything-to-pdf):** Convert Word DOCX, spreadsheets, presentation slides, multi-page TIFFs, video storyboards, and iOS photos into PDF with 1:1 original dimensions preserved.

