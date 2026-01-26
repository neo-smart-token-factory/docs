Perfeito. Aqui vai a **versão final pronta para GitHub**, sem emojis, com Markdown “limpo” (audit-grade) e incluindo um **gráfico ASCII** (arquitetura + fluxos). Sugestão de nome do arquivo:

* `docs/PROTOCOL_EVOLUTION_AND_SECURITY_2026.md`

---

# NΞØ SMART FACTORY — Protocol Evolution & Security Architecture (2026)

> **Status:** Draft (Audit-Ready)
> **Version:** v0.5.3 — THE NEURAL SMART CORE
> **Audience:** Protocol Engineers, Security Reviewers, Partners
> **Scope:** TON (Tact) contract layer + cross-chain security posture
> **Out of scope:** UI/UX, Telegram distribution, marketing APIs, token pricing/trading logic

---

## Executive Summary

The NΞØ Protocol has evolved from a UI-centric experiment into modular **Protocol Infrastructure** on the TON Blockchain. This evolution is powered by **Tact**, enabling strong typing, predictable message schemas, and safer serialization patterns.

The result is a protocol layer designed for scalability, auditability, and defense-in-depth security, while remaining compatible with machine-driven automation flows (Agents, MCP) and advanced signing strategies (Multi-Sig, MPC).

---

## Architectural Shift: From UI-Centric to Protocol-First

NΞØ transitioned from monolithic scripts and UI-driven deployment logic into a structured, modular on-chain architecture.

### Outcomes

* **Modularization:** responsibilities are decoupled into dedicated modules (constants, messages, minter, wallet, factory).
* **Predictability:** strong typing + controlled serialization reduces TON-specific failure cases (e.g., cell size/serialization edge cases).
* **Auditability:** contracts become human-readable and structured for continuous review.
* **Protocol-first posture:** UI becomes an interface; contracts become the source of truth.

---

## TON Contract Architecture (Tact)

The TON protocol layer is implemented as a modular structure:

```text
contracts/ton/tact/
├── constants.tact        # protocol fee + treasury configuration
├── messages.tact         # canonical message schema (TEP-74 compatible)
├── JettonMinter.tact     # mint logic + bridge hooks + withdraw split
├── JettonWallet.tact     # optimized user wallet implementation
└── JettonFactory.tact    # Factory V2: deploy tokens w/ parameterized supply + pricing
```

### Design intent

* `constants.tact` centralizes protocol parameters to prevent configuration drift.
* `messages.tact` defines the compatibility layer for tooling and versioning.
* `JettonFactory.tact` is treated as critical infrastructure and contains operational guardrails.
* `JettonMinter.tact` expresses token issuance logic deterministically.

---

## Cross-Chain Security Parity (TON + EVM)

NΞØ maintains architectural symmetry across chains:

* TON contracts represent the protocol core (Factory, Minters, Wallets).
* EVM contracts (e.g. `NeoTokenV2.sol`, `NeoSmartFactory.sol`, `NeoERC721.sol`) adopt equivalent security controls and operational handles.

This approach ensures:

* consistent governance direction
* shared security expectations across chains
* common mental model for auditors and integrators

---

## ASCII Architecture Graph (System Overview)

```text
                   NΞØ SMART FACTORY (Protocol-First)

    +--------------------------------------------------------------+
    |                          UI LAYER                            |
    |   Telegram Mini App / Web UI / CLI / Agents (MCP clients)    |
    +-------------------------------+------------------------------+
                                    |
                                    | (signed messages / requests)
                                    v
    +--------------------------------------------------------------+
    |                        INTEGRATION LAYER                     |
    |   - Auth: Telegram initData                                  |
    |   - Wallet SDKs: TON / Base                                  |
    |   - Observability: logs, alerts, anomaly triggers            |
    |   - Optional relays/oracles (untrusted by default)           |
    +-------------------------------+------------------------------+
                                    |
                                    | (contract messages, on-chain ops)
                                    v
    +--------------------------------------------------------------+
    |                       TON PROTOCOL LAYER                     |
    |                                                              |
    |  +-----------------+     +-------------------+               |
    |  | JettonFactory   | --> | JettonMinter      |               |
    |  | (deploy + rules)|     | (mint/bridge/etc) |               |
    |  +-----------------+     +-------------------+               |
    |            |                         |                       |
    |            v                         v                       |
    |      +-----------+            +---------------+              |
    |      | messages  |            | JettonWallet  |              |
    |      | (TEP-74)  |            | (users)       |              |
    |      +-----------+            +---------------+              |
    |            |                         |                       |
    |            v                         v                       |
    |      +-------------------------------+                       |
    |      | constants (fee + treasury)                            |
    |      +-------------------------------+                       |
    +--------------------------------------------------------------+

     Security controls:
       - circuit breaker (pause/unpause)
       - bounds checking
       - rate limiting
       - access control
       - replay protection (bridge paths)
```

