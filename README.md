# BhashaLens OCR

[BhashaLens OCR](https://probablyshubham.github.io/BhashaLens/) is a static, client-side web app for converting PDFs and DOCX files into clean UTF-8 `.txt` files. It is designed for English plus Indian regional languages and mixed-language document archives.

## What it does

- Converts `.pdf` and `.docx` files to `.txt`.
- Keeps the same base filenames, changing only the extension to `.txt`.
- Exports bulk results as one ZIP file.
- Uses fast PDF embedded-text extraction first.
- Uses Tesseract.js OCR when pages are scanned, empty, or likely garbled.
- Lets users select OCR languages such as English, Hindi, Assamese, Bengali, Gujarati, Kannada, Malayalam, Marathi, Nepali, Odia, Punjabi, Sanskrit, Tamil, Telugu, Urdu, and Sinhala.
- Runs document processing in the browser. Files and extracted text are not uploaded by the app.

## Privacy note

All document processing happens client-side in the user's browser. No PDF, DOCX, or extracted TXT content is sent to a server by this app.

The default HTML version loads open-source JavaScript, WebAssembly, and OCR language data from public CDNs. For a fully offline or high-security deployment, download those dependencies locally and update the `<script>` and Tesseract paths in `index.html`.

## How the extraction pipeline works

1. **PDF.js text layer extraction** reads embedded text from digital PDFs.
2. **Legibility scoring** checks each extracted PDF page for empty text, replacement characters, private-use glyphs, and common Indic mojibake patterns.
3. **Tesseract.js OCR fallback** renders suspicious pages to a canvas and recognizes the selected languages in a WebAssembly worker.
4. **DOCX raw text extraction** uses Mammoth.js.
5. **ZIP export** packages each `.txt` file plus `_BhashaLens_Extraction_Report.txt`.

## How to publish on GitHub Pages

1. Rename `bhashalens-ocr.html` to `index.html`.
2. Add `index.html` to a GitHub repository.
3. In the repository settings, enable GitHub Pages from the branch containing `index.html`.
4. Share the GitHub Pages URL.

The page includes a **Download this HTML** button so users can save the tool and use it personally without browsing the GitHub repository.

## Usage tips

- Use **Smart hybrid** mode for most archives.
- Use **Fast text only** for born-digital PDFs that already contain clean Unicode text.
- Use **Deep OCR every page** for scans, unreadable text layers, or older PDFs with broken custom fonts.
- Select only the languages present in the document. Selecting every language can slow OCR and reduce accuracy.
- Increase OCR render scale for faint, low-resolution, or photocopied scans.

## Known limitations

- Password-protected PDFs cannot be processed unless the browser library can open them.
- Very large PDFs can be slow because OCR happens locally on the user's device.
- OCR quality depends on scan resolution, page skew, contrast, font quality, and the selected language models.
- The default single-file deployment is not fully offline because it loads libraries and language data from CDNs.
