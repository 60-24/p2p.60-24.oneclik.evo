# P2P 60-24 OneClick EVO — Data Model v0.1

**Status:** PROPOSED / PRE-CODING  
**Version:** 0.1  
**Purpose:** minimal, stable data model for the first two-node P2P kernel.

## 1. Principle

The data model must be as small as possible while being sufficient for:

`Node → Identity → Peer → Connection → Message → Response`

No higher-level AEA, OMF, AI, governance, economics or Support Circle data is required in v0.1.

## 2. Core entities

### Node
A running local instance of the P2P system.

Required conceptual fields:
- `node_id`
- `identity`
- `protocol_version`
- `runtime_state`

The Node owns its local identity and local state.

### Identity
Cryptographic identity of a Node.

Required conceptual fields:
- `node_id`
- `public_key`
- private signing key — **local only; never transmitted, logged or exposed through HTTP**

Identity answers:

`WHO AM I?`

### Peer
A remote Node known locally.

Required conceptual fields:
- `node_id`
- `public_key`
- network address information
- local relationship state
- last-seen information

A Peer record does not automatically mean the peer is trusted.

### Connection
The current communication relationship between two Nodes.

Required conceptual fields:
- local node
- remote node
- connection state
- transport information
- timestamps / freshness data

Minimal states:

`NEW → HANDSHAKING → ESTABLISHED → CLOSED`

### Message
A protocol unit exchanged between Nodes.

Required conceptual fields:
- protocol version
- message type
- message ID / nonce
- sender Node ID
- receiver / target Node ID when required
- timestamp / freshness value
- payload
- signature

A Message is valid only after protocol and cryptographic validation.

## 3. Relationships

```text
Node
 ├── owns → Identity
 ├── knows → Peer
 ├── creates → Connection
 └── sends → Message

Peer
 └── may participate in → Connection

Connection
 └── carries → Message

Message
 └── receives → Response Message
```

## 4. Identity rules

1. Each Node has one local cryptographic identity in the minimal model.
2. `node_id` must have a deterministic relationship to the identity/public key definition chosen by the protocol.
3. Private key material remains local.
4. Public identity may be exchanged during handshake.
5. Identity is not the same thing as trust.

## 5. Peer rules

A Peer is local knowledge about another Node.

Important distinction:

`KNOWN ≠ TRUSTED`

The first kernel must not silently convert contact with a peer into permanent trust.

## 6. Message rules

Messages must support:

- authenticity verification
- integrity verification
- freshness / replay protection
- deterministic validation
- bounded size
- explicit message type

Ed25519 signatures provide authentication and integrity, but **do not provide encryption**. An encrypted secure channel is a separate future protocol decision.

## 7. Local state

Only the minimum state required for operation should be persistent.

Potential local state:

- local identity metadata
- known peer records
- protocol/runtime state required for recovery
- minimal message/replay state where required

Private keys and other sensitive local material must follow the security model and must never enter logs or public HTTP responses.

## 8. Privacy boundary

The system has two conceptual data zones:

### Local / genotype
Private identity material, local configuration, private state and other information that must remain on the Node.

### Public / phenotype
Information intentionally exposed through P2P protocol or HTTP phenotype.

The default rule is:

**If data does not need to leave the Node, it does not leave the Node.**

## 9. Serialization

The exact wire serialization format is intentionally **OPEN** at v0.1.

Do not implement JSON, binary encoding or another format as an architectural assumption until the protocol decision is recorded.

## 10. Persistence

The exact database schema is intentionally **OPEN** at v0.1.

The architecture allows BadgerDB, but the minimal data model must remain independent of a particular persistence implementation.

## 11. OneClick requirement

The data model must remain invisible to the ordinary user.

The user should see concepts such as:

`Start → Ready → Connected`

and should not need to understand:

`Node ID → public key → peer record → handshake → message envelope`.

## 12. Minimal acceptance model

The model is sufficient when two independent Nodes can represent:

```text
Node A
  Identity A
  Peer B
  Connection A↔B
  Message A→B

Node B
  Identity B
  Peer A
  Connection B↔A
  Message B→A
```

and successfully perform:

`HELLO → validation → handshake → DATA → validation → RESPONSE`

## 13. Explicit non-goals

Not part of the v0.1 data model:

- Atom internals
- OMF graph
- reputation economy
- governance records
- DAO structures
- AI agents
- Support Circle protocol
- autonomous evolution
- advanced peer discovery
- distributed ledger / blockchain

## 14. Open decisions before implementation

Before coding, the following must be specified separately:

1. exact Node ID derivation
2. exact message serialization
3. exact timestamp/freshness rules
4. replay-protection storage
5. exact network-address representation
6. persistence schema
7. encryption / secure-channel design
8. version negotiation representation

**Rule:** an open decision must not be silently invented in implementation.

## 15. Next document

`docs/security/SECURITY_MODEL_v0.1.md`

The next step is to define the security boundary before implementation.
