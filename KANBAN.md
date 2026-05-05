# Spontapp Kanban

Last updated: 2026-05-05

## Rules

- This is the team-facing project board.
- Private email logs and Codex notes stay local.
- Cards move between sections when status changes.
- Done cards move to `Done` with a done date and short note.
- Nil has final technical vote when architecture decisions are split.
- MVP scope stays focused on auth, create meetup, feed, detail, RSVP, My Meetups, host controls, deployment, and seed data.

## In Progress

| ID | Sprint | Priority | Card | Primary | Support | Checkpoint | Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S0-001 | Sprint 0 | P0 | Finalize simple data model diagram | Nil | Samara | 2026-05-08 | Working on MongoDB collections, relationships, and data structure. No blockers reported. |
| S0-002 | Sprint 0 | P0 | Confirm Vercel / Next.js / shadcn direction | Team | Nil final technical vote | 2026-05-06 | Decision email sent. Waiting for approvals, concerns, or standup decision. |
| S0-003 | Sprint 0 | P0 | Set up Markdown Kanban workflow | Martin | Codex | 2026-05-08 | Public project-board repo created and initial board published. |

## Ready

| ID | Sprint | Priority | Card | Primary | Support | Checkpoint | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S0-004 | Sprint 0 | P0 | Finalize MVP and cut list | Martin | Patrick | 2026-05-08 | Team agrees what will not be built before May 20. |
| S0-005 | Sprint 0 | P0 | Define demo story and click path | Martin | Patrick | 2026-05-08 | A 5-7 minute demo path exists in writing. |
| S0-006 | Sprint 0 | P0 | Define core acceptance criteria | Martin | Samara | 2026-05-08 | Auth, create, feed, detail, RSVP, and host controls are documented. |
| S0-007 | Sprint 0 | P0 | Create main wireframes | Patrick | Samara | 2026-05-08 | Feed, detail, create, profile, and My Meetups are sketched. |
| S0-008 | Sprint 0 | P0 | Set up simple auth frontend prototype | Samara + Patrick | Nil | 2026-05-08 | Simple auth screens exist for testing login/register wiring and design decisions. |
| S0-009 | Sprint 0 | P0 | Create app shell | Nil | Patrick | 2026-05-08 | App runs locally with main routes and layout. |
| S0-010 | Sprint 0 | P0 | Create backend/API skeleton with health check | Nil | Samara | 2026-05-08 | Health endpoint works locally. |
| S0-011 | Sprint 0 | P0 | Configure MongoDB connection | Nil | Samara | 2026-05-08 | Local backend connects to MongoDB Atlas/dev DB. |
| S0-012 | Sprint 0 | P0 | Start auth model/routes or route handlers | Nil | Samara | 2026-05-08 | Register/login/me direction is working or clearly stubbed. |
| S0-013 | Sprint 0 | P0 | Start deployment path | Nil | Martin | 2026-05-08 | First deployment path is chosen and started. |
| S0-014 | Sprint 0 | P0 | Prepare mentor session 1 questions | Martin | Team | 2026-05-05 | MVP scope, stack decision, wireframes, schema, and delivery risks are ready for Ryan. |

## Sprint 1 Backlog

