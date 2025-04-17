# Automated Resume Review Agent

This project provides an end-to-end, agentic pipeline for automatically processing resumes submitted via email, scoring them on key criteria, and sending personalized feedback emails—all powered by Python and open-source tools.

## Features

* Email Retrieval: Connects to a Gmail inbox via IMAP and downloads new PDF/DOCX resume attachments.

* Parsing & Masking: Extracts plaintext from each resume and redacts personal email addresses to ensure blind review.

* Heuristic Scoring: Computes sub-scores for:

Work Experience

Education

AI‑related Keywords

Job Description (JD) match via TF‑IDF similarity

Formatting & Clarity

* LLM Feedback Generation: Uses a local Hugging Face model (e.g., Falcon) to craft concise, professional feedback emails based on the computed scores.

* Email Delivery: Sends the generated feedback back to each candidate via SMTP.

* Logging & Tracking: Maintains a CSV log of processed resumes and email statuses.

## Repository Structure

* Assignment_agentic.ipynb # Main pipeline notebook
* requirements.txt       # Python dependencies
* README.md              # This file

## Requirements

Python 3.8+

GPU recommended for LLM inference (Colab GPU runtime or local CUDA-enabled GPU)

Gmail account with App Password (requires 2FA enabled)

Hugging Face account (for private models) or any open-source LLM ID

## Installation and Usage (Google Colab)

1- Prepare credentials:

Create a file secrets.json in your working directory with the following structure:

{
  "email": "you@gmail[dot]com",
  "app_password": "your_app_password",
  "hf_model_id": "tiiuae/falcon-7b",
  "hf_token": "hf_xxx"
}

Important: Do not commit secrets.json to version control.

2- Open notebooks/Asignment_agentic.ipynb in Google Colab.

3- Select Runtime → Change runtime type → GPU.

4- Upload your secrets.json file via the Files sidebar.

5- Run the cells in order:

Cell 1: Install dependencies

Cell 2: Create local folders

Cell 3: Load credentials

Cell 4: Imports & LLM setup

Cell 5: Core fetch/parse/score functions

Cell 6: Feedback & send functions

Cell 7: Pipeline & logging (this will fetch, process, send feedback, and log)

Check the Logs folder (/content/logs/process_log.csv) for results.


## Customization

Job Description: Edit the GENERIC_JD string in Cell 5 (or in score.py) to match your target role.

Scoring Weights: Adjust the weighting logic when computing the overall score in the pipeline cell.

LLM Model: Swap HF_MODEL_ID to any other compatible Hugging Face causal model. Or any other LLM of your choice.

Troubleshooting

IMAP Errors: Verify Gmail IMAP is enabled (Google Account → Data & privacy → More Google Account settings → Security → Enable IMAP).

Authentication Errors: Ensure 2FA is enabled and you’re using the correct App Password.

Dependency Issues: Run pip install --upgrade -r requirements.txt to reinstall.
