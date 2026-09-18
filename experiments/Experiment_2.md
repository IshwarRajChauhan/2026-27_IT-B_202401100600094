# Experiment 2

## Problem Identification and Feasibility: Software Design Principles

Identify the problem addressed by the selected software project and prepare its problem statement, objectives, scope, and technical and operational feasibility analysis.

**Course:** Software Design Principles (SDP)  
**Project Title:** AI-Based Resume Screening and Recruitment System  
**Class / Section:** IT-B (2026-27)  
**Prepared by:** Ramit Gupta (202401100600139)  
**Repository:** `https://github.com/IshwarRajChauhan/2026-27_IT-B_202401100600094`

### Team Members

| Name | Roll Number | Module |
|---|---|---|
| Ishwar Raj Chauhan (Team Leader) | 202401100600094 | Application Shell & Integration |
| Kartik Khandelwal | 202401100600099 | Embeddings & Vector Search |
| Ramit Gupta | 202401100600139 | Resume Ingestion & Parsing |
| Mukul Sharma | 202401100600116 | LLM Ranking & Justification |
| Nitin Kumar | 202401100600123 | Results UI, Export & Testing |

---


## Aim

To identify the problem addressed by the AI-Based Resume Screening and Recruitment System and prepare its problem statement, objectives, scope, and technical and operational feasibility analysis.

## Objectives

- Identify the real-world problem addressed by the software project.
- Prepare a clear problem statement.
- Define project objectives and scope.
- Perform technical and operational feasibility analysis.
- Evaluate the viability of the proposed solution.

## Introduction

Problem identification is the first step in software engineering. A well-defined problem statement and feasibility study ensure that the proposed software solution is practical, achievable and aligned with stakeholder requirements before development begins. For an AI-based system, feasibility must also consider the availability of models, data handling and the reliability of the generated output.

## Selected Project

Project Title: AI-Based Resume Screening and Recruitment System

Domain: Human Resources and Recruitment Technology

## Problem Statement

Recruiters receive hundreds of resumes for a single job opening and screen them manually, which is slow, tiring and inconsistent across reviewers. Keyword-based filters speed up this process but reject suitable candidates who describe the same skill in different words, and they give no explanation for their decisions.

The AI-Based Resume Screening and Recruitment System provides an automated screening platform where a recruiter uploads a batch of resumes along with a job description. The system parses the resumes, generates semantic embeddings using Hugging Face Sentence Transformers, stores them in the Pinecone vector database, and matches them against the job description by meaning rather than exact keywords. A Groq-hosted large language model then scores the top candidates and explains each score, and the recruiter reviews the ranked shortlist and exports the result.

## Project Objectives

- Provide bulk upload and parsing of resumes in PDF and DOCX formats.
- Generate semantic embeddings of resumes and job descriptions and match them using a vector database.
- Produce an AI-generated match score with matched skills, missing skills and a written justification.
- Present a ranked candidate shortlist that the recruiter can filter and review.
- Export the screening results as a CSV file.
- Protect candidate personal information and keep the final hiring decision with a human recruiter.

## Project Scope

The system supports recruiter login, bulk resume upload and parsing, job description input, masking of personal information, semantic matching using embeddings and a vector database, LLM-based scoring with justification, ranked shortlist display, recruiter status marking and CSV export. Session data is isolated per screening run and deleted after use.

Optical character recognition for scanned image resumes, integration with job portals or commercial Applicant Tracking Systems, interview scheduling, candidate communication and automatic rejection of candidates are outside the scope of this project.

## Technical Feasibility Analysis

| Factor | Assessment | Remarks |
|---|---|---|
| Technology | Feasible | Python, Streamlit, Git and GitHub support development |
| Resume Parsing | Feasible | PyPDF and python-docx extract text from text-based PDF and DOCX files |
| Embeddings | Feasible | Hugging Face Sentence Transformers models run on a normal CPU |
| Vector Database | Feasible | Pinecone provides managed similarity search with per-session namespaces |
| LLM Reasoning | Feasible | Groq API serves Llama-family models and supports JSON-formatted responses |
| Security | Feasible | API keys stored in environment files and personal data masked before LLM calls |
| Scalability | Feasible | Modular design and managed services support larger resume batches |

## Operational Feasibility Analysis

| Factor | Assessment | Remarks |
|---|---|---|
| User Acceptance | High | Simple upload and review workflow familiar to recruiters |
| Ease of Use | High | Minimal training required, screening completed in a few steps |
| Time Saving | High | First-level screening of large batches is much faster than manual reading |
| Transparency | High | Every score includes matched skills, missing skills and a justification |
| Human Control | High | System only recommends; the recruiter makes the final decision |
| Maintainability | High | Separate parsing, matching, ranking and interface modules simplify maintenance |

## Analysis

The feasibility study indicates that the AI-Based Resume Screening and Recruitment System is technically and operationally viable. The required libraries, models and managed services are available at free or project-scale usage limits, and the team's knowledge of Python and basic machine learning is sufficient for implementation.

The main risks are inconsistent LLM output, possible bias in evaluation and failure to extract text from scanned resumes. These are handled through structured prompts with low temperature, masking of personal information, clear flagging of unreadable files and mandatory human review of the shortlist.

## Observation

Clearly defining the problem, objectives, scope and feasibility provides a strong foundation for subsequent software design and development activities. For AI-based systems, treating explainability and data privacy as feasibility factors at this stage prevents costly redesign later.

## Result

The problem statement, objectives, project scope, and technical and operational feasibility analysis for the AI-Based Resume Screening and Recruitment System were successfully prepared.
