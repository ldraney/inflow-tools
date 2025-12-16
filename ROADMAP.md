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

### inflow-materialize (Enhancement)
The existing library needs data quality views that expose problems and quantify the mess.

**Data Quality Views (the "before"):**
- `v_duplicate_products` - products with same/similar names, confidence score
- `v_orphaned_records` - records with broken foreign keys
- `v_missing_fields` - products missing critical fields (reorder point, category, vendor)
- `v_naming_inconsistencies` - products that don't follow detected patterns
- `v_sku_format_violations` - SKUs that break the dominant pattern

**Summary Views (the stats):**
- `v_data_quality_summary` - counts of each issue type
- `v_completeness_score` - percentage of fields filled per entity
- `v_convention_compliance` - how well data follows detected patterns

**Clean Business Views (the "after"):**
- `v_products_enriched` - products with all relationships joined, nulls handled
- `v_inventory_status` - current stock with reorder alerts, days until stockout
- `v_order_pipeline` - orders with status, customer, line items denormalized

**Convention Detection:**
- Auto-detect naming patterns (categories, vendors, SKU formats)
- Flag outliers that break the pattern
- Suggest normalizations

**Tunnel content this creates:**
- Screenshots of duplicate detection
- Stats like "Found 847 issues in 3 seconds"
- Before/after comparisons

---

### inflow-dashboard
NextJS frontend that displays materialized views with focus on proving value.

**Stats Cards (the "holy shit" moment):**
- "Found X potential duplicates"
- "Y products missing reorder points"
- "Data completeness: Z%"
- "Convention compliance: W%"

**Data Quality Tables (drill into issues):**
- Duplicates table with confidence score, suggested merge
- Missing fields table grouped by field type
- Naming inconsistencies with suggested fixes
- Exportable to CSV

**Clean Data Tables (the "after"):**
- Products with all enrichments
- Inventory status with visual reorder alerts
- Order pipeline with status badges

**Before/After Toggle:**
- Switch between raw Inflow view and cleaned view
- Side-by-side comparison mode
- Highlight what changed

**Export & Reports:**
- CSV export of any view
- PDF data quality report (shareable proof)
- "Share with your team" link

**Tech:**
- NextJS App Router
- SQLite via better-sqlite3
- Tailwind CSS
- shadcn/ui components
- Recharts for visualizations

**Tunnel content this creates:**
- Screenshots of the dashboard
- GIFs of before/after toggle
- Sample PDF reports
- "Here's what we found in 30 seconds"

---

### inflow-put
Write adapter that maps view-shaped updates to Inflow API calls.

**MVP scope:**
- Update product reorder point
- Update product reorder quantity
- Bulk updates via CSV
- Apply convention fixes (rename to match pattern)

**Design questions:**
- Optimistic updates vs. wait for re-sync?
- Validation: client-side, server-side, or both?
- Error handling: rollback strategy?
- Dry-run mode to preview changes?

## GTM Stack

Active go-to-market execution. These repos turn passive awareness into qualified leads.

### inflow-demographics
WHO to target. Research and tooling to identify Inflow users who need data cleanup.

**Scope:**
- ICP (Ideal Customer Profile) definition
- SEO keyword research for Inflow pain points
- Audience list building (LinkedIn, forums, communities)
- Competitor analysis
- Ad targeting criteria

### inflow-marketing
HOW to reach them. Outreach execution and campaign management.

**Scope:**
- Email templates and sequences
- Ad copy (LinkedIn, Google, Reddit)
- Content calendar
- Outreach automation
- A/B testing framework

### inflow-tunnel
WHERE they convert. Landing pages with credibility-first design.

**Scope:**
- Landing page ("Is your Inflow data a mess?")
- **Credibility section:**
  - Personal bio/intro
  - LinkedIn profile link
  - Other projects/portfolio
  - Links to public GitHub repos (core stack)
  - Links to npm packages (inflow-client, inflow-api-types, inflow-get, inflow-materialize)
- Guide to get credentials from their Inflow account
- Credential input (companyID + token)
- Handoff to dashboard

**Why credibility first:**
Before asking for credentials, prove you're trustworthy:
- "Here's who I am"
- "Here's my work you can verify"
- "Here's the open source code that powers this"

**The funnel:**
```
Demographics (find them)
    → Marketing (reach them)
        → Tunnel (build trust, capture credentials)
            → Dashboard (prove value with their data)
                → Consulting (close: "want me to clean this up?")
                    → PUT (paid deliverable: conventions applied to their Inflow)
```

### The Sale

**What they see:** Dashboard shows their messy data transformed into clean, conventional views with stats on what was fixed.

**The offer:** "Want me to help you make this permanent?"

**What they pay for:**
- **Data cleanup & PUT** - conventions applied directly to their Inflow instance
- **Consulting** - ongoing help with data strategy and best practices
- **Custom tools** - tailored automation for their specific workflow
- **Team training** - teach their team to maintain clean data going forward

**Why they pay:** They see the golden nugget. Clean data, clear conventions, team can finally use it properly. "My god please take my money."

## Future Ideas

### Advanced Data Quality
- Historical trend analysis (data quality over time)
- Automated fix suggestions with confidence scores
- Machine learning for pattern detection
- Cross-entity consistency checks

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
