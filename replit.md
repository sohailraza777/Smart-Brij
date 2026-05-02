# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

## Artifacts

- **dairy-dashboard** (`artifacts/dairy-dashboard`) — React + Vite dairy management dashboard. Sidebar+navbar SaaS layout with 7 pages: Dashboard, Command Center (live monitoring of temperature/humidity/biogas/hydroponic/solar with auto-adjust controls, herd management table, AI-summarized Smart Project Reports, severity-tinted notifications feed), Collections, Customers, Sales, Payments, Analytics. Firebase Authentication (email/password) with split-screen login + signup pages, forgot-password flow, show/hide password, remember-me, role badge (admin/worker derived from email), last sign-in label on dashboard, and protected routes that redirect to `/login`. Auth context lives in `src/hooks/use-auth.tsx`; firebase init in `src/lib/firebase.ts` (uses VITE_FIREBASE_* env vars). INR currency, cream/green palette, Recharts visualizations, lucide-react icons.
- **api-server** (`artifacts/api-server`) — Express API exposing customers, collections, sales, payments, dashboard, command-center (snapshot/targets/auto-adjust/metric-history), herd, notifications, and AI report endpoints. Routes implemented in `src/routes/`. Auto-calculates amounts, derives sale status, and generates AI summaries via Anthropic (claude-sonnet-4-6) using the integrations-anthropic-ai workspace package.
- **mockup-sandbox** (`artifacts/mockup-sandbox`) — design preview server.

DB schema lives in `lib/db/src/schema/` (customers, collections, sales, payments). OpenAPI spec at `lib/api-spec/openapi.yaml`. Frontend imports types & hooks from `@workspace/api-client-react`.

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
