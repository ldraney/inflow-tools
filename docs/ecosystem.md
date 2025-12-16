# Ecosystem & Business Model

## Value Proposition

**"See what Inflow doesn't show you."**

We're not replacing Inflow—we're extending it for power users who need:
- Custom reporting beyond built-in views
- Data quality monitoring and cleanup
- Programmatic access for automation
- Integration with other systems

## Target Users

### Primary: Inflow Power Users
- Hit the ceiling on built-in reports
- Managing 1000+ SKUs
- Need reorder automation
- Want data exports for analysis

### Secondary: Developers/Consultants
- Building integrations for clients
- Need typed API access
- Want to automate inventory workflows

## Go-to-Market

### Phase 1: Open Source Credibility
- Publish all packages as MIT-licensed
- Documentation-first approach
- GitHub presence establishes trust

### Phase 2: Active Outreach (GTM Stack)
Three repos execute the go-to-market:

| Repo | Role |
|------|------|
| `inflow-demographics` | WHO - ICP research, audience lists, SEO keywords |
| `inflow-marketing` | HOW - Email sequences, ad copy, outreach automation |
| `inflow-tunnel` | WHERE - Landing pages, credential capture, conversion |

**The flow:**
```
Demographics → Marketing → Tunnel → Dashboard → Consulting
(find)         (reach)     (capture) (prove)    (close)
```

### Phase 3: Credibility-First Conversion
Before asking for credentials, prove trustworthiness via `inflow-tunnel`:
- Personal bio and LinkedIn
- Portfolio of other projects
- Links to public GitHub repos (core stack)
- Links to npm packages users can verify
- Guide to get credentials from their Inflow account

The open source core stack IS the credibility. They can audit the code that will touch their data.

### Phase 4: Self-Service Proof
- User enters companyID + token via `inflow-tunnel`
- We sync their data, run materialized views
- Dashboard shows: "Here's your data, cleaned, with stats on what was wrong"
- Zero trust required—they see their own mess fixed

### Phase 5: The Sale
**What they see:** Golden nugget - messy data transformed into clean, conventional views.

**The offer:** "Want me to help you make this permanent?"

**What they pay for:**
- Data cleanup & PUT - conventions applied to their Inflow instance
- Consulting - ongoing help with data strategy
- Custom tools - tailored automation for their workflow
- Team training - teach their team to maintain clean data

**Why they pay:** They see it working. Clean data is right there. Now they want it for real.

## Trust Ladder

```
Awareness    → Find us via search, Inflow forums, word of mouth
Interest     → Read docs, see architecture, understand value
Evaluation   → Run locally with their own data (zero trust needed)
Trial        → Use dashboard, see insights
Adoption     → Regular usage, depends on the tool
Advocacy     → Recommends to other Inflow users
Expansion    → Wants custom work → revenue
```

## Where to Find Inflow Users

Research lives in `inflow-demographics`. Starting points:

- **Inflow's own channels**: Forums, support community, social media
- **QuickBooks ecosystem**: Inflow integrates with QB, users overlap
- **Reddit**: r/inventory, r/smallbusiness, r/ecommerce
- **LinkedIn**: Inventory management, supply chain groups
- **YouTube**: Tutorial content for Inflow users

See `inflow-demographics` for ICP definition, keyword research, and audience lists.

## Competitive Landscape

| Alternative | Weakness |
|-------------|----------|
| Inflow built-in | Limited customization |
| Generic BI tools | No Inflow-specific models |
| Custom dev | Expensive, slow |
| **inflow-tools** | Open source, instant, extensible |

## Revenue Opportunities

1. **Consulting**: Custom integrations, data cleanup projects
2. **Managed Service**: We run the sync + dashboard for you
3. **Premium Features**: Advanced analytics, multi-company support
4. **Training**: Workshops for Inflow power users

## Success Metrics

- GitHub stars / forks (awareness)
- npm downloads (adoption)
- Chatbot conversations (qualified leads)
- Consulting engagements closed (revenue)
