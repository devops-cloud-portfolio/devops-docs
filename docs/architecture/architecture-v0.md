# Architecture v0

## Goal

This small poroject is built like a setup around one real workload (Agent Service).

## Workload: Agent Service

Components:

- API accepts a job and returns `job_id`
- Worker takes jobs from Redis and writes results to Postgres
- Redis job queue
- PostgreSQL job status and results

Notes:

- Logs include `job_id` so debugging is easier.
- Tests are basic but real (API and worker happy path).

## CI (pipeline)

CI runs in GitHub Actions.
It does lint, tests, build and later security scans.

Images:

- registry GHCR
- PR checks only (no push)
- main build and push (tag = commit SHA)
- release tag build, push (tag = semver) and release notes

## CD (GitOps)

Deployments are GitOps-based.

- source of truth `platform-k8s-gitops`
- Argo CD syncs the cluster from Git

Environments:

- dev auto-sync
- stage more controlled (promotion via PR)

Promotion is PR in the GitOps repo that bumps the image tag (or values).

## Kubernetes baseline (planned)

- non-root containers
- no privilege escalation
- RBAC with ServiceAccounts
- NetworkPolicy
- Pod Security Admission baseline

## Observability (planned)

Minimal setup:

- metrics/dashboards Prometheus and Grafana
- alerts Alertmanager
- logs Loki and Grafana

Target: at least 3 alerts and 3 runbooks.

## Backup / restore (planned)

- scheduled Postgres backups (CronJob)
- backups stored in S3-compatible storage
- restore test from time to time and short report (date, result, notes)

## Evidence I will produce

- CI runs and artifacts (lint, test, scan reports)
- GitOps promotion PR examples
- runbooks (crashloop, DB issues, low resources)
- restore test report
- postmortem after a controlled incident
