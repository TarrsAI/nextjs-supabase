# Next.js + Supabase starter

A Tarrs-ready Next.js 15 starter with Supabase magic-link auth wired up.
Deploys to Vercel out of the box.

## What's included

- Next.js 15 (App Router, React 19, TypeScript)
- Tailwind CSS 4
- Supabase Auth (magic-link via email — no Google config needed)
- Server / browser / middleware Supabase clients
- Protected `/dashboard` route example
- Sign-out button
- FontAwesome Free icons (no license needed)

## How Tarrs uses this

When a Tarrs customer creates a project from this template:

1. Tarrs creates a fresh GitHub repo from `TarrsAI/nextjs-supabase`
2. Tarrs creates a Supabase project (or uses linked one)
3. Tarrs auto-injects these env vars into the dev sandbox container:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `SUPABASE_SERVICE_ROLE_KEY` (server-only)
4. Customer files first ticket → AI extends the codebase

## Local dev

```bash
pnpm install
cp .env.example .env.local   # fill from your Supabase dashboard
pnpm dev
```

Open http://localhost:3000.

## Adding Google login later

Out of the box this template uses **email magic-link** — zero config. To
add Google as well:

1. Create OAuth credentials at [console.cloud.google.com](https://console.cloud.google.com/apis/credentials)
2. Supabase Dashboard → Authentication → Providers → Google → paste
   client ID + secret
3. In `app/login/page.tsx`, add a button that calls
   `supabase.auth.signInWithOAuth({ provider: 'google' })`

## Deploy to prod

Push to GitHub. Vercel detects Next.js and deploys. Add Supabase env vars
in Vercel project settings.

## Add a database table

Tarrs's AI agent has read access to your Supabase schema and can write
migrations. File a ticket like:

> "Add a `posts` table with title, body, author_id (fk users), created_at"

The agent will add a migration file under `supabase/migrations/` and you
can apply it via the Supabase dashboard or CLI.
