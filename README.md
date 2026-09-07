# Intelligent-Resume-Screening-and-Job-Recommendation-System# Intelligent Resume Screening and Job Recommendation System

An NLP-based system that automatically screens resumes against job descriptions and recommends the best-matching candidates for each job, using sentence embeddings and cosine similarity.

## Overview

Manually screening hundreds of resumes for every job opening is slow and inconsistent. This project automates that process: it reads a collection of resumes and a set of job descriptions, converts both into semantic vector representations, and ranks candidates by how closely their resume matches each job — going beyond simple keyword matching to capture actual meaning and context.

## Features

- **Automated resume parsing** — supports both pre-extracted resume text (CSV) and raw PDF resumes
- **Text preprocessing** — cleaning, stopword removal, and optional skills/education-section extraction
- **Semantic embeddings** — uses a pretrained Sentence-Transformer model (`all-MiniLM-L6-v2`) instead of simple keyword/TF-IDF matching
- **Similarity-based ranking** — cosine similarity between job and resume embeddings to score every candidate
- **Top-N recommendations** — outputs the best-matching resumes for each job posting
- **Exportable results** — saves rankings to a CSV file for further use

## Dataset

- **Resumes**: [Resume Dataset (Kaggle)](https://www.kaggle.com/datasets/snehaanbhawal/resume-dataset) — resumes labeled by job category (`ID`, `Resume_str`, `Category`), also available as raw PDFs organized by category.
- **Job Descriptions**: a CSV of job postings with a title and description column (any job-descriptions dataset works — column names are configurable).

## Tech Stack

| Component | Tool/Library |
|---|---|
| Language | Python 3 |
| Data handling | pandas, numpy |
| Text preprocessing | nltk |
| Embeddings | sentence-transformers (`all-MiniLM-L6-v2`) |
| Similarity scoring | scikit-learn (cosine similarity) |
| PDF parsing | pypdf |
| Environment | Google Colab / Jupyter |

## How It Works

1. **Load data** — read resumes and job descriptions into pandas DataFrames.
2. **Preprocess text** — lowercase, remove punctuation/numbers, remove stopwords.
3. **Generate embeddings** — encode both resumes and job descriptions into dense vectors using a Sentence-Transformer model.
4. **Compute similarity** — build a job × resume cosine similarity matrix.
5. **Rank & recommend** — for each job, sort resumes by similarity score and return the top N matches.
6. **Export results** — save the final rankings to `resume_job_matches.csv`.

## Project Structure

```
Intelligent-Resume-Screening/
│
├── Resume.csv                     # Resume dataset (ID, Category, Resume_str)
├── job_descriptions.csv           # Job postings (title + description)
├── resume_job_matching.ipynb      # Main notebook (Colab/Jupyter)
├── resume_job_matches.csv         # Output: ranked matches (generated after running)
└── README.md
```

## Getting Started

1. Open `resume_job_matching.ipynb` in Google Colab or Jupyter.
2. Install dependencies:
   ```
   pip install sentence-transformers pypdf nltk pandas numpy scikit-learn
   ```
3. Upload `Resume.csv` and `job_descriptions.csv` (or update the paths in the notebook to point to your files).
4. Run all cells in order — the notebook will:
   - Clean and embed the text
   - Compute similarity scores
   - Print the top matching resumes for each job
   - Save results to `resume_job_matches.csv`

## Sample Output

```
Job #0: Data Scientist
----------------------------------------------------------------
   ID         Category   similarity
 10298   Information-Technology   0.812
 22315   Information-Technology   0.789
 18734   Engineering               0.754
```

## Future Improvements

- Extract structured fields (skills, education, experience) separately for more targeted matching
- Add a scoring breakdown (skills match %, experience match %, education match %)
- Fine-tune the embedding model on resume/job data for domain-specific accuracy
- Build a simple web interface (Streamlit/Flask) for recruiters to upload resumes and get instant recommendations
- Add bias/fairness checks to ensure the system doesn't favor specific demographics unintentionally

## License

This project is intended for educational and research purposes.
