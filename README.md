<div align="center">

<img src="public/logo-mark-green.svg" width="116" alt="Gapwise deer mark" />

# Gapwise Status

### Independent service health for the full Gapwise ecosystem.

**The public monitoring and incident-communication surface for Gapwise applications, APIs, AI services, data and documentation surfaces, and selected operator-maintained systems.**

[![Live Status](https://img.shields.io/badge/Live_Status-status.gapwise.ca-36C692?style=for-the-badge&logo=vercel&logoColor=white)](https://status.gapwise.ca)
[![Monitoring](https://img.shields.io/badge/Monitoring-Hourly-36C692?style=for-the-badge)](https://status.gapwise.ca)

<sub>Astro · GitHub Actions · Vercel</sub>

<br />

**[Status](https://status.gapwise.ca)** · **[History](https://status.gapwise.ca/history/)** · **[Gapwise](https://gapwise.ca)** · **[Data](https://data.gapwise.ca)** · **[AI](https://ai.gapwise.ca)** · **[Docs](https://docs.gapwise.ca)**

</div>

---

## What Gapwise Status is

Gapwise Status is the independent operational-health surface for **Gapwise**, a multi-surface campus-intelligence ecosystem created and engineered by **Andrew Muratov**.

Gapwise spans a student web/PWA product, native mobile client, deterministic public campus API and SDKs, open data/provenance portal, permissioned OAuth/MCP AI integration, developer documentation, and this separately deployed monitoring and incident-communication service.

Andrew's work across the ecosystem spans **full-stack software engineering, cybersecurity and privacy engineering, platform architecture, API and SDK design, data engineering, developer infrastructure, mobile engineering, operations, and permissioned AI integration**.

This repository is deliberately deployed independently from the main app and developer documentation so a failure in those surfaces does not automatically remove the place used to communicate service health.

Canonical production URL:

```text
https://status.gapwise.ca
```

The site communicates the latest known state of Gapwise-owned production surfaces and selected operator-maintained services. It is not a contractual SLA and does not claim continuous third-party synthetic monitoring of every dependency.

---

## Monitoring model

Gapwise separates automated probes from services that require operator confirmation.

Automated checks cover safely observable public production surfaces such as the main application, public API, AI service, data portal, and developer documentation. Operator-maintained state is used when real health requires private-session or provider-side evidence that cannot be verified safely through a public HTTP probe alone.

Key behavior:

- automated checks are serialized to avoid competing publishers;
- stale monitoring data becomes visibly **unknown / monitoring delayed** rather than silently remaining green;
- operator-reported incidents remain visible when automation is stale;
- service-state transitions are retained for the public history view;
- current state and history are cached at the edge with GitHub-backed fallbacks;
- a failure to load status data is not itself presented as proof that Gapwise is down;
- external University of Toronto systems and other upstream dependencies remain outside Gapwise's control.

Public routes include `/` for current state, `/history/` for recorded transitions/incidents, `/_data/current`, and `/_data/history`.

---

## Gapwise ecosystem

| Repository | Role | Primary surface |
| --- | --- | --- |
| **[`gapwise`](https://github.com/andrewmuratov/gapwise)** | Core web/PWA, deterministic student/campus engine, public API, OpenAPI, and SDK source | [gapwise.ca](https://gapwise.ca) / [api.gapwise.ca](https://api.gapwise.ca/v1) |
| **[`gapwise-mobile`](https://github.com/andrewmuratov/gapwise-mobile)** | Native iOS and Android client | Native mobile app |
| **[`gapwise-ai`](https://github.com/andrewmuratov/gapwise-ai)** | OAuth/MCP layer for explicitly delegated student context and bounded actions | [ai.gapwise.ca](https://ai.gapwise.ca) |
| **[`gapwise-data`](https://github.com/andrewmuratov/gapwise-data)** | Open campus-data, provenance, schema, validation, and reuse portal | [data.gapwise.ca](https://data.gapwise.ca) |
| **[`gapwise-docs`](https://github.com/andrewmuratov/gapwise-docs)** | Canonical developer documentation | [docs.gapwise.ca](https://docs.gapwise.ca) |
| **[`gapwise-status`](https://github.com/andrewmuratov/gapwise-status)** | Independent service-health monitoring and incident communication | [status.gapwise.ca](https://status.gapwise.ca) |

`gapwise-status` owns operational communication, not product semantics. The main `gapwise` repository remains authoritative for deterministic timetable, routing, gap, campus, API, and student-state behavior.

---

## Local development

Requires Node.js 22 or newer.

```bash
git clone https://github.com/andrewmuratov/gapwise-status.git
cd gapwise-status
npm install
npm run check
npm run build
npm run dev
```

`main` is the production status branch and deploys through the dedicated `gapwise-status` Vercel project. `status.gapwise.ca` is independent from the `gapwise` and `gapwise-docs` deployments.

---

## Project relationship

Gapwise is an independent project created by Andrew Muratov. It is not an official University of Toronto service and is not affiliated with or endorsed by the University of Toronto.
