# Security Policy

## Supported deployment

Security fixes target the current `main` branch and the production deployment at `status.gapwise.ca`.

## Reporting a vulnerability

Do not open a public issue for a suspected vulnerability. Use GitHub private vulnerability reporting when available, or follow the canonical Gapwise reporting instructions at <https://gapwise.ca/security>.

Do not include credentials, tokens, private user data, or exploitable proof-of-concept details in public issues, workflow logs, or status-history comments.

## Status-data boundary

GitHub issue #1 is a machine-managed public status-data source. It must contain only public service state and sanitized operational detail. Automated checks and operator updates must never write secrets, authentication material, private request payloads, user identifiers, or internal-only incident evidence into that issue.

Production credentials belong in GitHub Actions or deployment-platform secret storage and must never be committed to the repository.
