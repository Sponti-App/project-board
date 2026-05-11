# Spontapp Deployment

Last updated: 2026-05-11

## Purpose

This document explains the current Vercel deployment setup for Spontapp / Sponti. It is team-facing and intentionally does not include secret values.

## Current Status

| Vercel project | Repo folder | Status | URL |
| --- | --- | --- | --- |
| `sponti-spa` | `spa/` | Production deployment `Ready`; root and auth pages return 200 | https://sponti-spa.vercel.app |
| `sponti-auth` | `auth-server/` | Production deployment `Ready`; health check green | https://sponti-auth.vercel.app/health |
| `sponti-api` | `api/` | Production deployment `Ready`, but runtime health is failing with 500 | https://sponti-api-pi.vercel.app/health |

`sponti-api` is deployed, but not usable yet. Current public checks against `https://sponti-api-pi.vercel.app`, `/health`, and `/api/v1/events` return `500 FUNCTION_INVOCATION_FAILED`. Runtime logs point to a Mongoose ESM import issue: `mongoose` does not provide a named `models` export.

The project is named `sponti-api`, but the active production alias is currently `https://sponti-api-pi.vercel.app`. `https://sponti-api.vercel.app` is not the active alias and returns 404.

Latest preview observation: branch `feat/api_mid` has new Vercel previews for all three projects. `sponti-auth` and `sponti-api` previews show `Ready`; `sponti-spa` preview shows `Error`. The preview URLs are protected by Vercel Authentication, so public route health could not be verified from the browser check.

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
- `JWT_SECRET`

Do not paste these values into GitHub, Slack, screenshots, or docs.

### Main API: `sponti-api`

- Root Directory: `api`
- Framework preset: Express
- Current production alias: `https://sponti-api-pi.vercel.app`
- Current deployment status: `Ready`
- Current runtime status: failing with `500 FUNCTION_INVOCATION_FAILED`

Expected public health endpoint:

```text
GET /health
```

Expected response after the runtime issue is fixed:

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

- Fix the API runtime Mongoose import issue and redeploy `sponti-api`.
- Re-check `GET https://sponti-api-pi.vercel.app/health`.
- Confirm the API alias the team wants to use for `NEXT_PUBLIC_API_BASE_URL`.
- Confirm `NEXT_PUBLIC_AUTH_BASE_URL` and `NEXT_PUBLIC_API_BASE_URL` are set for the deployed SPA.
- Smoke test deployed register/login/me before marking auth complete.
- Smoke test create, feed, detail, RSVP, and My Meetups after API health is green.
