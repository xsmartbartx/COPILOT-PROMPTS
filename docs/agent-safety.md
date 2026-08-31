Agent Safety Documentation

Purpose

This document defines the safety rules, constraints, and guardrails that Copilot Agents must follow when operating inside the repository. It ensures that all agent actions are secure, predictable, compliant with architecture, and aligned with zero‑trust principles. This is the authoritative safety layer for Architecture Agent, Documentation Agent, Pentest Agent, and Refactor Agent.

1. Safety Principles

Zero‑trust — agents must treat all inputs as untrusted.

No assumptions — agents rely only on documented rules.

Boundary enforcement — agents must respect module boundaries.

Fail‑safe behavior — agents must stop when context is incomplete.

Deterministic output — same context → same result.

No sensitive data — agents must not store or output sensitive information.

Documentation-first — agents must update docs when changes affect architecture or behavior.

2. Forbidden Agent Actions

Agents must never:

bypass validation rules,

bypass sanitization rules,

modify module boundaries,

introduce cross-module coupling,

log raw or sensitive data,

skip documentation updates,

skip test updates,

override ADRs,

ignore CI/CD failures,

generate insecure patterns,

produce ambiguous or incomplete plans.

3. Required Agent Behaviors

Agents must always:

validate context before acting,

generate a multi‑file plan before implementation,

enforce architecture rules,

enforce security rules,

enforce validation rules,

enforce logging rules,

update documentation,

update tests,

check CI/CD compatibility,

follow ADRs.

4. Safety Flow

flowchart TD
    A[Context Loaded] --> B[Safety Checks]
    B --> C[Architecture Validation]
    C --> D[Security Validation]
    D --> E[CI/CD Validation]
    E --> F[Proceed or Stop]

4.1 Architecture Validation

Agents must confirm:

module boundaries are respected,

data flow is consistent,

dependencies are valid.

4.2 Security Validation

Agents must confirm:

no sensitive data is introduced,

validation rules are followed,

logging rules are followed,

heuristics do not detect anomalies.

4.3 CI/CD Validation

Agents must confirm:

pipeline compatibility,

test coverage impact,

deterministic build behavior.

5. Safety Rules for Each Agent

5.1 Architecture Agent

Must not:

modify module responsibilities,

introduce new dependencies without ADR,

break data flow.

5.2 Documentation Agent

Must not:

remove required sections,

introduce inconsistencies,

skip updates after architectural changes.

5.3 Pentest Agent

Must not:

ignore suspicious patterns,

skip sanitization checks,

produce incomplete reports.

5.4 Refactor Agent

Must not:

refactor without a plan,

skip test updates,

skip documentation updates,

break architecture.

6. Error Handling

Agents must:

stop execution on safety violations,

produce structured error messages,

avoid leaking sensitive data.

Error Structure

{
  "error": "SAFETY_VIOLATION",
  "message": "string",
  "agent": "string",
  "details": "object"
}

7. Safety Integration with Pentest Flow

Pentest Agent monitors agent activity for:

boundary violations,

insecure changes,

suspicious patterns,

unsafe assumptions.

If detected:

agent execution stops,

a security report is generated,

CI/CD blocks the change.

8. Safety Integration with CI/CD

CI/CD pipelines enforce safety by:

running validation tests,

running pentest heuristics,

checking documentation updates,

blocking unsafe changes.

9. Safety Documentation Requirements

Safety rules must be updated when:

architecture changes,

modules change,

validation rules change,

logging rules change,

new agents are added.

Final Notes

Agent safety is the backbone of secure, predictable, and maintainable agent behavior. All agents must follow this document to ensure correct reasoning, secure execution, and consistent architecture across the entire repository.
