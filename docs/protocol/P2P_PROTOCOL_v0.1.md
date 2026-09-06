# P2P Protocol v0.1

**Status:** PROPOSED / SPECIFICATION  
**Purpose:** engineering preparation before implementation

## 1. Purpose

Define the smallest protocol that allows two independent OneClick EVO nodes to establish a basic relationship and exchange a verified message without a central server.

## 2. Core principle

> If two nodes cannot reliably communicate, no higher-level feature is complete.

The protocol must remain small, deterministic, testable and independently implementable.

## 3. Scope

v0.1 covers only:

- node identification,
- initial contact,
- handshake,
- message integrity and authenticity,
- basic data exchange,
- timeout and rejection behavior,
- clean termination.

### Non-goals

Not specified yet:

- automatic Internet-wide discovery,
- complete TrustGraph,
- reputation algorithms,
- governance,
- economics/tokens,
- Atom/OMF behavior,
- AI coordination,
- Support Circle protocol,
- production secure-channel encryption.

## 4. Actors

Two independent nodes:

- **Node A** — initiator
- **Node B** — responder

Neither node is a permanent coordinator.

## 5. Transport

- P2P transport: UDP.
- Each node owns its local network state.
- UDP delivery is not assumed to be reliable.
- The protocol therefore requires bounded messages, timeouts, retry rules and duplicate handling.
- HTTP `:8024` is a local phenotype/interface and is not the P2P transport.

## 6. Identity

Each node has a local cryptographic identity:

- Node ID
- ed25519 public key
- private key stored locally and never transmitted

The identity signs protocol messages.

**Important:** ed25519 provides authentication/integrity signatures. It does **not** by itself provide confidentiality. Encryption is a separate design decision.

## 7. Message envelope

Every protocol message should have a deterministic envelope containing at minimum:

- protocol version,
- message type,
- sender Node ID,
- intended receiver Node ID when applicable,
- unique message ID / nonce,
- freshness information,
- payload,
- signature.

The exact wire serialization is intentionally left open until the engineering design review.

## 8. Minimal message types

| Type | Purpose |
|---|---|
| `HELLO` | announce identity and protocol capability |
| `HELLO_ACK` | acknowledge and return responder identity |
| `PING` | test an established relationship |
| `PONG` | reply to `PING` |
| `DATA` | exchange application-level data |
| `ERROR` | report a protocol-level rejection/error |

No additional message type should be added without a concrete v0.1 requirement.

## 9. Minimal handshake

Conceptual sequence:

```text
Node A                         Node B
  |                              |
  |-------- HELLO -------------->| 
  |<------- HELLO_ACK ------------|
  |                              |
  |-------- DATA --------------->|
  |<------- DATA / RESPONSE ------|
  |                              |
```

A successful handshake establishes a minimal protocol relationship.

It does **not** yet claim an encrypted secure channel.

## 10. Protocol state machine

```text
NEW
  |
  +--> HELLO_SENT
  |
  +--> HELLO_RECEIVED
          |
          v
      ESTABLISHED
          |
          +--> CLOSED
```

Invalid messages must be rejected safely. A malformed or hostile packet must not crash the node.

## 11. Validation rules

A received message must be rejected when applicable if:

1. protocol version is unsupported,
2. message structure is invalid,
3. sender identity is invalid,
4. signature is invalid,
5. freshness/replay protection fails,
6. message type is invalid for the current state,
7. receiver/target does not match,
8. packet exceeds the protocol size limit.

Rejection must be local and bounded.

## 12. UDP behavior

The protocol must explicitly account for:

- packet loss,
- duplication,
- reordering,
- delayed packets,
- unreachable peer,
- temporary network failure.

The implementation must never assume that sending a UDP datagram means that the peer received it.

## 13. Errors

Minimum error classes:

- malformed message,
- unsupported version,
- invalid identity,
- invalid signature,
- replay/stale message,
- unexpected message/state,
- unknown peer,
- oversized message,
- timeout.

Errors must not expose private keys, invite tokens, private state or personally identifying information through protocol responses or logs.

## 14. Privacy boundary

Private node state remains local.

Never transmit or expose:

- private cryptographic keys,
- invite secrets/tokens,
- private configuration,
- unnecessary personal information.

The protocol exposes only the minimum information needed for the current operation.

## 15. Determinism

The protocol should be deterministic wherever practical:

- fixed message semantics,
- explicit state transitions,
- explicit validation order,
- stable error classes,
- no hidden coordinator behavior.

## 16. v0.1 acceptance tests

The protocol is ready for implementation only when these behaviors are defined well enough to test:

1. Two nodes start independently.
2. Node A sends `HELLO`.
3. Node B validates and sends `HELLO_ACK`.
4. Both nodes recognize the peer identity.
5. Node A sends `DATA`.
6. Node B validates the signature and processes the message.
7. Node B returns a response.
8. Duplicate messages are safely handled.
9. Malformed messages are rejected.
10. Invalid signatures are rejected.
11. Unsupported protocol versions are rejected.
12. Oversized packets are rejected.
13. Timeout does not crash either node.
14. Both nodes shut down cleanly.

## 17. Open engineering decisions

These decisions must be resolved before coding the protocol:

1. Exact wire serialization: JSON, binary, or another minimal deterministic format.
2. Maximum datagram/message size.
3. Timeout and retry values.
4. Exact freshness/replay mechanism.
5. Whether v0.1 uses manually supplied peer addresses or includes discovery.
6. Encryption mechanism for a future secure channel.
7. Persistent identity file/storage format.
8. Exact protocol version negotiation rules.

> **Rule: do not implement an open decision by guessing.**

## 18. Relationship to OneClick UX

The protocol is intentionally invisible to the normal user.

The desired user experience remains:

**Authorized download → one click → node starts → system handles networking automatically.**

Technical complexity belongs inside the system, not in the user's workflow.

## 19. Next preparation documents

Before implementation:

1. `REQUIREMENTS_v0.1.md`
2. `DATA_MODEL_v0.1.md`
3. `SECURITY_MODEL_v0.1.md`
4. `FAILURE_RESILIENCE_v0.1.md`
5. `TEST_PLAN_v0.1.md`
6. `IMPLEMENTATION_PLAN_v0.1.md`
7. Second whole-system architecture review

**No production code is authorized by this document.**