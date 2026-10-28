# Sourced

**Find an opportunity. See the evidence. Decide the next step.**

Built for the **Hong Kong AI Summit: BUILD ACROSS Hackathon**, Startup Track, **3–4 October 2026**. Sourced connects student opportunity search with a reviewed profile, comparison and application tracking.

[Architecture](docs/ARCHITECTURE.md) · [Local setup](docs/development.md) · [Search integration](docs/LIVE_SEARCH.md) · [Event](https://www.startmeup.hk/events-detail/hong-kong-ai-summit-build-across-hackathon/)

```mermaid
flowchart TD
    Search[Source-linked search] --> Review[Review criteria and unknowns]
    Passport[User-confirmed Passport] --> Review
    Review --> Compare[Compare and plan]
    Compare --> Journey[My Journey: browser storage]
    Compare --> Tracker[Tracker: Supabase account]
```

The two tracking flows are separate. Signing in does not migrate browser-local records.

## What I contributed

Peris's work connects the product to live data and the demo room: the Gmail integration that updates application statuses automatically from company emails, real-time dashboard cards and follow-up counts, the coffee-chat experience with AI-analysed comments and 21-day reminders, the backend backbone (database schema, email sign-in, edge functions, Lovable Cloud), and the scripted customer-pitch video. 

Teammates owned CV extraction, retrieval/source quality, and eligibility verification; the finance teammate owned the calculator integration — boundaries kept through shared TypeScript contracts.

## Decisions that protect the user

- **Unknown stays unknown.** Missing eligibility criteria are not treated as satisfied. Eligibility is an interpretation of listed requirements, not an admission decision.
- **Evidence stays attached.** Live results retain the source URL and retrieval time. Fictional Browse fixtures are labelled and have no real application links.
- **Review comes before commitment.** Extracted profile suggestions need confirmation. Tasks and checklists never submit an application or change its status automatically.
- **Assumptions stay separate.** Affordability scenarios do not overwrite sourced funding facts or treat missing values as zero.

## Run the prototype

```sh
git clone https://github.com/hajarmrifag/opportunity-compass.git
cd opportunity-compass
npm install
npm run dev
```

Use Node.js and npm, then open the URL printed by Vite. Browser-local Journey and fictional Browse data provide a first look. Account features require Supabase; live search and extraction need server-side integrations.

```sh
npm run build
npm test
npm run lint
```

[Environment setup, repository map and data limits](docs/development.md) · [Current documentation](docs/README.md)

**Scope:** a hackathon prototype. Retrieved pages can be incomplete or stale; users must verify the original source. Clearing browser storage loses local Journey data unless it has been exported. Gmail scanning is unavailable in this branch.

The repository's earlier names were **Opportunity Compass / OpportunityOS**. The app is branded **Sourced**, built with [Lovable](https://lovable.dev).
