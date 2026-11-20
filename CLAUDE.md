# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

@AGENTS.md

## Commands

- `npm run dev` — Next.js dev server on http://localhost:3000
- `npm run build` — production build (also the closest check for type errors; there is no separate `tsc` script)
- `npm run start` — serve the production build
- `npm run lint` — ESLint 9 flat config (`eslint.config.mjs`, Next core-web-vitals + TypeScript rules)
- No test runner is configured (no test script, no test files). Do not assume `npm test` exists.

## Architecture

- Next.js 16 App Router scaffold. Only `app/` exists: `layout.tsx` (root layout, Geist fonts via `next/font/google`), `page.tsx` (home), `globals.css` (Tailwind v4 `@import "tailwindcss"` plus CSS variables for light/dark).
- Tailwind v4 is wired through Turbopack, not PostCSS: `next.config.ts` maps `*.css` to the `@tailwindcss/turbopack` loader. Keep that rule when editing the config.
- `next.config.ts` enables `cacheComponents`, `partialPrefetching`, and `experimental.agentFeedback`. Pages and components must be written compatible with `cacheComponents`.
- Path alias `@/*` maps to the repo root (`tsconfig.json`).
- `next-env.d.ts`, `.next/`, and `node_modules/` are generated; do not edit them.

## Product spec

`prompt-arcade-vault.md` is the product brief for the target app, "ARCADE VAULT": a retro arcade portal with game library, game player (HTML games in a sandboxed iframe or canvas), auth screen, and Hall of Fame. Key constraints from it:

- All user-facing UI text is in Spanish (for example "JUGAR", "Salón de la Fama", "GUARDAR PUNTUACIÓN").
- Dark arcade theme: background `#0a0a0f`, neon accents `#00f5ff`, `#ff006e`, `#f5ff00`; fonts "Press Start 2P" (display) and "Courier Prime" (body).
- Guest scores go to localStorage; authenticated users need a backend (REST API or Supabase), which is not built yet.

The current `app/` still holds the stock Create Next App template (English text, "Create Next App" metadata, `lang="en"`). Replace it when implementing the spec.

## Working notes

- `AGENTS.md` (imported above) warns that this Next.js version has breaking changes. Read the matching guide in `node_modules/next/dist/docs/` before writing Next.js code.
- `README.md` has uncommitted edits (Spanish project description, "Spec Driven Design" section pointing to `/spec` and `/spec-impl`). Those folders do not exist in the repo yet.
