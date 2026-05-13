# receipt-ai-app

AI-powered web app that extracts key information from receipt images and auto-fills a form using generative AI.

---

## How to Run

### Option A — Open Directly (No Server Needed)
Just open `index.html` in any modern browser. No build step, no dependencies.

### Option B — Local Dev Server
```bash
npx serve .
# or
python3 -m http.server 8080
```
Then visit `http://localhost:8080`

### Option C — Deploy to Vercel
```bash
npm i -g vercel
vercel --prod
```

---

## Usage

1. **Enter your Gemini API key** — get one free at https://aistudio.google.com
2. **Upload a receipt image** (JPEG, PNG, WEBP) via drag-and-drop or file picker
3. Click **"Extract with AI"** — Gemini analyses the image and auto-fills the form
4. **Review and edit** the extracted fields if needed
5. Click **"Submit Entry"** — data is saved in-memory for the session

---

## Model & Prompt

**Model:** `gemini-2.5-flash` (Google — free tier via AI Studio)

**Prompt strategy:** Single-turn vision prompt with structured JSON output constraint.

The model receives the receipt image (base64) alongside this instruction:

> "Analyse this receipt image and extract exactly the following fields. Return ONLY a valid JSON object with no markdown..."

Get a free API key at: https://aistudio.google.com → "Get API Key"

Fields extracted:
| Field | Description |
|-------|-------------|
| `merchant_name` | Store/restaurant name |
| `date` | Transaction date (DD/MM/YYYY) |
| `total_amount` | Final total (numeric string, 2 decimals) |
| `currency` | ISO 4217 code (MYR, USD, SGD…) |

The model is instructed to infer the currency from symbols, country context, or language on the receipt if not explicitly stated.

---

## Tech Stack

- Vanilla HTML/CSS/JS (zero dependencies, zero build tools)
- Gemini 2.5 Flash API with vision (inline_data image block)
- In-memory storage for submissions

---

## Notes

- API key is used client-side only and never stored persistently
- Submissions are held in `window.submissions` array (in-memory, clears on refresh)
- The app is fully functional locally; for persistent storage, connect a backend
## Notes

- API key is used client-side only and never stored persistently
- Submissions are held in `window.submissions` array (in-memory, clears on refresh)
- The app is fully functional locally; for persistent storage, connect a backend
