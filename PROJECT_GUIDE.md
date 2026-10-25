# takebase/firebase-rtdb Project Guide

## Project identity

- Multica project: **takebase/firebase-rtdb** (`00ddb0ab-ec04-4f03-bf3b-e7d83a025cfc`).
- Workspace: **Segutrends** (`237ef0f7-262b-4830-9d1a-c86b40b59fda`).
- Attached local root: `/Volumes/Workspace/dev-drakecall/packages/node/takebase/firebase-rtdb`.
- Product: `@takebase/firebase-rtdb`, a REST-only Firebase Realtime Database client for Cloudflare Workers and Node.js. Its main consumer is the Takebase framework (Multica project Takebase, `6f84dfa1-a433-4994-bcc1-9a79819f297f`, repository `takebase/takebase`).
- Origin: SEGU-240 copied the private company package `@segutrends/segufirebase` 0.0.2 into the Takebase monorepo on 2026-10-24; it was then split into this repository with its history kept. SEGU-264 made it standalone.

Verify stored identity against the authenticated Multica CLI and the current folder before work. If the human has not named the project, ask. Never reuse another project's identity.

## Read order and roles

1. `PROJECT_GUIDE.md`, then `JUMBO.md`.
2. The local skill for the requested work (`.agents/skills/`).
3. The human-selected Multica issue, latest comments, accepted plan and decisions.
4. Relevant configuration and code.

OpenCode plans; the human starts Claude Code to implement the selected issue. Multica records plans, state, decisions, progress and evidence. Jumbo holds durable accepted knowledge only; Claude Code reads `JUMBO.md` but never invokes Jumbo commands. No agents, schedules, wakeups or automatic follow-up.

## Repository layout

- `src/`: `index.ts` (public exports), `client.ts`, `auth.ts`, `http.ts`, `paths.ts`, `errors.ts`.
- `test/`: unit tests with a scripted `fetch` (`client.test.ts`, `takebase-additions.test.ts`, `helpers.ts`) and `emulator.test.ts`, skipped unless the Firebase emulators are running.
- `firebase.json`, `.firebaserc` (demo alias only), `database.rules.json` (deny all): local emulator configuration only.
- `.gitea/workflows/ci.yml`: Gitea Actions CI.

## Verified commands

Run from the repository root with Node 24.21.0 and pnpm 12.15.0 (verified in SEGU-264):

- `pnpm install --frozen-lockfile`
- `pnpm lint`, `pnpm format`
- `pnpm typecheck`
- `pnpm test` (unit tests; the emulator test is skipped)
- `pnpm build` (emits `dist/`)
- `pnpm test:emulator`: `firebase emulators:exec --only auth,database --project demo-takebase` around the emulator test. Needs firebase-tools and Java; local evidence only, not run in CI.

Firebase is local only: demo-* projects and emulators. No remote Firebase, deploys or service-account keys.

## Evidence and review

Before edits: `wavelens status --repo <root>`, then `wavelens begin <issue-key> --repo <root> --wave <label> --workspace-id 237ef0f7-262b-4830-9d1a-c86b40b59fda`, and require the recorded baseline. Run checks through `wavelens record --repo <root> --scope local -- <command>`. At each checkpoint post a Multica comment and run `wavelens preview --no-open --publish --repo <root>`; local copies go to the git-ignored `reviews/`.

## Git, Gitea and GitHub

- Default branch `master`. `origin` is Gitea `ssh://git@gitea.home.lan:2222/takebase/firebase-rtdb.git`, which push-mirrors automatically to GitHub `https://github.com/takebase/firebase-rtdb`.
- Branches `feature/<ISSUE-KEY>-<short-description>` from current `master`; commit subjects `<ISSUE-KEY>: <imperative summary>`. Gitea Actions reports results to the Multica issue through the key.
- Branches land on `master` through a Gitea PR whose title carries the key. Never commit `reviews/` or `AGENTS.md`. No AI attribution lines.
- Push, PR, merge and publishing each require the human's explicit request.

## License and publishing

`"private": true` with no license. Not published to npm, and the GitHub mirror stays private, until the Takebase license is chosen (SEGU-239).

## Durable instruction ownership

`PROJECT_GUIDE.md`, `CLAUDE.md`, `JUMBO.md` and `.agents/skills/` are durable guidance. Root `AGENTS.md` belongs to Multica as temporary runtime context; never create, edit, stage or commit it.
