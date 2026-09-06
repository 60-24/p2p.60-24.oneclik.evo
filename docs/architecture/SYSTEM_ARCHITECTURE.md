# P2P 60-24 OneClick EVO — System Architecture

**Version:** 0.1  
**Status:** FOUNDATION / PROPOSED  
**Principle:** Maximization through minimization

---

## 1. Purpose

This document translates the Core Ontology into a simple system architecture.

It answers one question:

> **What is the smallest architecture that can grow into the P2P 60-24 ecosystem without breaking its principles?**

---

## 2. Architecture in one picture

```text
                    HUMAN
                      │
                decides / governs
                      │
                      ▼
              ┌───────────────┐
              │      NODE     │
              │               │
              │ Identity      │
              │ Local State   │
              │ P2P Engine    │
              │ Trust         │
              │ Modules       │
              └───────┬───────┘
                      │
                 P2P transport
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
        NODE        NODE        NODE
          \           |           /
           └──────── NETWORK ────┘
                      │
                      ▼
                  ECOSYSTEM
```

There is no central server in the core architecture.

---

## 3. Layers

The system is divided into layers so that each layer can be tested independently.

### Layer 0 — Process

The running program.

### Layer 1 — Node

The independent participant.

### Layer 2 — Identity

The cryptographic identity of the Node.

### Layer 3 — P2P Transport

Communication between independent Nodes.

### Layer 4 — Protocol

Rules for handshake, messages, validation and responses.

### Layer 5 — Local State

Data belonging to the local Node.

### Layer 6 — Trust

Local knowledge about relationships with other Nodes.

### Layer 7 — Atom / OMF / Modules

Higher-level ecosystem functionality.

### Layer 8 — AI / Governance / Ecosystem

Coordination, suggestions and collective evolution.

---

## 4. The minimal kernel

The first implementation target is deliberately tiny.

```text
PROCESS
  ↓
NODE
  ↓
IDENTITY
  ↓
P2P
  ↓
HANDSHAKE
  ↓
MESSAGE
  ↓
RESPONSE
```

Nothing above this is required to prove that the foundation works.

### Minikernel v0.1 success condition

Two independent Nodes must be able to:

1. start independently,
2. identify themselves,
3. discover or be given the other Node,
4. establish a connection/relationship,
5. exchange a message,
6. validate the message,
7. return a response,
8. shut down cleanly.

---

## 5. Separation of concerns

```text
IDENTITY       = Who am I?
TRANSPORT      = How do I reach another Node?
PROTOCOL       = What are we saying?
STATE          = What do I know locally?
TRUST          = How much do I trust this relationship?
ATOM           = What functional unit exists?
MODULE         = What capability is provided?
AI             = What can be suggested?
GOVERNANCE     = Who decides?
```

A component should answer one primary question.

---

## 6. Data flow

Minimal flow:

```text
Node A
  │
  ├── create message
  │
  ├── sign / validate identity
  │
  ▼
P2P transport
  │
  ▼
Node B
  │
  ├── receive
  ├── validate
  ├── process
  └── respond
  │
  ▼
Node A
```

The first kernel does not need AI, governance, reputation markets or complex ontology queries to complete this flow.

---

## 7. Locality principle

Each Node owns its local state.

```text
NODE A                    NODE B
local state               local state
     │                         │
     └────── messages ─────────┘
```

A Node should never depend on a permanent central database for normal operation.

---

## 8. Privacy boundary

The architecture separates the private genotype/state from the public communication phenotype.

```text
PRIVATE LOCAL STATE
       │
       │ controlled information
       ▼
PUBLIC P2P PHENOTYPE
       │
       ▼
OTHER NODE
```

Sensitive local information must not be exposed through public HTTP endpoints or logs.

---

## 9. HTTP boundary

HTTP is not the core P2P communication layer.

It is an interface/phenotype layer for interacting with a Node.

```text
P2P CORE
   │
   ├──────── UDP P2P
   │
   └──────── local/public HTTP interface
```

The HTTP interface must never become a hidden central coordinator.

---

## 10. Technology boundary

The current project architecture defines:

- Go
- UDP P2P
- HTTP phenotype interface
- ed25519 identity/signatures
- SHA256
- BadgerDB for local persistence

The architecture intentionally avoids introducing unnecessary infrastructure.

No Docker, Kubernetes, npm or pip are required by the core architecture.

---

## 11. Growth model

The architecture grows outward, never by making the kernel unnecessarily large.

```text
                 ECOSYSTEM
                     ▲
                  MODULES
                     ▲
                 ATOM / OMF
                     ▲
                   TRUST
                     ▲
                 PROTOCOL
                     ▲
                  P2P CORE
                     ▲
                  IDENTITY
                     ▲
                    NODE
```

Each upper layer must be able to rely on a stable lower layer.

---

## 12. Failure principle

A failure in a higher layer must not automatically destroy the minimal communication layer.

Example:

```text
AI failure       → P2P should continue
Module failure   → P2P should continue
OMF failure      → P2P should continue
Trust failure    → Node should fail safely
P2P failure      → higher communication cannot continue
```

This creates a clear dependency direction.

---

## 13. Dependency direction

```text
Ecosystem
   ↓
Governance / AI
   ↓
Modules / OMF / Atom
   ↓
Trust
   ↓
Protocol
   ↓
P2P Transport
   ↓
Identity
   ↓
Node / Process
```

Dependencies should point downward.

The kernel must not depend on the ecosystem.

---

## 14. Development rule

For every new feature ask three questions:

1. **Is it necessary now?**
2. **Can it be implemented without enlarging the kernel?**
3. **Can we test it independently?**

If the answer is no, postpone the feature.

---

## 15. Current roadmap

```text
[1] CORE ONTOLOGY          ← completed
        ↓
[2] SYSTEM ARCHITECTURE    ← this document
        ↓
[3] P2P PROTOCOL v0.1
        ↓
[4] MINIKERNEL v0.1
        ↓
[5] TEST TWO NODES
        ↓
[6] IDENTITY + TRUST
        ↓
[7] ATOM + OMF
        ↓
[8] MODULES
        ↓
[9] SUPPORT CIRCLE
        ↓
[10] AI + GOVERNANCE
        ↓
[11] ECOSYSTEM
```

The roadmap is sequential by default. A later stage may be changed only after analysis.

---

## 16. Architectural invariant

> **The smallest stable P2P kernel is more valuable than a large collection of unverified features.**

This is the main engineering interpretation of:

> **Maksymalizacja przez minimalizację.**

---

## 17. Next step

The next document is:

`docs/protocol/P2P_PROTOCOL_v0.1.md`

It will define only the minimum rules required for two Nodes to communicate.

No extra ecosystem features will be added there.