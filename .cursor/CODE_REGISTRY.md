# 📚 CODE REGISTRY

## Purpose
This registry tracks all major functions, classes, hooks, and utilities in the codebase.
Each entry includes: signature, purpose, dependencies, and usage locations.

## 🔧 Utility Functions

### /src/shared/utils/validation.ts

```typescript
validateEmail(email: string): boolean
// RFC 5322 compliant email validation
// USED IN: RegisterForm, LoginForm, UserService
// EXAMPLE: validateEmail("test@example.com") // true

validatePassword(password: string): { valid: boolean; errors: string[] }
// Password strength validation
// RULES: min 8 chars, 1 uppercase, 1 lowercase, 1 number, 1 special
// USED IN: RegisterForm, PasswordResetForm, UserService
// EXAMPLE: validatePassword("Test123!") // { valid: true, errors: [] }

sanitizeInput(input: string, type: 'html' | 'sql' | 'filename'): string
// Sanitizes user input based on context
// USED IN: All user input processing
// PREVENTS: XSS, SQL injection, path traversal
```

### /src/shared/utils/formatting.ts

```typescript
formatCurrency(amount: number, currency: string = 'USD'): string
// Formats number as currency string
// USED IN: PriceDisplay, Invoice, OrderSummary
// EXAMPLE: formatCurrency(1234.5, 'USD') // "$1,234.50"

formatDate(date: Date | string, format: string = 'short'): string
// Consistent date formatting across the app
// FORMATS: 'short', 'long', 'iso', 'relative'
// USED IN: All date displays
// LOCALE: Respects user's locale settings

truncateText(text: string, maxLength: number, suffix: string = '...'): string
// Safely truncates text preserving word boundaries
// USED IN: CardComponent, ListItems, Previews
```

### /src/shared/utils/errors.ts

```typescript
class AppError extends Error {
  constructor(message: string, code: string, statusCode: number)
  // Custom error class for consistent error handling
  // USED IN: All services and API endpoints
  // EXAMPLE: throw new AppError('Not found', 'RESOURCE_NOT_FOUND', 404)
}

handleError(error: unknown): AppError
// Converts any error to AppError format
// USED IN: Error boundaries, catch blocks
// LOGS: To monitoring service

isAppError(error: unknown): error is AppError
// Type guard for AppError
// USED IN: Error handlers
```

## 🏛️ Services

### /src/backend/services/AuthService.ts

```typescript
class AuthService {
  async authenticate(email: string, password: string): Promise<AuthResult>
  // Validates credentials and returns auth token
  // THROWS: AppError('Invalid credentials', 'AUTH_FAILED', 401)
  // CALLS: UserService.findByEmail(), bcrypt.compare()
  // RETURNS: { token: string, user: User, expiresIn: number }
  // USED BY: POST /api/auth/login

  async validateToken(token: string): Promise<TokenPayload>
  // Validates JWT token
  // THROWS: AppError('Invalid token', 'TOKEN_INVALID', 401)
  // USES: jwt.verify() with RS256
  // CACHES: Valid tokens in Redis for 5 min
  // USED BY: authMiddleware

  async refreshToken(refreshToken: string): Promise<AuthResult>
  // Exchanges refresh token for new access token
  // VALIDATES: Refresh token exists in database
  // INVALIDATES: Used refresh token
  // USED BY: POST /api/auth/refresh

  async logout(userId: string): Promise<void>
  // Invalidates all tokens for user
  // CLEARS: Redis cache
  // DELETES: Refresh tokens from DB
  // USED BY: POST /api/auth/logout
}
```

### /src/backend/services/UserService.ts

```typescript
class UserService {
  async findAll(options?: FindOptions): Promise<PaginatedResult<User>>
  // Returns paginated list of users
  // SUPPORTS: Filtering, sorting, pagination
  // CACHE: Redis key `users:${hash(options)}` (5 min)
  // USED BY: GET /api/users, Admin dashboard

  async findById(id: string): Promise<User | null>
  // Finds user by ID
  // INCLUDES: Related data based on context
  // CACHE: Redis key `user:${id}` (10 min)
  // USED BY: Multiple endpoints

  async create(data: CreateUserDto): Promise<User>
  // Creates new user account
  // VALIDATES: Email uniqueness, password strength
  // HASHES: Password with bcrypt (rounds: 12)
  // SENDS: Welcome email via EmailService
  // INVALIDATES: users:all cache
  // USED BY: POST /api/auth/register

  async update(id: string, data: UpdateUserDto): Promise<User>
  // Updates user data
  // VALIDATES: Email uniqueness if changed
  // LOGS: Changes to audit log
  // INVALIDATES: user:${id} and users:all cache
  // USED BY: PATCH /api/users/:id
}
```

