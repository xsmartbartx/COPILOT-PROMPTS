Agent Context Documentation

Purpose

This document defines how Copilot Agents build, manage, and use context when operating inside the repository. Context is the foundation of multi‑file reasoning, architectural understanding, security enforcement, and documentation consistency. All agents rely on this model to perform safe, predictable, and accurate actions.

1. What Agent Context Is

Agent context is the complete set of information an agent gathers before performing any action. It includes:

repository structure,

relevant files,

module boundaries,

validation rules,

logging rules,

security posture,

CI/CD configuration,

ADRs,

data flow diagrams,

previous agent outputs.

Context is dynamic and task‑dependent — each agent builds its own context based on the user request.

2. Context Gathering Flow

flowchart TD
    A[User Request] --> B[Determine Scope]
    B --> C[Collect Relevant Files]
    C --> D[Load Architecture]
    D --> E[Load Security Rules]
    E --> F[Load Validation Rules]
    F --> G[Load Logging Rules]
    G --> H[Load CI/CD]
    H --> I[Build Context]

3. Context Components

3.1 Repository Structure

Agents analyze:

directory layout,

module placement,

documentation structure,

CI/CD files.

3.2 Module Boundaries

Agents load:

responsibilities,

APIs,

dependencies,

validation rules.

3.3 Architecture Model

Agents use:

architecture.md,

system-overview.md,

data-flow.md,

component diagrams.

3.4 Security Model

Agents load:

security.md,

pentest-flow.md,

logging.md,

validation.md.

3.5 CI/CD Model

Agents load:

ci-cd.md,

pipeline definitions,

test requirements.

3.6 ADRs

Agents load:

ADR 0001,

future ADRs.

3.7 Documentation Standards

Agents load:

documentation.prompt.md,

architecture.prompt.md,

refactor.prompt.md.

4. Context Usage

Agents use context to:

understand the impact of changes,

enforce architecture rules,

enforce security rules,

validate module boundaries,

update documentation consistently,

generate multi‑file plans,

avoid unsafe assumptions.

5. Context Rules

No assumptions — agents must rely on documentation.

No cross‑module shortcuts — boundaries must be respected.

No raw input — validation rules apply to context.

No sensitive data — logs and context must be sanitized.

Deterministic reasoning — same context → same output.

Context completeness — agents must gather all relevant files.

6. Agent-Specific Context Behavior

6.1 Architecture Agent

Focuses on:

module boundaries,

data flow,

dependencies,

diagrams.

6.2 Documentation Agent

Focuses on:

Markdown structure,

cross‑file consistency,

documentation standards.

6.3 Pentest Agent

Focuses on:

security rules,

heuristics,

logs,

validation failures.

6.4 Refactor Agent

Focuses on:

multi‑file dependencies,

code structure,

test updates,

documentation updates.

7. Context Validation

Agents validate context before acting:

architecture consistency,

module boundaries,

security posture,

CI/CD compatibility,

documentation completeness.

If context is incomplete or inconsistent, agents must:

stop execution,

request clarification or correction.

8. Context Persistence

Agents may store:

analysis results,

diagrams,

reports,

documentation updates.

Agents must not store:

raw input,

sensitive data,

unvalidated structures.

Final Notes

Agent context is the backbone of safe, predictable, and intelligent agent behavior. All agents must follow this model to ensure correct reasoning, secure execution, and consistent documentation across the entire repository.
