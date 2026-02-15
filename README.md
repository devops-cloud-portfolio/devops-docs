# DevOps Portfolio Docs

Documentation hub for the DevOps portfolio:

- Architecture notes
- ADRs (Architecture Decision Records)
- Runbooks
- DR drills (backup/restore)
- CKA practice notes

## Status

\[ \] Done

- Basics: PR flow, required checks
- Docs: architecture v0 and ADR 0001
- Security basics: .gitignore, .env.example, secrets policy

\[ \] Next

- Workload MVP locally (docker-compose)
- CI build/publish rules + security scans

## Security

Never commit secrets (tokens, API keys, kubeconfigs, private keys).
Use .env loacally and Github Secrets.

> Everything is built via PRs and verified with CI.
