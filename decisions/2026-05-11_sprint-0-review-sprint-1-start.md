# Sprint 0 Review And Sprint 1 Start

Date: 2026-05-11
Sprint naming: Sprint 1 starts today, Monday 2026-05-11.

## Executive Summary

Sprint 0 achieved the deployment foundation: `sponti-spa`, `sponti-auth`, and `sponti-api` all exist as Vercel projects with the expected root directories. `sponti-spa` and `sponti-auth` are production-ready enough for Sprint 1 integration checks: the SPA loads, auth pages load, auth `/health` is green, and unauthenticated `/auth/me` returns 401 as expected.

The main carry-over is `sponti-api`: production deployment is `Ready`, but runtime requests fail with `500 FUNCTION_INVOCATION_FAILED`. Runtime logs point to a Mongoose ESM import problem: named import `models` from `mongoose`. A `feat/api_mid` branch appears to address this pattern, but it is not merged to `main` and its protected preview health could not be publicly verified.

## Current Verified State

| Area | Status | Evidence |
| --- | --- | --- |
| Main repo | `Sponti-App/Sponti` default branch is `main`; latest `main` commit checked is `7b38c258` from PR #16. | GitHub repo/commit/PR check. |
| Open PRs/issues | No open PRs or issues found in `Sponti-App/Sponti` or `Sponti-App/project-board`. | GitHub PR/issue list. |
| Preview branch | Branch `feat/api_mid` exists at `648831e`; latest Vercel previews were created from it. | GitHub branch list and Vercel deployment list. |
| `sponti-spa` | Production `Ready`; root, `/login`, and `/register` return 200. Root Directory is `spa`. | Vercel inspect and HTTP checks. |
| `sponti-auth` | Production `Ready`; `/health` returns `{"status":"ok","service":"auth-server"}`; unauthenticated `/auth/me` returns 401. Root Directory is `auth-server`. | Vercel inspect and HTTP checks. |
| `sponti-api` | Production `Ready`, but runtime health fails. Root Directory is `api`. Active production alias is `https://sponti-api-pi.vercel.app`. | Vercel inspect, HTTP checks, runtime logs. |

## Sprint 0 Review

Completed:

- Vercel monorepo deployment model confirmed: one project per service.
- `sponti-spa` deployed from `spa`.
- `sponti-auth` deployed from `auth-server` and has a green health endpoint.
- `sponti-api` deployed from `api`.
- Auth UI/client scaffolding exists in the SPA.
- Main API scaffold exists with models, routes, validation, auth middleware, and tests.
- Project board/coordination repo is active as the team-facing Markdown mirror.

Partially completed:

- API foundation exists but is not production-healthy.
- Auth is deployed, but real register/login/me smoke testing with demo users is still needed.
- Frontend has auth/API base URL support, but end-to-end app/API wiring is blocked until API health is green.
- Wireframes/UI direction exists, but MVP flow QA still needs Sprint 1 review.

Carried over:

- Fix and redeploy `sponti-api`.
- Verify deployed API `/health`.
- Confirm deployed SPA `NEXT_PUBLIC_AUTH_BASE_URL` and `NEXT_PUBLIC_API_BASE_URL`.
- Smoke test auth against production.
- Build and verify create, feed, detail, RSVP, My Meetups, host controls, and seed/demo data.

Deployment/technical lessons:

- A Vercel deployment can be `Ready` while all runtime routes fail.
- Public health endpoints and runtime logs are required before marking a service usable.
- Root Directory settings are now verified: `spa`, `auth-server`, `api`.
- The API public alias needs clarity: `sponti-api-pi.vercel.app` is active; `sponti-api.vercel.app` returns 404.
- API `ACCESS_JWT_SECRET` must match auth `JWT_SECRET`; do not document values.

Remaining blockers:

- API runtime import failure on production.
- API production alias mismatch/confusion.
- API preview routes are protected, so public health could not be checked there.
- Sprint 1 smoke checklist and seed/reset plan are not yet written.

## Blocker Report

