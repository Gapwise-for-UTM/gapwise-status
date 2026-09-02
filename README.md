# Gapwise Status

Independent public service-status surface for Gapwise.

## Public routes

- `/` — current service status
- `/history/` — recorded service-state transitions
- `/_data/current` — edge-cached current status source
- `/_data/history` — edge-cached incident-history source

The production hostname is `status.gapwise.ca`. Legacy `/status/` URLs redirect to the canonical root routes after deployment.

## Monitoring

The repository owns its own status data in issue `#1`.

- Automated production probes run hourly at minute 17.
- Authentication/sync and transactional auth email remain operator-maintained.
- State transitions are recorded as machine-readable comments on issue `#1`.
- Current state and history are cached at the Vercel edge with direct GitHub API fallbacks.

This status surface is intentionally deployment-independent from `gapwise-docs` and the main Gapwise application.

## Development

```bash
npm install
npm run dev
npm run check
npm run build
```

The status publisher scripts are syntax-checked as part of `check` and `build`.
