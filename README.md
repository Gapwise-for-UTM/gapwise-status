<div align="center">

<img src="public/logo-mark-green.svg" width="116" alt="Gapwise deer mark" />

# Gapwise Status

### Know when Gapwise is healthy — and when it is not.

**The independent public service-status surface for Gapwise applications, APIs, AI services, documentation, and operator-maintained systems.**

[![Live Status](https://img.shields.io/badge/Live_Status-status.gapwise.ca-36C692?style=for-the-badge&logo=vercel&logoColor=white)](https://status.gapwise.ca)
[![Monitoring](https://img.shields.io/badge/Monitoring-Hourly-36C692?style=for-the-badge)](https://status.gapwise.ca)
[![Gapwise](https://img.shields.io/badge/Gapwise-gapwise.ca-111111?style=for-the-badge)](https://gapwise.ca)

<sub>Astro · GitHub Actions · Vercel</sub>

<br />

**[Status](https://status.gapwise.ca)** · **[History](https://status.gapwise.ca/history/)** · **[Gapwise](https://gapwise.ca)** · **[Developer docs](https://docs.gapwise.ca)** · **[Gapwise AI](https://ai.gapwise.ca)** · **[Main repository](https://github.com/andrewmuratov/gapwise)**

</div>

---

## What this repository is

This repository is the canonical public service-status surface for the Gapwise ecosystem. It is deliberately deployed independently from the main Gapwise app and from the developer documentation so an application or docs deployment problem does not remove the place used to communicate service health.

The canonical production URL is:

```text
https://status.gapwise.ca
```

The status site communicates the latest known state of Gapwise-owned production surfaces and selected operator-maintained services. It is designed for clear current-state communication, incident history, and graceful handling of delayed monitoring data.

It is **not** a contractual SLA, a promise of continuous synthetic monitoring, or evidence that every upstream dependency was available at every point in the past.

---

## Status model

Gapwise separates automated probes from services that require operator confirmation.

| Group | What is represented |
| --- | --- |
| **Core platform** | Main Gapwise web application plus operator-maintained authentication and sync state |
| **APIs** | Public Gapwise API availability |
| **Gapwise AI** | Production AI/MCP service health |
| **Developer services** | Developer documentation plus operator-maintained transactional auth email state |

Automated production probes run approximately hourly. Operator-maintained services preserve explicit human-reported state rather than pretending that a safe external probe can verify behavior that requires a private user session.

When automated monitoring becomes stale, the site changes its presentation to make that uncertainty visible instead of continuing to present an old green result as current.

---

## Public routes

| Route | Purpose |
| --- | --- |
| `/` | Current service status and latest check freshness |
| `/history/` | Recorded service-state transitions and incident history |
| `/_data/current` | Edge-cached current status source |
| `/_data/history` | Edge-cached incident-history source |

Legacy `/status/` and `/status/history/` paths redirect to the canonical root routes.

The machine-managed source of truth lives in GitHub issue [`#1`](https://github.com/andrewmuratov/gapwise-status/issues/1). Status transitions are recorded as machine-readable issue comments so the site can render history without coupling its public frontend to the docs repository.

---

## Monitoring and incident behavior

The hourly workflow probes production surfaces that can be checked safely from outside a private account session. The operator workflow updates services whose real health cannot be established reliably by a public HTTP request alone.

Key behavior:

- automated checks are serialized to avoid competing publishers;
- operator-reported incidents remain visible even when automated monitoring is delayed;
- stale automated data is presented as **unknown / monitoring delayed**, not silently green;
- service transitions are retained for the public history view;
- current state and history are cached at the Vercel edge with direct GitHub API fallbacks;
- a failure to load status data is not itself presented as proof that Gapwise is down.

The public status page intentionally describes what is actually measured. University of Toronto systems and other external upstream services remain outside Gapwise's control.

---

## Brand

The status surface uses the canonical Gapwise deer geometry with a status-specific green presentation:

- `public/logo-mark-green.svg` — green Gapwise deer mark for the site header and README;
- `public/favicon.svg` — matching green deer mark for the browser tab.

The geometry is shared with the other Gapwise repositories; only the presentation color changes. Green is reserved here for the status identity and healthy-state visual language.

---

## Run locally

Requires Node.js 22 or newer.

```bash
git clone https://github.com/andrewmuratov/gapwise-status.git
cd gapwise-status
npm install
npm run check
npm run build
npm run dev
```

Useful commands:

```bash
npm run check
npm run build
npm run preview
```

The status-publisher scripts can also be syntax-checked independently through the package scripts before workflow changes are shipped.

---

## Gapwise ecosystem

The first-party repositories are separate execution and deployment surfaces with one product identity and a deliberate source-of-truth hierarchy:

| Repository | Role | Primary surface |
| --- | --- | --- |
| **[`gapwise`](https://github.com/andrewmuratov/gapwise)** | Core web/PWA product, canonical student-state behavior, deterministic UTM campus intelligence, public API, OpenAPI contract, and SDK source | [gapwise.ca](https://gapwise.ca) / [api.gapwise.ca](https://api.gapwise.ca/v1) |
| **[`gapwise-mobile`](https://github.com/andrewmuratov/gapwise-mobile)** | Native iOS and Android client consuming canonical Gapwise contracts and product semantics | Native mobile app |
| **[`gapwise-ai`](https://github.com/andrewmuratov/gapwise-ai)** | Permissioned OAuth/MCP layer for explicitly delegated student context and bounded AI actions | [ai.gapwise.ca](https://ai.gapwise.ca/api/mcp) |
| **[`gapwise-docs`](https://github.com/andrewmuratov/gapwise-docs)** | Canonical public developer documentation | [docs.gapwise.ca](https://docs.gapwise.ca) |
| **[`gapwise-status`](https://github.com/andrewmuratov/gapwise-status)** | Independent public service-health and incident-communication surface | [status.gapwise.ca](https://status.gapwise.ca) |

`gapwise` remains authoritative for deterministic timetable, routing, campus, API, and primary student-state semantics. The status repository owns only the communication and monitoring state needed to describe the operational health of those surfaces.

---

## Deployment

`main` is the production status branch and deploys through the dedicated `gapwise-status` Vercel project.

- `status.gapwise.ca` is attached only to the status project.
- `docs.gapwise.ca` is deployed independently from `gapwise-docs`.
- status changes do not require a docs deployment, and docs changes do not redeploy the status site.
- legacy docs `/status` URLs permanently redirect to this standalone surface.

Keep related status changes grouped and validated so production deployments remain intentional and the incident-communication surface stays dependable.
