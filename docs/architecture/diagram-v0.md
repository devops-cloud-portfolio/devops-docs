# Architecture diagram v0

```mermaid
flowchart LR
  subgraph CI[GitHub Actions]
    CIWF[ci workflow]
    GHCR[(GHCR)]
    CIWF -->|build + push| GHCR
  end

  subgraph GitOps[platform-k8s-gitops]
    GIT[(git repo)]
    ARGO[Argo CD]
    GIT --> ARGO
  end

  GHCR --> ARGO

  subgraph DEV[dev namespace]
    API[api]
    W[worker]
    R[(redis)]
    P[(postgres)]
    API -->|enqueue| R
    W -->|consume| R
    W -->|write| P
    API -->|read| P
  end

  subgraph STAGE[stage namespace]
    API2[api]
    W2[worker]
    R2[(redis)]
    P2[(postgres)]
  end

  ARGO --> DEV
  ARGO --> STAGE

