# Development, integrations and data boundaries

[Back to the project](../README.md)

Commands below run from the repository root.

## Run locally

Use Node.js and npm. The project also includes `bun.lock` for Bun users.

```bash
git clone https://github.com/hajarmrifag/opportunity-compass.git
cd opportunity-compass
npm install
npm run dev
```

Open the URL printed by Vite. The checked-in `.env` contains the public Supabase project URL and publishable key used by this project. For a different Supabase project, replace those public values and apply the SQL migrations in `supabase/migrations/` to that project. Never put a service role key or provider secret in a `VITE_` variable.

The browser-local Journey and fictional Browse data are useful for a first look. Account-backed Tracker features need a configured Supabase project. Live search, document extraction, and AI features also depend on server-side credentials or managed connectors; their availability is shown in the app. See [live search setup](../docs/LIVE_SEARCH.md) for the search integration.

```bash
npm run build     # production build
npm test          # Vitest suite
npm run lint      # ESLint and Prettier rules
```

## Repository map

| Path | Purpose |
| --- | --- |
| `src/routes/` | TanStack Start file-based pages and route layouts |
| `src/components/` | Shared interface components |
| `src/features/` | CV, application plan, and affordability features |
| `src/domain/` | Shared TypeScript contracts |
| `src/data/` | Demo fixtures and browser storage |
| `src/adapters/` | Eligibility and matching boundaries |
| `src/lib/` | Search, profile, tracker, finance, and other application logic |
| `src/integrations/` | Supabase and managed connector clients |
| `src/server.ts`, `src/lib/*.server.ts` | Server entry and server-only logic |
| `src/test/` | Vitest tests |
| `supabase/` | Database migrations and edge functions |
| `docs/` | Current guides and an `archive/` for early plans; start with the [docs index](../docs/README.md) |

TanStack Start generates `src/routeTree.gen.ts`; edit route files, not the generated tree. Shared data shapes live in `src/domain/types.ts`. The [architecture guide](ARCHITECTURE.md) explains the boundaries for demo data, user consent and source integrity.

For a short explanation of how data moves through the app, see [Architecture](../docs/ARCHITECTURE.md).

## Data and limitations

- **My Journey** stores data in browser storage. Clearing site data or switching browsers removes access to that local data unless you exported it.
- **Tracker** uses Supabase authentication and database tables. It is separate from My Journey; signing in does not migrate browser-local items.
- **Live search** retrieves pages through Firecrawl. A retrieved page is source-linked, but its facts can be stale or incomplete. Search requires the managed connection and credits.
- **Gmail** is not connected in this branch. The Tracker reports that scanning is unavailable and does not change application statuses.
- **Demo opportunities** are fictional and labelled as such. They have no real apply links.
