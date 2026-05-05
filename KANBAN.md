# Spontapp Kanban

Last updated: 2026-05-05

## Rules

- This is the team-facing project board.
- Private email logs and Codex notes stay local.
- Active sprint columns are: `Backlog`, `In Progress`, `Review`, `Blocked`, `Done`.
- A card moves to `Done` only when completion is confirmed by the owner, Martin, or accepted project evidence.
- Pending decisions stay as notes on the affected cards.
- Nil has final technical vote when architecture decisions are split.
- MVP scope stays focused on auth, create meetup, feed, detail, RSVP, My Meetups, host controls, deployment, and seed data.

## Sprint 0 - Current

Goal: Align MVP scope, wireframes, data model, app skeleton, backend/auth foundation, and deployment path by Friday 2026-05-08.

### In Progress

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S0-006 | P0 | Data, Backend | Finalize simple data model diagram | Nil | Samara | 2026-05-08 | Nil is working on the MongoDB data diagram, collections, relationships, and overall data structure. No blockers reported. |
| S0-018 | P0 | Technical decision, Standup-added | Confirm Vercel / Next.js / shadcn direction | Team | Nil final technical vote | 2026-05-06 | Decision email sent. Waiting for approvals, concerns, or standup decision. |
| S0-019 | P0 | Mentor, Standup-added | Prepare mentor session 1 questions | Martin | Team | 2026-05-05 | Prepare questions on MVP scope, Vercel/Next/shadcn, backend shape, wireframes, schema, and delivery risks for Ryan. |

### Review

No cards currently in review.

### Blocked

No confirmed blocked cards.

### Backlog

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Done when / notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S0-001 | P0 | Product, Scope | Finalize MVP and cut list | Martin | Patrick | 2026-05-08 | Team agrees what will not be built before May 20. |
| S0-003 | P0 | Product, Demo | Define demo user story and click path | Martin | Patrick | 2026-05-08 | A 5-7 minute demo path exists in writing. |
| S0-004 | P0 | Product, QA | Define acceptance criteria for core features | Martin | Samara | 2026-05-08 | Auth, create, feed, detail, RSVP, and host controls are documented. |
| S0-005 | P0 | Design | Create wireframes for main screens | Patrick | Samara | 2026-05-08 | Feed, detail, create, profile, and My Meetups are sketched. |
| S0-007 | P0 | Frontend, Pending stack decision | Create app shell | Nil | Patrick | 2026-05-08 | Roadmap original: React/Vite app shell. Update wording if Next.js is approved. |
| S0-008 | P0 | Backend, Pending stack decision | Create backend/API skeleton with health check | Nil | Samara | 2026-05-08 | Roadmap original: Express app skeleton with `/api/health`. Update wording if Next route handlers are approved. |
| S0-009 | P0 | Data, Backend | Configure MongoDB connection | Nil | Samara | 2026-05-08 | Local backend connects to MongoDB Atlas/dev DB. Runtime pattern depends on stack decision. |
| S0-010 | P0 | Backend, Auth, Pending stack decision | Create User model and auth routes | Nil | Samara | 2026-05-08 | Register/login/me direction works with hashed passwords, or route-handler equivalent if Next.js is approved. |
| S0-011 | P0 | Backend, Auth | Add auth middleware / auth guard | Nil | Samara | 2026-05-08 | Protected routes reject missing/invalid tokens, or equivalent auth guard is agreed. |
| S0-012 | P0 | Data, Deployment | Create MongoDB Atlas database | Martin | Nil | 2026-05-08 | Connection string works locally and in the chosen deployment target. |
| S0-013 | P0 | Deployment, Pending stack decision | Deploy backend/API to chosen platform | Nil | Martin | 2026-05-08 | `/api/health` or equivalent works in production/preview. Roadmap original target was Render; decision may change to Vercel. |
| S0-014 | P0 | Deployment, Pending stack decision | Deploy frontend/app to chosen platform | Nil | Martin | 2026-05-08 | Production/preview frontend loads. Roadmap original target was Render; decision may change to Vercel. |
| S0-015 | P0 | Deployment | Configure environment variables | Martin | Nil | 2026-05-08 | Frontend/backend/API URLs and secrets are configured for the chosen deployment target. |
| S0-016 | P0 | Deployment | Configure CORS or same-origin API policy | Nil | Martin | 2026-05-08 | Deployed frontend can call deployed backend/API. May be simplified if using a same-origin Next.js app. |
| S0-017 | P0 | Frontend, Design, Auth, Standup-added | Set up simple auth frontend prototype | Samara + Patrick | Nil | 2026-05-08 | Simple auth screens exist for testing login/register wiring and frontend decision points. |
| S0-022 | P0 | Deployment, Routing | Add frontend redirect/rewrite rule | Martin | Nil | 2026-05-08 | Refreshing nested routes does not 404, or equivalent Next.js routing behavior is verified. |
| S0-020 | P1 | Design | Decide visual style and component rules | Patrick | Team | 2026-05-08 | Color, spacing, buttons, forms, and cards have one shared direction. |
| S0-021 | P1 | Process | Prepare weekly sprint review notes | Martin | Team | 2026-05-08 | Friday review can show progress, blockers, and next sprint goals. |

