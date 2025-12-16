# RFC: GTM Stack - Demographics, Marketing, Tunnel

- **Status**: Draft
- **Author**: ldraney
- **Date**: 2025-12-15

## Summary

Introduce three new repositories to execute an active go-to-market strategy: `inflow-demographics` (find customers), `inflow-marketing` (reach them), and `inflow-tunnel` (capture and convert them).

## Motivation

The current inflow-tools ecosystem has strong technical foundations (client, types, get, materialize) but no active customer acquisition strategy. We have a valuable product (`inflow-materialize` creates clean views from messy Inflow data) but no systematic way to:

1. Identify who needs this
2. Reach them with the right message
3. Convert them into users/customers

**The business model:**
- Free: User enters credentials → we show them their data cleaned + stats on what was wrong
- Paid: Consulting to actually fix their Inflow instance via `inflow-put`

The dashboard proves value. The GTM stack gets people to the dashboard.

## Detailed Design

### Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     GTM STACK                                │
├─────────────────────────────────────────────────────────────┤
│  inflow-demographics    →    inflow-marketing    →    inflow-tunnel
│  (WHO)                       (HOW)                    (WHERE)
│                                                             │
│  ICP research               Email sequences          Landing pages
│  SEO keywords               Ad copy                  Credential capture
│  Audience lists             Content calendar         Free audit flow
│  Competitor analysis        Outreach automation      Dashboard handoff
│  Targeting criteria         A/B testing              Upsell CTA
└─────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────┐
│                     CORE STACK                               │
├─────────────────────────────────────────────────────────────┤
│  inflow-get → inflow-materialize → inflow-dashboard         │
│  (sync)       (clean)              (prove value)            │
│                                                             │
│                              inflow-put                     │
│                              (paid deliverable)             │
└─────────────────────────────────────────────────────────────┘
```

### inflow-demographics

**Purpose:** Research and tooling to identify Inflow users who need data cleanup.

**Contents:**
- `icp.md` - Ideal Customer Profile definition
- `keywords/` - SEO keyword research, search volume, difficulty
- `audiences/` - Platform-specific audience lists (LinkedIn, Reddit, forums)
- `competitors/` - Who else serves this market, their positioning
- `targeting/` - Ad platform targeting parameters

**Process:**
1. Define ICP hypotheses
2. Research where Inflow users congregate
3. Identify pain point keywords they search for
4. Map competitor landscape
5. Document targeting criteria for each ad platform

### inflow-marketing

**Purpose:** Outreach execution and campaign management.

**Contents:**
- `email/` - Templates, sequences, follow-ups
- `ads/` - Copy for LinkedIn, Google, Reddit
- `content/` - Blog posts, social content, calendar
- `automation/` - Scripts/configs for outreach tools
- `tests/` - A/B test results and learnings

**Process:**
1. Write copy based on ICP from demographics
2. Set up outreach automation
3. Launch campaigns
4. Track results, iterate

### inflow-tunnel

**Purpose:** Landing pages and conversion flow.

**Contents:**
- NextJS app with:
  - Landing page (value prop, social proof)
  - Credential input form (companyID + token)
  - Audit progress page
  - Redirect to dashboard
  - Upsell CTA

**Flow:**
```
Landing → Enter Credentials → Audit Running → Dashboard (with stats)
                                                    ↓
                                           "Want this permanent?"
                                                    ↓
                                              Consulting CTA
```

## Alternatives Considered

### 1. Single marketing repo
Could put all GTM in one repo. Rejected because:
- Different cadences (demographics is research-heavy upfront, marketing is ongoing)
- Different skill sets (research vs copywriting vs frontend)
- Cleaner separation of concerns

### 2. Marketing in inflow-dashboard
Could add landing pages to the dashboard repo. Rejected because:
- Dashboard is for authenticated users who've already converted
- Tunnel is for anonymous visitors we're trying to convert
- Different concerns, different deployments

### 3. No active marketing, rely on organic
Could just publish tools and hope people find them. Rejected because:
- Inflow is a niche product, limited organic discovery
- We have a consulting upsell that requires lead generation
- Active outreach is necessary for the business model

## Drawbacks

1. **Scope creep** - Three new repos is a lot. Risk of spreading too thin.
2. **Marketing is hard** - Technical founders often underestimate GTM difficulty.
3. **Maintenance burden** - More repos = more to maintain.

**Mitigations:**
- Start with demographics (research), then tunnel (needed for conversion), then marketing (scaling)
- Keep repos lean - documentation and scripts, not complex apps (except tunnel)

## Open Questions

1. **Tunnel tech stack** - NextJS assumed, but could be simpler (static site + serverless functions)?
2. **Credential security** - How do we handle user tokens securely in the tunnel flow?
3. **Dashboard integration** - Does tunnel hand off to a separate dashboard, or is it one app?
4. **Hosted vs local** - Does the free audit run on our infra or theirs?
5. **Pricing** - What do we charge for consulting? Per-engagement or retainer?
