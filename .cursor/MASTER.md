# MASTER PROJECT CONTROL DOCUMENT (Enterprise Edition)

## Purpose

This MASTER document combines the Project State Document (PSD) with enterprise-grade workflow, governance, CI/CD, and observability rules.
Use it as the single source of truth for large teams and long-running projects.

## Project State Document (PSD) — Template

### Version: 1.0.0

### Last Updated: [update manually]

### Architecture Overview

- Frontend: React + TypeScript + Tailwind
- Backend: Node.js + Express + PostgreSQL
- ORM: Prisma
- Auth: JWT + refresh tokens
- State Management: Redux Toolkit
- Infrastructure: Docker, Kubernetes (optional), Terraform for IaC

### Compliance & Governance

- Code reviews: required for all PRs
- Security scans: Snyk/Dependabot enabled
- CI gates: lint → test → build → security scan
- Release policy: semantic versioning, release branch protection

### Completed Features

- [ ] Fill in

### In Progress

- [ ] Fill in

### Known Issues

- [ ] Fill in

### Checkpoints / Tags

Use `git tag checkpoint-vX.Y` for stable milestones.

### Code Structure (suggested)

```
/src
  /apps
    /web (frontend)
    /api (backend)
  /libs
    /shared
    /utils
  /infra
    /terraform
    /k8s
```

### Key Decisions

- Document why each major tech was chosen and compatibility constraints.

---

## Enterprise Workflow Rules

1. **PSD First**: Every new prompt or task must start with:

   ```
   Here's my current PSD: [paste only the relevant PSD section]
   ```

   Limit PSD paste to the minimal relevant parts (service, interfaces, or configs).

2. **Role-Based Prompts**: Always specify role (Security, Performance, Architect, QA).

3. **Checkpoint & Rollback**:

   ```
   CHECKPOINT v1.2:
   - summary...
   - commit: abc123
   ```

   To rollback: "Let's rollback to CHECKPOINT v1.2 and try alternate approach."

4. **Pre-flight Checklist** (enforced in CI):

   - TypeScript strict mode
   - Linting (ESLint)
   - Format (Prettier)
   - Unit & Integration tests
   - Security scans
   - Dependency updates policy

5. **Release & Branching**:

   - protected main branch
   - feature branches `feature/...`
   - release branches `release/...`
   - PR template required

6. **Observability**:

   - Structured logging (correlation IDs)
   - Tracing for hot paths
   - Error budgets and SLOs defined

7. **LLM Interaction Rules**:

   - Always include a PSD snippet.
   - Start prompts with "Here's my current PSD: [paste]"
   - Responses must include: ✶ What works now ✶ Risks ✶ Incremental plan ✶ Compatibility notes
   - Refuse changes that violate PSD without explicit acceptance from architects.

---

## Output Standard

Responses should follow:

### ✓ What works now

### ⚠ Potential issues

### ➤ Recommended approach (step-by-step)

### ⬇ Implementation (only when requested)

### ✔ Compatibility notes

---

## Enterprise Addenda

- Data retention policy summary
- Security contact & incident response procedure
- On-call rotation and escalation

