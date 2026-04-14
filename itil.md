---
title: ITIL 4
nav_order: 6
---

# ITIL 4 — IT Service Management Framework

**ITIL (Information Technology Infrastructure Library)** is a globally recognized framework of best practices for IT Service Management (ITSM). Originally created in the 1980s by the UK government and now owned by AXELOS/PeopleCert, the current version is **ITIL 4** (2019).

The core idea: IT should be managed as a set of **services delivered to customers**, not just as technology. ITIL provides common vocabulary and structured practices so organizations can deliver, support, and continuously improve those services.

---

## Core concept: the Service Value System (SVS)

Everything in ITIL 4 revolves around the SVS — a model that turns demand into value through a central engine called the Service Value Chain.

```mermaid
flowchart TB
    Demand([Opportunity / Demand]) --> SVC
    subgraph SVS[Service Value System]
        GP[Guiding Principles]
        GOV[Governance]
        SVC[Service Value Chain]
        CI[Continual Improvement]
        PR[Practices - 34 total]
        GP --- SVC
        GOV --- SVC
        CI --- SVC
        PR --- SVC
    end
    SVC --> Value([Value])
```

### The 7 Guiding Principles
1. Focus on value
2. Start where you are
3. Progress iteratively with feedback
4. Collaborate and promote visibility
5. Think and work holistically
6. Keep it simple and practical
7. Optimize and automate

---

## The Service Value Chain

Six interconnected activities. They are **not** sequential — different value streams combine them in different orders.

```mermaid
flowchart LR
    Plan[Plan]
    Improve[Improve]
    Engage[Engage]
    DT[Design & Transition]
    OB[Obtain / Build]
    DS[Deliver & Support]

    Engage --> Plan
    Engage --> DT
    Engage --> OB
    Engage --> DS
    Plan --> DT
    DT --> OB
    OB --> DS
    DS --> Engage
    Improve --- Plan
    Improve --- DT
    Improve --- OB
    Improve --- DS
    Improve --- Engage
```

---

## Key practices: Incident vs Problem vs Change

The three practices you'll hear most often in any ServiceNow-based support team.

```mermaid
flowchart TD
    User([User reports issue]) --> SD[Service Desk]
    SD --> INC[Incident Management<br/>Restore service ASAP]
    INC -->|Recurring or unknown cause| PRB[Problem Management<br/>Find root cause]
    PRB -->|Solution requires modification| CHG[Change Enablement<br/>Assess, approve, deploy]
    CHG --> Prod[(Production)]
    INC -->|Service restored| Closed([Ticket Closed])
    PRB -->|Workaround documented| KB[(Knowledge Base)]
    KB --> SD
```

---

## Incident Management lifecycle

The standard flow a support ticket follows from detection to closure.

```mermaid
flowchart LR
    A[Detect / Report] --> B[Log & Categorize]
    B --> C[Prioritize<br/>Impact x Urgency]
    C --> D[Investigate & Diagnose]
    D --> E{Resolved at<br/>L1?}
    E -->|Yes| H[Resolve & Recover]
    E -->|No| F[Escalate L2/L3]
    F --> D
    H --> I[Close & Document]
    I --> J[(Knowledge Base)]
```

---

## How ITIL works together with Agile

ITIL doesn't compete with Agile — it complements it. Agile **builds** software iteratively; ITIL **operates and supports** it reliably over its full lifecycle. ITIL 4 explicitly embraces Agile, DevOps, and Lean.

```mermaid
flowchart LR
    subgraph DEV[Development World - Agile/Scrum]
        Backlog[Product Backlog] --> Sprint[Sprint]
        Sprint --> Build[Build & Test]
        Build --> Release[Release Candidate]
    end
    subgraph OPS[Operations World - ITIL]
        CHG[Change Enablement]
        DEP[Deployment]
        INC[Incident Mgmt]
        PRB[Problem Mgmt]
        CI[Continual Improvement]
    end
    Release --> CHG
    CHG --> DEP
    DEP --> Prod[(Production)]
    Prod --> INC
    INC --> PRB
    PRB --> CI
    CI -.feedback.-> Backlog
```

**Key handoffs:**
- Agile team finishes a release → ITIL **Change Enablement** assesses risk and approves deployment
- Production incidents are managed under **Incident Management** with SLAs
- Recurring issues feed **Problem Management**, which generates new backlog items for the Agile team
- **Continual Improvement** closes the loop between operations and development

---

## Quick reference

| Concept | One-line description |
|---|---|
| **SVS** | Top-level model turning demand into value |
| **Service Value Chain** | Six activities: Plan, Improve, Engage, Design & Transition, Obtain/Build, Deliver & Support |
| **Incident** | Unplanned interruption — restore service fast |
| **Problem** | Underlying cause of one or more incidents |
| **Change** | Addition, modification, or removal of anything that could affect services |
| **SLA** | Service Level Agreement — measurable commitments to the customer |
| **CMDB** | Configuration Management Database — inventory of IT assets and relationships |

---

## Team roles

ITIL organizations have formalized roles around each practice. You will see these job titles (often in ServiceNow-based shops).

```mermaid
flowchart TB
    User([User / Customer]) --> SD[Service Desk Agent<br/>L1 triage]
    SD --> L2[L2 / L3 Support Engineer<br/>technical resolution]
    SD -.escalate major incident.-> MIM[Major Incident Manager]
    L2 -.recurring.-> PRBM[Problem Manager<br/>root-cause analysis]
    PRBM --> CHGM[Change Manager<br/>Change Enablement]
    CHGM --> CAB[CAB<br/>Change Advisory Board]
    CAB --> RM[Release Manager<br/>deployment]
    CFGM[Configuration Manager<br/>CMDB owner] -.supports all.-> L2
    SLM[Service Level Manager<br/>SLA owner] -.monitors.-> SD
    SO[Service Owner<br/>accountable for service] --- SLM
```

| Role | Primary responsibility |
|---|---|
| **Service Owner** | End-to-end accountability for a service across its lifecycle |
| **Service Desk Agent (L1)** | First contact, logs and triages incidents and requests |
| **L2 / L3 Support Engineer** | Technical investigation and resolution of escalated tickets |
| **Incident Manager** | Owns the Incident Management practice; coordinates response |
| **Major Incident Manager** | Leads high-severity incidents; drives comms and resolution |
| **Problem Manager** | Root-cause analysis for recurring or high-impact incidents |
| **Change Manager** | Assesses change risk, chairs the CAB, approves deployments |
| **Release Manager** | Plans and coordinates deployment of approved changes |
| **Configuration Manager** | Owns the CMDB; maintains CI accuracy and relationships |
| **Service Level Manager** | Negotiates and monitors SLAs, OLAs, and underpinning contracts |
| **Knowledge Manager** | Curates the knowledge base so fixes are reusable |
