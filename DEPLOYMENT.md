# Spontapp Deployment

Last updated: 2026-05-11

## Purpose

This document explains the current Vercel deployment setup for Spontapp / Sponti. It is team-facing and intentionally does not include secret values.

## Current Status

| Vercel project | Repo folder | Status | URL |
| --- | --- | --- | --- |
| `sponti-spa` | `spa/` | Production deployment `Ready`; root and auth pages return 200 | https://sponti-spa.vercel.app |
| `sponti-auth` | `auth-server/` | Production deployment `Ready`; auth smoke green | https://sponti-auth.vercel.app/health |
| `sponti-api` | `api/` | Production deployment `Ready`; `/health` and event CRUD-by-ID smoke green, feed/list routes return 500 | https://sponti-api-pi.vercel.app/health |

`sponti-api` is deployed and the previous pre-auth route crash is cleared. After rotating the Mongo URI and redeploying, `GET /api/v1/events` with an invalid bearer token returns 401 instead of 500. With a real auth-issued token, event create, read by ID, update, RSVP/membership update, and cancel pass. The remaining backend issue is the list/feed-style route group returning 500: `GET /api/v1/events`, `/api/v1/events/calendar/upcoming`, `/api/v1/events/map/active`, `/api/v1/connections`, and `/api/v1/users/search`.

The project is named `sponti-api`, but the active production alias is currently `https://sponti-api-pi.vercel.app`. `https://sponti-api.vercel.app` is not the active alias and returns 404.

Production deployments are from `Sponti-App/Sponti` `main`. Latest checked `main` and deployed auth/API commit is `86f0415`.

## Monorepo Setup

The implementation repo is a monorepo:

```text
spa/          frontend app
auth-server/  authentication service
api/          future main API service
```

Vercel handles this by creating one Vercel project per service and setting a different **Root Directory** for each project. For example, `sponti-spa` uses `spa/`, so Vercel builds from `spa/package.json` and ignores sibling folders for that deployment.

## Vercel Environment Model

Vercel uses different environments:

- **Production**: deployments from the configured production branch, currently `main`.
- **Preview**: deployments from pull requests or non-production branches.
- **Development**: local development environment used with Vercel CLI/dev workflows.

Recommended team flow:

```text
feature branch -> pull request -> Vercel Preview -> review/test -> merge to main -> Production
```

## Ownership

Martin owns Vercel access, project configuration, environment-variable checks, redeploys, and deployment-status verification. Codex may assist Martin locally with Vercel checks from Martin's environment.

Nil owns the implementation/runtime fixes in the codebase when a deployed service fails because of API, auth, database, or build code. Samara and Patrick should treat Vercel configuration questions as routed through Martin, not as something they need direct Vercel access for.

Secret values must stay out of GitHub, Slack, screenshots, and docs.

## Service Notes

### Frontend: `sponti-spa`

- Root Directory: `spa`
- Framework: Next.js
- Uses Vercel's default Next.js build settings.
- Public environment variable names:
  - `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY`
  - `NEXT_PUBLIC_GOOGLE_MAPS_ID`

These are browser-exposed by design. The Google Maps key should still be restricted in Google Cloud before production/demo use.

### Auth: `sponti-auth`

- Root Directory: `auth-server`
- Framework preset: Express
- Health check:

```text
GET https://sponti-auth.vercel.app/health
```

Expected response:

```json
{"status":"ok","service":"auth-server"}
```

Required secret environment variable names:

- `MONGO_URI`
- `ACCESS_JWT_SECRET`
- `REFRESH_JWT_SECRET`

`ACCESS_JWT_SECRET` must match `sponti-api` `ACCESS_JWT_SECRET`. `JWT_SECRET` may still exist in Vercel as an old variable, but current `main` auth code uses `ACCESS_JWT_SECRET` and `REFRESH_JWT_SECRET`.

Do not paste these values into GitHub, Slack, screenshots, or docs.

### Main API: `sponti-api`

- Root Directory: `api`
- Framework preset: Express
- Current production alias: `https://sponti-api-pi.vercel.app`
- Current deployment status: `Ready`
- Current runtime status: `/health` is green; event CRUD-by-ID works with a real token; feed/list-style routes return 500

Expected public health endpoint:

```text
GET /health
```

Expected response:

```json
{"data":{"status":"ok","service":"sponti-api"}}
```

Required secret environment variable names:

- `MONGO_URI`
- `DB_NAME`
- `CLIENT_BASE_URL`
- `ACCESS_JWT_SECRET`

`ACCESS_JWT_SECRET` must match the auth service JWT signing secret so auth-issued access tokens work against `/api/v1/*`.

## MongoDB Atlas Notes

`sponti-auth` connects to MongoDB Atlas through `MONGO_URI`.

The first Vercel auth deployment failed because Atlas allowed Martin's local IP, but not Vercel's runtime IPs. For Vercel Hobby deployments, the practical setup is an Atlas Network Access entry for:

```text
0.0.0.0/0
```

Because this allows network access from anywhere, the database user password must be strong and the app should use a limited app database user, not an admin user.

## Safe Deployment Checklist

Before treating a deployment as usable:

1. Confirm the Vercel project points to the correct repo and branch.
2. Confirm the Root Directory matches the service folder.
3. Confirm required environment variables exist in the correct Vercel environment.
4. Deploy or redeploy without exposing secret values.
5. Check the public URL or health endpoint.
6. Review Vercel runtime logs if the build is green but the route fails.

## Next Steps

- Diagnose the 500s on `GET /api/v1/events`, `/api/v1/events/calendar/upcoming`, `/api/v1/events/map/active`, `/api/v1/connections`, and `/api/v1/users/search`.
- Add sanitized server logging or local reproduction for the failing list/feed routes, because current Vercel logs show request rows without stack traces.
- Keep `GET https://sponti-api-pi.vercel.app/health` green and preserve the passing auth/event CRUD-by-ID smoke path.
- Browser-smoke the deployed frontend auth and create-flow UX against the current production services.
