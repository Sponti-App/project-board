# Spontapp Kanban

Last updated: 2026-05-18

## Rules

- This is the team-facing project board.
- Private email logs and Codex notes stay local.
- Active sprint columns are: `Backlog`, `In Progress`, `Review`, `Blocked`, `Done`.
- A card moves to `Done` only when completion is confirmed by the owner, Martin, or accepted project evidence.
- Cards should describe reviewable outcomes, not every backend/frontend subtask.
- Pending decisions stay as notes on the affected cards.
- Nil has final technical vote when architecture decisions are split.
- MVP scope stays focused on auth, create meetup, feed, detail, RSVP, My Meetups, host controls, deployment, and seed data.

## Sprint 0 - Closed

Goal: Align MVP scope, wireframes, data model, app/API foundation, auth foundation, and deployment path by Friday 2026-05-08.

Sprint 0 is closed as of 2026-05-11. The foundation work is done enough for Sprint 1 to proceed; remaining work has been moved into Sprint 1 cards.

### Done

| ID | Priority | Labels | Card | Primary | Done date | Done note |
| --- | --- | --- | --- | --- | --- | --- |
| S0-001 | P0 | Product, Technical decision | Confirm MVP scope and technical direction | Martin + Nil | 2026-05-08 | Vercel monorepo deployment direction confirmed: `spa/`, `auth-server/`, and `api/` are separate Vercel projects. Sprint 1 remains focused on the true MVP flow. |
| S0-002 | P0 | Data, Backend | Finalize data model and database plan | Nil | 2026-05-08 | API models/routes exist. Sprint 1 will narrow implementation focus to the MVP flow. |
| S0-003 | P0 | Foundation, Deployment | Create deployable app/API foundation | Nil | 2026-05-08 | `sponti-spa`, `sponti-auth`, and `sponti-api` production deployments exist. API runtime health is tracked in Sprint 1. |
| S0-004 | P0 | Data, Deployment | Set up database and environment variables | Martin + Nil | 2026-05-07 | MongoDB Atlas and Vercel env names are configured for deployed auth. Secret values are not documented here. |
| S0-005 | P0 | Auth, Frontend, Backend | Build auth foundation and prototype | Nil + Samara | 2026-05-08 | Auth service is deployed and health is green; SPA auth pages and client wiring exist. Sprint 1 owns full auth smoke testing. |
| S0-006 | P0 | Design | Create main wireframes and visual rules | Patrick | 2026-05-08 | Core UI/page direction exists in the SPA. Sprint 1 owns MVP flow UX review. |
| S0-007 | P0 | Product, QA, Demo | Define acceptance criteria, demo path, and sprint review notes | Martin | 2026-05-08 | Sprint review inputs are captured; Sprint 1 owns smoke checklist and demo data. |
| S0-008 | P0 | Process | Create Markdown Kanban board / GitHub project-board repo | Martin | 2026-05-05 | Public `Sponti-App/project-board` repo created and initial team-facing Kanban published. |

### Key Lessons

- Vercel Root Directory must match each service folder: `spa`, `auth-server`, `api`.
- A Vercel deployment can be `Ready` while the runtime route is still failing; public health checks and runtime logs are required before marking a service usable.
- The API production alias is currently `https://sponti-api-pi.vercel.app`; `https://sponti-api.vercel.app` is not the active alias.
- API and auth JWT secrets must match before authenticated API routes can work with auth-issued access tokens.

## Sprint 1 - Core MVP

Goal: Build the true MVP flow end to end by Friday 2026-05-15.

Sprint 1 is accepted for transition to Sprint 2 as of 2026-05-18. Production smoke cleared the previous list/feed blocker: register, create event, `GET /events`, `GET /events/calendar/upcoming`, `GET /events/map/active`, `GET /connections`, `GET /users/search`, `GET /events/mine/upcoming`, and cancel all returned 200/201 with a real auth token.

