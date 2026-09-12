# SafeStack Autonomous Constitution v0.1 — Constitutional Audit

Status: COMPLETED WITH ACTIVATION BLOCKERS  
Target branch: `draft/autonomous-constitution-v0.1`

## Scope

Audited:
- `AUTONOMOUS_CONSTITUTION.json`
- `CONSTITUTION_SCHEMA.json`
- `STATE_MODEL.md`
- `ROOT_REFERENCE.txt`
- `ROOT_REFERENCE.json`
- `TECHNICAL_CANON_1.1.0_CANDIDATE.json`
- `HASH_REGISTRY.json`
- current `node-os` runtime behavior

## Findings

### F-01 — Machine-readable constitution
Resolved. `AUTONOMOUS_CONSTITUTION.json` exists and is schema-bound.

### F-02 — Exact invariant set
Resolved. The nine constitutional invariants are fixed and omission/substitution is rejected.

### F-03 — State transition determinism
Resolved. Allowed transitions are explicit and `TERMINAL` is absorbing.

### F-04 — Recovery semantics
Resolved. Recovery is predeclared, locally validated, audited, and cannot function as an override.

### F-05 — Recovery after autonomy severance
Severity: CRITICAL

Root Canon v1.0.0 explicitly prohibits `recovery_after_autonomy_severance`.

Correction:
- `RECOVERY` is valid only while autonomy remains intact;
- autonomy severance maps to `TERMINAL`;
- silent identity regeneration after loss of established identity is prohibited.

Result: RESOLVED IN CANDIDATE MODEL.

### F-06 — Root Genesis reference
The canonical root repository contains `GENESIS_HASH.txt` with SHA-256:

`76e14917fd96326f36870c77f1375eb2cda54870955e34957585fb6ffdc199d7`

The value cross-checks against the current `ROOT_CANON.json` byte representation with CRLF line endings.

Correction:
- placeholder removed from `ROOT_REFERENCE.txt`;
- machine-readable `ROOT_REFERENCE.json` added.

Result: RESOLVED.

### F-07 — Destructive self-erasure default
Resolved in candidate constitution. `TERMINAL` is secure refusal, not default destructive erasure, and audit evidence preservation has priority.

### F-08 — Current NodeOS runtime incompatibility
Severity: CRITICAL

Current `node-os/main` contains two behaviors incompatible with the candidate constitution:

1. missing identity triggers automatic `REBIRTH`;
2. a manifest flag may trigger destructive `SelfDestruct` on a critical self-check result.

These conflict with the new fail-closed identity model and the Root Canon prohibition on recovery after autonomy severance.

Result: OPEN — ACTIVATION BLOCKER. A separate compatibility branch is required before activation.

### F-09 — Candidate signature
Severity: CRITICAL

`TECHNICAL_CANON_1.1.0_CANDIDATE.json` is not yet signed by the authorized signing process. The existing v1.0.0 signature must not be reused.

Result: OPEN — ACTIVATION BLOCKER.

## Validation performed

- Root Genesis reference resolution: PASS
- Root Canon hash cross-check: PASS
- JSON Schema Draft 2020-12 structural check: PASS
- Constitution instance/schema consistency: PASS
- Root principle alignment: PASS
- Document-level deterministic replay: PASS
- Node runtime compatibility: FAIL pending runtime branch
- Candidate signature: PENDING

## Activation decision

Current decision: `DEFER`

Remaining blockers:
1. align NodeOS runtime with the candidate constitution;
2. regenerate final SHA-256 registry after runtime/constitution freeze;
3. sign `TECHNICAL_CANON_1.1.0_CANDIDATE.json` using the authorized RSA-4096 process;
4. perform final node-local replay/compatibility validation.

No `FORCE_ACCEPT` path exists.
