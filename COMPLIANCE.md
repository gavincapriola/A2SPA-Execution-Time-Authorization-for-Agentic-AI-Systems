# A2SPA Compliance Mapping
## Execution-Time Authorization in Regulated Environments

### Overview
This document maps A2SPA execution-time authorization concepts
to common security and compliance frameworks.

### SOC 2
CC6 (Logical Access): Execution payload authorization enforces least privilege at execution.
CC7 (Change Management): Signed payloads prevent unauthorized action changes.
CC8 (Monitoring): Execution artifacts provide audit evidence.

### NIST (Zero Trust Principles)
Explicit Verification: Payloads are verified at execution.
Least Privilege: Constraints enforced cryptographically.
Assume Breach: No trust is assumed beyond verification.

### ISO 27001
A.9 Access Control: Authorization bound to execution payloads.
A.12 Operations Security: Controls enforced at execution boundaries.
A.16 Incident Management: Immutable artifacts support forensics.

### Financial & Infrastructure Controls
Non-repudiation of execution
Replay protection
Deterministic authorization enforcement

### Note
A2SPA complements compliance controls but does not replace
organizational governance, risk, or audit processes.