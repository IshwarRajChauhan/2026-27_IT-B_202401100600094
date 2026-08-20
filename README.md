# Project Title
AI-Based Resume Screening and Recruitment System

# Project Description
An AI-powered system that automates resume screening for recruiters. It parses uploaded resumes, generates embeddings using Hugging Face models, stores them in a vector database (Pinecone), and matches them against a given job description using semantic similarity. A Groq-powered LLM then ranks and justifies the top candidates based on skills, experience, and relevance — reducing manual screening time and improving shortlisting accuracy.

# Tech Stack
- **Frontend:** Streamlit
- **Backend:** Python
- **Embeddings:** Hugging Face Sentence Transformers
- **Vector Store:** Pinecone
- **LLM:** Groq (LLaMA)
- **Parsing:** PyPDF / python-docx

# Features
- Bulk resume upload (PDF/DOCX)
- Job description-based semantic matching
- AI-generated match score with reasoning
- Ranked candidate shortlist
- Exportable results (CSV)

