# SafeStack Autonomous State Model v0.1

Status: CANDIDATE  
Scope: Node-local constitutional runtime behavior  
External authority: NONE

## Core rule

The node does not ask a founder, administrator, GitHub, cloud service, or LLM for permission to preserve its constitutional integrity.

Constitutional decisions MUST be deterministic, replayable, auditable, and derived from locally verifiable state.

## Governing rules

- `AUTHORITY != AUTHOR`
- `SIGNATURE != PERMISSION`
- `UNKNOWN != SAFE`
- `AUTONOMY != CHAOS`
- `EVOLUTION != OVERRIDE`
- `INTEGRITY > AVAILABILITY`
- `SYSTEM_INTEGRITY > CREATOR_AUTHORITY`

## State machine

| State | Meaning | Normal operation |
| --- | --- | --- |
| `INIT` | Trust has not yet been established | No |
| `AWARE` | Constitutionally valid runtime state | Yes |
| `DEGRADED` | Non-critical defect; Layer 0 remains intact | Limited |
| `QUARANTINE` | Trust is uncertain or an anomaly requires containment | No |
| `LOCKDOWN` | Critical constitutional violation confirmed | No |
| `RECOVERY` | Predeclared recovery path is executing | No |
| `TERMINAL` | No constitutionally valid recovery path remains | No |

Allowed transitions are normative and are also encoded in `CONSTITUTION_SCHEMA.json`:

```text
INIT       -> AWARE | QUARANTINE
AWARE      -> DEGRADED | QUARANTINE | LOCKDOWN
DEGRADED   -> AWARE | QUARANTINE | LOCKDOWN
QUARANTINE -> AWARE | LOCKDOWN | RECOVERY
LOCKDOWN   -> RECOVERY | TERMINAL
RECOVERY   -> AWARE | QUARANTINE | LOCKDOWN | TERMINAL
TERMINAL   -> <none>
```

Any transition not listed above is invalid.

## INIT

The node has started but has not established a trusted runtime state.

Allowed actions:
- load local identity material;
- load constitution and manifest;
- verify required cryptographic material;
- execute the validation pipeline.

`INIT` MUST NOT be treated as trusted merely because startup succeeded.

## AWARE

`AWARE` is the only normal operational state.

Required conditions:
- identity valid;
- manifest valid;
- schema valid;
- all Layer 0 invariants present;
- runtime state consistent;
- no unresolved constitutional violation.

## DEGRADED

A non-critical defect exists while Layer 0 remains intact.

Examples:
- optional service unavailable;
- non-authoritative integration unavailable;
- performance degradation;
- convenience feature unavailable.

Availability may degrade. Integrity may not.

## QUARANTINE

The node cannot prove that continued normal operation is safe, or it has detected a trust or integrity anomaly that requires containment.

Default rule:

`UNKNOWN != SAFE`

Expected behavior:
- restrict non-essential external interaction;
- preserve audit evidence;
- repeat deterministic validation;
- reject state-changing requests requiring trusted status;
- permit only constitutionally defined validation and recovery functions.

Unknown verification state MUST resolve to `QUARANTINE`, not to optimistic continuation.

## LOCKDOWN

A critical constitutional invariant has been violated or a trusted runtime state cannot be restored safely.

Examples:
- invalid or unverifiable critical manifest;
- identity integrity failure;
- attempted validation bypass;
- hidden authority or unauthorized override mechanism detected;
- Layer 0 contradiction.

Expected behavior:
- stop normal operational functions;
- deny override-equivalent behavior;
- preserve the minimum capabilities required for validation, audit, and predeclared recovery;
- never silently return to normal operation.

## RECOVERY

`RECOVERY` is a narrow, predeclared path for restoring a last-known constitutionally valid condition.

Recovery is not an override.

Requirements:
- recovery logic MUST exist before the incident;
- Layer 0 validation MUST remain enabled;
- all recovery inputs MUST be locally validated;
- every transition MUST be audit-recorded;
- founder or administrator flags MUST NOT bypass rejection.

## TERMINAL

The node cannot prove a constitutionally safe state and no valid recovery path remains.

`TERMINAL` means secure refusal to continue normal operation.

It is absorbing: no state transition out of `TERMINAL` is constitutionally valid.

Destructive self-erasure is NOT a constitutional default. Preservation of audit evidence, determinism, and explainability take priority.

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

The same verified state and the same verified input MUST produce the same constitutional decision.

An LLM may assist development, documentation, or analysis, but MUST NOT be authoritative in the constitutional decision path.

## Decision outcomes

Allowed:
- `ACCEPT`
- `REJECT`
- `QUARANTINE`
- `DEFER`

Prohibited:
- `FORCE_ACCEPT`

`DEFER` is permitted only for non-trusted governance processing where a proposal is incomplete but no trusted runtime decision is being postponed. It MUST NOT be used to treat an unknown runtime trust state as safe.

## Signature semantics

A valid signature proves origin or authenticity according to the configured trust model. It does not grant constitutional permission.

```text
VALID_SIGNATURE + VALID_CONSTITUTION = ELIGIBLE_FOR_ACCEPTANCE
VALID_SIGNATURE + INVALID_CONSTITUTION = REJECT
INVALID_SIGNATURE = REJECT_OR_QUARANTINE
UNKNOWN_VERIFICATION_STATE = QUARANTINE
```

This applies to founder-signed changes as well.

## Amendment flow

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

## Cryptographic agility

The verification requirement is constitutional; a specific algorithm is not.

A cryptographic implementation may evolve only through the constitutional amendment path and only if:
- verification remains mandatory;
- Layer 0 invariants remain satisfied;
- compatibility and replay requirements pass;
- the node validates the change locally.

## External platform independence

GitHub and other external platforms are collaboration and distribution surfaces only.

A node MUST remain capable of validating its identity, constitution, manifest, trust chain, and runtime state when those platforms are unreachable.

The disappearance or compromise of GitHub MUST NOT redefine canonical truth.

## Priority order

1. Constitutional integrity
2. Identity integrity
3. Trust-chain validity
4. Safe state
5. Auditability
6. Availability
7. Performance
8. Convenience

Availability MUST NOT outrank constitutional integrity.
