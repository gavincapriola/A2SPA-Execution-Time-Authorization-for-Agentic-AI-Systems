# A2SPA Specification
## Execution-Time Authorization for Agentic AI Systems

### Status
Draft / Informational

### Abstract
This document specifies **A2SPA (Agent-to-Secure Payload Authorization)**, a protocol-level control plane for enforcing **execution-time authorization** in agentic and autonomous AI systems.

A2SPA defines how intent is cryptographically bound, verified, and enforced **at the moment an action executes**, rather than inferred from prior access checks, identity assertions, or transport security.

---

## 1. Problem Statement

Modern AI systems commonly rely on:
- Transport-layer security (e.g., TLS)
- Identity and access management (RBAC, OAuth, MFA)
- Policy engines and monitoring

These controls authenticate *who may request an action*, but do not guarantee that a **specific action is authorized at execution time**, particularly in:
- asynchronous workflows
- delayed execution
- agent-driven automation
- cross-system action chaining

As systems transition from recommendation to autonomous execution, **execution becomes the primary attack surface**.

---

## 2. Design Goals

A2SPA is designed to:
- Enforce authorization **inline at execution**
- Prevent execution of mutated, replayed, or expired actions
- Bind authorization to the **exact payload**
- Produce a single verifiable execution artifact
- Operate independently of agent frameworks or models

---

## 3. Non-Goals

A2SPA does not:
- Replace TLS, IAM, RBAC, OAuth, or MFA
- Govern model alignment or reasoning
- Provide orchestration logic
- Perform monitoring or detection after execution
- Define UI or prompt security

---

## 4. Terminology

- **Execution Payload**: A structured representation of an action to be executed.
- **Execution Boundary**: The point where an action becomes irreversible.
- **Authorization Artifact**: Cryptographic proof of authorized execution.
- **Freshness**: Guarantees preventing replay or delayed misuse.

---

## 5. Protocol Overview

### 5.1 Payload Construction

Each execution payload MUST include:
- action identifier
- parameters
- permission scope
- execution constraints
- expiration timestamp
- nonce or freshness value

The payload represents the **unit of authorization**.

---

### 5.2 Cryptographic Binding

The payload MUST be cryptographically signed using:
- asymmetric keys, or
- symmetric HMAC (implementation-dependent)

The signature binds:
- who authorized the action
- what action is authorized
- under which constraints
- for how long

Any mutation invalidates authorization.

---

### 5.3 Execution-Time Verification

Verification MUST occur:
- inline on the execution path
- synchronously
- immediately before irreversible action

Verification MUST validate:
- signature authenticity
- payload integrity
- constraint compliance
- freshness (nonce / expiration)

---

### 5.4 Enforcement

If verification fails:
- execution MUST NOT occur
- no partial execution is permitted
- no fallback execution is allowed

---

### 5.5 Authorization Artifact

On successful execution, the system MUST emit a verifiable artifact containing:
- payload hash
- signature
- execution timestamp
- execution result reference

This artifact MUST be immutable and auditable.

---

## 6. Threat Model

A2SPA is designed to mitigate:
- payload mutation attacks
- replay attacks
- delayed execution misuse
- spoofed agent actions
- unauthorized privilege escalation
- assumed trust in autonomous workflows

---

## 7. Deployment Locations

A2SPA SHOULD be enforced at:
- API endpoints performing writes or side effects
- workflow engines at job start / dequeue
- infrastructure automation triggers
- financial or asset execution points
- privilege or capability issuance paths

---

## 8. Security Considerations

- Keys MUST be protected using standard key management practices
- Nonce storage MUST prevent reuse
- Verification latency MUST be bounded
- Failure paths MUST default to non-execution

---

## 9. Summary

A2SPA defines execution-time authorization as a distinct control plane.

- Transport secures data in motion
- Identity secures access
- Monitoring detects misuse
- **A2SPA enforces whether an action is allowed to execute**

As AI systems act autonomously, authorization must be enforced where execution occurs.
