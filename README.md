# AI Gmail Auto-Reply & Triage (n8n + Gemini + Google Sheets)

## What this project does
This n8n workflow:
- Fetches unread Gmail emails
- Uses Gemini (AI Agent) to decide whether to reply and to generate a reply (structured JSON)
- Replies only when needed (IF condition)
- Logs every email + decision to Google Sheets
- Prevents duplicate replies using a Gmail label: `AUTO_REPLIED`

## Workflow overview
Schedule Trigger → Get All Emails → Get Single Email → AI Agent (Gemini) → Edit Fields → IF  
**IF True:** Reply to a message → Add label to message (`AUTO_REPLIED`) → Google Sheets log  
**IF False:** (optional) Google Sheets log (skipped)

## Key protections
### 1) No duplicate replies
- After replying, the workflow adds Gmail label: `AUTO_REPLIED`
- The email fetch query includes: `-label:AUTO_REPLIED`

### 2) Spam / newsletter avoidance
- IF condition requires:
  - `should_reply == true`
  - AND category is NOT in: `spam`, `newsletter`, `promo`, `promotion`

## Files in this repo
- `gmail-auto-reply.json` — n8n workflow export (import into n8n)
- `workflow.png` — workflow screenshot
- `sheet_log_blurred.png` — Google Sheets logging screenshot (blurred)

## How to use (high level)
1. Import `gmail-auto-reply.json` into n8n
2. Create credentials in n8n:
   - Gmail account
   - Gemini / Google AI
   - Google Sheets
3. Create Gmail label: `AUTO_REPLIED`
4. In “Get All Emails” node, use a query like:
   - `is:unread -label:AUTO_REPLIED`
5. Activate the workflow

## Rate-limit note
If you see “Too many requests” or temporary AI overload errors:
- Reduce “Get All Emails” limit (e.g., 3–5)
- Increase schedule interval (e.g., 5–10 minutes)
- Add small delay between items (2–5 seconds)
- Enable retries/backoff on AI + Gmail nodes
