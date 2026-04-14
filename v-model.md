---
title: V-Model
nav_order: 7
---

# V-Model — Verification & Validation for Safety-Critical Systems

The **V-Model** is a development methodology where each design phase has a corresponding test phase, forming a "V" shape. It is the dominant model in **safety-critical embedded systems**: automotive (ISO 26262), medical devices (IEC 62304), aerospace (DO-178C), railway (EN 50128), and industrial (IEC 61508).

Core principle: **every requirement must be traceable to a test**, and every test must verify a defined requirement.

---

## The V-Model diagram

The left side decomposes the system; the right side integrates and verifies it. Horizontal arrows show the verification relationship.

```mermaid
flowchart TB
    UR[User Requirements] --> SR[System Requirements]
    SR --> AD[Architecture Design]
    AD --> MD[Module Design]
    MD --> Code[Implementation / Coding]
    Code --> UT[Unit Test]
    UT --> IT[Integration Test]
    IT --> ST[System Test]
    ST --> AT[Acceptance Test]

    MD -.verifies.-> UT
    AD -.verifies.-> IT
    SR -.verifies.-> ST
    UR -.verifies.-> AT
```

---

## Traceability — the heart of the V-Model

Every artifact must trace forward to tests and backward to requirements. This is what regulators audit.

```mermaid
flowchart LR
    Req[Requirement<br/>REQ-001] --> Spec[Spec / Design<br/>DES-014]
    Spec --> Code[Code<br/>module_x.c]
    Code --> Test[Test Case<br/>TC-042]
    Test --> Result[Test Result<br/>PASS]
    Result -.evidence.-> Req
```

---

## Industry standards by domain

| Domain | Standard | Safety levels |
|---|---|---|
| Automotive | **ISO 26262** | ASIL A → D |
| Automotive process | **ASPICE** | Level 0 → 5 |
| Medical devices | **IEC 62304** | Class A → C |
| Aerospace | **DO-178C** | DAL E → A |
| Railway | **EN 50128** | SIL 0 → 4 |
| Industrial | **IEC 61508** | SIL 1 → 4 |
| Functional safety (general) | **IEC 61508** | SIL 1 → 4 |

---

## Tooling

| Purpose | Tools |
|---|---|
| **Requirements management** | IBM DOORS, Polarion, Jama Connect, codeBeamer |
| **Modeling** | MATLAB/Simulink, Stateflow, Enterprise Architect, Cameo |
| **Static analysis** | Polyspace, LDRA, Coverity, SonarQube |
| **Unit testing (C/C++)** | VectorCAST, Cantata, Tessy, Google Test |
| **HIL/SIL testing** | dSPACE, Vector CANoe, NI VeriStand |
| **Coverage** | LDRA, VectorCAST, Bullseye |
| **Configuration mgmt** | Git + strict branching, IBM Rational Synergy |

---

## V-Model vs Agile

They seem opposed but increasingly coexist:

| Aspect | V-Model | Agile |
|---|---|---|
| Approach | Sequential, document-heavy | Iterative, working software |
| Strength | Traceability, audit, safety | Speed, adaptability |
| Best for | Embedded, regulated industries | Web, SaaS, internal tools |
| Risk | Late discovery of issues | Hard to certify |

**Hybrid: Agile-V / SafeScrum** — Iterations within the V, with each sprint producing traceable artifacts. Common in modern automotive (Tesla, OEMs adopting ASPICE + Agile).

---

## When you'll encounter it

Given your embedded background: any role in **automotive, medical imaging, robotics with safety functions, industrial automation, aerospace, or defense** will use some form of the V-Model. Even when teams say "we do Agile," the underlying compliance work follows V-Model traceability.
