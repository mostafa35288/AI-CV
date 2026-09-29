# 🤖 AI CV Screening & ATS Automation

An AI-powered CV screening and recruitment automation workflow built with **n8n**.

The system automatically retrieves candidate CVs, extracts their content, evaluates them against an AI/ML Engineer job description using an LLM, generates an ATS-style assessment, and stores the results back in Google Sheets.

---

## 📌 Overview

Recruitment teams often need to review a large number of CVs before identifying candidates who match a specific position.

This project automates the initial CV screening process using **n8n, Google Drive, Google Sheets, PDF extraction, and an AI Recruitment Agent**.

The workflow evaluates candidates based on job-related qualifications and produces a structured assessment containing:

- Candidate Score
- Strong Points
- Weak Points
- Skills Match
- Experience Match
- Education Match
- Job Fit
- Recruitment Decision
- Short Reasoning

---

## 🔄 Workflow Architecture

```text
                 ┌──────────────────┐
                 │  Schedule Trigger│
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │   Google Sheets  │
                 │ Get Candidates   │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │      Filter      │
                 │ Unprocessed CVs  │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │  Loop Candidates │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │   Google Drive   │
                 │   Download CV    │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │   PDF Extraction │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │   AI Recruiter   │
                 │    / ATS Agent   │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │ JavaScript Parser│
                 │ ATS Structuring  │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │  Update Google   │
                 │      Sheets      │
                 └──────────────────┘
🧠 AI Recruitment Agent

The AI Agent is configured to evaluate candidates for an:

AI / Machine Learning Engineer

position.

The evaluation focuses on job-related qualifications such as:

Technical Skills
Python
Machine Learning
Scikit-learn
Pandas
NumPy
SQL
Data Preprocessing
Model Training & Evaluation
Classification & Regression
Git
Preferred Skills
Deep Learning
TensorFlow / PyTorch
NLP
Computer Vision
XGBoost
LightGBM
CatBoost
Streamlit
Docker
Cloud Platforms
Experience

The system considers:

Relevant work experience
Academic projects
Internships
Freelance experience
Personal AI/ML projects
Responsibilities related to the target position
Education

The candidate's education is compared against the job requirements.

Projects

The system evaluates the relevance of projects and gives more importance to projects demonstrating practical experience with the required technologies.

📊 Candidate Scoring

The AI assessment uses the following weighting:

Evaluation Category	Weight
Technical Skills	40%
Relevant Experience	25%
Projects	15%
Education	10%
Job Requirements Match	10%
Total	100%

The candidate receives a score from 0 to 100 based on the evidence available in the CV.

🎯 Job Fit Classification

The system classifies candidates into:

Strong Fit
Good Fit
Partial Fit
Weak Fit
Not a Fit

The workflow also generates a recruitment recommendation:

Shortlist
Consider
Reject

Mandatory job requirements are treated as important constraints during the assessment.

⚙️ ATS Processing

After the AI Agent generates its assessment, a custom JavaScript Code node processes the response.

The code:

Extracts the candidate score.
Validates that the score is between 0 and 100.
Extracts the candidate's strong points.
Extracts weaknesses.
Extracts skills match.
Extracts experience match.
Extracts education match.
Normalizes the job-fit category.
Normalizes the recruitment recommendation.
Retrieves the Google Sheets row number.
Produces structured ATS output.

This allows the free-form AI response to be converted into structured data that can be stored in the ATS sheet.

🛠️ Tech Stack
n8n — Workflow automation
Google Sheets — Candidate database & ATS results
Google Drive — CV storage
PDF Extraction — Resume text extraction
n8n AI Agent — Candidate evaluation
OpenRouter — LLM provider
JavaScript — ATS parsing and validation
🤖 AI Model

The workflow uses an OpenRouter Chat Model connected to the n8n AI Agent.

Configured model:

nvidia/nemotron-3-super-120b-a12b:free
📂 Project Structure
ai-cv-screening-n8n/
│
├── workflow/
│   └── ai-cv-screening-ats.json
│
├── screenshots/
│   └── workflow.png
│
├── README.md
└── .gitignore
🚀 Setup
1. Import the Workflow

Open your n8n instance and import:

workflow/ai-cv-screening-ats.json
2. Connect Your Accounts

Configure your own:

Google Sheets credentials
Google Drive credentials
OpenRouter credentials
3. Configure Google Sheets

Create a candidate sheet containing the required fields for:

Candidate Name
CV
Score
Strong Points
Weak Points
Job Fit
Recommendation
4. Configure the Job Description

Modify the job description and evaluation criteria inside the AI Agent according to the position you want to screen for.

5. Test the Workflow

Upload sample CVs and execute the workflow.

The system will automatically process the candidates and write the assessment back to Google Sheets.

🔐 Security

Never upload sensitive credentials or private candidate information to GitHub.

Do not commit:

API Keys
OAuth Tokens
Passwords
Private Google Drive Links
Candidate CVs
Personal Candidate Information
Production Credentials

The workflow file in this repository is sanitized for public sharing.

You should connect your own credentials after importing the workflow.

⚠️ Important Note

This project is an AI-assisted recruitment automation and decision-support system.

AI-generated scores and recommendations should be reviewed by a qualified human before making employment decisions.

The system is designed to evaluate candidates based on job-related information and should not be used to make decisions based on protected or irrelevant personal characteristics.

🔮 Future Improvements
Multi-job-description support
Semantic CV-to-job matching
Structured LLM JSON output
Candidate ranking dashboard
Automated recruiter notifications
Interview scheduling
Advanced skill extraction
Duplicate candidate detection
Human approval workflow
Recruitment analytics dashboard
Candidate history and audit logs
👨‍💻 Author

Mostafa Mohamed

AI / Machine Learning Developer
