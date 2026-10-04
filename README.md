# Study Buddy

An NLP-powered study assistant — glassmorphic UI, adjustable learner level and focus area, backed by a small Express proxy so your Anthropic API key never touches the browser.

## Setup

1. Install dependencies
   ```
   npm install
   ```

2. Add your API key
   ```
   cp .env.example .env
   ```
   Open `.env` and paste your key from https://console.anthropic.com/settings/keys into `ANTHROPIC_API_KEY`.

3. Run both the backend and frontend together
   ```
   npm run dev:all
   ```
   This starts:
   - the Express proxy on `http://localhost:3001`
   - the Vite dev server on `http://localhost:5173`

4. Open `http://localhost:5173` in your browser.

   (Alternatively, run `npm run server` and `npm run dev` in two separate terminals.)

## Why a backend?

The frontend never calls Anthropic directly — it calls `/api/chat` on your own Express server, which holds the real API key and forwards the request. This keeps your key out of the browser and avoids CORS issues, which is the standard way to call any LLM API from a web app.

## Requirements

- Node.js 18 or newer (for built-in `fetch`)
- An Anthropic API key with available credits

## Build for production

```
npm run build
```
Outputs static files to `dist/`. Serve `dist/` from any static host, and deploy `server/index.js` (with your `ANTHROPIC_API_KEY` set as an environment variable) separately, or behind the same domain with a reverse proxy.
