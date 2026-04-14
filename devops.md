---
title: DevOps
nav_order: 4
---

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

---

## Team roles

DevOps is a culture more than a job title, but in practice several specialized roles own the pipeline, platform, and shared tooling.

```mermaid
flowchart TB
    subgraph Dev[Development]
        SWE[Software Engineer<br/>owns code + CI/CD for service]
    end
    subgraph Platform[Platform / DevOps]
        DOE[DevOps Engineer<br/>pipelines, IaC, automation]
        PE[Platform Engineer<br/>internal developer platform]
        CA[Cloud Architect<br/>cloud design]
    end
    subgraph Sec[Security]
        SEC[DevSecOps Engineer<br/>shift-left security]
    end
    subgraph Ops[Operations]
        SRE[SRE<br/>reliability & on-call]
        RM[Release Manager<br/>coordination]
    end
    SWE --> DOE
    DOE --> PE
    PE --> SRE
    SEC --- DOE
    CA --- PE
```

| Role | Primary responsibility |
|---|---|
| **Software Engineer** | Builds the service and owns its CI/CD pipeline end-to-end |
| **DevOps Engineer** | Automates build, test, deploy, and infrastructure provisioning |
| **Platform Engineer** | Delivers the internal developer platform (IDP) — self-service infra for devs |
| **Cloud Architect** | Designs cloud topology, networking, cost, and multi-region strategy |
| **DevSecOps / Security Engineer** | Embeds security scanning (SAST/DAST/SBOM) into pipelines |
| **Release Manager** | Coordinates releases across teams (more common in large/regulated orgs) |
| **Site Reliability Engineer** | Reliability, observability, incident response (see SRE page) |
