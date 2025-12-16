# Roadmap

## Current State

### Done
- [x] `inflow-client` - API client with auth & rate limiting
- [x] `inflow-api-types` - Zod schemas for API validation
- [x] `inflow-get` - Sync Inflow → SQLite
- [x] `inflow-materialize` - Materialized views library

### In Progress
- [ ] Project documentation (this repo)

## Next Up

### inflow-dashboard
NextJS frontend that displays materialized views.

**MVP scope:**
- Product inventory status table
- Reorder alerts list
- Open orders pipeline view
- Basic filtering/sorting

**Tech:**
- NextJS App Router
- SQLite via better-sqlite3
- Tailwind CSS
- shadcn/ui components

### inflow-put
Write adapter that maps view-shaped updates to Inflow API calls.

**MVP scope:**
- Update product reorder point
- Update product reorder quantity
- Bulk updates via CSV

**Design questions:**
- Optimistic updates vs. wait for re-sync?
- Validation: client-side, server-side, or both?
- Error handling: rollback strategy?

## Future Ideas

### Data Quality Tools
- Duplicate detection
- Missing data alerts
- Naming convention enforcement
- Historical trend analysis

### Integrations
- QuickBooks sync status
- Shopify inventory sync
- CSV import/export automation

### Multi-Company Support
- Switch between Inflow accounts
- Consolidated reporting across companies

### Hosted Version
- OAuth authentication
- Scheduled syncs
- Managed infrastructure
- Subscription billing

## How to Propose Changes

For significant features, create an RFC in `rfcs/`:

1. Copy `rfcs/000-template.md`
2. Fill in the sections
3. Open a PR
4. Discuss
5. Merge when accepted

For smaller changes, open an issue first to discuss.
