# Development notes

## Current architecture

Single-file browser application:

```text
PDF input
→ PDF.js text extraction
→ text-quality check
→ OCR fallback if required
→ relevance filtering
→ rules / Chrome AI / WebLLM / hybrid extraction
→ normalization and deduplication
→ medication table, timeline, exports
```

## UI/UX goals

- Keep default path safe and fast.
- Make local processing state visible.
- Show progress by phase.
- Preserve evidence for reviewer confidence.
- Avoid silent AI failures.

## Backend upgrade idea

Recommended backend structure:

```text
frontend/
  index.html
api/
  FastAPI extraction service
workers/
  OCR worker
  LLM normalization worker
db/
  SQLite/Postgres extraction jobs
```

## Next implementation steps

- Split single HTML into modular JS/CSS files.
- Add automated browser smoke tests.
- Add golden-output tests for sample PDFs.
- Add optional local backend endpoint.
- Add drug dictionary and synonym map.
- Add confidence scoring.
