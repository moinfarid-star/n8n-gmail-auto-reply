# AI Gmail Auto-Reply & Triage (n8n + Gemini + Google Sheets) — Localhost v1
Demo video: [docs/demo.mp4](docs/demo.mp4)

## What it does
- Fetches emails on a schedule
- Classifies intent (AI agent)
- Applies IF rules (no spam/newsletters, no double replies)
- Sends reply when valid
- Adds label + logs result to Google Sheets

## Workflow files
workflows/email-automation-localhost-v1.json

## Setup (local)
1) Import the workflow JSON into n8n
2) Create credentials:
   - Gmail OAuth
   - Google Sheets OAuth
   - Gemini API (or your model provider)
3) Update the nodes:
   - Gmail query / filters
   - Label name (e.g., AutoReplied)
   - Sheet ID + tab name
4) Run once manually, then enable Schedule Trigger

## Safety rules included
- Duplicate replies blocked
- Spam/newsletters ignored
- Logging enabled for traceability

## Next improvements
- Fallback handling when AI fails (NeedsReview label)
- Monitoring summary (daily counts)
