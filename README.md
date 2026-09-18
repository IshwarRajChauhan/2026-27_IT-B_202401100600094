# AI-Based Resume Screening and Recruitment System

An AI-powered system that helps recruiters screen resumes faster. It parses bulk resumes (PDF/DOCX), converts them into semantic embeddings, stores them in a vector database, matches them against a job description, and uses an LLM to score, rank and justify the best-fit candidates. The recruiter reviews the ranked shortlist and makes the final decision.

## Overview

Recruiters and campus placement cells still shortlist candidates by reading resumes one by one, or by using keyword-based filters that miss candidates who describe the same skill in different words. This project replaces that with a semantic screening workflow:

- The recruiter uploads a batch of resumes and pastes (or uploads) a job description.
- Resumes are parsed, cleaned and PII-masked, then split into chunks and embedded using Hugging Face Sentence Transformers.
- Embeddings are stored in Pinecone and matched against the job description using semantic (cosine) similarity.
- The top candidates are sent to a Groq-hosted Llama model, which returns a match score, matched and missing skills, and a short evidence-based justification.
- The recruiter reviews the ranked shortlist, marks candidate status, and exports the results as CSV.

The system **recommends**; it never auto-rejects a candidate. The final decision always stays with a human recruiter.

## Core Features

1. **Bulk Resume Upload & Parsing**: Upload many PDF/DOCX resumes at once. Text is extracted, cleaned and PII-masked. Files that cannot be parsed (e.g. scanned images) are flagged without stopping the batch.
2. **Job Description-Based Semantic Matching**: Resume chunks and the job description are embedded and compared in Pinecone, so "built REST APIs with FastAPI" can match "backend API development" even without exact keywords.
3. **AI-Generated Match Score with Reasoning**: A Groq-hosted LLM evaluates the top candidates and returns structured JSON: score (0–100), matched skills, missing skills and a justification grounded in the resume.
4. **Ranked Candidate Shortlist**: Candidates are ranked on a combined score (semantic similarity + LLM score). The recruiter can filter by score and mark each candidate as Shortlisted / On Hold / Rejected.
5. **Exportable Results (CSV)**: The full ranked table, including recruiter decisions, can be downloaded as a CSV file.

## System Architecture

```text
                    Recruiter (Web Browser)
                              |
                              v
                 +-------------------------+
                 |   Streamlit Web App     |
                 |  (upload, JD, results)  |
                 +------------+------------+
                              |
      +-----------------------+------------------------+
      |                       |                        |
      v                       v                        v
+-------------+     +-------------------+     +-------------------+
|  Resume     |     |  Embedding &      |     |  LLM Ranking &    |
|  Parser     |---->|  Matching Module  |---->|  Justification    |
| (PyPDF,     |     | (Sentence-        |     |  Module           |
| python-docx,|     |  Transformers)    |     |  (Groq API)       |
| PII masking)|     +---------+---------+     +---------+---------+
+-------------+               |                         |
                              v                         v
                    +-------------------+     +-------------------+
                    |     Pinecone      |     |  Ranked Shortlist |
                    |  (vector index,   |     |  + CSV Export     |
                    |  per-session      |     +-------------------+
                    |  namespaces)      |
                    +-------------------+
```

- **Frontend:** Streamlit (single web app with upload, job description input, and results views).
- **Parsing:** PyPDF for PDF files, python-docx for DOCX files, followed by text cleaning and PII masking.
- **Embeddings:** Hugging Face Sentence Transformers (e.g. `all-MiniLM-L6-v2`, 384-dimensional vectors).
- **Vector store:** Pinecone serverless index (cosine metric). Each screening session uses its own namespace so batches never mix.
- **LLM:** Llama-family model served through the Groq API, prompted to return strict JSON.
- **Export:** pandas DataFrame to CSV.
- **Config & secrets:** `.env` locally / `.streamlit/secrets.toml` on deployment (both are git-ignored).

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| Backend | Python 3.13 |
| Package / env management | uv |
| Resume parsing | PyPDF, python-docx |
| Embeddings | Hugging Face Sentence Transformers |
| Vector database | Pinecone |
| LLM | Groq API (Llama-family model) |
| Data handling & export | pandas (CSV) |
| Testing | pytest |
| Version control | Git / GitHub |

## Data Model (high level)

`Recruiter -> ScreeningSession -> JobDescription`
`ScreeningSession -> Resume -> ResumeChunk (vector stored in Pinecone)`
`Resume -> CandidateEvaluation (semantic score, LLM score, matched/missing skills, justification, recruiter status)`

## Team & Roles