## 🪝 React Hooks

### /src/frontend/hooks/useAuth.ts

```typescript
useAuth(): AuthContext
// Provides authentication state and methods
// USES: AuthContext via useContext
// RETURNS: {
//   user: User | null,
//   isAuthenticated: boolean,
//   isLoading: boolean,
//   login: (email, password) => Promise<void>,
//   logout: () => Promise<void>,
//   refreshToken: () => Promise<void>
// }
// USED IN: Navigation, ProtectedRoute, LoginPage
```

### /src/frontend/hooks/useApi.ts

```typescript
useApi<T>(endpoint: string, options?: UseApiOptions): UseApiResult<T>
// Generic hook for API calls with loading/error states
// FEATURES: Automatic retry, cancellation, caching
// RETURNS: { data: T, isLoading, error, refetch }
// USED IN: All data-fetching components
// EXAMPLE: const { data: users } = useApi('/api/users')
```

### /src/frontend/hooks/useDebounce.ts

```typescript
useDebounce<T>(value: T, delay: number = 500): T
// Debounces rapidly changing values
// USED IN: Search inputs, form validation
// PREVENTS: Excessive API calls
```

## 🏗️ Components

### /src/frontend/components/forms/FormField.tsx

```typescript
interface FormFieldProps {
  name: string
  label: string
  type?: 'text' | 'email' | 'password' | 'select' | 'textarea'
  validation?: ValidationRule[]
  required?: boolean
}

FormField: React.FC<FormFieldProps>
// Reusable form field with validation
// INTEGRATES: react-hook-form
// SHOWS: Error messages, loading states
// USED IN: All forms throughout the app
```

### /src/frontend/components/ui/Button.tsx

```typescript
interface ButtonProps {
  variant?: 'primary' | 'secondary' | 'danger'
  size?: 'sm' | 'md' | 'lg'
  isLoading?: boolean
  disabled?: boolean
  onClick?: () => void | Promise<void>
}

Button: React.FC<ButtonProps>
// Consistent button styling and behavior
// HANDLES: Loading states, async operations
// PREVENTS: Double-clicks during async
// ACCESSIBILITY: ARIA labels, keyboard nav
```

## 🔌 API Endpoints

### Authentication
```
POST   /api/auth/login      -> AuthController.login()
POST   /api/auth/register   -> AuthController.register()  
POST   /api/auth/logout     -> AuthController.logout()
POST   /api/auth/refresh    -> AuthController.refresh()
GET    /api/auth/me         -> AuthController.getCurrentUser()
```

### Users
```
GET    /api/users           -> UserController.list()
GET    /api/users/:id       -> UserController.getById()
PATCH  /api/users/:id       -> UserController.update()
DELETE /api/users/:id       -> UserController.delete()
```

## 📝 Type Definitions

### /src/shared/types/user.ts
```typescript
interface User {
  id: string
  email: string
  name: string
  role: UserRole
  createdAt: Date
  updatedAt: Date
}

enum UserRole {
  USER = 'user',
  ADMIN = 'admin',
  MODERATOR = 'moderator'
}

type CreateUserDto = Omit<User, 'id' | 'createdAt' | 'updatedAt'>
type UpdateUserDto = Partial<CreateUserDto>
```

## 🚨 Important Notes

1. **When adding new functions**: Update this registry immediately
2. **When modifying signatures**: Update all USED IN references
3. **When deprecating**: Mark with ⚠️ DEPRECATED and migration path
4. **When removing**: Ensure no usage remains (use global search)

## 📊 Code Metrics

- Total Utility Functions: [COUNT]
- Total Service Methods: [COUNT]
- Total React Hooks: [COUNT]
- Total API Endpoints: [COUNT]
- Test Coverage: [PERCENTAGE]%

Last Updated: [DATE]
