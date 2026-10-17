# EvidenceLens AI

A cloud-powered GRC audit-assistance prototype for Hacktoberfest Hack Day Bhopal. It uses the Google Gemini API to suggest evidence-to-control mappings and draft audit findings. **No local Gemma model or Ollama installation is required.**

## Features
- Cloud inference through the Google Gemini API
- PDF, TXT, Markdown and CSV evidence input, plus pasted text
- Curated ISO/IEC 27001:2022 Annex A control subset
- Exact evidence excerpts, draft risk levels, recommendations and mapping confidence
- JSON and CSV report downloads
- Human-review and evidence limitations made explicit

## Prerequisites
- Python 3.10+
- Internet connection
- A Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey)

## Run on Windows PowerShell
Open PowerShell in the extracted `EvidenceLensAI` project folder.

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Set the API key for the current PowerShell session (replace the placeholder with your own key):

```powershell
$env:GEMINI_API_KEY = "PASTE_YOUR_GEMINI_API_KEY_HERE"
$env:GEMINI_MODEL = "gemini-2.5-flash"
.\.venv\Scripts\python.exe -m streamlit run app.py
```

Open the local URL Streamlit prints, usually `http://localhost:8501`.

The environment variable is session-only. If you open a new PowerShell window, set it again. Never paste your API key into source code, screenshots, issue reports, or GitHub.

## Model selection
The default is `gemini-2.5-flash`. If your Google AI Studio account exposes a different compatible model, set `GEMINI_MODEL` to that model's exact API name before starting Streamlit.

## Demo
Use the included `sample_access_review.txt`. The sample is fictional and intentionally incomplete.

## Privacy and limitations
- This is a cloud configuration: the evidence text you upload or paste is sent to Google Gemini for processing. Use only synthetic or sanitized evidence; never upload confidential client records or real personal data.
- The control catalogue is a small demonstrator subset, not the complete ISO/IEC 27001 standard.
- AI output is a draft. It does not establish compliance, operating effectiveness, or certification.
- A missing statement in one file is not proof that a control is absent.
- Verify every quote and control mapping against the source and authoritative standard.

## Suggested hackathon demo
1. Set `GEMINI_API_KEY` in PowerShell.
2. Upload `sample_access_review.txt`.
3. Click **Analyze evidence with cloud AI**.
4. Expand a finding and show the excerpt, mapping rationale, draft risk and next step.
5. Download JSON and CSV reports.
6. Explain that an auditor remains responsible for validating evidence and conclusions.

## License
MIT. See `LICENSE`.
