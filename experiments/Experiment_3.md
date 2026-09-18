# Experiment 3: Software Design Principles

Identify stakeholders and perform requirement elicitation for the selected software project using suitable techniques such as interviews, questionnaires, observation, or user personas; prepare user stories and the Requirement Gathering Report.

**Course:** Software Design Principles (SDP)  
**Project Title:** AI-Based Resume Screening and Recruitment System  
**Class / Section:** IT-B (2026-27)  
**Prepared by:** Nitin Kumar (202401100600123)  
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

To identify stakeholders and perform requirement elicitation for the AI-Based Resume Screening and Recruitment System using suitable elicitation techniques, prepare user stories, and develop a Requirement Gathering Report.

## Objectives

- Identify key stakeholders of the AI-Based Resume Screening and Recruitment System.
- Apply requirement elicitation techniques.
- Gather functional and non-functional requirements.
- Prepare user stories with acceptance criteria.
- Document the Requirement Gathering Report.

## Introduction

Requirement elicitation is the process of discovering stakeholder needs and expectations. The quality of software depends on how accurately user requirements are captured. Common elicitation techniques include interviews, questionnaires, observation, workshops and user personas. For an AI-based screening system, elicitation must also capture expectations about accuracy, explainability, fairness and the protection of candidate data.

## Selected Project

Project Title: AI-Based Resume Screening and Recruitment System

Domain: Human Resources and Recruitment Technology

## Stakeholder Identification

| Stakeholder | Role | Requirements |
|---|---|---|
| Recruiter / HR Executive | Uploads resumes and runs screening | Fast bulk screening with accurate and explainable ranking |
| Hiring Manager | Reviews the shortlist prepared by HR | Relevant candidates with visible matched and missing skills |
| Job Applicant | Candidate whose resume is evaluated | Fair evaluation on skills and protection of personal data |
| Training and Placement Cell | Screens student resumes for campus drives | Quick filtering of large resume batches against company criteria |
| System Administrator | Maintains the application and configuration | Secure API key handling and configurable models and settings |
| External AI Services | Provide vector search and LLM inference | Correct API usage within rate and usage limits |

## Requirement Elicitation Techniques

| Technique | Purpose | Outcome |
|---|---|---|
| Interview | Discuss the screening workflow and pain points with recruiters | Detailed functional requirements |
| Questionnaire | Collect feedback from multiple HR users and placement coordinators | User expectations and feature priorities |
| Observation | Observe manual shortlisting of sample resumes against a job description | Usability and workflow requirements |
| Document Analysis | Study sample resumes, job descriptions and keyword filter behaviour | Input formats and matching requirements |
| User Persona | Model representative users | User-centred requirements |

## Sample Requirement Gathering

Interview Findings:

- Recruiters want to screen a full batch of resumes in one run instead of one file at a time.
- Recruiters need to know why a candidate was ranked high or low before trusting the result.
- Hiring managers prefer a shortlist that clearly lists matched and missing skills.
- Recruiters want to record their own decision for each candidate and export the shortlist.

Observation Findings:

- Reviewers first look for required skills, then relevant experience, then projects and certifications.
- Different reviewers apply slightly different criteria to the same resume, causing inconsistency.
- Most screening time is spent on clearly unsuitable resumes that could be filtered earlier.

Questionnaire Findings:

- Explainability and data privacy are the highest priorities for users.
- Users prefer a simple workflow with minimal configuration.
- Spreadsheet export is expected for sharing the shortlist with hiring managers.

Document Analysis Findings:

- Resumes are received mainly as PDF and DOCX files with varied layouts.
- Some PDF resumes are scanned images and contain no extractable text.
- Job descriptions mix mandatory skills, preferred skills and experience in free text.
- Keyword filters depend on exact terms and miss synonyms and related technologies.

## Functional Requirements

| ID | Requirement | Description |
|---|---|---|
| FR1 | Recruiter Login | Only authenticated recruiters can access screening features |
| FR2 | Bulk Resume Upload | Multiple PDF and DOCX resumes can be uploaded in one batch |
| FR3 | Resume Parsing | Text is extracted and cleaned, and unreadable files are flagged |
| FR4 | Data Masking | Personal information is masked before storage and before LLM evaluation |
| FR5 | Job Description Input | Job description can be pasted or uploaded for the screening session |
| FR6 | Embedding and Indexing | Resume chunks are embedded and stored in the vector database |
| FR7 | Semantic Matching | Resumes are matched with the job description and scored by similarity |
| FR8 | LLM Evaluation | Top candidates receive a match score, matched skills, missing skills and justification |
| FR9 | Ranked Shortlist | Candidates are displayed in ranked order with filtering |
| FR10 | Recruiter Decision | Recruiter can mark each candidate as shortlisted, on hold or rejected |
| FR11 | CSV Export | Ranked results and decisions can be downloaded as a CSV file |
| FR12 | Session Cleanup | Session data is deleted from the vector database when the session ends |

