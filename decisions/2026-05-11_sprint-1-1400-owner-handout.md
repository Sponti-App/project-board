# Sprint 1 14:00 Owner Handout

Date: 2026-05-11
Purpose: Align Sprint 1 owners on the next reviewable outcomes.

## Current Deployment State

- `sponti-spa`: production `Ready`; root, `/login`, and `/register` return 200.
- `sponti-auth`: production `Ready`; `/health` is green; unauthenticated `/auth/me` returns 401.
- `sponti-api`: production `Ready`; `/health` is green at `https://sponti-api-pi.vercel.app/health`.
- `sponti-api`: protected route `GET /api/v1/events` still returns 500, including with an invalid bearer token.
- `sponti-api`: required production env names are present; values were not exposed.
- Use `https://sponti-api-pi.vercel.app` as the active API alias. `https://sponti-api.vercel.app` is not active.

## Owner Focus

| Owner | Sprint 1 focus | First reviewable outcome |
| --- | --- | --- |
| Martin | Board, smoke checklist, demo data/reset plan, Vercel checks, Google Calendar research | Keep S1 board current; capture API deployment evidence and a first smoke checklist draft. |
| Nil | API protected route 500, JWT compatibility, technical review | Explain why `/api/v1/events` returns 500 while `/health` is green; define the minimal fix or next debug step. |
| Samara | Create flow, RSVP, My Meetups, feature integration | Prepare create/feed integration work that can resume once protected API route behavior is clear. |
| Patrick | MVP route/page gap audit, Google Maps UI/config, responsive UX review | Mark event detail, settings/account/notification settings, QR/share, and manage-friends as build now, fold into existing page, or defer. |

## Immediate Sequence

1. Nil diagnoses the protected API route 500.
2. Nil/Samara verify one auth-issued token against one protected API route after the 500 is resolved.
3. Samara continues create/feed/detail/RSVP/My Meetups integration.
4. Patrick completes the MVP page/route gap audit and Google Maps config review.
5. Martin drafts demo data/reset expectations and Google Calendar handoff options.

## Guardrails

- Keep secrets out of GitHub, Slack, screenshots, and docs.
- Do not ask Nil to verify Vercel settings directly; Martin owns Vercel access/config checks.
- Keep Sprint 1 focused on auth, create, feed/detail, RSVP, My Meetups, host controls, deployment, and seed data.
- Defer chat, DMs, push notifications, advanced privacy, QR scanning, payments, recommendations, and AI event creation unless P0 is already green.
