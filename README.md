# Extraction

Browser-only PDF medication extraction prototype.

## App

Open:

```text
index.html
```

Alternative original filename:

```text
extraktor_v3_ocr_full.html
```

## Features

- PDF.js text extraction
- OCR fallback for image-only PDFs
- Tesseract.js OCR path
- Rules-only extraction mode
- Chrome Built-in AI mode where available
- WebLLM mode where compatible
- Safer WebGPU/WebLLM fallback after shader errors
- Hybrid extraction mode
- Medication table
- Medication bullet output
- Medication timeline
- JSON / CSV / Markdown export
- Colored status progress bar
- Evidence, extracted text, raw AI, and performance panels
- Local settings persistence
- Five synthetic sample PDFs for testing

## Test dataset

```text
sample_pdfs/
├── 01_text_current_medications.pdf
├── 02_text_stopped_medications.pdf
├── 03_text_german_mixed_medications.pdf
├── 04_image_only_scanned_med_list.pdf
└── 05_image_only_discharge_scan.pdf
```

The first three PDFs have a text layer. The last two are image-only scans intended for OCR fallback testing.

Expected values are documented in:

```text
dataset_manifest.json
```

## Recommended test order

1. Open `index.html` in a desktop browser.
2. Test `Rules only` with `01_text_current_medications.pdf`.
3. Test OCR fallback with `04_image_only_scanned_med_list.pdf`.
4. Try `Hybrid`.
5. Try Chrome Built-in AI if the browser supports it.
6. Try WebLLM only if WebGPU works on your browser/GPU.

## Known WebLLM issue

Some browser/GPU combinations fail with errors like:

```text
Invalid ShaderModule ... entryPoint: "index_kernel"
```

This is a WebGPU/WebLLM shader compilation problem, not a PDF or OCR problem. The app now catches this and falls back to rules where possible.

## Local serving

Some browsers block module/CDN behavior from `file://`. Run a simple local server if needed:

```bash
python3 -m http.server 8080
```

Then open:

```text
http://localhost:8080
```

## Production/backend optimization path

For a stronger production architecture:

- Add a backend service with FastAPI
- Add OCR worker queue
- Add local Ollama or server-side inference endpoint
- Add deterministic drug dictionary
- Add robust date normalization
- Store extraction jobs in SQLite/Postgres
- Add clinician review/approval workflow
- Stream progress with SSE or WebSocket

## Clinical warning

This is a prototype. It is not a medical device. Clinical review is required before using any extracted output.
