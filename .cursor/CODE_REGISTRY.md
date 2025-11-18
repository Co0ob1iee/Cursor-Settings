# 📚 CODE REGISTRY

## Purpose
This registry tracks all major functions, classes, hooks, and utilities in the codebase.
Each entry includes: signature, purpose, dependencies, and usage locations.

## 🔧 Utility Functions

### [Path to your utility file]

```[language]
[functionName]([params]): [ReturnType]
// [Description of what the function does]
// USED IN: [Component/Service names that use this]
// EXAMPLE: [functionName]([example params]) // [expected result]

[functionName]([params]): [ReturnType]
// [Description of what the function does]
// RULES: [validation rules or constraints]
// USED IN: [Component/Service names that use this]
// EXAMPLE: [functionName]([example params]) // [expected result]

[functionName]([params], [params]): [ReturnType]
// [Description of what the function does]
// USED IN: [Where it's used]
// PREVENTS: [Security concerns it addresses]
```

### [Path to your utility file]

```[language]
[functionName]([params], [optionalParams] = [default]): [ReturnType]
// [Description of what the function does]
// USED IN: [Component/Service names that use this]
// EXAMPLE: [functionName]([example params]) // [expected result]

[functionName]([params], [params] = '[default]'): [ReturnType]
// [Description of what the function does]
// FORMATS: [supported formats or options]
// USED IN: [Where it's used]
// LOCALE: [Localization behavior]

[functionName]([params], [params], [params] = '...'): [ReturnType]
// [Description of what the function does]
// USED IN: [Component/Service names that use this]
```

### [Path to your utility file]

```[language]
class [ClassName] extends [BaseClass] {
  constructor([params])
  // [Description of the class]
  // USED IN: [Where it's used]
  // EXAMPLE: [usage example]
}

[functionName]([params]): [ReturnType]
// [Description of what the function does]
// USED IN: [Where it's used]
// LOGS: [Logging behavior]

[functionName]([params]): [ReturnType]
// [Description of what the function does]
// USED IN: [Where it's used]
```

## 🏛️ Services

### [Path to your service file]

```[language]
class [ServiceName] {
  async [methodName]([params]): Promise<[ReturnType]>
  // [Description of what the method does]
  // THROWS: [Error conditions]
  // CALLS: [Other services/methods called]
  // RETURNS: [Return value description]
  // USED BY: [API endpoint or component]

  async [methodName]([params]): Promise<[ReturnType]>
  // [Description of what the method does]
  // THROWS: [Error conditions]
  // USES: [Library/function used]
  // CACHES: [Caching strategy]
  // USED BY: [Where it's used]

  async [methodName]([params]): Promise<[ReturnType]>
  // [Description of what the method does]
  // VALIDATES: [Validation rules]
  // INVALIDATES: [What gets invalidated]
  // USED BY: [Where it's used]

  async [methodName]([params]): Promise<[ReturnType]>
  // [Description of what the method does]
  // CLEARS: [What gets cleared]
  // DELETES: [What gets deleted]
  // USED BY: [Where it's used]
}
```

### [Path to your service file]

```[language]
class [ServiceName] {
  async [methodName]([params]?): Promise<[ReturnType]>
  // [Description of what the method does]
  // SUPPORTS: [Features supported]
  // CACHE: [Caching strategy]
  // USED BY: [Where it's used]

  async [methodName]([params]): Promise<[ReturnType] | null>
  // [Description of what the method does]
  // INCLUDES: [What's included in response]
  // CACHE: [Caching strategy]
  // USED BY: [Where it's used]

  async [methodName]([params]): Promise<[ReturnType]>
  // [Description of what the method does]
  // VALIDATES: [Validation rules]
  // [ACTION]: [What action is performed]
  // INVALIDATES: [What gets invalidated]
  // USED BY: [Where it's used]

  async [methodName]([params], [params]): Promise<[ReturnType]>
  // [Description of what the method does]
  // VALIDATES: [Validation rules]
  // LOGS: [What gets logged]
  // INVALIDATES: [What gets invalidated]
  // USED BY: [Where it's used]
}
```