---

## Security Posture: Defense-in-Depth (The DAO & Beyond)

NΞØ implements a multifaceted security approach: prevention, containment, recovery.

### Principles

* do not trust UI clients (including Telegram Mini Apps)
* assume adversarial inputs (payload size, spamming, forged sequences)
* enforce invariants on-chain
* enable emergency containment

---

## 1) Circuit Breakers (Pausability / Kill-Switch)

Critical contracts introduce a circuit breaker mechanism designed to reduce blast radius during incidents.

### Design goals

* **Guardian role:** dedicated address to pause operations instantly.

  * recommended: Multi-Sig or MPC-managed authority
* **Scope:** pause affects

  * new deployments
  * bridge-sensitive operations
  * high-risk state mutations
* **Non-impact:** pause does not block

  * read-only methods (getters)
  * transparency / monitoring
  * post-incident forensics

### Rationale

If a vulnerability emerges in the factory/bridge layer or off-chain relays, circuit breakers allow rapid containment.

---

## 2) Guardrails & Bounds Checking

Factory-based deployment is a high-value attack surface. Parameterized token creation increases adversarial leverage.

### Mandatory constraints

* **Supply bounds:** enforce max/min ranges to prevent overflow patterns and unrealistic payloads
* **Decimals bounds:** enforce rational range aligned with standard
* **Metadata bounds:** cap metadata size to TON-safe limits
* **Rate limiting:** prevent spam deployments and resource exhaustion

### Rationale

Bounded behavior is the foundation of resistance against denial-of-service patterns, griefing, and payload abuse.

---

## 3) Governance & Treasury Evolution

Protocols cannot scale while retaining single points of suspicion.

### Current stage

MVP parameters may be constants for speed and deterministic behavior.

### Evolution direction

* migrate treasury/fee configuration from constants to governed state variables
* role-based access control:

  * `admin` for configuration changes
  * `guardian` for emergency pause
* introduce time-locked changes
* adopt Multi-Sig or MPC-based treasury authority

---

## Threat Model & Assumptions

### Primary threats

1. spam deployments / factory griefing
2. oversized metadata / serialization abuse
3. bridge spoof / unauthorized mint
4. treasury compromise
5. off-chain relay compromise / replay attacks

### Assumptions

* signing occurs only in external wallet SDKs (no private keys in protocol UI)
* Telegram Mini Apps are untrusted clients (anyone can emulate requests)
* off-chain systems must be treated as untrusted by default
* privileged integrations require server-side validation and monitoring

---

## Protocol Invariants (Audit Checklist)

The protocol is designed to maintain invariants across contract upgrades and integrations.

### Supply + Mint

* `total_supply` increases only through explicitly authorized mint paths
* bridge-driven issuance must include:

  * caller validation
  * replay protection (nonce/seqno)
  * bounded mint amounts

### Fees + Treasury

* protocol fee is bounded:

  * `0 <= fee_bps <= MAX_FEE_BPS`
* treasury cannot be set to invalid/unreachable addresses
* withdrawal split rules are deterministic and traceable

### Pause behavior

* when paused:

  * factory deploy operations must fail deterministically
  * bridge-sensitive paths must fail deterministically
  * getters remain functional

### Access control

* privileged methods must verify role:

  * `admin`, `guardian`
* role changes must be explicit and traceable

---

## Future-Ready: Agents, MCP, MPC, AA

### MCP (Model Context Protocol)

Tact deterministic message schemas and predictable getters enable safe automation and reproducible contract calls by AI agents.

### MPC (Multi-Party Computation)

MPC impacts only signing. Protocol execution remains compatible regardless of signer strategy.

### Account Abstraction (TON-native)

TON contract-as-account model enables native sponsored flows and plugin-like execution patterns.

---

## Implementation Status Disclaimer

This document describes architecture intent and security model.

Implementation completeness is verified by repository artifacts:

* contract code
* tests
* deployment scripts
* review / audit notes (when available)

---

**v0.5.3 — THE NEURAL CORE // NΞØ PROTOCOL**
Resilience is not the absence of failure, but the presence of structure.
