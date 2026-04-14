---
title: SRE
nav_order: 5
---

# SRE — Site Reliability Engineering

**Site Reliability Engineering** is Google's engineering approach to operations: "what happens when you ask a software engineer to design an operations team." Codified in the *Google SRE Book* (2016), it treats operations as a software problem.

Key idea: reliability is a **feature** that must be measured, budgeted, and traded off against new development.

---

## Core concepts: SLI, SLO, SLA, Error Budget

```mermaid
flowchart TB
    SLI[SLI<br/>Service Level Indicator<br/>e.g. request latency, error rate]
    SLO[SLO<br/>Service Level Objective<br/>internal target, e.g. 99.9% success]
    SLA[SLA<br/>Service Level Agreement<br/>contractual promise to customer]
    EB[Error Budget<br/>100% - SLO<br/>e.g. 0.1% allowed failure]
    SLI --> SLO
    SLO --> SLA
    SLO --> EB
    EB --> Decision{Budget<br/>remaining?}
    Decision -->|Yes| Ship[Ship new features]
    Decision -->|No| Freeze[Freeze releases<br/>focus on reliability]
```

---

## The error budget loop

The mechanism that balances velocity vs reliability.

```mermaid
flowchart LR
    Define[Define SLO] --> Measure[Measure SLI]
    Measure --> Calc[Calculate Error Budget]
    Calc --> Check{Budget OK?}
    Check -->|Yes| Innovate[Allow risky releases]
    Check -->|No| Stabilize[Pause features<br/>fix reliability]
    Innovate --> Measure
    Stabilize --> Measure
```

---

## Toil and automation

**Toil** = manual, repetitive operational work. SREs aim to cap toil at < 50% of their time and automate the rest.

```mermaid
flowchart LR
    Toil[Manual Toil<br/>tickets, on-call, restarts] --> Identify[Identify patterns]
    Identify --> Auto[Build automation<br/>scripts, runbooks, self-healing]
    Auto --> Reduce[Reduced toil]
    Reduce --> Engineer[More time for<br/>engineering work]
```

---

## On-call and incident response

```mermaid
flowchart TD
    Alert([Alert fires]) --> Page[On-call paged<br/>via PagerDuty]
    Page --> Ack[Acknowledge]
    Ack --> Inv[Investigate<br/>dashboards, logs, traces]
    Inv --> Mitigate[Mitigate<br/>rollback, restart, failover]
    Mitigate --> Resolved([Service restored])
    Resolved --> PM[Postmortem<br/>blameless]
    PM --> Actions[Action items<br/>backlog]
```

---

## Tooling

| Category | Tools |
|---|---|
| **Metrics** | Prometheus, Datadog, New Relic, CloudWatch |
| **Dashboards** | Grafana, Datadog |
| **Logs** | Loki, ELK stack, Splunk, Datadog Logs |
| **Tracing** | Jaeger, Tempo, Honeycomb, OpenTelemetry |
| **Alerting / On-call** | PagerDuty, Opsgenie, VictorOps |
| **Incident mgmt** | incident.io, FireHydrant, Rootly |
| **Chaos engineering** | Chaos Monkey, Gremlin, LitmusChaos |

---

## SRE vs DevOps vs ITIL

| Aspect | DevOps | SRE | ITIL |
|---|---|---|---|
| Origin | Community movement | Google engineering | UK government / ITSM |
| Focus | Culture + automation | Reliability as engineering | Service management |
| Key metric | DORA metrics | SLO / Error Budget | SLA compliance |
| Best for | Modern web/cloud teams | High-scale, high-reliability services | Enterprise IT operations |

> "SRE is a concrete implementation of DevOps principles."
