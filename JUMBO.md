# takebase/firebase-rtdb — Accepted Project Knowledge

Read `PROJECT_GUIDE.md` for identity and workflow. This file holds durable, non-secret accepted knowledge only; Multica owns plans, task state and evidence.

## Accepted direction

- REST only, no Firebase SDK. Authentication is Firebase Auth email/password with user-scoped ID tokens, so Database Security Rules apply to backends too. No Admin SDK, service accounts or database secrets (accepted 2026-10-24, SEGU-216/SEGU-240).
- The client knows nothing about the data it carries; record contracts belong to the consumer.
- Strict target URLs: exactly the local emulator, or an HTTPS `*.firebaseio.com` / `*.firebasedatabase.app` origin without path, query, port or user info. Redirects are never followed.
- Errors use fixed codes with content-free messages. `isRetryable` separates temporary failures (timeouts, connection failures, 408/429/5xx) from permanent ones.
- Web APIs only and no runtime dependencies, so it runs in Cloudflare Workers and Node.
- Maintained separately from the company package `@segutrends/segufirebase`; changes are not synced between them.
- Takebase direction (SEGU-241): adapters and clients are independent packages users can plug in or replace; this package must not depend on `@takebase/core`.

## Memory boundaries

Claude Code treats this file as static guidance and never invokes Jumbo commands. Never store secrets, customer data, raw conversations, full plans or temporary status here.
