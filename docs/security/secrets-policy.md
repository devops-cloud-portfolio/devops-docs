# Secrets policy

## Rules

- Secrets must never be committed to git (tokens, passwords, private keys, kubeconfigs).
- Local development uses a `.env` file (kept out of the repo via `.gitignore`).
- The repository contains only `.env.example` as a documented template.
- CI secrets are stored in GitHub Actions Secrets (repository or organization level).
- GitOps secrets are encrypted with SOPS and age. Only encrypted files are committed.

## What counts as a secret

- Cloud credentials, API keys, access tokens
- Database passwords and connection strings
- Private keys (SSH, age private key)
- Kubeconfig files containing cluster credentials

## If a secret is leaked

1. Revoke, rotate the secret immediately.
1. Remove the secret from git history (e.g., `git filter-repo`).
1. Add a CI guard (secret scanning, gitleaks) to prevent recurrence.
1. Document the incident briefly in `docs/drills/` or `docs/postmortems/` (if applicable).
