# inflow-tools

A suite of open-source tools for Inflow Inventory power users.

## The Problem

Inflow Inventory is solid for basic inventory management, but power users hit walls:
- No custom reporting beyond built-in views
- Data quality issues accumulate silently
- No programmatic access patterns for automation
- Limited integration options

## The Solution

A modular toolkit that gives you full control over your Inflow data:

```
Your Inflow Account
        ↓ (token + companyID)
   inflow-get          → Seeds local SQLite from Inflow API
        ↓
   inflow-materialize  → Creates business-friendly views
        ↓
   inflow-dashboard    → Instant NextJS analytics UI
        ↓
   inflow-put          → Write changes back to Inflow
```

## Packages

### Core Stack

| Package | Status | Description |
|---------|--------|-------------|
| [inflow-client](https://github.com/ldraney/inflow-client) | ✅ Published | API client with auth & rate limiting |
| [inflow-api-types](https://github.com/ldraney/inflow-api-types) | ✅ Published | Zod schemas for API validation |
| [inflow-get](https://github.com/ldraney/inflow-get) | ✅ Published | Sync Inflow → SQLite |
| [inflow-materialize](https://github.com/ldraney/inflow-materialize) | ✅ Published | Materialized views library |
| inflow-dashboard | 🚧 Planned | NextJS analytics frontend |
| inflow-put | 🚧 Planned | Write adapter (view → API mutations) |

### GTM Stack (Private)

| Package | Status | Description |
|---------|--------|-------------|
| inflow-demographics | 🔒 Private | ICP research, audience identification, SEO keywords |
| inflow-marketing | 🔒 Private | Outreach campaigns, email templates, ad copy |
| inflow-tunnel | 🔒 Private | Landing pages, credibility/bio, lead capture |

> GTM repos are private. Core stack is open source for credibility - tunnel links back to public repos/npm packages as proof of expertise.

## Quick Start

```bash
mkdir my-inventory-insights && cd my-inventory-insights
npm init -y
npm install inflow-get inflow-materialize

# Create seed script
cat > seed.js << 'EOF'
import { createDb, seedAll } from 'inflow-get';
import { createViews } from 'inflow-materialize';

const db = createDb('./inflow.db');
await seedAll(db, {
  token: process.env.INFLOW_TOKEN,
  companyId: process.env.INFLOW_COMPANY_ID
});
createViews(db.$sqlite);
console.log('Done! Query your views in inflow.db');
EOF

INFLOW_TOKEN=xxx INFLOW_COMPANY_ID=yyy node seed.js
```

## Architecture

See [docs/architecture.md](docs/architecture.md) for system design.

## Who This Is For

- **Inflow power users** who've outgrown the built-in reports
- **Developers** integrating Inflow with other systems
- **Consultants** helping clients clean up inventory data

## Contributing

This project uses [RFCs](rfcs/) for significant changes. Open an issue to discuss before submitting large PRs.

## License

MIT
