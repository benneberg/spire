# Spire OS

**Deterministic product incubation.** Upload a codebase ZIP → get a brand system, market strategy, and landing page — in under 60 seconds.

```
AI analyses → deterministic engines build → Context Graph persists
```

-----

## Architecture

|Package                  |Role                                                     |
|-------------------------|---------------------------------------------------------|
|`@spire/context-graph`   |Event-sourced state — IndexedDB, time-travel, snapshots  |
|`@spire/graphic-forge`   |Brand system — colour palettes, typography, spacing      |
|`@spire/ai-orchestration`|AI layer — circuit breaker, Zod validation, caching      |
|`@spire/market-me`       |Market intelligence — TAM/SAM/SOM, RICE scoring, personas|
|`@spire/launch-pad`      |HTML assembly — 7 template variants, SEO, CSS variables  |
|`spire-shell`            |Next.js 15 app — pipeline UI, Zustand store, API routes  |

**202 tests across the five core packages, all green.**

-----

## Prerequisites

- Node.js ≥ 20
- pnpm ≥ 9 (`npm install -g pnpm`)

-----

## Setup

```bash
# 1. Clone
git clone https://github.com/your-org/spire-os.git
cd spire-os

# 2. Install all workspace packages
pnpm install

# 3. Configure API keys (optional — Spire works without them)
cp spire-shell/.env.local.example spire-shell/.env.local
# Edit spire-shell/.env.local and add your GROQ_API_KEY and/or GEMINI_API_KEY

# 4. Start the dev server
pnpm dev
# → http://localhost:3000
```

-----

## Running tests

```bash
# All packages
pnpm test

# Single package
pnpm --filter @spire/graphic-forge test
pnpm --filter @spire/market-me test
```

-----

## Using Spire

1. **Upload** — drop a project ZIP (node_modules, .git, dist are auto-excluded)
1. **Name** — enter your product name
1. **Run Pipeline** — watch the five stages execute in sequence:
- **Analyse** — AI extracts features and architecture (falls back to static analysis without a key)
- **Brand** — deterministic colour system, typography pair, spacing scale
- **Market** — TAM/SAM/SOM, RICE roadmap, ICP personas
- **Launch** — HTML landing page assembled from brand + market contracts
1. **Download** — grab the self-contained `landing-page.html` from the Launch panel

**The event log** (top-right) shows every Context Graph event in real time, including which steps used AI vs deterministic generation.

-----

## AI keys

Keys can be set in two ways (server env vars take precedence):

|Method               |How                               |
|---------------------|----------------------------------|
|Server (recommended) |`spire-shell/.env.local`          |
|Browser (per session)|Settings panel (⚙ icon, top-right)|

Without any keys, all AI steps fall back gracefully — outputs are less personalised but still fully generated.

-----

## Design principles

- **AI for analysis only** — AI classifies and extracts; it never generates brand assets or copy directly
- **Determinism** — identical inputs always produce identical outputs from the deterministic engines
- **Event sourcing** — every state change is an immutable event in the Context Graph, replayable at any sequence point
- **No lock-in** — every output is a plain file (HTML, JSON). No proprietary formats.

-----

## Project structure

```
spire-os/
├── pnpm-workspace.yaml
├── package.json
├── spire-context-graph/    @spire/context-graph
├── spire-graphic-forge/    @spire/graphic-forge
├── spire-ai-orchestration/ @spire/ai-orchestration
├── spire-market-me/        @spire/market-me
├── spire-launch-pad/       @spire/launch-pad
└── spire-shell/            Next.js app
    ├── app/
    │   ├── api/analyze/    POST — AI orchestration endpoint
    │   ├── layout.tsx
    │   └── page.tsx
    ├── components/
    │   ├── modules/        UploadModule CoreModule ForgeModule MarketModule LaunchModule
    │   ├── shared/         EventLog SettingsPanel StatusBadge SectionPanel
    │   └── shell/          TopBar StepRail
    └── lib/
        ├── store.ts        Zustand store (pipeline state + artifacts)
        ├── graph.ts        Context Graph singleton
        └── pipeline.ts     Full pipeline orchestrator
```

-----

## License

MIT (core packages) · See individual package `package.json` for details.
