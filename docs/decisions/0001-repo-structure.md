# ADR 0001: Repo structure

## Context

This project should be easy to review fast (around 10 minutes), but still show the full DevOps chain:
CI, images, GitOps, Kubernetes, security, observability, backup/restore, IaC and automation.

## Decision

I split the work into a few repos in one GitHub org:

- `start` - landing page and links (10-min demo)
- `devops-docs` - docs hub: architecture, ADRs, runbooks, drills, reports
- `agent-service` - app code (API, worker) and docker-compose
- `platform-k8s-gitops` - GitOps repo (Argo CD, dev/stage, manifests/Helm)
- `infra-aws-terraform` - Terraform for AWS (remote state, OIDC, CI checks)
- `ansible-ops` - host automation (bootstrap, runner, basic hardening)

## Consequences

- Clear separation, easier review and cleaner history
- Easier `start` is the entry point
- More cross-links between repos (solved by `start` and consistent docs structure)

## Alternatives I considered

1. Monorepo

- plus - everything in one place
- minus - mixed topics, harder to review fast

1. One repo for app and platform

- plus - fewer repos
- minus - app code and GitOps config become too coupled

1. GitHub Wiki for docs

- plus - easy browsing
- minus - weaker PR flow and less “docs as code”
