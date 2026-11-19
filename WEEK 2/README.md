# AI Document Intelligence & Compliance Agent (Module 1)

Document ingestion and review assistant for contracts, SLAs and business documents:
traceable extraction, obligation tracking and human review. **Not legal advice.**

## Run
    python -m venv venv
    venv\Scripts\activate          (Windows)   |   source venv/bin/activate  (Mac/Linux)
    pip install -r backend/requirements.txt
    uvicorn backend.main:app --reload

Open http://127.0.0.1:8000/docs

## Test
    python -m pytest -v

## Progress

| Week | Dates | Status | Evidence |
|---|---|---|---|
| 1 | 04 - 10 Nov 2026 | Done | `docs/week-01/` |
| 2 | 11 - 17 Nov 2026 | Done | `docs/week-02/` |

### Week 1 - Discovery, data, schema, baseline
- Requirements and exclusions: `docs/week-01/requirements.md`
- 15 synthetic sample documents: `data/samples/` (see `data/README.md`)
- Extraction schema: `backend/schemas/extraction.py`, `docs/week-01/extraction-schema.md`
- Manual labels: `data/labels/`
- Baseline scorecard: `docs/week-01/baseline-scorecard.md`
- Weekly report: `docs/week-01/WEEK_01_REPORT.md`

### Week 2 - Ingestion, parsing, storage, OCR review
- Upload API (PDF / DOCX / TXT) with validation, duplicate detection and versioning: `backend/api/documents.py`
- Page-level parsers: `backend/document_processing/parsers.py`; scanned-page check: `quality.py`
- Metadata DB (documents, versions, pages): `backend/models/document.py`
- API guide: `docs/week-02/ingestion-api.md`
- Parsing quality report (scanned PDF / OCR assessment): `docs/week-02/parsing-quality-report.md`
- Weekly report: `docs/week-02/WEEK_02_REPORT.md`

## API (so far)
| Method | Path | Purpose |
|---|---|---|
| GET | `/health` | Health check |
| POST | `/documents` | Upload a document |
| GET | `/documents` | List documents |
| GET | `/documents/{id}` | Document with all versions |
| POST | `/documents/{id}/versions` | Upload a new version |
| GET | `/documents/{id}/text?version=N` | Parsed text per page |

## Useful scripts (run from the project root)
    python scripts/generate_samples.py      # re-create the synthetic samples (needs scripts/requirements-dev.txt)
    python scripts/export_schema.py         # export the extraction JSON schema
    python scripts/baseline_scorecard.py    # rebuild the baseline scorecard
    python scripts/parsing_quality_report.py  # parsing quality + OCR assessment (OCR needs Tesseract installed)

## Project structure
    backend/
      api/                  FastAPI routers (health, documents)
      config.py             settings from .env
      database/             SQLAlchemy engine/session
      document_processing/  parsers (PDF/DOCX/TXT) and scanned-page check
      models/               database tables
      schemas/              extraction.py (output schema), labels.py (manual labels), document.py (API models)
      services/             ingestion, versioning and file storage
      tests/
    uploads/                stored uploaded files (created at runtime, ignored by Git)
    data/                   synthetic samples, labels, ground-truth text, baseline timings
    docs/week-XX/           weekly evidence and reports
    scripts/                data generation and reporting scripts
