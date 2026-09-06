# P2P 60-24 OneClick EVO — Engineering Requirements v0.1

**Status:** PROPOSED / PRE-CODING  
**Version:** 0.1  
**Date:** 2026-09-06

## 1. Purpose

This document defines the minimum engineering requirements that must be understood before implementation begins.

The project follows the principle:

> **Maximization through minimization.**

The first implementation must be small, stable, testable and able to grow without breaking the core architecture.

## 2. Human-first requirement — OneClick

OneClick is not an optional interface feature. It is an architectural requirement.

The intended user flow is:

**Download → Allow → One Click → Ready**

A normal user must not need to understand:
- P2P,
- UDP,
- cryptographic keys,
- network configuration,
- node configuration,
- technical protocols.

Technical complexity remains inside the system.

Errors shown to the user must be simple, calm and understandable.

## 3. Minimal runtime requirements

Version 0.1 must support:

1. Two independent Nodes can start locally.
2. Each Node has a local identity.
3. Nodes can communicate directly over P2P transport.
4. A Node can authenticate messages from another Node.
5. Nodes can exchange a minimal DATA message.
6. A receiving Node can validate and respond.
7. Both Nodes can shut down cleanly.

Nothing above may require a central coordinating server.

## 4. Identity and security requirements

- Private identity material remains local to the Node.
- Private keys must never be exposed through HTTP, logs or network messages.
- Messages requiring authentication must have a verifiable signature.
- Invalid signatures must be rejected.
- Malformed messages must be rejected safely.
- Replay protection/freshness must be defined before implementation.
- Message size limits must be defined before implementation.
- Unknown peers must not automatically become trusted peers.
- Personal or sensitive information must not be placed in public phenotype interfaces or logs.

**Important:** Ed25519 provides signatures/authentication and integrity. It does **not** by itself provide encryption. A secure encrypted channel is a separate requirement and must be specified explicitly.

## 5. Resilience requirements

UDP is an unreliable transport. The implementation must therefore define:

- timeouts,
- retry behavior,
- duplicate handling,
- malformed-packet handling,
- oversized-packet handling,
- invalid-message handling,
- clean failure behavior.

A bad network packet must never crash the Node.

Failure of a higher layer must not automatically destroy the minimal communication kernel.

## 6. Determinism and testability

The minimal protocol must have:

- deterministic state transitions,
- deterministic validation rules,
- repeatable test cases,
- explicit acceptance criteria,
- no hidden or unspecified behavior.

If a behavior is not specified, it must not be guessed in code.

## 7. System boundaries

The minimal core consists of:

**Process → Node → Identity → P2P → Protocol → Message → Response**

The following remain outside the minimal kernel for v0.1:

- full OMF,
- advanced discovery,
- economics/tokens,
- governance implementation,
- autonomous AI decisions,
- Support Circle protocol,
- autonomous evolution,
- large module ecosystem.

HTTP remains the phenotype/interface layer and must not become the central coordination mechanism.

## 8. Technology constraints

The current architecture defines:

- Go 1.21+
- UDP P2P
- HTTP phenotype
- Ed25519
- SHA-256
- BadgerDB

The project does not introduce Docker/Kubernetes/npm/pip or a central cloud service into the minimal kernel.

## 9. Definition of pre-coding readiness

Implementation may begin only after this chain is sufficiently specified:

**Ontology → Architecture → Protocol → Requirements → Data Model → Security → Failure/Resilience → Tests → Implementation Plan → Code**

The goal is not to document everything before writing any code. The goal is to remove architectural ambiguity from the minimal kernel before coding it.

## 10. Open-decision rule

When an important implementation detail is not specified, the implementation must stop at that boundary and record the architectural decision first.

**Do not guess architecture in code.**

## 11. Acceptance principle

The first real proof of the system is simple:

> Two independent Nodes can start, recognize each other, communicate directly, validate a message, exchange a response, handle failure safely and shut down cleanly.

If this cannot be demonstrated reliably, higher-level functionality is not considered complete.

## 12. Next document

Next planned document:

`docs/data/DATA_MODEL_v0.1.md`

No implementation is started by this document.
