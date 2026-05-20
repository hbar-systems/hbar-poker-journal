# Poker Journal

A brain-app for [BrainFoundry](https://brainfoundry.ai) brains.

Created: 2026-05-20

**A field journal for poker, kept inside your own brain.**

Most poker study lives in spreadsheets, PDFs, scattered notes, or
trackers owned by someone else. Poker Journal is a thin instrument for
keeping the record where your other thinking lives — in your brain.

Four modes:

- **Hand** — paste a hand-history export (e.g. PokerStars text). Your
  brain reads it and proposes a session entry plus zero or more leak
  entries. You approve per entry.
- **Reflect** — post-session prompts (what felt off, where discipline
  slipped, dominant emotion). Your brain synthesises impression and
  leak proposals. You approve per entry.
- **Ask** — grounded chat scoped to your poker corpus. The brain
  answers from your own hand histories, leaks, impressions, and any
  framework documents you have ingested.
- **Theory** — click a poker concept (pot odds, Nash equilibrium,
  ergodicity, ICM, ...). The brain explains it, grounded in any
  theory material you have ingested. "Keep this" saves notable
  explanations into your own memory.

Every brain answer (Ask and Theory) carries a **Keep this** button —
opens an inline propose-card, you edit the title/content and pick a
layer, your brain stores it.

## Install

In your brain: **Settings → Apps**, paste this repository's URL,
**Preview**, **Install**. The app adds a *Poker* tab.

## How it works

The app carries no intelligence of its own. It borrows the host
brain's reasoner and memory through the brain-app `postMessage`
bridge:

- `llm.complete` — reads pasted text (Hand) or reflection answers
  (Reflect), returns a JSON array of proposed memory entries; for
  Ask, returns a grounded answer; for Theory, returns a concept
  explanation grounded in ingested theory material. Retrieval is
  scoped to the read-mode layers declared in `brain-app.yaml`.
- `memory.write` — one call per approved proposal, appended to the
  layer the operator confirmed. Also fires once per Keep-this from a
  brain answer.

Until the operator clicks Approve, nothing touches the brain's memory.
Skip discards a proposal.

Opened standalone — as a file, with no host brain — the app shows a
"no brain attached" message rather than fabricate local proposals.

## Naturalist phase

The default disposition is observational, not coaching. Hand histories
are the experimental instrument; impressions are the phenomenological
layer; leaks are named patterns. Variance is the medium. Decisions and
outcomes are tracked separately.

You can override that disposition in your brain's persona at any time.

## Permissions

| Permission     | Why |
|----------------|---|
| `llm.invoke`   | read pasted hands / reflections / questions and produce proposals or grounded answers (RAG over the declared read-mode layers) |
| `memory.write` | append each approved proposal to its layer (episodic / semantic / procedural) |

See `brain-app.yaml` for the full manifest.

## Build

None. One self-contained `index.html` — no dependencies, no CDN, no
build step. A sovereignty claim shouldn't ship third-party script.

## Part of hbar.poker

`hbar.poker` is the umbrella for poker work in the constellation:

- The gated personal journal site at hbar.poker (private repo).
- This public brain-app (`hbar-poker-journal`).
- Future apps may join (e.g. sparring AI, equity drill).

## License

AGPL-3.0 — see [`LICENSE`](./LICENSE). Brain-apps must be
license-compatible with the brain they install into.
