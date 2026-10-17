# EvidenceLens AI

A cloud-powered GRC audit-assistance prototype built for Hacktoberfest Hack Day Bhopal. An auditor uploads evidence, picks the ISO/IEC 27001:2022 Annex A controls to test, and the Google Gemini API drafts an evidence assessment for each control. **A human auditor must review every result.**

## Features
- Evidence input: PDF, TXT, Markdown, CSV, **screenshots (PNG/JPG/WEBP)**, or pasted text
- **93 Annex A controls** loaded from `controls.json` (converted from an ISO 27001:2022 audit checklist); choose 1-5 to test
- The checklist's gap-assessment questions and expected evidence are used as the audit criteria
- Per-control status: Supported, Partially Supported, Missing, Needs Review
- Exact evidence excerpts, draft risk, confidence, reasoning and recommended next step
- "Reviewed by auditor" tick per finding, saved into the exports
- JSON and CSV report downloads
- Automatic retry and fallback model when the main model is busy (HTTP 429/500/503)

## Requirements
- Windows PowerShell (or any shell), internet connection
- [uv](https://docs.astral.sh/uv/) (installs Python 3.12 for you), or Python 3.10+ with `venv`
- A Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey)

## Run
From the project folder:

```powershell
uv venv --python 3.12
uv pip install -r requirements.txt
$env:GEMINI_API_KEY = "PASTE_YOUR_KEY_HERE"
uv run streamlit run app.py
```

Open `http://localhost:8501`. The key lives only in that terminal session. Never paste it into code, screenshots or GitHub.

## Models
Defaults: `gemini-3.8-flash` (main) and `gemini-3.5-flash` (fallback). These names were present in the model list returned for the author's key on 17 Oct 2026. Model availability changes, so list what your key can use and override if needed:

```powershell
$env:GEMINI_MODEL = "exact-model-name"
$env:GEMINI_FALLBACK_MODEL = "another-exact-model-name"
```

## Demo files
- `sample_access_review.txt`: synthetic, intentionally incomplete access-review text (try A.5.16, A.5.18, A.8.2, A.8.15)
- `sample_log_settings_screenshot.png`: synthetic logging-settings screenshot (try A.8.15)

## Privacy and limitations
- Evidence you upload or paste is sent to Google Gemini. Free-tier requests may be used by Google to improve its products. Use only synthetic or sanitized evidence; never upload confidential client data or personal data.
- AI output is a draft. It does not establish compliance, control effectiveness or certification.
- Evidence presence does not prove a control is effective. A missing statement in one document does not prove a control is absent.
- Text read from images can contain errors. Verify every quote and mapping against the original source and the authoritative standard.
- The control catalogue was converted from a checklist; check it against the published standard before relying on it.

## Demo flow
1. Upload `sample_access_review.txt`, select A.5.16, A.5.18, A.8.2 and A.8.15, click **Analyze**.
2. Open a finding: show the excerpt, status, risk, reasoning and next step.
3. Upload the screenshot with A.8.15 to show image evidence.
4. Tick **Reviewed by auditor** and download the JSON/CSV report.
5. Point out that the auditor stays responsible for the conclusion.

## License
MIT. See `LICENSE`.