This does not mean code freeze. Sprint 2 owns release-candidate review, branch promotion, demo data, polish, and final smoke.

### Done

| ID | Priority | Labels | Card | Primary | Done date | Done note |
| --- | --- | --- | --- | --- | --- | --- |
| S1-001 | P0 | Auth, App shell | Complete auth and protected app shell | Nil + Samara | 2026-05-18 | Auth production health and register flow are green. SPA auth routes build and deployed `/login` returns 200. |
| S1-002 | P0 | Events, Create flow | Create meetup vertical slice | Samara + Nil | 2026-05-18 | Production smoke created and cancelled a real event with an auth-issued token. |
| S1-003 | P0 | Feed, Detail | Feed and detail vertical slice | Nil + Samara | 2026-05-18 | Previous authenticated list/feed 500 blocker is cleared in production smoke across feed, calendar, map, connections, and user search routes. |
| S1-004 | P0 | RSVP | RSVP join/leave vertical slice | Samara + Nil | 2026-05-18 | Backend membership endpoint exists and local API tests cover RSVP-related event membership behavior. Final UX smoke stays in Sprint 2. |
| S1-005 | P0 | My Meetups, Host controls | My Meetups and host controls | Samara + Nil | 2026-05-18 | `/events/mine/upcoming`, host edit, cancel, and reactivate surfaces exist; production smoke verified my-upcoming and cancel. |
| S1-007 | P0 | Deployment, QA | Deployed MVP integration and smoke checklist | Martin + Nil | 2026-05-18 | API tests/build, auth build, SPA typecheck/build, and production runtime smoke are green. |
| S1-014 | P0 | Frontend, Routing, UX | Complete MVP page/route gap audit | Patrick + Samara | 2026-05-18 | Latest `dev` has home map/calendar, auth, menu pages, onboarding, settings, circles, event create/edit/dashboard, profile pages, QR route, and QR share flow. |
| S1-015 | P1 | Product, Onboarding, UX | Define onboarding flow | Martin + Patrick | 2026-05-18 | Onboarding route exists in latest `dev`; Sprint 2 should only polish and demo-test it. |

### Deferred / Folded Into Sprint 2

| ID | Priority | Labels | Card | Disposition |
| --- | --- | --- | --- | --- |
| S1-006 | P0 | Demo, Data | Demo data and seed reset | Folded into S2-003 and S2-005 because demo data is now a freeze/readiness concern. |
| S1-008 | P1 | QA, Process | Basic automated checks before merge | Replaced by S2-007 continuous review loop. |
| S1-009 | P1 | Friends, Trust | Basic friendship flow | QR/contact and connections exist; any trust/privacy expansion is deferred to P1 unless needed for demo. |
| S1-010 | P1 | RSVP | Capacity enforcement | Deferred unless the demo script depends on capacity limits. |
| S1-011 | P1 | Comments | Event comments | Deferred; not needed for the Wednesday demo. |
| S1-012 | P1 | Maps, Frontend, UX | Get Google Maps API working for event location UI | Folded into S2-002 polish and S2-005 final smoke. |
| S1-013 | P2 | Calendar, Research | Research Google Calendar event export/integration | Deferred to stretch; use route/map convenience only if it is already stable. |

## Sprint 2 - Freeze / Demo

Goal: Stabilize, polish, smoke test, rehearse, and freeze by Wednesday 2026-05-20.

