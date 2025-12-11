# JavaScript/TypeScript Coding Standards

JS/TS conventions and patterns.

---

## Variable Declarations

```javascript
// ✅ const by default
const MAX_RETRIES = 3;
const config = loadConfig();

// ✅ let when reassignment needed
let currentIndex = 0;
currentIndex += 1;

// ❌ Never use var
var oldStyle = "bad";
```

---

## Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Files | kebab-case or camelCase | `data-processor.ts` |
| Classes | PascalCase | `DataProcessor` |
| Functions | camelCase | `processData()` |
| Variables | camelCase | `userCount` |
| Constants | UPPER_SNAKE | `MAX_RETRIES` |
| Interfaces | PascalCase (I prefix optional) | `UserData` or `IUserData` |
| Types | PascalCase | `RequestOptions` |

---

## Functions

```typescript
// ✅ Arrow functions for short operations
const double = (x: number): number => x * 2;

// ✅ Regular functions for complex logic or when using 'this'
function processData(items: Item[]): Result {
    // ... complex logic
    return result;
}

// ✅ Async/await over .then()
async function fetchUser(id: string): Promise<User> {
    const response = await fetch(`/api/users/${id}`);
    if (!response.ok) {
        throw new Error(`Failed to fetch user: ${response.status}`);
    }
    return response.json();
}

// ❌ Avoid .then() chains when async/await works
function fetchUserBad(id: string): Promise<User> {
    return fetch(`/api/users/${id}`)
        .then(res => res.json())
        .then(data => data);
}
```

---

## TypeScript Types

```typescript
// Interfaces for object shapes
interface User {
    id: string;
    name: string;
    email: string;
    role: UserRole;
    createdAt: Date;
}

// Types for unions, intersections, or computed types
type UserRole = 'admin' | 'user' | 'guest';
type AsyncResult<T> = Promise<Result<T>>;

// Generic types
interface Result<T> {
    success: boolean;
    data?: T;
    error?: string;
}

// Utility types
type PartialUser = Partial<User>;
type UserWithoutId = Omit<User, 'id'>;
type UserKeys = keyof User;
```

---

## Error Handling

```typescript
// Custom error classes
class ApiError extends Error {
    constructor(
        message: string,
        public statusCode: number,
        public code: string
    ) {
        super(message);
        this.name = 'ApiError';
    }
}

// Throwing and catching
async function fetchData(url: string): Promise<Data> {
    try {
        const response = await fetch(url);
        if (!response.ok) {
            throw new ApiError(
                `Request failed: ${response.statusText}`,
                response.status,
                'FETCH_FAILED'
            );
        }
        return response.json();
    } catch (error) {
        if (error instanceof ApiError) {
            console.error(`API Error [${error.code}]: ${error.message}`);
            throw error;
        }
        console.error('Unexpected error:', error);
        throw new ApiError('Unknown error', 500, 'UNKNOWN');
    }
}
```

---

## Async Patterns

```typescript
// Sequential execution
async function processSequential(items: Item[]): Promise<Result[]> {
    const results: Result[] = [];
    for (const item of items) {
        const result = await processItem(item);
        results.push(result);
    }
    return results;
}

// Parallel execution
async function processParallel(items: Item[]): Promise<Result[]> {
    return Promise.all(items.map(item => processItem(item)));
}

// Parallel with error handling
async function processParallelSafe(items: Item[]): Promise<Result[]> {
    const results = await Promise.allSettled(
        items.map(item => processItem(item))
    );
    return results
        .filter((r): r is PromiseFulfilledResult<Result> => r.status === 'fulfilled')
        .map(r => r.value);
}
```

---

## Destructuring & Spread

```typescript
// Object destructuring
const { name, email, role = 'user' } = user;

// Array destructuring
const [first, second, ...rest] = items;

// Spread for immutable updates
const updatedUser = { ...user, name: 'New Name' };
const extendedArray = [...existingArray, newItem];

// Rest parameters
function logAll(message: string, ...args: unknown[]): void {
    console.log(message, ...args);
}
```

---

## Optional Chaining & Nullish Coalescing

```typescript
// Optional chaining
const street = user?.address?.street;
const firstItem = items?.[0];
const result = callback?.();

// Nullish coalescing (null/undefined only, not falsy)
const displayName = user.name ?? 'Anonymous';
const count = data.count ?? 0;

// Combined
const city = user?.address?.city ?? 'Unknown';
```

---

## Modules

```typescript
// Named exports (preferred)
export function processData(data: Data): Result { ... }
export const DEFAULT_CONFIG: Config = { ... };
export interface UserData { ... }

// Default export (use sparingly, one per file)
export default class DataProcessor { ... }

// Re-exports
export { processData, DataProcessor } from './processor';
export * from './types';
```

---

## Common Pitfalls

```typescript
// ❌ == with type coercion
if (value == null) { }

// ✅ === for strict equality
if (value === null || value === undefined) { }
// Or use nullish check
if (value == null) { } // Only == null is acceptable

// ❌ Floating promises
async function bad() {
    doAsyncThing(); // Promise ignored!
}

// ✅ Await or handle
async function good() {
    await doAsyncThing();
    // or
    doAsyncThing().catch(console.error);
}

// ❌ Using 'any' type
function process(data: any) { }

// ✅ Use proper types or 'unknown'
function process(data: unknown) {
    if (isValidData(data)) {
        // Now properly typed
    }
}
```

---

## React Specific (if applicable)

```tsx
// Functional components with TypeScript
interface ButtonProps {
    label: string;
    onClick: () => void;
    disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({ label, onClick, disabled = false }) => {
    return (
        <button onClick={onClick} disabled={disabled}>
            {label}
        </button>
    );
};

// Hooks
const [count, setCount] = useState<number>(0);
const userRef = useRef<HTMLDivElement>(null);
```
