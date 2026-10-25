# Claude Code Instructions

@PROJECT_GUIDE.md
@JUMBO.md

OpenCode plans interactively. Claude Code implements the human-selected issue. Multica holds accepted plans, decisions, progress, and verification evidence.

## Resolve the current project

If the human has not explicitly named the current Multica project, ask: "Which Multica project should I use for this folder?" Wait for the answer. Use the Multica CLI to resolve its project and workspace IDs and verify that its attached local directory matches the current repository root. Stop on a missing or mismatched attachment.

The verified identity is **takebase/firebase-rtdb** (`00ddb0ab-ec04-4f03-bf3b-e7d83a025cfc`), workspace Segutrends (`237ef0f7-262b-4830-9d1a-c86b40b59fda`), root `/Volumes/Workspace/dev-drakecall/packages/node/takebase/firebase-rtdb`. Reverify it each session; stored identity is not permission to skip the CLI or human selection. Verified commands are listed in PROJECT_GUIDE.md.

Read PROJECT_GUIDE.md, JUMBO.md and the local skill for the requested work. Before source edits read `.agents/skills/execute-approved-plan/SKILL.md`. For separately authorized Git delivery read `.agents/skills/commit-and-close-issue/SKILL.md` in the same implementing session.

## Multica CLI access

Use direct `multica` commands for the human's requested project and issue operations, including descriptions, plans and progress comments. The prohibition on dispatching agents does not prohibit these CLI operations. Read existing content, preserve unrelated content, and verify the saved result. Use the installed CLI's supported flags; do not disable secret protections.

## One wave at a time

1. The human names the wave and selects the issue. Do not choose or start work independently.
2. Read the selected issue, latest comments, accepted plan and decisions with the Multica CLI, then map the relevant code (CodeGraph when `.codegraph/` exists, codebase-memory-mcp otherwise).
3. Before edits run `wavelens status --repo <root>`, conditionally `wavelens begin <issue-key> --repo <root> --wave <label> --workspace-id 237ef0f7-262b-4830-9d1a-c86b40b59fda`, and recheck. Require the matching pre-edit baseline. Never replace another wave automatically.
4. Implement the approved scope. Run checks through `wavelens record --repo <root> --scope local -- <command>`. Preserve failures and distinguish unavailable checks from passed checks.
5. At each agreed checkpoint, post a `multica issue comment add` with what changed, checks passed/failed/unavailable and remaining work. Check patch scope and privacy, then run `wavelens preview --no-open --publish --repo <root>` (retry `wavelens publish` if only publication failed).
6. Stop for human review.

## Selected issue status lifecycle

The human's request to plan or implement a selected issue authorizes routine status updates (`multica issue status <issue> <key> --no-start`, then read back). Planning → Awaiting Approval → In Progress → In Review while a human acceptance or delivery step is pending → Done once acceptance criteria and checks pass, the Wavelens review is attached and, for code that ships, the PR to `master` is merged (record the PR link and merge commit). Blocked for a concrete unresolved prerequisite or failed check. Passing CI alone never makes an issue Done. Publication never changes status.

## Coding conventions

- Arrow functions (`const name = (...) => { ... }`), not function declarations.
- Runtime code uses Web APIs only (fetch, Web Streams, AbortSignal, TextEncoder/TextDecoder): no runtime dependencies, no Node-only APIs. It must run in workerd and Node.
- Never keep mutable per-user or per-request state at module scope. A client instance holds its own credentials and tokens in a closure; consumers create it in their composition root.
- Errors are `FirebaseRtdbError` with fixed codes and content-free messages: never include URLs, paths, tokens, credentials or response bodies.
- Biome formatting (tabs, width 120, double quotes); `.ts` import extensions.

Root AGENTS.md is temporary Multica context; never create, edit, delete, stage or commit it. Do not invoke Jumbo commands or dispatch agents, wakeups, schedules, or automatic follow-up. Commit, push, pull request, merge, publish and deploy require the corresponding human request. Never add `Co-Authored-By:` or other AI attribution lines.
