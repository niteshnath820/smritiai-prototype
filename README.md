# SmritiAI — India's AI Decision Memory for Governments

**AI for Bharat Hackathon 2026** · Track: Smart Public Transport & Civic Infrastructure

> Governments should not repeat mistakes because people changed. SmritiAI ensures every public decision leaves behind intelligence — not just records.

---

## The Problem

Municipal bodies repeatedly repair the same roads, drains and utility lines because the reasoning behind each past decision — which contractor, which root cause, why a cheaper fix was chosen over a durable one — lives in disconnected tender PDFs, inspection notes and complaint logs, not in any system a new officer can query. Departmental transfers happen every 2–3 years; the paper trail does not travel with the person who understood it. The result is not missing data but missing **reasoning**.

## The Solution

SmritiAI ingests a municipality's maintenance reports, tenders, inspection notes and citizen complaints for a given asset, and builds a decision memory an officer can actually query:

1. **OCR** digitizes scanned tenders and inspection PDFs into structured text (PaddleOCR)
2. **Knowledge graph** links each decision to the asset, department, officer, cost and stated reason (Neo4j)
3. **Timeline reconstruction** orders these linked decisions chronologically per asset, surfacing repeat interventions
4. **Root-cause + recommendation engine** (LLM constrained to reason only over retrieved graph context) flags recurring failure patterns and drafts an evidence-backed recommendation, with an auditable savings calculation — not a bare number

**Initial scope:** one ward's road and drainage assets, proving the full pipeline end-to-end before scaling to new asset classes and departments.

## Why Not Just Use ChatGPT / Gemini / Claude?

A general-purpose LLM has no access to a municipality's fragmented tender files, inspection PDFs and complaint logs sitting unlinked across departments. The hard part SmritiAI solves is **data integration**, not language generation: OCR-ing legacy records, linking them to the correct physical asset over time, and constraining the reasoning step to only draw on that verified, linked history — so a recommendation is traceable back to the specific past decisions that justify it.

## This Repository

This repo contains the **working prototype** submitted for the Build Round: an interactive decision-memory dashboard demonstrating the full pipeline on three sample civic assets.

```
├── SmritiAI_Prototype.html   # Self-contained interactive prototype — open directly in a browser
└── README.md
```

### Running the prototype

No build step or dependencies required — it's a single static HTML file.

- **Locally:** download `SmritiAI_Prototype.html` and open it in Chrome or any modern browser
- **Live demo:** [add your hosted link here once deployed, e.g. via GitHub Pages or Netlify]

### What the prototype demonstrates

- Three sample civic assets (a high-risk road, a medium-risk storm drain, a healthy streetlight line) with full decision timelines spanning 2020–2026
- A rendered knowledge graph linking each asset to its decisions, department and root cause
- A live 5-stage pipeline animation (OCR → Graph → Timeline → Root cause → Recommendation)
- An AI recommendation card with a **"Show calculation" toggle** — the estimated savings figure is shown as an explicit, auditable calculation rather than an unexplained number

Asset records, timelines and the knowledge graph shown are a synthetic dataset standing in for real municipal tenders and inspection files, while formal data-sharing access with a municipality is arranged. The pipeline logic and savings calculation are wired to run on this dataset end-to-end, not hard-coded per asset.

## Proposed Tech Stack

| Layer | Component |
|---|---|
| Document ingestion | PaddleOCR, rule-based parsers for structured complaint logs |
| Knowledge graph | Neo4j |
| Temporal reasoning | Python service ordering linked decisions per asset |
| Recommendation engine | LLM (Gemma/Llama) + BGE embeddings for retrieval, NetworkX for pattern detection |
| Dashboard | React, Tailwind, MapLibre |
| Backend & infra | FastAPI, PostgreSQL + PostGIS, Docker |

## Impact & Scalability

- The same asset–decision–department graph schema extends from one ward to a full municipal corporation, and from roads/drainage to any asset class with a paper trail (water utilities, streetlights, public buildings)
- Reduces duplicated expenditure on repeat failures — a quiet but significant source of waste in municipal infrastructure spend
- Creates an audit trail that survives officer transfers, insulating institutional knowledge from being lost when the person who made a decision moves on

---

*Submitted for the AI for Bharat Hackathon 2026 — Smart Public Transport & Civic Infrastructure track.*
