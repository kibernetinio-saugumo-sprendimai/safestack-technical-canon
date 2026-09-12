# SafeStack Autonomous State Model v0.1

Status: DRAFT  
Scope: Node-local constitutional runtime behavior  
External authority: NONE

## Core rule

The node does not ask a founder, administrator, GitHub, cloud service, or LLM for permission to preserve its constitutional integrity.

Its constitutional decisions must be deterministic, replayable, auditable, and derived from locally verifiable state.

## States

### INIT
The node has started but has not yet established a trusted runtime state.

Allowed actions:
- load local identity material;
- load constitution and manifest;
- verify required cryptographic material;
- begin validation pipeline.

Forbidden assumption:
- INIT must never be treated as trusted merely because startup succeeded.

Primary transition:
- INIT -> AWARE when all mandatory checks pass.
- INIT -> QUARANTINE when trust cannot be established.

### AWARE
The node has established a constitutionally valid runtime state.

Conditions:
- identity valid;
- manifest valid;
- schema valid;
- required invariants present;
- runtime state consistent;
- no unresolved constitutional violation.

AWARE is the only normal operational state.

### DEGRADED
A non-critical defect exists, but Layer 0 constitutional invariants remain intact.

Examples:
- optional service unavailable;
- non-authoritative integration unavailable;
- performance degradation;
- telemetry or convenience feature unavailable.

Rules:
- availability may degrade;
- integrity must not degrade;
- node must continue validation;
- unresolved degradation may escalate to QUARANTINE if trust becomes uncertain.

### QUARANTINE
The node cannot prove that continued normal operation is safe, or it has detected a trust/integrity anomaly that requires containment.

Default rule:

`UNKNOWN != SAFE`

Expected behavior:
- restrict non-essential external interaction;
- preserve audit evidence;
- re-run deterministic validation;
- reject state-changing requests that require trusted status;
- permit only constitutionally defined validation and recovery functions.

Possible transitions:
- QUARANTINE -> AWARE after successful revalidation;
- QUARANTINE -> LOCKDOWN after confirmed critical violation;
- QUARANTINE -> RECOVERY only through the defined recovery path.

### LOCKDOWN
A critical constitutional invariant has been violated or a trusted runtime state cannot be restored safely.

Examples:
- invalid or unverifiable critical manifest;
- identity integrity failure;
- attempted validation bypass;
- hidden authority or unauthorized override mechanism detected;
- constitutional Layer 0 contradiction.

Expected behavior:
- stop normal operational functions;
- deny FORCE_ACCEPT style behavior;
- preserve the minimum capabilities required for validation, audit, and constitutionally allowed recovery;
- do not silently return to normal operation.

Possible transitions:
- LOCKDOWN -> RECOVERY if recovery is explicitly allowed by constitutional policy;
- LOCKDOWN -> TERMINAL if safe recovery cannot be proven.

### RECOVERY
A narrowly defined state for restoring a last-known constitutionally valid condition.

Recovery is not an override.

Requirements:
- process must be defined before the incident;
- process must not disable Layer 0 validation;
- all recovery inputs must be locally validated;
- all transitions must be audit-recorded;
- no administrator or founder flag may bypass rejection.

Possible transitions:
- RECOVERY -> AWARE after full validation;
- RECOVERY -> QUARANTINE if uncertainty remains;
- RECOVERY -> LOCKDOWN or TERMINAL if recovery fails safely.

### TERMINAL
The node cannot prove a constitutionally safe state and no valid recovery path remains.

TERMINAL means secure refusal to continue normal operation.

This model does not define destructive self-erasure as a constitutional default. Preservation of evidence, determinism, and auditability take priority over destructive reaction.

## Constitutional decision pipeline

```text
INPUT
  |
  v
IDENTITY_CHECK
  |
  v
SIGNATURE_CHECK
  |
  v
SCHEMA_CHECK
  |
  v
INVARIANT_CHECK
  |
  v
RUNTIME_CONSISTENCY_CHECK
  |
  v
RISK_CLASSIFICATION
  |
  v
STATE_TRANSITION
  |
  v
AUDIT_RECORD
```

The same verified state and the same verified input must result in the same constitutional decision.

An LLM may assist development, documentation, or analysis, but it must not be an authority in the constitutional decision path.

## Allowed decision outcomes

- `ACCEPT`
- `REJECT`
- `QUARANTINE`
- `DEFER`

The following outcome is prohibited:

- `FORCE_ACCEPT`

## Signature semantics

A valid signature proves origin/authenticity according to the configured trust model.

It does not grant constitutional permission.

```text
VALID_SIGNATURE + VALID_CONSTITUTION = ELIGIBLE_FOR_ACCEPTANCE
VALID_SIGNATURE + INVALID_CONSTITUTION = REJECT
INVALID_SIGNATURE = REJECT_OR_QUARANTINE
UNKNOWN_VERIFICATION_STATE = QUARANTINE
```

This rule applies to founder-signed changes as well.

## Constitutional amendment flow

```text
PROPOSAL
  |
  v
ORIGIN VERIFICATION
  |
  v
SCHEMA VALIDATION
  |
  v
LAYER 0 INVARIANT CHECK
  |
  v
REPLAY TEST
  |
  v
COMPATIBILITY TEST
  |
  v
LOCAL NODE VALIDATION
  |
  +--> REJECT
  +--> QUARANTINE
  +--> DEFER
  `--> ACCEPT
```

There is no emergency god mode and no founder override path.

## External platform independence

GitHub and other external platforms are collaboration and distribution surfaces only.

A node must remain capable of validating its identity, constitution, manifest, trust chain, and runtime state when those platforms are unreachable.

The disappearance or compromise of GitHub must not automatically redefine canonical truth.

## Priority order

1. Constitutional integrity
2. Identity integrity
3. Trust-chain validity
4. Safe state
5. Auditability
6. Availability
7. Performance
8. Convenience

Availability must never outrank constitutional integrity.

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