## Non-Functional Requirements

| ID | Category | Requirement |
|---|---|---|
| NFR1 | Performance | A batch of resumes is parsed, embedded and matched within a few minutes |
| NFR2 | Reliability | One unreadable file must not stop processing of the remaining files |
| NFR3 | Availability | If the LLM service fails, ranking falls back to semantic similarity only |
| NFR4 | Security | API keys are stored in environment or secrets files, never in source code |
| NFR5 | Privacy | Candidate personal information is masked before it is sent to external services |
| NFR6 | Fairness | Protected attributes must not influence the score |
| NFR7 | Explainability | Every AI score is accompanied by skills evidence and a justification |
| NFR8 | Usability | The complete screening workflow requires only a few simple steps |
| NFR9 | Maintainability | Parsing, matching, ranking and interface are separate modules |
| NFR10 | Scalability | Batch processing and a managed vector database support larger volumes |

## User Personas

| Persona | Age | Goal | Pain Point |
|---|---|---|---|
| HR Executive | 29 | Shortlist the best candidates from a large batch quickly | Hours spent reading unsuitable resumes |
| Hiring Manager | 38 | Receive a small, relevant shortlist with clear reasons | Shortlists lack context about skill gaps |
| Placement Coordinator | 32 | Match many student resumes to company criteria before a drive | Very large volumes and tight deadlines |
| Job Applicant | 22 | Be evaluated fairly on skills and projects | Automated filters reject resumes over wording |

## User Stories

| ID | User Story | Acceptance Criteria |
|---|---|---|
| US1 | As a recruiter, I want to log in securely so that only authorised users can screen resumes. | Valid credentials grant access and invalid credentials are rejected with a generic message. |
| US2 | As a recruiter, I want to upload many resumes at once so that I can screen a batch together. | Multiple PDF and DOCX files are accepted and unsupported files are rejected with a clear message. |
| US3 | As a recruiter, I want unreadable resumes to be flagged so that I can review them manually. | Files with no extractable text are listed as parse failed and the remaining files continue processing. |
| US4 | As a recruiter, I want to enter a job description so that candidates are matched against the correct role. | Job description can be pasted or uploaded and a very short description triggers a warning. |
| US5 | As a recruiter, I want candidates ranked by relevance so that I can review the best matches first. | Results are displayed in descending order of final score. |
| US6 | As a hiring manager, I want to see matched and missing skills so that I can judge the fit quickly. | Each evaluated candidate displays matched skills and missing skills. |
| US7 | As a recruiter, I want a justification for each score so that I can trust the ranking. | Each evaluated candidate has a short justification based on resume content. |
| US8 | As a recruiter, I want to mark candidate decisions so that my shortlist is recorded. | Status can be set to shortlisted, on hold or rejected and is shown in the results table. |
| US9 | As a recruiter, I want to export the results as CSV so that I can share them with the hiring manager. | The downloaded file contains rank, scores, skills, justification and status for each candidate. |
| US10 | As a job applicant, I want my personal details hidden from the AI so that I am judged only on job-relevant information. | Email addresses, phone numbers and profile links are masked before evaluation. |

## Requirement Gathering Report

The elicitation process identified bulk resume upload and parsing, masking of personal data, semantic matching with the job description, LLM-based scoring with justification, ranked shortlist display, recruiter decision recording and CSV export as the primary requirements. Stakeholder feedback emphasised speed, explainability, fairness, protection of candidate data and human control over the final hiring decision. The main constraints identified were varied resume layouts, scanned resumes without extractable text and usage limits of external AI services.

## Observation

Using multiple elicitation techniques improves requirement completeness and reduces ambiguity. Document analysis exposes technical constraints such as unreadable resume formats, while interviews, questionnaires and personas bring out user-centred needs such as trust, transparency and fairness, which are especially important for AI systems that influence hiring opportunities.

## Result

Stakeholders were identified, requirements were elicited using suitable techniques, user personas and user stories with acceptance criteria were prepared, and the Requirement Gathering Report for the AI-Based Resume Screening and Recruitment System was successfully completed.