| ID | Priority | Card | Primary | Support | Done when |
| --- | --- | --- | --- | --- | --- |
| S1-001 | P0 | Auth works end to end | Nil | Samara | User can register, log in, log out, and load current user state. |
| S1-002 | P0 | Seed demo users | Martin | Samara | Demo users can be recreated reliably. |
| S1-003 | P0 | Create meetup works | Samara | Patrick | User can create a NOW/SOON meetup with required fields and validation. |
| S1-004 | P0 | Feed works | Nil | Patrick | Feed loads visible meetups and supports NOW/SOON/upcoming treatment. |
| S1-005 | P0 | Detail page works | Samara | Nil | Detail page shows host, time, location, participant count, and RSVP state. |
| S1-006 | P0 | RSVP / join / leave works | Samara | Nil | User can join, leave, and see UI/backend state update. |
| S1-007 | P0 | My Meetups works | Samara | Martin | Created and joined meetups are visible. |
| S1-008 | P0 | Host edit/cancel works | Samara | Martin | Host can edit/cancel own meetup; non-host cannot. |
| S1-009 | P0 | Backend validation and errors | Samara | Nil | Required fields and invalid IDs return useful errors. |
| S1-010 | P0 | Deployed frontend talks to backend | Nil | Martin | Production frontend can call production backend/API routes. |
| S1-011 | P0 | Smoke test checklist | Martin | Samara | Login, create, feed, detail, RSVP, and My Meetups pass on deployed app. |
| S1-012 | P0 | Demo seed reset procedure | Martin | Samara | Team can restore demo data before rehearsal. |
| S1-013 | P0 | Sprint review demo | Martin | Team | Friday review can show rough but real deployed/local MVP flow. |

## Sprint 2 Backlog

| ID | Priority | Card | Primary | Support | Done when |
| --- | --- | --- | --- | --- | --- |
| S2-001 | P0 | Full deployed smoke test | Martin | Samara | Production demo path passes end to end. |
| S2-002 | P0 | Stable demo accounts and seed data | Martin | Samara | Credentials and seeded events are ready for demo. |
| S2-003 | P0 | Responsive polish pass | Patrick | Samara | Core pages work on mobile and laptop widths. |
| S2-004 | P0 | Bug triage before freeze | Martin | Team | Bugs are marked blocking or non-blocking before May 18. |
| S2-005 | P0 | Final mentor risk review | Martin | Nil | Ryan reviews final code/demo risk on May 19. |
| S2-006 | P0 | Final demo script | Martin | Team | Script fits 5-7 minutes and avoids technical detours. |
| S2-007 | P0 | Presenter roles | Martin | Team | Everyone has a speaking part and one person drives the app. |
| S2-008 | P0 | Fallback screenshots | Patrick | Martin | Demo story can still be shown if deployment is slow. |
| S2-009 | P0 | Architecture slide | Nil | Patrick | One simple diagram explains frontend, backend/API, and database. |
| S2-010 | P0 | Rehearse full flow | Team | Martin | Team completes the demo twice within time. |
| S2-011 | P0 | Code freeze | Martin | Nil | Final smoke test passes and no more feature PRs merge. |

## Should-Have Backlog

| ID | Priority | Card | Primary | Support | Start condition |
| --- | --- | --- | --- | --- | --- |
| P1-001 | P1 | Pulse feed polish | Patrick | Samara | MVP flow works locally and deployed. |
| P1-002 | P1 | Empty/loading/error states | Martin | Patrick | Main API states exist. |
| P1-003 | P1 | Capacity limit | Samara | Nil | RSVP flow is stable. |
| P1-004 | P1 | Shareable meetup link | Samara | Martin | Detail page is stable. |
| P1-005 | P1 | Friend add by username | Nil | Samara | Core flow is deployed and green. |
| P1-006 | P1 | Event comments | Nil | Samara | MVP is green and backend route time remains. |
| P1-007 | P1 | Basic automated checks | Nil | Samara | Core implementation structure exists. |
| P1-008 | P1 | Cross-device visual check | Patrick | Samara | Main pages are implemented. |
| P1-009 | P1 | Lessons-learned slide | Martin | Team | Presentation outline exists. |

## Blocked

No confirmed blocked cards.

## Review

No cards currently in review.

## Done

No cards confirmed done yet.

When a card is confirmed done, move it here:

| ID | Sprint | Priority | Card | Primary | Done date | Done note |
| --- | --- | --- | --- | --- | --- | --- |

## Cut / Deferred

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

## Stretch Only

- AI-assisted create flow / event draft helper
- QR contact card generation
- External calendar export
- Simple map link
- Event categories/interests
- Regular meetups marked manually
