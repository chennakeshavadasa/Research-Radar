# RESEARCH RADAR

> A self-contained research intelligence terminal for AI, Chip Design, Quant Finance, and more — no backend, no install, runs entirely in your browser.

**Live →** [chennakeshavadasa.github.io/Research-Radar](https://chennakeshavadasa.github.io/Research-Radar)

---

## What it does

Research Radar aggregates papers, preprints, and blog posts from **6 live sources simultaneously**, streams them into a unified feed as they arrive, and uses Claude AI to generate structured analysis of any paper on demand.

| Source | What you get |
|--------|-------------|
| **arXiv** | Latest preprints by category (cs.LG, eess.SP, q-fin, etc.) |
| **Semantic Scholar** | Cited papers + author-specific feeds for top professors |
| **OpenAlex** | 250M open papers, concept-filtered, free, no key |
| **CrossRef** | 130M DOI-indexed works, query-based |
| **RSS Blogs** | Lab blogs (DeepMind, Meta AI, OpenAI, SemiAnalysis…) |
| **Google Scholar** | Real-time via SerpApi (optional, 100 free/month) |

---

## Domains covered

`AI` · `AI × Finance` · `Quant` · `HFT` · `Computing` · `VLSI` · `AMS/RF` · `SerDes` · `AI Chips`

---

## Features

- **Progressive streaming** — each source streams in independently as it resolves; feed updates live
- **Claude AI explainer** — structured breakdown of any paper: what they built, what problem it solves, key contribution; streams token-by-token
- **Expert / Simple modes** — toggle explainer between domain-expert and accessible language
- **Full-text filter** — searches title, authors, abstract, venue simultaneously
- **Sort** by date or citation count
- **Narrow** by source (arXiv / S2 / OpenAlex / CrossRef / Blog / Scholar)
- **Year filter** — show only papers from last 1Y / 2Y / 3Y / 5Y
- **Bookmarks** — persist across sessions via `localStorage`
- **BibTeX copy** — one click / one keypress (`c`) to copy a formatted citation
- **Markdown copy** — copy paper + AI analysis as clean Markdown
- **Keyboard-first** — `j/k` navigate, `Enter` open, `o` PDF, `s` bookmark, `e` explain, `c` BibTeX, `/` filter, `r` refresh, `?` help
- **Persistent API keys** — Claude and SerpApi keys survive page refresh
- **Resizable panels** — drag the divider between feed and detail
- **Dark theme** — designed for long reading sessions

---

## Usage

### Option 1 — Live (no setup)
Open **[chennakeshavadasa.github.io/Research-Radar](https://chennakeshavadasa.github.io/Research-Radar)** in any browser.

### Option 2 — Local
```bash
git clone https://github.com/chennakeshavadasa/Research-Radar.git
cd Research-Radar
python3 -m http.server 8080
# open http://localhost:8080
```
> Must use a local server (not `file://`) — browser APIs require HTTP for CORS to work.

### Option 3 — Single file
Download `index.html`, serve it from any static host.

---

## API Keys (optional but recommended)

| Key | Where to get | What it unlocks |
|-----|-------------|-----------------|
| **Anthropic Claude** | [console.anthropic.com](https://console.anthropic.com) | AI paper explainer with streaming |
| **SerpApi** | [serpapi.com](https://serpapi.com/users/sign_up?plan=free) — free 100/month | Google Scholar author feeds |

Keys are entered in the header, stored in `localStorage`, and never leave your browser. No backend touches them.

---

## Architecture

```
index.html  (single file, ~110KB, zero dependencies, zero build step)
│
├─ CSS        Dark theme, CSS variables, animations
├─ HTML       Static shell, all content injected by JS
└─ JS
   ├─ Constants   DOMAINS, ARXIV_CATS, S2_QUERIES, BLOG_FEEDS, PROF_AUTHORS …
   ├─ State        Reactive STATE object, domain cache, filter state
   ├─ Fetchers    fetchArxiv · fetchSemanticScholar · fetchOpenAlex
   │               fetchCrossRef · fetchBlogFeeds · fetchScholarAuthor
   ├─ Ingest      Progressive merge with title-normalised dedup
   ├─ Render      Smart diff feed renderer, detail panel, explainer
   ├─ Claude API  Streaming SSE explainer (claude-sonnet-4-20250514)
   └─ Events      Keyboard shortcuts, resize, filter, sort, bookmarks
```

Everything runs client-side. GitHub Pages serves the one file. The browser does all the work.

---

## Keyboard shortcuts

| Key | Action |
|-----|--------|
| `j` / `k` | Navigate feed |
| `Enter` | Open paper URL |
| `o` | Open PDF |
| `s` | Bookmark |
| `e` | Run AI explainer |
| `c` | Copy BibTeX |
| `/` | Focus filter |
| `r` | Refresh domain |
| `?` | Keyboard help |

---

## Contributing

PRs welcome. The whole app is one file — find the section you want to change (sections are labelled A through K in the JS comments) and edit.

Common additions:
- New domain: add entry to `DOMAINS`, `ARXIV_CATS`, `S2_QUERIES`, `BLOG_FEEDS`, `PROF_AUTHORS`, `SCHOLAR_AUTHORS`, `DOMAIN_KEYWORDS`
- New source: add a `fetch*()` function and a `.then()` call in `fetchAllSourcesProgressive()`

---

## License

MIT
