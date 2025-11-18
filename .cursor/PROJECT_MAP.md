# 🗺️ PROJECT DEPENDENCY MAP

## 🏗️ Architecture Diagram
```
[Frontend] --> [API Gateway] --> [Services] --> [Database]
     |              |                |              |
     v              v                v              v
  [State Mgmt]  [Auth Layer]   [Business Logic]  [ORM]
```

## 📦 Module Dependencies

### Frontend (/src/frontend)

#### Components
```
- App.tsx
  - USES: `Router` from 'react-router-dom'
  - USES: `AuthProvider` from '/contexts/AuthContext'
  - USES: `ThemeProvider` from '/contexts/ThemeContext'
  - CHILDREN: All page components

- LoginPage.tsx
  - USES: `useAuth` from '/hooks/useAuth'
  - USES: `apiClient.login()` from '/api/client'
  - USES: `Button, Input` from '/components/ui'
  - EMITS: onLoginSuccess
  - REDIRECTS: to /dashboard on success
```

#### Hooks
```
- useAuth.ts
  - USES: `AuthContext` from '/contexts/AuthContext'
  - USES: `apiClient` from '/api/client'
  - PROVIDES: user, login(), logout(), isAuthenticated
  - STORAGE: localStorage for token
```

#### API Client
```
- /api/client.ts
  - USES: `axios` for HTTP requests
  - USES: `authToken` from localStorage
  - IMPLEMENTS: interceptors for auth
  - EXPORTS: apiClient instance with methods
```

### Backend (/src/backend)

#### API Routes
```
- /api/auth/login (POST)
  - HANDLER: AuthController.login
  - VALIDATES: email, password
  - CALLS: AuthService.authenticate()
  - RETURNS: { token, user }
  - ERRORS: 401 Unauthorized, 400 Bad Request

- /api/users (GET)
  - MIDDLEWARE: authMiddleware
  - HANDLER: UserController.list
  - CALLS: UserService.findAll()
  - RETURNS: User[]
  - CACHE: Redis key 'users:all' (5 min)
```

#### Services
```
- AuthService
  - METHODS:
    - authenticate(email, password): Promise<AuthResult>
      - CALLS: UserService.findByEmail()
      - CALLS: bcrypt.compare()
      - CALLS: TokenService.generate()
    - validateToken(token): Promise<User>
      - CALLS: jwt.verify()
      - CALLS: UserService.findById()

- UserService  
  - DEPENDENCIES: prisma (database)
  - METHODS:
    - findAll(filters?): Promise<User[]>
    - findById(id): Promise<User>
    - create(data): Promise<User>
    - update(id, data): Promise<User>
```

#### Middleware
```
- authMiddleware
  - USES: `AuthService.validateToken()`
  - SETS: req.user
  - ERRORS: 401 if invalid token

- errorHandler
  - CATCHES: all errors
  - LOGS: to monitoring service
  - RETURNS: formatted error response
```

### Database Schema
```
- User
  - id: UUID (PRIMARY KEY)
  - email: STRING (UNIQUE)
  - password: STRING (HASHED)
  - createdAt: DATETIME
  - updatedAt: DATETIME
  - RELATIONS:
    - hasMany: Posts
    - hasMany: Comments

- Post  
  - id: UUID (PRIMARY KEY)
  - userId: UUID (FOREIGN KEY)
  - title: STRING
  - content: TEXT
  - RELATIONS:
    - belongsTo: User
    - hasMany: Comments
```

### Shared Types (/src/shared/types)
```
- User.ts
  - Interface used by both frontend and backend
  - Validation schemas (zod)

- ApiResponse.ts  
  - Standard response format
  - Error response format
```

## 🔄 Data Flow Examples

### Login Flow
```
1. LoginPage.tsx captures credentials
2. Calls apiClient.login(email, password)
3. API POST /auth/login
4. AuthController validates input
5. AuthService.authenticate() checks credentials
6. TokenService generates JWT
7. Response sent to frontend
8. Token stored in localStorage
9. AuthContext updated with user
10. Redirect to dashboard
```

### Data Fetch Flow (Authenticated)
```
1. Component calls custom hook
2. Hook uses apiClient with auth token
3. authMiddleware validates token
4. Service fetches from database
5. Data potentially cached in Redis
6. Response formatted and sent
7. Frontend updates state
```

## 🚨 Critical Dependencies

### Must Not Break
- Authentication flow (breaking change affects all users)
- Database schema migrations (require careful planning)
- API response formats (mobile apps depend on these)
- Token structure (invalidates all sessions if changed)

### Can Carefully Modify  
- Internal service methods (if interfaces preserved)
- UI components (with feature flags)
- Caching strategies
- Logging formats

## 📝 Notes
- Update this document whenever adding new dependencies
- Mark deprecated items with ⚠️ DEPRECATED
- Add migration notes for breaking changes