### Done

| ID | Priority | Labels | Card | Primary | Done date | Done note |
| --- | --- | --- | --- | --- | --- | --- |
| S0-002 | P0 | Process, Standup-added | Create Markdown Kanban board / GitHub project-board repo | Martin | 2026-05-05 | Public `Sponti-App/project-board` repo created and initial team-facing Kanban published. |

## Sprint 1 - Core MVP

Goal: Build the true MVP flow end to end by Friday 2026-05-15.

### Backlog

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S1-001 | P0 | Auth, Frontend | Implement auth pages | Nil | Samara | 2026-05-15 | User can register/login/logout from the UI. |
| S1-002 | P0 | Auth, Frontend | Implement protected route behavior | Nil | Samara | 2026-05-15 | Logged-out users are redirected or shown login where needed. |
| S1-003 | P0 | Backend, Data | Create Event model | Samara | Nil | 2026-05-11 | Events can be created and queried. |
| S1-004 | P0 | Backend, Data | Create EventParticipant model | Samara | Nil | 2026-05-11 | Unique event/user participation is enforced. |
| S1-005 | P0 | Backend, Events | Implement event create route | Samara | Nil | 2026-05-12 | Creating an event also creates the host participant record. |
| S1-006 | P0 | Frontend, Create flow | Implement create meetup flow | Samara | Patrick | 2026-05-12 | User can create a meetup with required fields and validation. |
| S1-007 | P0 | Backend, Feed | Implement event feed route | Nil | Samara | 2026-05-13 | Feed returns visible, non-cancelled events sorted by start time. |
| S1-008 | P0 | Frontend, Feed | Implement feed page | Nil | Patrick | 2026-05-13 | Feed loads events and filters NOW/SOON/upcoming. |
| S1-009 | P0 | Backend, Detail | Implement event detail route | Samara | Nil | 2026-05-13 | Detail includes host and participant summary. |
| S1-010 | P0 | Frontend, Detail | Implement event detail page | Samara | Nil | 2026-05-13 | Detail page shows event data and current RSVP state. |
| S1-011 | P0 | Backend, RSVP | Implement RSVP route | Samara | Nil | 2026-05-13 | User can join/leave/update RSVP safely. |
| S1-012 | P0 | Frontend, RSVP | Implement RSVP actions | Samara | Nil | 2026-05-13 | Join/leave updates backend and UI. |
| S1-013 | P0 | Frontend, My Meetups | Implement My Meetups page | Samara | Martin | 2026-05-15 | Created and joined meetups are visible. |
| S1-014 | P0 | Backend, Host controls | Implement host edit/cancel routes | Samara | Nil | 2026-05-15 | Only host can edit/cancel. |
| S1-015 | P0 | Frontend, Host controls | Implement host edit/cancel UI | Samara | Martin | 2026-05-15 | Host sees controls; non-host does not. |
| S1-016 | P0 | Backend, Validation | Backend validation and error responses | Samara | Nil | 2026-05-15 | Required fields and invalid IDs return useful status codes. |
| S1-017 | P0 | Data, Demo | Seed script | Martin | Samara | 2026-05-15 | Demo users, friends, events, and participants can be recreated quickly. |
| S1-018 | P0 | Deployment | Deployed frontend talks to backend/API | Nil | Martin | 2026-05-15 | Deployed app supports auth, create, feed, detail, RSVP, and My Meetups. |
| S1-019 | P0 | QA | Smoke test checklist | Martin | Samara | 2026-05-15 | Login, create, feed, detail, RSVP, and My Meetups pass on deployed app. |
| S1-020 | P0 | Demo, Data | Demo seed reset procedure | Martin | Samara | 2026-05-15 | Team can restore demo data before rehearsal. |
| S1-021 | P1 | Backend, Friends | Friendship routes | Nil | Samara | After P0 flow is green | Add/request/accept works if chosen for MVP. |
| S1-022 | P1 | Backend, RSVP | Capacity enforcement | Samara | Nil | After RSVP is stable | Join is blocked when max participants is reached. |
| S1-023 | P1 | Backend, Comments | Comments route | Nil | Samara | After MVP is green | Comments work only if frontend has time. |
| S1-024 | P1 | Frontend, Comments | Event comments UI | Nil | Samara | After MVP is green | Comment thread works only if backend route exists and MVP is green. |
| S1-025 | P1 | QA | Basic automated checks | Nil | Samara | 2026-05-15 | At least lint/build or minimal API route test runs before merge. |

## Sprint 2 - Freeze / Demo

