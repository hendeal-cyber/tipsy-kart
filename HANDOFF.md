# Tipsy Kart: Handoff

This file is a resume point. It lets a fresh session pick the project up if the current container is lost.

## Project

Tipsy Kart is an ORIGINAL browser-based 3D kart racer for Beerio-Kart-style party play. Up to 4 humans play on phones, with CPU karts filling the field, and everything is served from a localhost Node server (`npm start`).

IP rule: no code, data or assets are copied from Nintendo or Mario Kart. That includes riidefi/mkw, snailspeed3/mkw and any other Mario Kart decompilation. Do not clone, fetch or copy from them.

## Where things live

This repo (`hendeal-cyber/tipsy-kart`) holds the game at its root. It was imported from the `tipsy-kart/` folder of `hendeal-cyber/Modern-Labor-Market-Data-Submission`, branch `claude/beerio-kart-multiplayer-t2w870` at d8aba66, where the multi-lane integration happened. Paths in the lane docs that start with `tipsy-kart/` refer to this repo's root.

**Status: INTEGRATED.** All lanes were merged into the integration branch at their final tips, and every automated suite passes on the merged tree.

Lane branches. They lived in the original container, not in this repo,, and each one was worked on in its own git worktree under `.claude/worktrees/`:

| Branch | Model | Purpose | Final SHA merged |
| --- | --- | --- | --- |
| `lane/research-phone` | Opus | Phone-controller research spec (`docs/research/phone-controls.md`) | f53bbe0 |
| `lane/research-impairment` | Opus | Drink-impairment research spec (`docs/research/impairment.md`) | f1cf4cc |
| `lane/engine` | Opus | Core game and server | 068eb7d |
| `lane/controller` | Sonnet | Phone controller, built to the phone spec | f3a5033 |
| `lane/impairment` | Sonnet | Drink impairment, built to the impairment spec | 40840d1 |

They were merged in the order engine, impairment, controller, with no conflicts. `package.json` holds the union of every lane's deps and scripts. The review findings from the research lanes were fixed in each lane before this merge. Each lane's status file is at `docs/handoff/<lane>.md`, and its integration notes are in `docs/INTEGRATION-<lane>.md`.

## Test results on the integrated tree

All suites were run one at a time from the game folder (this repo's root) after `npm install`, on a quiet machine.

| Suite | Command | Result |
| --- | --- | --- |
| Engine smoke (headless browser, impairment plugin installed) | `npm test` | 42/42 PASS, "All smoke checks passed" (about 2.3 min) |
| Impairment unit | `node --test test/impairment/` | 67 tests: 65 pass, 0 fail, 2 skipped (the opt-in CALIBRATE and E2E runs) |
| Impairment calibration (20 seeds) | `CALIBRATE=1 node test/impairment/calibrate.mjs` | 26/26 PASS, "ALL TARGETS MET" |
| Impairment e2e (real game, 4 players, drinks 0/2/5) | `E2E=1 node --test test/impairment/` | 67 tests: 66 pass, 0 fail, 1 skipped (CALIBRATE) |
| Controller / net (4 phones + host on the real game, protocol, tilt, timing) | `npm run test:net` | 50/50 pass, 5 suites |
| Manual server check | `npm start` then `curl` | `/`, `/controller` and `/api/info` return 200 over HTTP on 3000 and over HTTPS on 3443 (self-signed). `/api/info` lists both plugins and `joinUrl` `https://<lan-ip>:3443/controller` |

IP sweep: the keyword grep over the game folder has no hits in game code, assets or UI. The only matches are the IP-rule statements in this file and in `docs/research/phone-controls.md`, plus the CSS colour name `peachpuff` inside vendored three.js.

The real-phone checks the automated suites cannot cover are in `docs/ON-DEVICE-CHECKLIST.md`. The "Playing a Beerio night" section of `README.md` explains how to play.

This public repo was populated from d8aba66 at the user's request. The integration branch in Modern-Labor-Market-Data-Submission keeps the same files under `tipsy-kart/`.

## Remaining plan

1. Run `docs/ON-DEVICE-CHECKLIST.md` on real iPhone and Android phones. Send any failures back to the owning lane.
2. Make further changes here on branches off `main`, keeping all test suites green.

Never commit `node_modules/`, `.cert/` (it holds the self-signed private key), `test/screenshots/` or `.env` files. `.gitignore` covers all of them.

## Models and workflow

- Opus for research and engine, Sonnet for implementation and integration.
- Each lane works in its own git worktree.

## Resuming in a fresh session

1. Clone `hendeal-cyber/tipsy-kart` and, from the repo root, run `npm install && npm test && npm run test:net && node --test test/impairment/`.
2. For parallel work, give each lane its own worktree off `main`, for example `git worktree add ../tk-controller -b lane/controller-2`.
3. Read `docs/handoff/*.md` and `docs/research/*.md`, then continue the plan above.