| Category | Blocker | Owner |
| --- | --- | --- |
| Deployment | `sponti-api` production returns 500 on `/`, `/health`, `/api/health`, and `/api/v1/events`. | Nil |
| Deployment | Latest `feat/api_mid` `sponti-spa` preview shows Vercel `Error`; `sponti-auth` and `sponti-api` previews show `Ready` but protected. | Nil + Patrick/Samara depending on failing SPA build surface |
| API/backend | Runtime log: `mongoose` does not provide named export `models`. `main` imports `models` from `mongoose` in API models. | Nil |
| API/backend | Verify API env names exist in production: `MONGO_URI`, `DB_NAME`, `CLIENT_BASE_URL`, `ACCESS_JWT_SECRET`; do not expose values. | Nil + Martin |
| Frontend integration | SPA needs confirmed production `NEXT_PUBLIC_AUTH_BASE_URL` and `NEXT_PUBLIC_API_BASE_URL`. | Nil + Samara |
| Frontend integration | Google Maps API needs to be configured and verified for event location UI. | Patrick |
| Frontend integration | Create/feed/detail/RSVP cannot be verified against production until API health is green. | Samara + Nil |
| Product/UX | Sprint 1 acceptance checklist and demo seed/reset expectations need to be made concrete. | Martin |
| Product/UX | Google Calendar integration is research-only in Sprint 1; avoid adding OAuth/calendar-write scope until MVP is green. | Martin |
| Product/UX | Create/detail/RSVP/My Meetups responsive UX needs review before freeze. | Patrick |

## Sprint 1 Priorities

1. Fix `sponti-api` runtime and redeploy production.
   Acceptance: `GET https://sponti-api-pi.vercel.app/health` returns 200 with service `sponti-api`; runtime logs have no import crash.

2. Verify auth/API JWT compatibility.
   Acceptance: an auth-issued access token can call one protected API route and receives expected success or domain-level validation, not token rejection due to secret/payload mismatch.

3. Confirm frontend env wiring.
   Acceptance: production SPA points to deployed auth and API base URLs; missing base URL errors do not occur in browser flows.

4. Smoke test auth.
   Acceptance: user can register/login/logout; current-user state works; protected pages reject logged-out users.

5. Build and verify create meetup vertical slice.
   Acceptance: user can create a meetup through the UI; event and host/member records are created; validation errors are understandable.

6. Build feed/detail/RSVP/My Meetups.
   Acceptance: feed and detail show deployed data; user can join/leave; created and joined meetups appear; only host can edit/cancel.

7. Prepare demo data and smoke checklist.
   Acceptance: demo users/events/trust context can be recreated, and the deployed smoke checklist passes before Sprint 1 review.

8. Get Google Maps API working for event location UI.
   Acceptance: deployed SPA has required public Google Maps env vars configured, map/location UI renders without key/config errors, and key restrictions are checked before demo use.

9. Research Google Calendar event handoff.
   Acceptance: Martin documents options for "put this event in your calendar" and recommends the lowest-risk MVP path. This is research only during Sprint 1, not an implementation commitment.

## Ownership

- Martin: board/status, acceptance criteria, smoke checklist, demo data/reset plan, Sprint 1 coordination.
- Martin: Google Calendar research for event calendar handoff; research only at this stage.
- Nil: API runtime fix, deployment health, JWT/env compatibility, technical review, merge readiness.
- Samara: frontend/backend integration, create flow, RSVP, My Meetups, feature QA.
- Patrick: Google Maps API setup for location UI, create/detail/RSVP UX review, responsive polish, visual QA, demo screenshots.

## What To Do First Today

1. Nil verifies or merges the minimal API runtime fix from `feat/api_mid`, then redeploys `sponti-api`.
2. Martin/Nil re-check API production health and alias.
3. Nil/Samara verify one auth token against one protected API route.
4. Samara starts create-flow wiring only after API health is green.
5. Patrick checks Google Maps API env/config and reviews the create/detail/RSVP screens for obvious UX blockers.
6. Martin captures Google Calendar integration options without starting implementation.

## Can Wait

- Friend flow beyond seeded trust context.
- Capacity enforcement until RSVP basics are stable.
- Comments.
- AI-assisted event creation.
- Google Calendar implementation beyond research.
- QR/contact, notifications polish, privacy/friend-list refinements.

## Sprint Numbering Check

The clean naming is:

- Sprint 0: 2026-05-04 to 2026-05-08, foundation/deployment setup.
- Sprint 1: 2026-05-11 to 2026-05-15, core MVP flow.
- Sprint 2: 2026-05-18 to 2026-05-20, stabilization/freeze/demo.

The board previously said `Sprint 0 - Current`; it is now updated to `Sprint 0 - Closed` and Sprint 1 is the active sprint.

## Could Not Verify

- Protected Vercel preview route health for `feat/api_mid`; previews returned Vercel Authentication pages.
- Actual secret presence or values; intentionally not inspected or documented.
- Full register/login flow with real demo credentials; no credentials were used.
