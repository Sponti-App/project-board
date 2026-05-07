# Deployment Foundation Outcome

Date: 2026-05-07

## Decision

Use Vercel monorepo projects for the current deployment foundation:

| Vercel project | Root directory | Purpose |
| --- | --- | --- |
| `sponti-spa` | `spa/` | Frontend app |
| `sponti-auth` | `auth-server/` | Authentication service |
| `sponti-api` | `api/` | Future main API service |

Production deployments should continue to come from `main`. Pull request and feature-branch deployments should be used as Vercel Previews before merging.

## Current Evidence

- `sponti-spa` is live: https://sponti-spa.vercel.app
- `sponti-auth` is live: https://sponti-auth.vercel.app/health
- Auth health check returns:

```json
{"status":"ok","service":"auth-server"}
```

The implementation repo's latest checked `main` commit is `ef78477` (`Merge pull request #6 from Sponti-App/dev`).

Current repo shape on `main`:

- `spa/` has a real Next.js app and builds on Vercel.
- `auth-server/` has a real Express/Mongo auth service and deploys on Vercel.
- `api/` still has no real service code yet.

## Notes

The first SPA deployment showed a 404 because Vercel initially had incorrect framework/output settings. Resetting the SPA project to Next.js defaults fixed the deployment.

The first auth runtime failed because MongoDB Atlas allowed Martin's local IP but not Vercel runtime traffic. Atlas Network Access was updated so Vercel can connect. Secret values remain outside this repo.

## Follow-Up

- Decide the smallest useful `api/` scaffold before creating `sponti-api`.
- Add frontend environment wiring for deployed service URLs when integration starts.
- Add CORS/origin rules before the deployed SPA calls the auth service from the browser.
- Smoke test register/login/me against deployed auth before treating auth as feature-complete.

## Related Files

- [KANBAN.md](../KANBAN.md)
- [DEPLOYMENT.md](../DEPLOYMENT.md)
