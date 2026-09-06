# P2P 60-24 OneClick EVO — Core Ontology

**Version:** 0.1  
**Status:** FOUNDATION / PROPOSED  
**Purpose:** minimal common language for the project

---

## 1. Fundamental principle

> **Maximization through minimization.**
>
> Build the smallest correct system first. Add complexity only when a tested need requires it.

The ontology defines **what exists** in the system. It does not yet define implementation details.

---

## 2. System boundary

P2P 60-24 OneClick EVO is a distributed ecosystem of independent nodes.

```text
NODE ↔ NODE ↔ NODE
       ↓
    NETWORK
       ↓
   ECOSYSTEM
```

There is no central coordinating server in the core architecture.

---

## 3. Primary entities

### Node

An independent participant in the P2P network.

A Node has at minimum:

- Node ID
- public identity key
- local state
- peer knowledge
- communication capability

### Peer

A Node known to another Node through a network relationship.

```text
Node A ── peer relationship ── Node B
```

### Message

A unit of information exchanged between Nodes.

```text
Sender → Message → Receiver
```

### Atom

A minimal functional unit of the future ecosystem.

```text
ATOM
├── Data Core
├── Logic Core
├── Interface Layer
├── Reputation / Trust Field
└── External Data
```

At the current foundation stage, Atom is a conceptual entity. It must not complicate the minimal P2P kernel.

### Relation

A defined connection between entities.

Examples:

```text
Node ──knows──> Peer
Node ──sends──> Message
Atom ──depends_on──> Atom
Node ──trusts──> Node
```

### Trust

A local, contextual property of a relationship between Nodes.

Trust is not a global currency and must not require a central authority.

---

## 4. Entity hierarchy

```text
ATOM
  ↓
NODE
  ↓
NETWORK
  ↓
ECOSYSTEM
```

This is a conceptual hierarchy, not a requirement that every Node must contain an Atom immediately.

---

## 5. Minimal runtime ontology

Before all higher layers exist, the system needs only:

```text
Node
  ↓
Peer
  ↓
Connection
  ↓
Message
  ↓
Response
```

This is the foundation of **P2P Minikernel v0.1**.

Acceptance concept:

> Two independent Nodes can establish a valid relationship and exchange a verified message without a central server.

---

## 6. Identity

Every Node must have an identity that can be used to distinguish it from another Node.

The current architecture uses **ed25519** for cryptographic identity and signatures.

Private identity material is local and must never be exposed through HTTP or logs.

---

## 7. Communication

The core communication model is:

```text
Node A
  │
  │ P2P transport
  ▼
Node B
```

Current architectural direction:

- UDP for P2P communication
- HTTP only as the local/public phenotype interface
- no central message broker

The exact protocol belongs in a separate specification.

---

## 8. Human and AI roles

### Human

The human remains the final decision authority for governance and important system changes.

### AI

AI is a decision-support layer:

```text
AI → analyse → suggest → optimise
                    ↓
                 HUMAN
                 decides
```

AI suggestions are not automatically architectural truth.

---

## 9. Evolution

The project evolves by adding validated layers:

```text
ONTOLOGY
   ↓
P2P MINIKERNEL
   ↓
IDENTITY
   ↓
TRUST
   ↓
ATOM
   ↓
OMF
   ↓
MODULES
   ↓
ECOSYSTEM
```

A future layer must not destabilize a previously validated lower layer without an explicit architectural decision.

---

## 10. Non-goals of v0.1

This document does **not** define yet:

- complete OMF semantics,
- reputation algorithms,
- governance protocol,
- economics or tokens,
- Support Circle protocol,
- AI autonomy,
- module implementation,
- final network discovery algorithm.

Those belong to later specifications.

---

## 11. First invariant

> **If two Nodes cannot reliably communicate, no higher-level feature is considered complete.**

Therefore the immediate engineering target is:

```text
ONE NODE
   ↓
TWO NODES
   ↓
HANDSHAKE
   ↓
MESSAGE
   ↓
VERIFIED RESPONSE
```

Only after this works should the next layer be added.

---

## 12. Ontological summary

```text
PROJECT
└── P2P 60-24 OneClick EVO
    ├── Entity
    │   ├── Node
    │   ├── Peer
    │   ├── Message
    │   ├── Atom
    │   └── Relation
    │
    ├── Foundation
    │   ├── Identity
    │   └── P2P Communication
    │
    ├── Intelligence
    │   └── AI → Suggests
    │
    ├── Governance
    │   └── Human → Decides
    │
    └── Evolution
        └── Small validated steps
```

**Next document:** `docs/architecture/SYSTEM_ARCHITECTURE.md`

**Next technical milestone:** P2P Minikernel v0.1.