# Marginal (web app)

A Vite + React scaffold around `src/App.jsx` — the writing-voice app with
drafting, outlines, research, essay-health checks, and the "Rewrite in your
voice" tool (with per-change accept/reject) used by the browser extension.

## Run it

```bash
npm install
npm run dev
```

Opens on `http://localhost:5173`.

## Important: this is the frontend only

`src/App.jsx` calls a backend at relative `/api/...` paths:

- `POST /api/login`
- `POST /api/signup`
- `GET  /api/profile`
- `POST /api/gemini` — proxies to the Anthropic/Gemini completion endpoint
  using a server-side key, and is what powers autocomplete, essay-health
  checks, research summarization, and the rewrite tool.

None of that server code was part of the original upload, so there's no
`server/` directory here — the UI will load, but login, drafts, and any
AI-powered feature will fail against a 404 until a backend exists.

`vite.config.js` proxies `/api` to `http://localhost:8787` in dev, so the
quickest path to a working app is standing up a small server (Express,
Fastify, Next.js API routes, Cloudflare Worker, whatever you like) on that
port that implements the four routes above and stores users/profiles/drafts
somewhere (a database, or even a JSON file for local testing). Happy to
build that server for you if you want — just say the word and which stack
you'd prefer (Node/Express is the simplest match for this proxy setup).

## Structure

```
index.html
vite.config.js
src/
  main.jsx     — React entry point
  App.jsx      — the whole app (pages, editor, rewrite tool, etc.)
```
