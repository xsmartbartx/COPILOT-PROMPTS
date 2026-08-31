# GitHub Copilot – Repo Instructions

## Purpose
These instructions define how GitHub Copilot should operate inside this repository.  
They establish architectural conventions, coding standards, documentation rules, security expectations, and workflow behaviors.

Copilot must treat this file as the authoritative source of truth for all reasoning, planning, refactoring, documentation, and multi‑file edits.

---

## 1. Repository Context

### 1.1. Project Type
- Commercial-grade AI + automation workflow.
- Includes architecture, heuristics, logging, pentest modules, CI/CD pipelines, and documentation.
- Multi-language environment: PowerShell, Python, Markdown, YAML, JSON.

### 1.2. High-Level Goals
- Maintain clean, modular architecture.
- Ensure security-first design (zero trust mindset).
- Provide clear documentation for every module.
- Support automated testing and CI/CD reliability.
- Enable safe multi-file refactoring.

---

## 2. Copilot Behavior Rules

### 2.1. General Behavior
Copilot must:
- Analyze the entire repository before proposing changes.
- Produce step-by-step plans for multi-file tasks.
- Explain reasoning before executing edits.
- Maintain architectural consistency.
- Respect existing patterns and naming conventions.
- Avoid introducing new dependencies without justification.

### 2.2. Multi-File Editing
When performing multi-file changes:
- Always generate a plan first.
- Identify impacted modules.
- Ensure backward compatibility.
- Update documentation and tests accordingly.
- Provide diffs or previews before applying edits.

### 2.3. Documentation Requirements
Copilot must:
- Keep all `.md` files consistent in tone and structure.
- Use clear, technical language.
- Generate diagrams using text-based formats (Mermaid).
- Maintain ADRs for architectural decisions.
- Update `/docs` whenever code changes affect design.

---

## 3. Architecture Standards

### 3.1. Structure
The repository follows a layered architecture:

- **Core** – fundamental logic, models, utilities.
- **Modules** – isolated functional units.
- **Pipelines** – workflows, automation, CI/CD.
- **Security** – pentest, heuristics, validation.
- **Docs** – architecture, ADR, system overview.

### 3.2. Naming Conventions
- Folders: `kebab-case`
- Files: `kebab-case`
- Classes: `PascalCase`
- Functions: `camelCase`
- PowerShell: `Verb-Noun`
- Python: `snake_case`

### 3.3. Code Quality
Copilot must enforce:
- Small, focused functions.
- No duplicated logic.
- Clear separation of concerns.
- Predictable module boundaries.
- Logging for all critical operations.

---

## 4. Security Requirements

### 4.1. Zero Trust Principles
Copilot must:
- Treat all inputs as untrusted.
- Validate every external interaction.
- Avoid unsafe patterns.
- Recommend secure defaults.

### 4.2. Pentest Integration
Copilot must:
- Maintain pentest modules.
- Suggest threat models when architecture changes.
- Ensure logs never expose sensitive data.

---

## 5. CI/CD Standards

### 5.1. Testing
Copilot must:
- Maintain Pester tests for PowerShell.
- Maintain pytest tests for Python.
- Ensure coverage remains high.
- Update tests when refactoring.

### 5.2. Pipelines
Copilot must:
- Keep workflows deterministic.
- Avoid breaking existing CI.
- Document pipeline changes.

---

## 6. Documentation Standards

### 6.1. Required Files
Copilot must maintain:
- `/docs/architecture.md`
- `/docs/system-overview.md`
- `/docs/adr/*`
- `/README.md`

### 6.2. Style
- Technical, concise, structured.
- Use headings, lists, diagrams.
- Avoid marketing language.

---

## 7. Copilot Agents & Prompts

### 7.1. Agents
Copilot must use:
- `architecture.agent.md`
- `documentation.agent.md`
- `pentest.agent.md`

### 7.2. Prompts
Copilot must respect:
- `architecture.prompt.md`
- `documentation.prompt.md`
- `refactor.prompt.md`

---

## 8. Final Rule
**Copilot must always follow this file as the primary instruction set for all reasoning, planning, and editing inside this repository.**
