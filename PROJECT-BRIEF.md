# Spontapp Project Brief

Last updated: 2026-05-11

## Product Summary

Spontapp / Sponti is a social meetup planning app for quick, low-pressure coordination of small activities happening now or soon.

The product should help students and young professionals create, discover, and join trusted small-group meetups without the overhead of formal event platforms or noisy group chats.

## MVP Scope

The MVP is a deployed app where a user can:

- sign in
- see basic profile/trust context
- create a NOW or SOON meetup
- discover meetups in a feed
- open meetup details
- RSVP / join / leave
- see created and joined meetups in My Meetups
- edit or cancel their own hosted meetup

The demo must be supported by deployed frontend/backend/database services and stable seed data.

## Team Roles

| Person | Role | Main responsibilities |
| --- | --- | --- |
| Martin | Project / product coordination | Scope, board, mentor prep, decision tracking, acceptance criteria, QA/smoke tests, demo story, seed/demo data, Vercel access/config coordination, AI-supported workflow. |
| Nil | Technical Lead | Architecture, app/repo skeleton, backend foundation, auth, API structure, CORS/env requirements, code quality, technical blockers, runtime fixes. |
| Samara | Implementation Lead | Feature delivery, frontend/backend integration, event models/routes, create flow, RSVP, detail page, validation, feature QA. |
| Patrick | UX/UI Lead | Wireframes, user flows, visual system, create-flow UX, responsive/design QA, screenshots, presentation visuals. |

## Review Rules

- Nil or Samara reviews code-facing P0 work before merge.
- Patrick reviews UX/UI-affecting work before the team locks in flows or screens.
- Martin owns product acceptance, scope control, demo readiness, and board coordination.
- Nil has final technical vote when architecture decisions are split.

## Sprint Checkpoints

| Sprint | Dates | Goal |
| --- | --- | --- |
| Sprint 0 | 2026-05-04 to 2026-05-08 | Align MVP scope, wireframes, data model, app skeleton, backend/auth foundation, and deployment path. |
| Sprint 1 | 2026-05-11 to 2026-05-15 | Build the core MVP flow end to end: auth, create, feed, detail, RSVP, My Meetups, host controls, deployment. |
| Sprint 2 | 2026-05-18 to 2026-05-20 | Stabilize, polish, smoke test, rehearse, and freeze before Demo Day. |

## Current Technical Direction

The current implementation direction is a Vercel monorepo with one Vercel project per service:

- `spa/`: Next.js frontend, deployed as `sponti-spa`.
- `auth-server/`: Express authentication service, deployed as `sponti-auth`.
- `api/`: Express main business API, deployed as `sponti-api`.
- MongoDB Atlas + Mongoose for persistence.

Sprint 1 should stabilize this deployed shape rather than reopening framework or deployment decisions. Nil keeps final technical vote on implementation details.

## Cut / Deferred For MVP

These should not block the May 20 freeze:

- full chat
- direct messages
- push/email/in-app notification system
- granular privacy/friends lists
- friends-of-friends visibility
- QR scanning
- payments/ticketing
- advanced matching/recommendations
- post-event albums/photos
- AI voice/transcript planning
- background group-chat bot

AI-assisted event creation is stretch only. The app must work without AI.
