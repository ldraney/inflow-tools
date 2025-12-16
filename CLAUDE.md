# inflow-tools

Meta repository for the inflow-tools ecosystem. This repo contains documentation, roadmaps, and project governance—not code.

## What This Repo Is

- Project-wide architecture docs
- Roadmap and planning
- RFCs for design decisions
- Issue templates for cross-cutting concerns

## Related Repositories

| Repo | Purpose |
|------|---------|
| `inflow-client` | API client with auth & rate limiting |
| `inflow-api-types` | Zod schemas for API validation |
| `inflow-get` | Sync Inflow → SQLite |
| `inflow-materialize` | Materialized views on synced data |
| `inflow-dashboard` | NextJS frontend (planned) |
| `inflow-put` | Write adapter (planned) |

## Key Concepts

### Materialization-Centric Architecture
Views are the contract layer. Frontends and PUT services are dumb adapters that read/write view-shaped data. Business logic lives in view definitions.

### Trust Ladder
Users run tools locally first (zero trust required), then optionally adopt hosted services after establishing trust.

## Working in This Repo

- **Updating docs**: Edit markdown files in `docs/`
- **New features**: Create RFC from `rfcs/000-template.md`
- **Diagrams**: Use Mermaid in markdown (GitHub renders it)
- **Cross-repo issues**: Create here, link to implementation repos

## File Structure

```
docs/
  architecture.md   # System design, data flow diagrams
  ecosystem.md      # Business model, go-to-market
rfcs/
  000-template.md   # Copy this for new proposals
ROADMAP.md          # What's done, what's next
```

## When Editing

- Keep docs concise and scannable
- Use Mermaid for diagrams (not external images)
- Update ROADMAP.md when package status changes
- Link to specific repos for implementation details
