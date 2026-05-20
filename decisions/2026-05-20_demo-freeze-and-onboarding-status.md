# Demo freeze and onboarding status

Date: 2026-05-20

## Decision

- Keep `main` as the presentable fallback for the final presentation.
- Continue feature and polish work on `dev`.
- If `dev` becomes unstable, present from `main`.

## Current repo status

- `main` is frozen as the fallback baseline.
- `dev` remains the active integration branch for demo polish.
- The historical 3-step pre-auth onboarding route was called `/onboarding`.
- The historical post-register home navigation overlay was implemented as `HomeTour` with helper state in `lib/onboarding.ts`.
- Both `/onboarding` and `HomeTour` were removed from the current `main` and `dev` source state before the final demo pass.

## Handoff note

If the team wants to recover or inspect the old onboarding work, search implementation history for:

- `spa/app/onboarding/page.tsx`
- `spa/components/home-tour.tsx`
- `spa/lib/onboarding.ts`
- `markHomeTourPending`
- `shouldShowHomeTour`
- commit `e3c2c96` (`Add onboarding flow`)
- commit `9373a7d` (`Remove home demo tour`)

If the home tour appears during testing, first verify that the tester is using latest `main` or `dev`, not an older feature branch, stale local dev server, stale build output, or old deployment preview.
