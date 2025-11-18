# 📝 CHANGELOG TEMPLATE

## Format dla każdej zmiany wprowadzonej przez AI

```markdown
## [Data] - [Funkcjonalność]

### 🤖 AI Assistant: [Claude/GPT-4]
### 👤 Developer: [Twoje imię]

### Prompt użyty:
```
[Wklej dokładny prompt]
```

### Wygenerowany kod:
- `path/to/file1.ts` - [co dodano/zmieniono]
- `path/to/file2.ts` - [co dodano/zmieniono]

### Manualne zmiany:
- [Lista zmian które sam wprowadzałeś]

### Testy:
- ✅ Unit testy przechodzą
- ✅ Integracyjne testy przechodzą  
- ✅ Manualne testy OK

### Impact:
- Nowe zależności: [lista]
- Breaking changes: [tak/nie]
- Migracje wymagane: [tak/nie]

### Notes:
[Dodatkowe uwagi, problemy, TODO]

---
```

## Przykład wypełniony:

```markdown
## 2024-01-20 - System autentykacji

### 🤖 AI Assistant: Claude 3
### 👤 Developer: Clobers

### Prompt użyty:
```
Here's my current PSD:
- Backend: Express + PostgreSQL + TypeScript
- Empty project

Task: Add JWT authentication
Requirements: Register, login, middleware
```

### Wygenerowany kod:
- `/src/services/AuthService.ts` - Kompletny serwis auth
- `/src/middleware/auth.ts` - JWT validation middleware
- `/src/routes/auth.ts` - Endpoints register/login
- `/src/types/auth.ts` - TypeScript interfaces

### Manualne zmiany:
- Zmieniono JWT secret na env variable
- Dodano rate limiting do login endpoint
- Poprawiono error message w register

### Testy:
- ✅ Unit testy przechodzą (15/15)
- ✅ Integracyjne testy przechodzą (5/5)
- ✅ Manualne testy OK

### Impact:
- Nowe zależności: jsonwebtoken, bcrypt
- Breaking changes: NIE
- Migracje wymagane: TAK - add users table

### Notes:
- TODO: Dodać refresh token
- TODO: Email verification
- Rate limiting tylko basic, do poprawy

---
```

## Dlaczego to ważne?

1. **Debugging** - Wiesz co AI generowało
2. **Team** - Inni widzą co się działo
3. **Rollback** - Łatwo cofnąć zmiany
4. **Learning** - Uczysz się które prompty działają
5. **Audit** - Dokumentacja dla compliance

## Git Commit Message

Po zmianach AI używaj formatu:
```
feat(auth): add JWT authentication [AI-assisted]

- Added AuthService with login/register
- Added auth middleware  
- Added auth routes

AI: Claude 3
Prompt: See CHANGELOG.md
Manual changes: env variables, rate limiting
```

## Integracja z PR

W Pull Request dodaj sekcję:
```markdown
## AI Assistance Disclosure

This PR contains AI-generated code:
- AI Model: Claude 3
- Files affected: 4
- Manual review: ✅ Completed
- Security review: ✅ Passed
- Tests added: ✅ 20 tests

See `CHANGELOG.md` for detailed prompts and modifications.
```