Goal: Stabilize, polish, smoke test, rehearse, and freeze by Wednesday 2026-05-20.

### Backlog

| ID | Priority | Labels | Card | Primary | Support | Checkpoint | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S2-001 | P0 | Frontend, Responsive | Responsive pass | Patrick | Samara | 2026-05-18 | Core pages work on mobile and laptop widths. |
| S2-002 | P0 | QA | Bug triage list | Martin | Team | 2026-05-18 | Bugs are marked blocking/non-blocking before May 18. |
| S2-003 | P0 | Demo, Data | Prepare demo accounts | Martin | Samara | 2026-05-18 | Credentials are known and data is seeded. |
| S2-004 | P0 | Presentation | Draft elevator pitch | Martin | Patrick | 2026-05-18 | Problem, audience, and solution fit in 60-90 seconds. |
| S2-005 | P0 | Presentation | Draft final demo script | Martin | Team | 2026-05-18 | Script fits 5-7 minutes and avoids deep technical detours. |
| S2-006 | P0 | Presentation | Assign presenter roles | Martin | Team | 2026-05-18 | Everyone has a speaking part and one person drives the app. |
| S2-007 | P0 | Presentation, Fallback | Prepare fallback screenshots | Patrick | Martin | 2026-05-18 | If deployment is slow, the story can still be shown. |
| S2-008 | P0 | Mentor, Risk | Final mentor risk review | Martin | Nil | 2026-05-19 | Ryan reviews final code/demo risk before freeze. |
| S2-009 | P0 | QA, Deployment | Full deployed smoke test | Martin | Samara | 2026-05-20 | Deployed app has passed the primary demo path. |
| S2-010 | P0 | Demo | Rehearse full flow | Team | Martin | 2026-05-20 | Team completes the demo twice within time. |
| S2-011 | P0 | Freeze | Code freeze | Martin | Nil | 2026-05-20 | Final smoke test passes and no more feature PRs merge. |
| S2-012 | P1 | Frontend, Polish | Empty/loading/error states | Martin | Patrick | After main API states exist | Main API states are understandable to users. |
| S2-013 | P1 | QA, Design | Cross-device visual check | Patrick | Samara | After pages are implemented | Mobile/laptop layout issues are fixed or documented. |
| S2-014 | P1 | Presentation, Architecture | Prepare brief architecture slide | Nil | Patrick | 2026-05-19 | One simple diagram explains frontend, backend/API, and database. |
| S2-015 | P1 | Presentation | Prepare lessons-learned slide | Martin | Team | 2026-05-20 | Each member has one concise learning point. |

## Later - Should-Have / Stretch

These cards should not start until the deployed P0 flow is green.

### P1 Should-Have

| ID | Priority | Labels | Card | Primary | Support | Start condition | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| P1-001 | P1 | Feed, Polish | Pulse feed polish | Patrick | Samara | After MVP is green | Better sorting, empty states, activity labels, and NOW/SOON visual treatment. |
| P1-002 | P1 | Sharing | Shareable meetup link | Samara | Martin | After detail page is stable | User can copy/open a link to meetup detail. |
| P1-003 | P1 | Friends | Friend add by username | Nil | Samara | After core flow is green | Search user, request, and accept if chosen for MVP. |
| P1-004 | P1 | Notifications | Basic notification preferences UI | Martin | Patrick | After MVP is green | Simple per-event mute/preference UI only; no real push/email notification system. |
| P1-005 | P1 | Privacy | Profile privacy toggle | Samara | Nil | After visibility checks are stable | Public/private profile toggle if time remains. |
| P1-006 | P1 | Invites | Host guest-invite toggle | Samara | Patrick | After MVP is green | Store/show field only; no full invite-limit logic. |

### P2 Stretch

| ID | Priority | Labels | Card | Primary | Support | Start condition | Done when |
| --- | --- | --- | --- | --- | --- | --- | --- |
| P2-001 | P2 | AI, Create flow | AI-assisted create flow / event draft helper | Martin | Nil | Only after P0 flow is green | Optional and non-blocking. App must work with AI disabled. |
| P2-002 | P2 | Profile, QR | QR contact card UI | Patrick | Martin | Only after profile/friend flow is stable | Generated QR/contact link appears on profile. |
| P2-003 | P2 | Calendar | External calendar export | Samara | Martin | Only after event times are reliable | Download `.ics` or use calendar URL. |
| P2-004 | P2 | Location | Simple map link | Samara | Patrick | Only after P0 flow is deployed and green | Open address in Google Maps. No embedded map. |
| P2-005 | P2 | Feed, Filters | Event categories/interests | Patrick | Samara | Only if filtering is easy | Tags like food, study, sports, drinks. |
| P2-006 | P2 | Events | Regular meetups marked manually | Samara | Martin | Only after MVP is green | Do not build recurrence rules. |

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
