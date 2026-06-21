# Evidence — Neon Tetris, built by an LLM across 5 governed batches

This records the actual run so *"coded by Claude Opus 4.8, under a Matrix Builder contract"*
is verifiable, not asserted.

## Environment

| | |
|---|---|
| Contract engine | `agent-generator` 0.2.0 (the `mb` CLI) |
| Coder driver | GitPilot (`gitcopilot`) — `gitpilot generate` |
| LLM provider / model | `claude` / **`claude-opus-4-8`** (Anthropic Claude Opus 4.8) |
| Endpoint | `https://api.anthropic.com/v1/messages` (`anthropic-version: 2023-06-01`) |

## The 5 batches

Each batch ran: `mb next` → `mb prompt --coder gitpilot` → `gitpilot generate` (Opus 4.8,
given the contract + the current file + the batch spec) → `mb check`. The allow-list for every
batch was **`frontend/index.html` only**; the model never wrote outside it.

| # | Batch | Result file | `mb check` | Matrix Commit |
|---|---|---|---|---|
| 1 | Foundation (board, 7 pieces, render loop, gravity, lock) | 11,025 B | approved · 100 | `mc-e5da1ec40b74` |
| 2 | Controls + SRS rotation + wall kicks + lock delay + DAS | 20,599 B | approved · 100 | `mc-ed8f08a81d49` |
| 3 | Line clears, scoring, levels, next preview, hold | 28,402 B | approved · 100 | `mc-1e2903a575aa` |
| 4 | Ghost, particles/flash, WebAudio SFX, mobile touch, responsive | 44,472 B | approved · 100 | `mc-11c9835f1a93` |
| 5 | Start/pause/game-over, high score (localStorage), a11y, credit | 56,449 B | approved · 100 | `mc-c186f714b6a1` |

```text
$ mb timeline
Tetris Under Contract  v1.0.0
  Batch 01  Foundation                              ✓ commit 001 mc-e5da1ec40b74
  Batch 02  Controls and SRS rotation               ✓ commit 002 mc-ed8f08a81d49
  Batch 03  Line clears, scoring, levels, next/hold  ✓ commit 003 mc-1e2903a575aa
  Batch 04  Juice: ghost, particles, sound, mobile   ✓ commit 004 mc-11c9835f1a93
  Batch 05  Game states, high score, accessibility   ✓ commit 005 mc-c186f714b6a1
```

## A representative batch (Batch 4)

```text
$ export GITPILOT_PROVIDER=claude GITPILOT_CLAUDE_MODEL=claude-opus-4-8
$ export ANTHROPIC_API_KEY=sk-ant-…          # redacted, temporary, rotated after
$ mb next "Juice: ghost, particles, sound, mobile, responsive"
$ mb prompt --coder gitpilot
$ gitpilot generate -m "$(cat coder-prompts/gitpilot.md) + current file + batch spec" -o .
Provider: claude · Model: claude-opus-4-8
  Created: frontend/index.html (44454 bytes)
$ mb check frontend/index.html
MATRIX_STATUS: approved  score=100
  committed mc-11c9835f1a93
```

## Independent sanity checks

- After **every** batch, the extracted `<script>` passed `node --check` (valid JavaScript) and
  the file ended with a complete `</html>`.
- Final feature scan confirmed: SRS rotation + wall kicks, ghost piece, 7-bag, next/hold,
  scoring/levels, particles, `AudioContext` SFX, `localStorage` high score, touch handlers,
  and `prefers-reduced-motion` handling are all present.

## Tooling note (honest)

GitPilot's Anthropic provider didn't set an explicit `max_tokens`, so litellm's low default
truncated large single-file generations. I added a configurable `max_tokens`
(`GITPILOT_MAX_TOKENS`, default 32000) to `gitpilot/llm_provider.py` so a full game fits in one
response. That's a genuine upstream improvement, not a workaround in the game itself.

The Anthropic API key used was temporary and has been rotated.
