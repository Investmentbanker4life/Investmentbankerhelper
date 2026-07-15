# ATLAS-7 — AI Investment Banking Analyst

A single-file, self-hosted AI assistant for investment banking work: valuation frameworks, financial modeling guidance, M&A process, pitch materials, and deal terminology — plus a built-in offline DCF and comps calculator.

![no-build](https://img.shields.io/badge/build-none%20needed-2be9d6) ![offline-calc](https://img.shields.io/badge/valuation%20calc-client--side-d4af37)

## What it is

ATLAS-7 is one HTML file (`index.html`) with no backend and no build step. Open it in a browser, drop in an API key from any provider, and it becomes a chat assistant tuned for banking work — DCF walkthroughs, comps analysis setup, LBO mechanics, due diligence checklists, pitch book outlines, and deal-term explanations. A separate **Quick Valuation Calc** panel runs entirely client-side (no API call) for fast DCF and comps-multiple math.

## Bring your own key — any provider

Click **Connection** in the top bar and choose:

- **Anthropic (Claude)** — e.g. `claude-sonnet-4-6`
- **OpenAI (GPT)** — e.g. `gpt-4o`
- **Groq** — e.g. `llama-3.3-70b-versatile`
- **Custom (OpenAI-compatible)** — point it at any endpoint that speaks the OpenAI chat-completions format (self-hosted models, OpenRouter, LM Studio, etc.)
- **Run Locally — no key** — runs a real model entirely inside your browser via [WebGPU](https://developer.chrome.com/blog/webgpu-release) ([WebLLM](https://github.com/mlc-ai/web-llm)). No key, no server, nothing leaves your machine. First connect downloads the model (hundreds of MB to a few GB) and caches it in the browser; needs a recent Chrome or Edge. Answers are noticeably less sharp than the hosted providers above since local models are much smaller — good for glossary/definition-style questions, weaker on nuanced modeling judgment calls.

By default your key is stored only in your browser's `localStorage` and is sent directly from your browser to the provider you pick — this repo has no server component and never sees your key.

## Live market data

Click **Market Data** to pull a real-time-ish quote and fundamentals (price, change, market cap, P/E, 52-week range, sector) for any ticker, using either:

- **Financial Modeling Prep** — free tier, [get a key here](https://site.financialmodelingprep.com/developer/docs)
- **Alpha Vantage** — free tier, [get a key here](https://www.alphavantage.co/support/#api-key) (rate-limited on the free plan)

Hit **Send to ATLAS-7 chat** and the fetched figures get dropped into the chat as grounding context, so the model reasons from real numbers instead of its own training data — which will not reflect current prices or filings.

Free-tier market data from either provider may be delayed rather than truly real-time; check the provider's docs for your plan's latency before relying on it for anything time-sensitive.

## Storing keys locally (without committing them)

Typing a key into the Connection panel every time gets old. Two ways to make it stick, in order of preference:

**1. `config.js` (recommended)** — copy `config.example.js` to `config.js`, fill in your real keys, and it will auto-load on startup. `config.js` is already in `.gitignore`, so it's never committed even if you `git add .`.

**2. Obfuscated single-file "bake" (private repos only)** — in Connection → *Advanced: local key storage*, click **Generate obfuscated snippet** and paste the result into `index.html` where the `const BAKED = "";` line is. This is **obfuscation, not encryption** — anyone who opens dev tools on the deployed page can recover the key in seconds. Only ever do this in a private repo or a file that never leaves your machine. Never use this in a public repository.

## Getting started

1. Download or clone this repo.
2. Open `index.html` in any modern browser (or serve it with GitHub Pages).
3. Add your API key when prompted.
4. Pick a deal module on the left, or just start typing.

No npm install, no server, no build pipeline.

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. Repo **Settings → Pages → Deploy from branch**, select `main` and `/root`.
3. Your assistant is live at `https://<you>.github.io/<repo>/`.

## Important

ATLAS-7 is a drafting and reasoning aid. It does not have live market data, is not a licensed financial or legal advisor, and every figure, model, and recommendation it produces should be independently verified and reviewed by a qualified professional before any client, committee, or regulatory use.

## License

MIT — do whatever you like with it.
