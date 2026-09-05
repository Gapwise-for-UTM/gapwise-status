# Gapwise ecosystem integration

`gapwise-status` is the independently deployed operational-health and incident-communication surface for the six-repository Gapwise ecosystem. It observes availability; it does not own product semantics, package contracts, data truth, or release definitions.

## Surfaces in scope

- Main product: `https://gapwise.ca`
- Public API: `https://api.gapwise.ca/v1`
- OpenAPI: `https://api.gapwise.ca/openapi.json`
- Data/provenance: `https://data.gapwise.ca`
- Developer docs: `https://docs.gapwise.ca`
- AI service: `https://ai.gapwise.ca`
- Core source/API/SDKs: `Gapwise-for-UTM/gapwise`
- Native mobile: `Gapwise-for-UTM/gapwise-mobile`

## Current developer-platform release facts

- TypeScript `@gapwise/sdk@0.1.1` is canonically published on both npm and JSR with provenance through trusted GitHub Actions publishing.
- The same JavaScript/TypeScript SDK is mirrored publicly on GitHub Packages as `@gapwise-for-utm/sdk@0.1.1`; the organization-scoped name is required by GitHub Packages and does not replace the canonical npm/JSR identity.
- Node, Bun, and Deno are runtime targets for the same TypeScript implementation, not separately monitored SDK products.
- Python `gapwise==0.1.0` is published on PyPI through Trusted Publishing.
- TypeScript and Python are equal first-party SDK implementations of the same public API v1 semantics.

Registry publication is release metadata, not service health. Status may link to released package information, but availability reporting should focus on the API/docs/data/AI/product endpoints that can actually be probed or operator-confirmed.

## Status-specific rules

1. A failed probe is evidence about that probe/surface, not proof that the entire Gapwise ecosystem is down.
2. Stale automation becomes `unknown` / monitoring delayed rather than silently remaining healthy.
3. Operator incidents remain visible when automated data is stale.
4. Third-party University/provider outages are distinguished from Gapwise-owned failures where evidence permits.
5. Package registry existence, app-store release state, and docs claims are sourced from their owning release systems and are not inferred from HTTP uptime.
6. New public first-party services should trigger explicit review of monitoring coverage rather than being silently omitted.
7. Renames/deprecations in the core API, docs, data, or AI surfaces must be reflected here without creating alternate canonical URLs.

## Change impact

When monitoring changes, check:

- `gapwise` for canonical production endpoints and API behavior;
- `gapwise-docs` for public operations guidance;
- `gapwise-data` for data-surface endpoints;
- `gapwise-ai` for health/MCP endpoints and privacy-safe observability;
- `gapwise-mobile` only for mobile-specific backend dependencies that have meaningful public/operator health signals.

Status is intentionally independent in deployment and deliberately dependent on the rest of the ecosystem for the meaning of what it monitors.