## 🪝 [Framework] Hooks / Custom Hooks

### [Path to your hook file]

```[language]
[hookName](): [ReturnType]
// [Description of what the hook provides]
// USES: [Context/Library] via [method]
// RETURNS: {
//   [property]: [Type],
//   [property]: [Type],
//   [method]: ([params]) => [ReturnType],
//   [method]: () => [ReturnType]
// }
// USED IN: [Components/Pages that use this]
```

### [Path to your hook file]

```[language]
[hookName]<[GenericType]>([params], [params]?): [ReturnType]
// [Description of what the hook does]
// FEATURES: [Features provided]
// RETURNS: { [property]: [Type], [property]: [Type], [property]: [Type] }
// USED IN: [Where it's used]
// EXAMPLE: [usage example]
```

### [Path to your hook file]

```[language]
[hookName]<[GenericType]>([params], [params] = [default]): [ReturnType]
// [Description of what the hook does]
// USED IN: [Where it's used]
// PREVENTS: [What it prevents]
```

## 🏗️ Components

### [Path to your component file]

```[language]
interface [ComponentName]Props {
  [propName]: [Type]
  [propName]: [Type]
  [propName]?: [Type]
  [propName]?: [Type]
}

[ComponentName]: [Framework].[ComponentType]<[ComponentName]Props>
// [Description of what the component does]
// INTEGRATES: [Libraries/frameworks integrated]
// SHOWS: [What it displays]
// USED IN: [Where it's used]
```

### [Path to your component file]

```[language]
interface [ComponentName]Props {
  [propName]?: '[value]' | '[value]' | '[value]'
  [propName]?: '[value]' | '[value]' | '[value]'
  [propName]?: [Type]
  [propName]?: [Type]
  [propName]?: () => [ReturnType] | Promise<[ReturnType]>
}

[ComponentName]: [Framework].[ComponentType]<[ComponentName]Props>
// [Description of what the component does]
// HANDLES: [What it handles]
// PREVENTS: [What it prevents]
// ACCESSIBILITY: [Accessibility features]
```

## 🔌 API Endpoints

### [Resource Category]
```
[METHOD]   /api/[resource]/[action]      -> [Controller].[method]()
[METHOD]   /api/[resource]/[action]     -> [Controller].[method]()  
[METHOD]   /api/[resource]/[action]      -> [Controller].[method]()
[METHOD]   /api/[resource]/[action]      -> [Controller].[method]()
[METHOD]   /api/[resource]/[action]      -> [Controller].[method]()
```

### [Resource Category]
```
[METHOD]   /api/[resource]              -> [Controller].[method]()
[METHOD]   /api/[resource]/:id           -> [Controller].[method]()
[METHOD]   /api/[resource]/:id            -> [Controller].[method]()
[METHOD]   /api/[resource]/:id           -> [Controller].[method]()
```

## 📝 Type Definitions

### [Path to your types file]
```[language]
interface [TypeName] {
  id: [Type]
  [fieldName]: [Type]
  [fieldName]: [Type]
  [fieldName]: [Type]
  createdAt: [DateType]
  updatedAt: [DateType]
}

enum [EnumName] {
  [VALUE] = '[value]',
  [VALUE] = '[value]',
  [VALUE] = '[value]'
}

type [TypeName] = Omit<[BaseType], '[field]' | '[field]' | '[field]'>
type [TypeName] = Partial<[BaseType]>
```

## 🚨 Important Notes

1. **When adding new functions**: Update this registry immediately
2. **When modifying signatures**: Update all USED IN references
3. **When deprecating**: Mark with ⚠️ DEPRECATED and migration path
4. **When removing**: Ensure no usage remains (use global search)

## 📊 Code Metrics

- Total Utility Functions: [COUNT - update as you add functions]
- Total Service Methods: [COUNT - update as you add methods]
- Total [Framework] Hooks: [COUNT - update as you add hooks]
- Total API Endpoints: [COUNT - update as you add endpoints]
- Test Coverage: [PERCENTAGE]% - [update with actual coverage]

Last Updated: [DATE - update when you modify this registry]
