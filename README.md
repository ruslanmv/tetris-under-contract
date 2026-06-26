<div align="center">

# 🟦🟨🟪 Neon Tetris — Under Contract

### A full, colorful Tetris game built with **GitPilot** across **5 governed batches** — under contract, with proof.

**[GitPilot](https://gitpilot.ruslanmv.com)** built this game one batch at a time — each batch bound by a **[Matrix Builder](https://github.com/agent-matrix/matrix-builder)** contract with an allow-list of `frontend/index.html` only, and validated by `mb check` **before** it could land. Five batches, five `approved` Matrix Commits.

[![Play now](https://img.shields.io/badge/▶_PLAY_NOW-00f0ff?style=for-the-badge\&labelColor=07060f\&color=00f0ff)](https://ruslanmv.github.io/tetris-under-contract/)
 
[![5 batches](https://img.shields.io/badge/built_in-5_governed_batches-ff00d4?style=for-the-badge\&labelColor=07060f)](EVIDENCE.md)

[![Built with GitPilot](https://img.shields.io/badge/built_with-GitPilot-D95C3D?style=flat-square\&labelColor=1C1C1F)](https://gitpilot.ruslanmv.com)
[![Contract](https://img.shields.io/badge/contract-Matrix_Builder-ffd400?style=flat-square\&labelColor=1C1C1F)](https://github.com/agent-matrix/matrix-builder)
[![Validation](https://img.shields.io/badge/validation-mb_check-21e600?style=flat-square\&labelColor=1C1C1F)](EVIDENCE.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-21e600?style=flat-square\&labelColor=1C1C1F)](LICENSE)

<img src="assets/hero.svg" alt="Neon Tetris — built with GitPilot across 5 governed contract batches" width="760" />

</div>

---

## 🎮 [Play it → ruslanmv.github.io/tetris-under-contract](https://ruslanmv.github.io/tetris-under-contract/)

![Neon Tetris gameplay — HUD, hold, next queue, ghost piece](assets/screenshot.png)

One self-contained HTML file. No install, no build. Desktop **and** mobile.

**Controls:** ← → move · ↑/X rotate CW · Z rotate CCW · ↓ soft drop · **Space** hard drop · **C/Shift** hold · **P/Esc** pause.
**Touch:** on-screen buttons + swipe gestures.

Features: 7-bag randomizer · **SRS rotation with wall kicks** · ghost piece · hold + next preview · line-clear particles & flash · level/speed curve · **WebAudio** SFX with mute toggle · high score via localStorage · start / pause / game-over screens · neon CRT styling.

---

## The point: GitPilot built something *real* — and stayed in scope the whole way

This is not a toy snippet. It is a complete Tetris game, about 56 KB, generated with **GitPilot** and built through an auditable contract workflow.

Every step is recorded in [`EVIDENCE.md`](EVIDENCE.md). What makes the result trustworthy is not a promise — it is the process: each batch was bound by a Matrix Builder contract, constrained to a single allowed file, validated with `mb check`, and approved only when it stayed in scope.

GitPilot touched **only** `frontend/index.html`, every single batch.

---

## How it was built — 5 batches, each under contract

Each batch ran the same loop:

`mb next` → `mb prompt --coder gitpilot` → `gitpilot generate` → `mb check` → immutable Matrix Commit

GitPilot handled the implementation work batch by batch, while Matrix Builder defined the scope, generated the contract, validated the output, and blocked anything that failed the checks.

| # | Batch               | What GitPilot added                                                               | Size  | Matrix Commit     |
| - | ------------------- | --------------------------------------------------------------------------------- | ----- | ----------------- |
| 1 | Foundation          | 10×20 board, 7 colored tetrominoes, render loop, gravity, lock, 7-bag             | 11 KB | `mc-e5da1ec40b74` |
| 2 | Controls + rotation | move/soft/hard drop, **SRS rotation + wall kicks**, lock delay, DAS               | 20 KB | `mc-ed8f08a81d49` |
| 3 | Lines + scoring     | line clears, scoring, levels/speed, **next** preview, **hold**                    | 28 KB | `mc-1e2903a575aa` |
| 4 | Juice               | ghost piece, particles + flash, **WebAudio** SFX, mobile touch, responsive layout | 44 KB | `mc-11c9835f1a93` |
| 5 | States + polish     | start/pause/game-over, **high score** via localStorage, a11y, credit              | 56 KB | `mc-c186f714b6a1` |

```text
$ mb timeline
Tetris Under Contract  v1.0.0
  Batch 01  Foundation                         ✓ mc-e5da1ec40b74
  Batch 02  Controls and SRS rotation          ✓ mc-ed8f08a81d49
  Batch 03  Line clears, scoring, levels …      ✓ mc-1e2903a575aa
  Batch 04  Juice: ghost, particles, sound …    ✓ mc-11c9835f1a93
  Batch 05  Game states, high score, polish     ✓ mc-c186f714b6a1
```

Every batch returned `MATRIX_STATUS: approved score=100`. Full transcript in [`EVIDENCE.md`](EVIDENCE.md).

---

## The GitPilot loop

```bash
pip install agent-generator gitcopilot crewai

# Configure GitPilot with your preferred provider and model.
export GITPILOT_PROVIDER=your-provider
export GITPILOT_MODEL=your-model
export GITPILOT_API_KEY=your-api-key

mb init "A polished neon Tetris game, single self-contained HTML file" --quality standard

for batch in foundation controls scoring juice states; do
  mb next "$batch"                                   # plan a scoped batch
  mb prompt --coder gitpilot                         # render the contract
  gitpilot generate -m "$(cat coder-prompts/gitpilot.md) + current file + batch spec" -o .
  mb check frontend/index.html                       # validate, fail-closed
done
```

---

## What's in this repo

```text
tetris-under-contract/
├── frontend/index.html              ← the whole game, generated with GitPilot
├── EVIDENCE.md                      ← the 5-batch run: sizes, verdicts, commits
├── coder-prompts/gitpilot.md        ← the contract-bound GitPilot prompt
├── .gitpilotrules                   ← repo guardrails for GitPilot
├── .mb/                             ← the Matrix Bundle: blueprint + 5 batches + 5 commits
├── .github/workflows/contract.yml   ← CI: re-runs `mb check`, then deploys to Pages
└── README.md
```

---

## Why this matters

This repository demonstrates **AI-assisted software generation under contract**.

GitPilot produced the implementation, but the work was governed by Matrix Builder:

* one planned batch at a time
* one allowed file target
* validation before commit
* immutable Matrix Commit evidence
* fail-closed checks with `mb check`

The result is a playable browser game with a traceable build history: five batches, one file, zero out-of-scope edits.

---

## Links

* 🚁 **GitPilot** → [gitpilot.ruslanmv.com](https://gitpilot.ruslanmv.com)
* 🧩 **Matrix Builder** → [agent-matrix/matrix-builder](https://github.com/agent-matrix/matrix-builder)
* ⚙️ **Engine + `mb` CLI** → [ruslanmv/agent-generator](https://github.com/ruslanmv/agent-generator)
* 🕹️ **Also:** [Pong, under contract](https://github.com/ruslanmv/pong-under-contract)

---

<div align="center">

*Five batches. One file. Zero out-of-scope edits. ⭐ if that is how AI should ship code.*

Built with [GitPilot](https://gitpilot.ruslanmv.com) by [Ruslan Magana Vsevolodovna](https://ruslanmv.com) · MIT licensed

</div>
