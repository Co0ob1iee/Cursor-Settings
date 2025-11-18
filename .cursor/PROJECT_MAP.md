# 🗺️ PROJECT DEPENDENCY MAP

## 🏗️ Architecture Diagram
```
[Frontend] --> [API Gateway] --> [Services] --> [Database]
     |              |                |              |
     v              v                v              v
  [State Mgmt]  [Auth Layer]   [Business Logic]  [ORM]
```

## 📦 Module Dependencies

### Frontend ([Your Frontend Path])

#### Components
```
[Example structure - customize for your project]
- App.[ext]
  - USES: `[Router Library]` from '[package]'
  - USES: `[AuthProvider]` from '/contexts/[AuthContext]'
  - USES: `[ThemeProvider]` from '/contexts/[ThemeContext]'
  - CHILDREN: All page components

- [PageComponent].[ext]
  - USES: `[CustomHook]` from '/hooks/[hookName]'
  - USES: `[ApiClient].[method]()` from '/api/[client]'
  - USES: `[UI Components]` from '/components/ui'
  - EMITS: [eventName]
  - REDIRECTS: to [route] on success
```

#### Hooks/Utilities
```
[Example structure - customize for your project]
- [hookName].[ext]
  - USES: `[Context]` from '/contexts/[ContextName]'
  - USES: `[ApiClient]` from '/api/[client]'
  - PROVIDES: [returned values/functions]
  - STORAGE: [storage mechanism] for [data]
```

#### API Client
```
[Example structure - customize for your project]
- /api/[client].[ext]
  - USES: `[HTTP Library]` for HTTP requests
  - USES: `[AuthToken]` from [storage]
  - IMPLEMENTS: [interceptors/middleware] for [purpose]
  - EXPORTS: [exported instance/methods]
```

### Backend ([Your Backend Path])

#### API Routes
```
[Example structure - customize for your project]
- /api/[resource]/[action] ([METHOD])
  - HANDLER: [Controller].[method]
  - VALIDATES: [validation rules]
  - CALLS: [Service].[method]()
  - RETURNS: [return type]
  - ERRORS: [error codes and types]

- /api/[resource] ([METHOD])
  - MIDDLEWARE: [middleware name]
  - HANDLER: [Controller].[method]
  - CALLS: [Service].[method]()
  - RETURNS: [return type]
  - CACHE: [caching strategy] (if applicable)
```

#### Services
```
[Example structure - customize for your project]
- [ServiceName]
  - METHODS:
    - [methodName]([params]): [ReturnType]
      - CALLS: [OtherService].[method]()
      - CALLS: [Library].[function]()
      - CALLS: [Service].[method]()
    - [methodName]([params]): [ReturnType]
      - CALLS: [Library].[function]()
      - CALLS: [Service].[method]()

- [ServiceName]  
  - DEPENDENCIES: [dependency] ([purpose])
  - METHODS:
    - [methodName]([params]?): [ReturnType]
    - [methodName]([params]): [ReturnType]
    - [methodName]([params]): [ReturnType]
    - [methodName]([params], [params]): [ReturnType]
```

#### Middleware
```
[Example structure - customize for your project]
- [middlewareName]
  - USES: `[Service].[method]()`
  - SETS: [request property]
  - ERRORS: [error conditions]

- [middlewareName]
  - CATCHES: [error types]
  - LOGS: to [logging destination]
  - RETURNS: [formatted response]
```

### Database Schema
```
[Example structure - customize for your project]
- [EntityName]
  - id: [ID Type] (PRIMARY KEY)
  - [fieldName]: [Type] ([CONSTRAINTS])
  - [fieldName]: [Type] ([CONSTRAINTS])
  - createdAt: [DateTime Type]
  - updatedAt: [DateTime Type]
  - RELATIONS:
    - [relationType]: [RelatedEntity]

- [EntityName]  
  - id: [ID Type] (PRIMARY KEY)
  - [foreignKeyField]: [ID Type] (FOREIGN KEY)
  - [fieldName]: [Type]
  - [fieldName]: [Type]
  - RELATIONS:
    - [relationType]: [RelatedEntity]
    - [relationType]: [RelatedEntity]
```

### Shared Types ([Your Shared Types Path])
```
[Example structure - customize for your project]
- [TypeName].[ext]
  - Interface/Type used by both frontend and backend
  - Validation schemas ([validation library])

- [TypeName].[ext]  
  - Standard response format
  - Error response format
```

## 🔄 Data Flow Examples

### [Example Flow Name]
```
[Example flow - customize for your project]
1. [Component/Module] [action]
2. Calls [API Client].[method]([params])
3. API [METHOD] /[endpoint]
4. [Controller] validates [input]
5. [Service].[method]() [action description]
6. [Service/Library] [action description]
7. Response sent to frontend
8. [Data] stored in [storage]
9. [Context/State] updated with [data]
10. Redirect to [route] / [action]
```

### [Example Flow Name] (Authenticated)
```
[Example flow - customize for your project]
1. [Component] calls [hook/function]
2. [Hook/Function] uses [API Client] with [auth mechanism]
3. [Middleware] validates [token/credentials]
4. [Service] fetches from [data source]
5. Data potentially cached in [cache solution]
6. Response formatted and sent
7. Frontend updates [state/context]
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
