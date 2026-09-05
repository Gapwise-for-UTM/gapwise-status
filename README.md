<div align="center">

<img src="public/logo-mark-green.svg" width="116" alt="Gapwise deer mark" />

# Gapwise Status

### Independent service health for the full Gapwise ecosystem.

**The public monitoring and incident-communication surface for Gapwise applications, APIs, AI services, data and documentation surfaces, and selected operator-maintained systems.**

[![Live Status](https://img.shields.io/badge/Live_Status-status.gapwise.ca-36C692?style=for-the-badge&logo=vercel&logoColor=white)](https://status.gapwise.ca)
[![Monitoring](https://img.shields.io/badge/Monitoring-Every_15_Min-36C692?style=for-the-badge)](https://status.gapwise.ca)

<sub>Astro · GitHub Actions · Vercel</sub>

<br />

**[Status](https://status.gapwise.ca)** · **[History](https://status.gapwise.ca/history/)** · **[Gapwise](https://gapwise.ca)** · **[Data](https://data.gapwise.ca)** · **[AI](https://ai.gapwise.ca)** · **[Docs](https://docs.gapwise.ca)** · **[GitHub](https://github.com/Gapwise-for-UTM)**

</div>

---

## What Gapwise Status is

Gapwise Status is the independent operational-health surface for **Gapwise**, a multi-surface campus-intelligence ecosystem created and engineered by **Andrew Muratov**. The canonical repositories are owned by the **Gapwise for UTM** GitHub organization (`Gapwise-for-UTM`); Andrew remains the creator and primary maintainer.

Gapwise spans a student web/PWA product, native mobile client, deterministic public campus API and published JavaScript/TypeScript and Python SDKs, open data/provenance portal, permissioned OAuth/MCP AI integration, developer documentation, and this separately deployed monitoring and incident-communication service.

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

- automatic public-surface checks run every 15 minutes and are serialized to avoid competing publishers;
- stale monitoring data becomes visibly **unknown / monitoring delayed** rather than silently remaining green;
- operator-reported incidents remain visible when automation is stale;
- service-state transitions are retained for the public history view;
- current state and history are cached at the edge with GitHub-backed fallbacks;
- a failure to load status data is not itself presented as proof that Gapwise is down;
- external University of Toronto systems and other upstream dependencies remain outside Gapwise's control.

Public routes include `/` for current state, `/history/` for recorded transitions/incidents, `/_data/current`, and `/_data/history`.

---

## Current developer-platform state

Gapwise's public developer surface is versioned at `https://api.gapwise.ca/v1` with an OpenAPI 3.1 contract at `https://api.gapwise.ca/openapi.json`. The current first-party SDK releases are public through canonical npm, JSR, and PyPI channels, with a source-adjacent GitHub Packages mirror:

```bash
npm install @gapwise/sdk@0.1.1
# JSR: @gapwise/sdk@0.1.1
# GitHub Packages mirror: @gapwise-for-utm/sdk@0.1.1
python -m pip install gapwise==0.1.0
```

The JavaScript/TypeScript SDK is canonically published as `@gapwise/sdk` on npm and JSR and mirrored on GitHub Packages as `@gapwise-for-utm/sdk`; the Python SDK is published on PyPI. The GitHub Packages scope differs because GitHub requires package scopes to match the owning organization. SDK registry availability is a developer-platform release fact, not a status-page substitute: operational availability still belongs to live monitoring of the API and related production services.

---

## Gapwise ecosystem

| Repository | Role | Primary surface |
| --- | --- | --- |
| **[`gapwise`](https://github.com/Gapwise-for-UTM/gapwise)** | Core web/PWA, deterministic student/campus engine, public API, OpenAPI, and published SDK source | [gapwise.ca](https://gapwise.ca) / [api.gapwise.ca](https://api.gapwise.ca/v1) |
| **[`gapwise-mobile`](https://github.com/Gapwise-for-UTM/gapwise-mobile)** | Native iOS and Android client | Native mobile app |
| **[`gapwise-ai`](https://github.com/Gapwise-for-UTM/gapwise-ai)** | OAuth/MCP layer for explicitly delegated student context and bounded actions | [ai.gapwise.ca](https://ai.gapwise.ca) |
| **[`gapwise-data`](https://github.com/Gapwise-for-UTM/gapwise-data)** | Open campus-data, provenance, schema, validation, and reuse portal | [data.gapwise.ca](https://data.gapwise.ca) |
| **[`gapwise-docs`](https://github.com/Gapwise-for-UTM/gapwise-docs)** | Canonical developer documentation | [docs.gapwise.ca](https://docs.gapwise.ca) |
| **[`gapwise-status`](https://github.com/Gapwise-for-UTM/gapwise-status)** | Independent service-health monitoring and incident communication | [status.gapwise.ca](https://status.gapwise.ca) |

`gapwise-status` owns operational communication, not product semantics. The main `gapwise` repository remains authoritative for deterministic timetable, routing, gap, campus, API, SDK, and student-state behavior.

---

## Local development

Requires Node.js 22 or newer.

```bash
git clone https://github.com/Gapwise-for-UTM/gapwise-status.git
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
