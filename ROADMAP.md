# Roadmap

## Current State

### Done
- [x] `inflow-client` - API client with auth & rate limiting
- [x] `inflow-api-types` - Zod schemas for API validation
- [x] `inflow-get` - Sync Inflow → SQLite
- [x] `inflow-materialize` - Materialized views library
- [x] `inflow-mock` - Generates clean baseline mock data (all 37 tables)

### In Progress
- [ ] Project documentation (this repo)
- [ ] `inflow-clean` - Data quality patterns: create, detect, fix (see below)
- [ ] `inflow-app` - Next.js frontend

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

### inflow-app (In Progress)
Next.js frontend for real Inflow data. Displays materialized views with focus on proving value.

**Core Features:**
- Display data from inflow-materialize views
- Run inflow-clean patterns on user's data
- Show detected issues with severity/confidence
- Export reports

**Tech:**
- NextJS App Router
- SQLite via better-sqlite3
- Tailwind CSS
- shadcn/ui components

**Integration with inflow-clean:**
- Import patterns from inflow-clean
- Run detect() on user's synced data
- Display issues in UI with actionable fixes

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

## Mock, Clean & Demo Stack

### inflow-mock (Done)
Generates comprehensive clean baseline mock data for all 37 tables in the inflow-get schema. Used as a library by other projects.

```typescript
import { generate, createDb } from 'inflow-mock'
const db = createDb('./test.db')
const data = generate({ products: 100, customers: 20, vendors: 15 })
```

### inflow-clean (In Progress)
Data quality patterns: create mess, detect it, fix it. **The core insight: create/detect/fix are symmetric.** If you can create a type of mess, you can detect and fix it.

**Patterns include:**
- `duplicates` - same product entered multiple ways
- `missing-reorder` - products without safety stock settings
- `sku-chaos` - inconsistent or missing SKU formats
- `vendor-sprawl` - same vendor named differently
- `category-mess` - flat/overlapping/inconsistent categories
- `orphaned-records` - broken foreign key references
- `naming-anarchy` - no naming conventions

**Each pattern has:**
- `create(db)` - inject this problem into clean data
- `detect(db)` - surface the problem, return issues
- `fix(db, issues)` - resolve the problem

**The proof:** Running `detect()` after `fix()` returns zero issues.

**Workflow for new patterns:**
1. See weird mess in real client data
2. Write `create` that replicates it
3. Write `detect` that surfaces it
4. Write `fix` that resolves it
5. Pattern is now part of the library

### inflow-demo (Planned)
Shows inflow-clean in action. Part of the sales funnel - demonstrates the cleanup story:

```
Step 0: Import messy.db → Score: 34%
Step 1: Resolve duplicates → Score: 52%
Step 2: Fix missing fields → Score: 71%
Step 3: Normalize vendors → Score: 85%
Step 4: SKU standardization → Score: 94%
```

**Each step shows:** Problem type, count found, how it was fixed.

**Transparency:** Users see exactly what "clean" means and how we get there.

---

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
