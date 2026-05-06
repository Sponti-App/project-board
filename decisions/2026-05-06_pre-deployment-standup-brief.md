# Pre-Deployment Standup Brief

Date: 2026-05-06
Focus: first Vercel deploy target for Thursday 2026-05-07, then Friday 2026-05-08 instructor/demo checkpoint.

## Standup Goal

Use this standup to confirm blockers before the first Vercel deploy and to lock the minimum page/API wiring direction.

The meeting should answer:

- What must be finished before the first Vercel deploy on 2026-05-07?
- What can wait until the Friday checkpoint on 2026-05-08?
- Which technical decisions still block Nil, Samara, Patrick, or Martin?

## Deployment-Critical Checklist

These should be resolved before or during Thursday's first Vercel deploy.

| Check | Card | Owner | Needed by | Standup question |
| --- | --- | --- | --- | --- |
| Backend wiring shape is decided | [S0-001](../KANBAN.md#sprint-0---current) | Martin + Nil | 2026-05-06 | Do API/auth routes live in Next.js route handlers, or in the separate Express `auth-server`? |
| MVP data subset is agreed | [S0-002](../KANBAN.md#sprint-0---current) | Nil | 2026-05-07 | Which collections are needed for first wiring: users, events, event members, basic connections only? |
| Vercel deploy path is unblocked | [S0-003](../KANBAN.md#sprint-0---current) | Nil | 2026-05-07 | Does the current Next app build and deploy? Who owns fixing build blockers? |
| Database/env plan is clear | [S0-004](../KANBAN.md#sprint-0---current) | Martin + Nil | 2026-05-07 | Which env vars are needed in Vercel and locally? Who creates/configures MongoDB Atlas access? |
| Auth/page prototype target is clear | [S0-005](../KANBAN.md#sprint-0---current) | Nil + Samara | 2026-05-07 | What is the minimum auth flow/page set needed before backend wiring is locked? |
| Wireframes are usable for routing/page stubs | [S0-006](../KANBAN.md#sprint-0---current) | Patrick + Martin | 2026-05-06 | Which pages must be represented today: home/feed, create/host, event detail, profile, settings/auth? |

## Friday Checkpoint Checklist

These do not have to block the first Vercel deploy, but should be clear by Friday's checkpoint.

| Check | Card | Owner | Needed by | Done when |
| --- | --- | --- | --- | --- |
| Sprint review notes and demo path | [S0-007](../KANBAN.md#sprint-0---current) | Martin | 2026-05-08 | The team can explain what works, what is blocked, and what Sprint 1 builds next. |
| Auth/app shell direction | [S1-001](../KANBAN.md#sprint-1---core-mvp) | Nil | 2026-05-15 | Register/login/logout and protected routes are planned against the chosen backend shape. |
| Create meetup vertical slice plan | [S1-002](../KANBAN.md#sprint-1---core-mvp) | Samara | 2026-05-12 | Data model, route, and UI expectations are aligned before implementation starts. |
| Feed/detail plan | [S1-003](../KANBAN.md#sprint-1---core-mvp) | Nil + Samara | 2026-05-13 | Page and API contract are clear enough for Sprint 1 work. |

## Decisions Needed

### 1. Backend Shape

Decision needed: Next.js route handlers vs separate Express `auth-server`.

Recommendation: use **Next.js App Router route handlers** for MVP API/auth.

Reason:

- The app repo is already Next.js + shadcn.
- Vercel is the deployment target.
- Next route handlers deploy naturally as Vercel Functions.
- Same-origin `/api/...` routes avoid CORS and two-service deployment wiring before Thursday.
- The separate `auth-server` is currently only a stub, so little work is being discarded.

Suggested decision wording:

```text
For MVP, backend/auth/API routes live in the Next.js app via route handlers.
Use Node.js runtime for MongoDB/Mongoose, bcrypt, and JWT.
The separate auth-server can be archived or ignored unless Nil explicitly wants to own a two-service setup.
```

### 2. MVP Data Subset

Decision needed: which parts of the data model are used now.

Recommendation: lock the deploy/wiring subset to:

- `users`
- `events`
- `event_members` or `event_participants`
- simple `connections` only if trust/visibility needs it

Defer for now:

- circles/friend lists
- QR contact tokens
- notification settings
- guest invite limits
- advanced profile privacy

Reason: Patrick's page map and Nil's data model include useful later features, but the Friday checkpoint needs a small model that supports auth, create, feed, detail, RSVP, and host controls.

### 3. Page Scope Before Wiring

Decision needed: which pages are real Sprint 0/1 pages vs placeholders.

Recommendation for first deploy/page stubs:

- home/feed
- event detail
- create/host event
- manage hosted event
- profile
- auth/login/register
- basic settings placeholder only if needed for navigation

Defer or placeholder:

- About
- FAQ/support/T&Cs
- Friend Lists
- QR Code
- Notifications flyout/settings
- Account settings beyond auth basics

## Known Risks To Raise

- Current code inspection showed a Next/shadcn scaffold and separate `auth-server` stub, not a working API yet.
- Current code inspection showed `@vercel/analytics/next` imported in `app/layout.tsx`; if the package is not installed, this may block build.
- Backend route shape must be chosen before Samara/Nil wire auth and event routes.
- Wireframes should guide routes and page stubs, but should not pull QR, notifications, friend lists, or static support pages into MVP.

## Suggested Standup Order

1. Confirm Vercel deploy owner and build blocker owner.
2. Confirm backend shape.
3. Confirm MVP data subset.
4. Confirm page/wireframe scope for today's page stubs.
5. Confirm Friday checkpoint deliverables.
6. Ask each person for blockers.

## Sources

- [KANBAN.md](../KANBAN.md)
- [PROJECT-BRIEF.md](../PROJECT-BRIEF.md)
- Read-only inspection of `https://github.com/NilAngelats/Sponti` at commit `e18a92c`
- Patrick's Miro page map shared by Martin on 2026-05-06
- Nil's data model screenshot shared by Martin on 2026-05-06
- Vercel documentation: [Next.js App Router route handlers deploy as Vercel Functions](https://vercel.com/docs/functions/runtimes/edge-runtime)