### In Progress

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S2-001 | P0 | QA, Risk | Bug triage and freeze-candidate risk review | Martin | Team + Nil | 2026-05-18 | Bugs are marked blocking/non-blocking, final code/demo risks are reviewed, and the team knows what must be fixed before freeze. |
| S2-002 | P0 | Frontend, Design, Polish | Responsive and UX polish pass | Patrick | Samara + Martin | 2026-05-18 | Core pages work on mobile and laptop widths; empty/loading/error states are understandable; visual issues are fixed or documented. |
| S2-003 | P0 | Demo, Fallback | Demo readiness and fallback package | Martin + Patrick | Samara | 2026-05-18 | Demo accounts and data are ready, fallback screenshots exist, and the demo environment is known. |
| S2-006 | P0 | Git, Release | Reconcile `dev` and `main`, then cut release candidate | Nil + Martin | Samara | 2026-05-18 | `dev` and `main` divergence is reviewed, the release branch/PR is created, Vercel previews are green, and production receives only the approved release candidate. |
| S2-007 | P0 | Code review, Security | Start continuous code and security review loop | Martin + Nil | Codex | 2026-05-18 | Every final PR gets automated checks plus a focused Codex code review and security pass before merge or freeze approval. |

### Backlog

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S2-004 | P0 | Presentation, Rehearsal | Final presentation and rehearsal | Martin | Team | 2026-05-20 | Elevator pitch, demo script, presenter roles, architecture/lessons slides, and full rehearsal are complete within the target time. |
| S2-005 | P0 | QA, Deployment, Freeze | Final deployed smoke test and code freeze | Martin + Nil | Samara | 2026-05-20 | Final deployed smoke test passes, main branch is frozen, and no more feature PRs merge. |
| S2-008 | P1 | Security, Dependencies | Resolve or explicitly accept SPA dependency advisory | Nil | Martin | 2026-05-18 | `npm audit --audit-level=moderate` is reviewed; the Next/PostCSS advisory is upgraded, suppressed with rationale, or accepted as non-demo-blocking without using a breaking forced downgrade. |
| S2-009 | P1 | QA, Frontend | Clean non-blocking lint warnings | Samara + Patrick | Nil | 2026-05-19 | SPA lint has no stale unused variables or unused eslint-disable directives, or the remaining warnings are documented as non-blocking. |

## Later - Should-Have / Stretch

These cards should not start until the deployed P0 flow is green.

### P1 Should-Have

| ID | Priority | Labels | Card | Primary | Support | Start condition | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| P1-001 | P1 | Feed, Sharing, Polish | Feed and sharing polish | Patrick + Samara | Martin | After MVP is green | Feed sorting/labels/empty states are clearer and users can copy/open a meetup detail link. |
| P1-002 | P1 | Trust, Privacy, Invites | Trust and privacy refinements | Nil + Samara | Patrick | After core flow is green | Friend add, profile privacy, or host guest-invite toggle are added only if they are still useful and low risk. |
| P1-003 | P1 | Notifications | Basic notification preferences UI | Martin | Patrick | After MVP is green | Simple per-event mute/preference UI only; no real push/email notification system. |

### P2 Stretch

| ID | Priority | Labels | Card | Primary | Support | Start condition | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| P2-001 | P2 | AI, Create flow | AI-assisted create flow / event draft helper | Martin | Nil | Only after P0 flow is green | Optional and non-blocking. App must work with AI disabled. |
| P2-002 | P2 | Calendar, Location | Calendar and map conveniences | Samara | Martin + Patrick | Only after event times and location fields are reliable | Download `.ics`, open calendar URL, or open address in Google Maps. No embedded map required. |
| P2-003 | P2 | Profile, QR | QR contact card UI | Patrick | Martin | Only after profile/friend flow is stable | Generated QR/contact link appears on profile. |
| P2-004 | P2 | Feed, Events | Categories and lightweight recurrence | Patrick + Samara | Martin | Only after MVP is green | Categories/tags or manual regular meetup marking are added only if filtering remains simple. |

## Cut / Deferred

These should not block the May 20 freeze.

- Full real-time group chat
- Direct host DMs
- Push/email/in-app notification system
- Detailed quiet hours
- Granular privacy per friends list
- Friends-of-friends visibility
- Host/admin role delegation
- QR scanning
- Payments/ticketing
- Marketplace organizer tools
- Advanced matching/recommendations
- Weekly social goal tracking
- Post-event albums/photos
- AI voice/transcript planning
- Background group-chat bot
