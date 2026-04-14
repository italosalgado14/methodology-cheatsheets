# DevOps — Unifying Development and Operations

**DevOps** is a cultural and technical movement that unifies software development (Dev) and IT operations (Ops) to deliver software faster, more reliably, and with shorter feedback loops. It emerged around 2009 from the Agile and Lean movements.

Core pillars: **CAMS** — Culture, Automation, Measurement, Sharing.

---

## The DevOps infinity loop

The classic representation: an endless cycle where development and operations feed each other.

```mermaid
flowchart LR
    Plan[Plan] --> Code[Code]
    Code --> Build[Build]
    Build --> Test[Test]
    Test --> Release[Release]
    Release --> Deploy[Deploy]
    Deploy --> Operate[Operate]
    Operate --> Monitor[Monitor]
    Monitor --> Plan
```

---

## CI/CD pipeline

The technical backbone of DevOps: every commit flows automatically through build, test, and deploy.

```mermaid
flowchart LR
    Dev([Developer commit]) --> Git[(Git repo)]
    Git --> CI[CI: Build & Unit Test]
    CI --> Artifact[(Artifact / Image)]
    Artifact --> CD[CD: Deploy to Staging]
    CD --> E2E[E2E / Integration Tests]
    E2E --> Prod[(Production)]
    Prod --> Mon[Monitoring & Logs]
    Mon -.feedback.-> Dev
```

---

## Tooling landscape

```mermaid
flowchart TB
    subgraph SCM[Source Control]
        Git[Git / GitHub / GitLab]
    end
    subgraph CI[CI/CD]
        GHA[GitHub Actions]
        GLC[GitLab CI]
        Jenkins
    end
    subgraph PKG[Packaging]
        Docker
        Helm
    end
    subgraph IAC[Infrastructure as Code]
        Terraform
        Ansible
    end
    subgraph ORCH[Orchestration]
        K8s[Kubernetes]
    end
    subgraph OBS[Observability]
        Prometheus
        Grafana
        Datadog
    end
    SCM --> CI --> PKG --> ORCH
    IAC --> ORCH
    ORCH --> OBS
```

---

## DORA metrics — measuring DevOps performance

Industry-standard metrics from the DORA research:

| Metric | What it measures | Elite target |
|---|---|---|
| **Deployment Frequency** | How often you release | Multiple per day |
| **Lead Time for Changes** | Commit → production | < 1 hour |
| **Change Failure Rate** | % of deploys causing issues | 0–15% |
| **Mean Time to Restore (MTTR)** | Time to recover from failure | < 1 hour |

---

## When to adopt DevOps

- Cloud-native or web/SaaS products
- Multiple deployments per week (or more)
- Cross-functional teams that own services end-to-end
- Less suited (in pure form) to safety-critical embedded — though CI/CD principles still apply
