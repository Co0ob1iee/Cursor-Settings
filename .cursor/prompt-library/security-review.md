# Security review (senior) — Cursor snippet

Act as Senior Security Engineer. Context (paste minimal PSD):
- service: auth
- stack: Node.js + Express + Prisma
- constraints: TypeScript strict, no new deps

Focus:
- injection
- auth/session
- ACL
- secrets/PII
- insecure defaults in infra

Output format:
### Findings
- file:line — issue — evidence

### Severity
- Critical / High / Medium / Low

### Minimal Fix (diff)
```diff
[patch]
```

### Tests to add
- unit / integration tests
