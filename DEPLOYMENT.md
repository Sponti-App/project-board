# Spontapp Deployment

Last updated: 2026-05-07

## Purpose

This document explains the current Vercel deployment setup for Spontapp / Sponti. It is team-facing and intentionally does not include secret values.

## Current Status

| Vercel project | Repo folder | Status | URL |
| --- | --- | --- | --- |
| `sponti-spa` | `spa/` | Deployed | https://sponti-spa.vercel.app |
| `sponti-auth` | `auth-server/` | Deployed, health check green | https://sponti-auth.vercel.app/health |
| `sponti-api` | `api/` | Pending | Not deployed yet |

`sponti-api` is pending because the `api/` folder does not contain a real API service yet.

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

No real API service exists yet. When the team is ready, start with a minimal deployed health check before adding business routes.

Recommended first endpoints:

```text
GET /
GET /health
```

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

- Add `NEXT_PUBLIC_AUTH_API_URL` to the frontend when auth UI integration starts.
- Add CORS rules so `sponti-spa` can call `sponti-auth` safely.
- Create the initial `api/` service only when the team agrees on the minimum API shape.
- Add `sponti-api` to Vercel after `api/` has a real health endpoint.
