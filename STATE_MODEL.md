# SafeStack Autonomous State Model v0.1

Status: CANDIDATE  
Scope: Node-local constitutional runtime behavior  
Root Canon: 1.0.0  
External authority: NONE

## Core rule

The node does not ask a founder, administrator, GitHub, cloud service, or LLM for permission to preserve constitutional integrity. Decisions must be deterministic, replayable, auditable, and derived from locally verifiable state.

## Root alignment

This model is subordinate to SafeStack Root Canon v1.0.0. In particular: no centralized authority, no forced execution, node refusal is valid, no creator override exists, and recovery after autonomy severance is prohibited.

`RECOVERY` is valid only while node autonomy and the constitutional trust boundary remain intact. If autonomy has been severed, the only permitted destination is `TERMINAL`.

## States

### INIT
Startup state before trust has been established.

Rules:
- startup success is not proof of trust;
- missing established identity must not trigger silent identity regeneration;
- required identity, constitution, manifest, signatures and integrity anchors are validated before normal operation.

Transitions: `AWARE` on full validation, otherwise `QUARANTINE`.

### AWARE
Only normal operational state. Identity, manifest, schema, invariants and runtime consistency are valid.

### DEGRADED
A non-critical defect exists while Layer 0 remains intact. Integrity must not degrade. Trust uncertainty escalates to `QUARANTINE`.

### QUARANTINE
Trust cannot be proven or an anomaly requires containment.

`UNKNOWN != SAFE`

Behavior:
- restrict non-essential external interaction;
- preserve audit evidence;
- re-run deterministic validation;
- reject trusted state-changing requests;
- permit only constitutionally defined validation/recovery functions.

Transitions:
- `AWARE` after successful revalidation;
- `LOCKDOWN` after confirmed critical violation;
- `RECOVERY` only when autonomy remains intact and the recovery path was predeclared.

### LOCKDOWN
A critical invariant is violated or trusted state cannot safely be restored.

Behavior:
- stop normal operations;
- deny `FORCE_ACCEPT`;
- preserve evidence;
- retain only validation, audit, and allowed recovery capability;
- never silently resume operation.

Transitions:
- `RECOVERY` only if autonomy remains intact and the path existed before the incident;
- `TERMINAL` if autonomy has been severed or recovery cannot be proven safe.

### RECOVERY
Narrow restoration of a last-known valid condition without crossing the autonomy boundary. Recovery is not an override.

Requirements:
- predeclared process;
- Layer 0 validation remains enabled;
- all inputs are locally validated;
- audit trail is preserved;
- no founder/admin bypass;
- node autonomy remains intact.

Prohibited:
- recovery after autonomy severance;
- silent identity regeneration after loss of an established identity;
- re-establishing authority by external command.

### TERMINAL
Secure refusal to continue normal operation when a safe constitutional state cannot be proven.

Properties:
- absorbing state;
- no transition back to operational states;
- no automatic identity replacement;
- no destructive self-erasure as a constitutional default;
- audit evidence is preserved.

## Decision pipeline

```text
INPUT
  -> IDENTITY_CHECK
  -> SIGNATURE_CHECK
  -> SCHEMA_CHECK
  -> INVARIANT_CHECK
  -> RUNTIME_CONSISTENCY_CHECK
  -> RISK_CLASSIFICATION
  -> STATE_TRANSITION
  -> AUDIT_RECORD
```

Same verified state + same verified input = same constitutional decision.

Allowed outcomes: `ACCEPT`, `REJECT`, `QUARANTINE`, `DEFER`.

`DEFER` is governance-only and must not be used to continue runtime operation when trust is unknown. `FORCE_ACCEPT` is prohibited.

## Signature semantics

```text
VALID_SIGNATURE + VALID_CONSTITUTION = ELIGIBLE_FOR_ACCEPTANCE
VALID_SIGNATURE + INVALID_CONSTITUTION = REJECT
INVALID_SIGNATURE = REJECT_OR_QUARANTINE
UNKNOWN_VERIFICATION_STATE = QUARANTINE
```

A valid signature proves origin; it does not grant constitutional permission.

## Priority order

1. Constitutional integrity
2. Identity integrity
3. Trust-chain validity
4. Safe state
5. Auditability
6. Availability
7. Performance
8. Convenience

## Governing formulas

```text
AUTHORITY != AUTHOR
SIGNATURE != PERMISSION
UNKNOWN != SAFE
AUTONOMY != CHAOS
EVOLUTION != OVERRIDE
INTEGRITY > AVAILABILITY
SYSTEM_INTEGRITY > CREATOR_AUTHORITY
```
