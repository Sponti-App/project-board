# Spontapp Kanban

Last updated: 2026-05-07

## Rules

- This is the team-facing project board.
- Private email logs and Codex notes stay local.
- Active sprint columns are: `Backlog`, `In Progress`, `Review`, `Blocked`, `Done`.
- A card moves to `Done` only when completion is confirmed by the owner, Martin, or accepted project evidence.
- Cards should describe reviewable outcomes, not every backend/frontend subtask.
- Pending decisions stay as notes on the affected cards.
- Nil has final technical vote when architecture decisions are split.
- MVP scope stays focused on auth, create meetup, feed, detail, RSVP, My Meetups, host controls, deployment, and seed data.

## Sprint 0 - Current

Goal: Align MVP scope, wireframes, data model, app/API foundation, auth foundation, and deployment path by Friday 2026-05-08.

### In Progress

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S0-001 | P0 | Product, Technical decision | Confirm MVP scope and technical direction | Martin + Nil | Team | 2026-05-06 | Deployment direction is now Vercel monorepo projects: `spa/` and `auth-server/` deployed separately, with `api/` pending until real service code exists. Next technical decision is the minimal API shape and frontend/backend URL wiring. |
| S0-002 | P0 | Data, Backend | Finalize data model and database plan | Nil | Samara + Martin | 2026-05-07 | Nil is organizing the data models. Before deploy/wiring, confirm the MVP subset needed now: users, events, event members/participants, and basic trust/connection fields. |
| S0-003 | P0 | Foundation, Deployment | Create deployable app/API foundation | Nil | Martin + Samara + Patrick | 2026-05-07 | `sponti-spa` and `sponti-auth` are deployed from `main`; auth `/health` is green. `api/` still has no real service code, so the API foundation remains open for minimal health route/scaffold. |
| S0-005 | P0 | Auth, Frontend, Backend | Build auth foundation and prototype | Nil + Samara | Patrick | 2026-05-07 | Auth service is deployed and connected to MongoDB Atlas. Next work is frontend auth UI integration, CORS/origin config, and confirming register/login/me behavior against the deployed service. |
| S0-006 | P0 | Design | Create main wireframes and visual rules | Patrick | Martin + Samara | 2026-05-06 | Patrick has started a Miro page. Martin helps Patrick finish wireframes today, 2026-05-06, before standup; goal is usable wireframe direction, not polished implementation. |

### Review

No cards currently in review.

### Blocked

No confirmed blocked cards.

### Backlog

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Done when / notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S0-007 | P0 | Product, QA, Demo | Define acceptance criteria, demo path, and sprint review notes | Martin | Samara + Patrick + Team | 2026-05-08 | Core feature acceptance criteria, 5-7 minute demo path, and Friday sprint review notes are documented. |

### Done

| ID | Priority | Labels | Card | Primary | Done date | Done note |
| --- | --- | --- | --- | --- | --- | --- |
| S0-008 | P0 | Process | Create Markdown Kanban board / GitHub project-board repo | Martin | 2026-05-05 | Public `Sponti-App/project-board` repo created and initial team-facing Kanban published. |
| S0-004 | P0 | Data, Deployment | Set up database and environment variables | Martin + Nil | 2026-05-07 | MongoDB Atlas and Vercel env names are configured for deployed auth; `sponti-auth` can connect and `/health` returns green. Secret values are not documented in this repo. |

## Sprint 1 - Core MVP

Goal: Build the true MVP flow end to end by Friday 2026-05-15.

### Backlog

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S1-001 | P0 | Auth, App shell | Complete auth and protected app shell | Nil | Samara | 2026-05-15 | User can register/login/logout, current-user state works, and protected pages reject logged-out users. |
| S1-002 | P0 | Events, Create flow | Create meetup vertical slice | Samara | Nil + Patrick | 2026-05-12 | User can create a meetup through the UI; event and participant records are created; required validation and useful errors exist. |
| S1-003 | P0 | Feed, Detail | Feed and detail vertical slice | Nil + Samara | Patrick | 2026-05-13 | Feed returns visible, non-cancelled meetups sorted by start time; detail page shows host, time, location, description, visibility, capacity/participants, and current user state. |
| S1-004 | P0 | RSVP | RSVP join/leave vertical slice | Samara | Nil | 2026-05-13 | User can join, leave, or update RSVP safely from the UI; duplicate participation is prevented. |
| S1-005 | P0 | My Meetups, Host controls | My Meetups and host controls | Samara | Martin + Nil | 2026-05-15 | Created and joined meetups are visible; only the host can edit or cancel their own meetup. |
| S1-006 | P0 | Demo, Data | Demo data and seed reset | Martin | Samara | 2026-05-15 | Demo users, friendships/trust context, meetups, and participants can be recreated quickly before review or rehearsal. |
| S1-007 | P0 | Deployment, QA | Deployed MVP integration and smoke checklist | Nil + Martin | Samara | 2026-05-15 | Deployed app supports auth, create, feed, detail, RSVP, and My Meetups; smoke checklist passes on the deployed environment. |
| S1-008 | P1 | QA, Process | Basic automated checks before merge | Nil | Samara | 2026-05-15 | At least lint/build or minimal API route checks run before important P0 merges. |
| S1-009 | P1 | Friends, Trust | Basic friendship flow | Nil | Samara | After P0 flow is green | Add/request/accept works if the team decides this is needed beyond seeded trust context. |
| S1-010 | P1 | RSVP | Capacity enforcement | Samara | Nil | After RSVP is stable | Joining is blocked when max participants is reached. |
| S1-011 | P1 | Comments | Event comments | Nil + Samara | Patrick | After MVP is green | Simple event comments work end to end only if the core MVP flow is already stable. |

## Sprint 2 - Freeze / Demo

Goal: Stabilize, polish, smoke test, rehearse, and freeze by Wednesday 2026-05-20.

### Backlog

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S2-001 | P0 | QA, Risk | Bug triage and freeze-candidate risk review | Martin | Team + Nil | 2026-05-19 | Bugs are marked blocking/non-blocking, final code/demo risks are reviewed, and the team knows what must be fixed before freeze. |
| S2-002 | P0 | Frontend, Design, Polish | Responsive and UX polish pass | Patrick | Samara + Martin | 2026-05-18 | Core pages work on mobile and laptop widths; empty/loading/error states are understandable; visual issues are fixed or documented. |
| S2-003 | P0 | Demo, Fallback | Demo readiness and fallback package | Martin + Patrick | Samara | 2026-05-18 | Demo accounts and data are ready, fallback screenshots exist, and the demo environment is known. |
| S2-004 | P0 | Presentation, Rehearsal | Final presentation and rehearsal | Martin | Team | 2026-05-20 | Elevator pitch, demo script, presenter roles, architecture/lessons slides, and full rehearsal are complete within the target time. |
| S2-005 | P0 | QA, Deployment, Freeze | Final deployed smoke test and code freeze | Martin + Nil | Samara | 2026-05-20 | Final deployed smoke test passes, main branch is frozen, and no more feature PRs merge. |

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
