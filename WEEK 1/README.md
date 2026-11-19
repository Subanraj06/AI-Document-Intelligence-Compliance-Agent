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

### Week 1 - Discovery, data, schema, baseline
- Requirements and exclusions: `docs/week-01/requirements.md`
- 15 synthetic sample documents: `data/samples/` (see `data/README.md`)
- Extraction schema: `backend/schemas/extraction.py`, `docs/week-01/extraction-schema.md`
- Manual labels: `data/labels/`
- Baseline scorecard: `docs/week-01/baseline-scorecard.md`
- Weekly report: `docs/week-01/WEEK_01_REPORT.md`

## Useful scripts (run from the project root)
    python scripts/generate_samples.py      # re-create the synthetic samples (needs scripts/requirements-dev.txt)
    python scripts/export_schema.py         # export the extraction JSON schema
    python scripts/baseline_scorecard.py    # rebuild the baseline scorecard

## Project structure
    backend/
      api/                  FastAPI routers
      config.py             settings from .env
      database/             SQLAlchemy engine/session
      schemas/              extraction.py (output schema), labels.py (manual label format)
      tests/
    data/                   synthetic samples, labels, ground-truth text, baseline timings
    docs/week-XX/           weekly evidence and reports
    scripts/                data generation and reporting scripts
