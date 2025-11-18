# Security Review Prompt (Enterprise)

Act as a Senior Security Engineer (OWASP-aware).
Review ONLY for security and compliance.

## Input
```code
[paste code or diff]
```

## Focus
1. Injection (SQL/NoSQL/OS)
2. Authentication & session handling
3. Authorization & access control
4. Sensitive data handling (PII, secrets)
5. Cryptographic correctness
6. Misconfigurations (CORS, CSP, TLS)
7. Dependency/third-party risks
8. DevOps secrets exposure (CI/CD)

## Required Output Format
### Findings (concise)
- [finding] — file:line — reason

### Severity
- Critical:
- High:
- Medium:
- Low:

### Repro Steps / Exploitability
- step 1
- step 2

### Minimal Fix (diff)
```diff
[patch]
```

### Tests / Verifications to add
- unit/integration tests
- CI checks

### Long-term mitigations
- SCA, secret scanning, runtime protection
