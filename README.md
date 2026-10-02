# OPTIMUS — Web (static, no backend, free hosting)

Pure HTML/CSS/JS. No server, no database, no Python. Deploys free on GitHub
Pages, Netlify, or Cloudflare Pages — just these files.

## Why this version exists
The FastAPI version needs a Python host (Heroku/Render/HF Spaces). This
version needs nothing but static file hosting, which is what GitHub Pages
actually gives you for free. Everything runs in the visitor's own browser.

## Deploy (GitHub Pages)
1. Push this folder's contents to a GitHub repo.
2. Settings → Pages → Deploy from a branch → `main`, `/ (root)` → Save.
3. Open the `https://<you>.github.io/<repo>/` link it gives you.

Netlify: drag this folder onto app.netlify.com/drop, or connect the repo
with an empty build command and `/` as the publish directory.

## Choose your AI provider
Settings now has a provider dropdown:
- **Google Gemini** — free key at aistudio.google.com/apikey. Only one with live search grounding, image generation, and voice input.
- **Groq** — free key at console.groq.com/keys. Very fast responses, supports voice input (Whisper), no search grounding or image generation.
- **OpenRouter** — free key at openrouter.ai/keys. Access to many free community models, text only.

Each provider's key is stored separately, so switching providers in Settings
doesn't erase the others — come back to Gemini later and your key is still
there. A **Test connection** button in Settings checks a key actually works
before you rely on it.

If a feature isn't supported by the provider you've picked (e.g. live search
on Groq), OPTIMUS tells you in plain language and quietly falls back instead
of throwing a raw error — image generation always uses a Gemini key
specifically (paste one just for that, even if you're chatting with Groq).

## Built for "no errors"
- Every page render is wrapped so a bug in one screen shows a "Try again /
  Go home" card instead of a blank app.
- Every AI call normalizes provider error codes (401/403/429/5xx) into a
  plain-English message instead of raw JSON.
- If a reply fails, your typed message is restored instead of lost.
- Global handlers catch anything that slips through and show a toast rather
  than failing silently.
- Offline detection warns before a request is even attempted.
- Private/incognito mode (where storage may not persist) is detected and
  flagged up front.

## Data & privacy
Chats, files, memory, and generated images are stored in this browser's
IndexedDB — nothing is sent to any OPTIMUS server, because there isn't one.
Use Settings → Export to back up your data as a `.json` file, and Import to
restore it (or move it to another browser/device).

## Limits of a backend-free app
- No shared/multi-device sync — it's per-browser.
- PDF/DOCX text extraction happens in-browser (pdf.js / mammoth.js, loaded
  from cdnjs on first use).
- Image generation needs a Gemini key specifically; other providers here
  don't offer native image output yet.