| Name | Roll Number | Module | Responsibilities |
|---|---|---|---|
| Ishwar Raj Chauhan (Team Leader) | 202401100600094 | Application Shell & Integration | Repository setup, Streamlit app structure, recruiter login and session management, module integration, release/deployment |
| Kartik Khandelwal | 202401100600099 | Embeddings & Vector Search | Chunking strategy, Sentence Transformer embeddings, Pinecone index and namespaces, job description matching and score aggregation |
| Ramit Gupta | 202401100600139 | Resume Ingestion & Parsing | PDF/DOCX text extraction, text cleaning, PII masking, duplicate detection, parsing report UI |
| Mukul Sharma | 202401100600116 | LLM Ranking & Justification | Groq prompt design, strict JSON output and validation, retries and rate-limit handling, combined scoring |
| Nitin Kumar | 202401100600123 | Results UI, Export & Testing | Results dashboard, candidate status, CSV export, pytest suite, evaluation on a labelled resume set |

## Lab Documentation

The Software Design Principles experiments for this project are in `experiments/`, with the analysis model images in `docs/diagrams/`.

| Experiment | Document | Prepared by |
|---|---|---|
| Experiment 2 | Problem Identification and Feasibility | Ramit Gupta |
| Experiment 3 | Requirement Gathering and User Stories | Nitin Kumar |
| Experiment 4 | Software Requirements Specification (SRS) | Mukul Sharma |
| Repository setup & README | Project overview and structure | Ishwar Raj Chauhan |
| Architecture diagrams | DFD, use case, ER and sequence diagrams | Kartik Khandelwal |

Each experiment is available in `experiments/` as both Markdown (`.md`, renders on GitHub) and Word (`.docx`, for the lab file) — for example `experiments/Experiment_4.md` and `experiments/Experiment_4.docx`.

## Project Structure

```text
2026-27_IT-B_202401100600094/
├── docs/
│   └── diagrams/            # SRS analysis model images (DFD, use case, ER, sequence)
├── experiments/             # Software Design Principles lab experiments (.md + .docx)
│   ├── Experiment_2.md      # problem identification and feasibility
│   ├── Experiment_2.docx
│   ├── Experiment_3.md      # requirement gathering
│   ├── Experiment_3.docx
│   ├── Experiment_4.md      # software requirements specification (SRS)
│   └── Experiment_4.docx
├── src/                     # application source code
│   └── resume_screener/     # (planned) parsing/, matching/, ranking/, ui/
├── test/                    # unit and integration tests (pytest)
├── main.py                  # uv entry point (placeholder)
├── pyproject.toml           # project metadata and dependencies
├── .python-version          # Python 3.13
├── .env.example             # required environment variables
├── .gitignore
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.13
- [uv](https://docs.astral.sh/uv/)
- Git
- A Pinecone API key and a Groq API key

### Setup

```bash
git clone https://github.com/IshwarRajChauhan/2026-27_IT-B_202401100600094.git
cd 2026-27_IT-B_202401100600094

# Install dependencies into the project environment
uv sync
uv add streamlit sentence-transformers pinecone groq pypdf python-docx pandas python-dotenv
uv add --dev pytest

# Configure secrets
cp .env.example .env   # then fill in your own keys
```

### Run (once the Streamlit app module is added)

```bash
uv run streamlit run src/resume_screener/app.py
```

Never commit `.env` or `.streamlit/secrets.toml`. Both are already listed in `.gitignore`.

## Branching Strategy

- `main`: stable, reviewed work only
- `dev`: integration branch for application code
- `feature/<module>-<short-description>`: one branch per coding task, e.g. `feature/parsing-pii-masking` (PR into `dev`)
- `experiment-<n>-<short-name>`: one branch per lab experiment, e.g. `experiment-3-requirements` (PR into `main`)

Each member commits from their own GitHub account. Every PR needs at least one review from another team member before merging.

## Responsible AI

- PII such as email addresses, phone numbers and profile links is masked before any text is sent to the LLM.
- The LLM is instructed to evaluate only job-relevant evidence and to ignore protected attributes (gender, age, religion, caste, marital status, photo, etc.).
- Every score comes with a justification, so recruiters can see *why* a candidate was ranked.
- The system only recommends. It never rejects a candidate automatically.

## Status

- [x] Repository and uv project setup
- [x] Experiment 2: Problem identification and feasibility
- [x] Experiment 3: Requirement gathering and user stories
- [x] Experiment 4: Software Requirements Specification (SRS)
- [ ] Resume parsing and PII masking module
- [ ] Embedding and Pinecone matching module
- [ ] LLM ranking and justification module
- [ ] Streamlit UI and CSV export
- [ ] Testing and evaluation
- [ ] Deployment

## License

To be decided by the team (e.g., MIT).
