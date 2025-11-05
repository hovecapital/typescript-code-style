# Quick Reference

Daily commands and patterns for TypeScript development with Claude Code.

## OpenSpec Commands

### Start New Feature

```bash
/openspec:proposal <feature-name>
```

Creates proposal structure in `openspec/changes/<feature-name>/`

### Review Feature

```bash
openspec show <feature-name>
```

Displays proposal, tasks, and spec deltas.

### Implement Feature

```bash
/openspec:apply <feature-name>
```

Claude implements following TDD workflow.

### Archive Feature

```bash
/openspec:archive <feature-name> --yes
```

Merges specs, archives change.

### List Changes

```bash
openspec list
```

Shows active and archived changes.

## Superpowers Commands

### Brainstorm Design

```bash
/superpowers:brainstorm
```

Interactive design refinement.

### Create Plan

```bash
/superpowers:write-plan
```

Generate detailed implementation plan.

### Execute Plan

```bash
/superpowers:execute-plan
```

Batch execution of planned tasks.

### Debug Issue

```bash
/superpowers:debug
```

Systematic 4-phase debugging.

### Verify Work

```bash
/superpowers:verify
```

Check completion criteria.

## Development Commands

### Type Checking

```bash
npm run type-check
# or
tsc --noEmit
```

### Linting

```bash
npm run lint
# or
eslint src/**/*.ts
```

### Testing

```bash
npm test                    # Run all tests
npm test -- --watch         # Watch mode
npm test -- user.test.ts    # Single file
```

### Build

```bash
npm run build              # Production build
npm run dev                # Development mode
```

## Context7 Queries

### Get Library Docs

```
"Get Zod validation examples"
"Show TypeScript utility types"
"Get tRPC setup guide"
"Show Prisma query examples"
```

Claude will fetch current documentation.

## Git Workflow

### Check Status

```bash
git status
git diff
```

### View History

```bash
git log --oneline -10
git show HEAD
```

### Branch Operations

```bash
git branch <feature-name>
git checkout <feature-name>
```

## Common Patterns

### Result Type

```typescript
type Result<T, E = Error> = 
  | { success: true; data: T }
  | { success: false; error: E };

function divide(a: number, b: number): Result<number> {
  if (b === 0) {
    return { success: false, error: new Error('Division by zero') };
  }
  return { success: true, data: a / b };
}
```

### Type Guard

```typescript
function isUser(value: unknown): value is User {
  return (
    typeof value === 'object' &&
    value !== null &&
    'id' in value &&
    'email' in value
  );
}
```

### Branded Type

```typescript
type UserId = string & { readonly __brand: 'UserId' };

function createUserId(id: string): UserId {
  return id as UserId;
}
```

### Runtime Validation (Yup)

```typescript
import * as yup from 'yup';

const schema = yup.object({
  email: yup.string().email().required(),
  age: yup.number().positive().integer(),
});

async function validate(data: unknown) {
  try {
    const valid = await schema.validate(data);
    return { success: true, data: valid };
  } catch (error) {
    return { success: false, error };
  }
}
```

### Runtime Validation (Zod)

```typescript
import { z } from 'zod';

const schema = z.object({
  email: z.string().email(),
  age: z.number().positive().int(),
});

function validate(data: unknown) {
  const result = schema.safeParse(data);
  if (result.success) {
    return { success: true, data: result.data };
  }
  return { success: false, error: result.error };
}
```

### Discriminated Union

```typescript
type LoadingState = 
  | { status: 'idle' }
  | { status: 'loading' }
  | { status: 'success'; data: User }
  | { status: 'error'; error: Error };

function handle(state: LoadingState) {
  switch (state.status) {
    case 'idle':
      return 'Not started';
    case 'loading':
      return 'Loading...';
    case 'success':
      return state.data.name;
    case 'error':
      return state.error.message;
  }
}
```

### Conditional Type

```typescript
type IsArray<T> = T extends any[] ? true : false;

type A = IsArray<string[]>;  // true
type B = IsArray<string>;    // false
```

### Mapped Type

```typescript
type Nullable<T> = {
  [K in keyof T]: T[K] | null;
};

type User = {
  id: string;
  email: string;
};

type NullableUser = Nullable<User>;
// { id: string | null; email: string | null }
```

## File Structure

### Service Pattern

```typescript
// src/services/user.service.ts
import type { User, CreateUserInput } from '@/types/user';
import type { Result } from '@/types/result';

export class UserService {
  async create(input: CreateUserInput): Promise<Result<User>> {
    // Implementation
  }
}
```

### Repository Pattern

```typescript
// src/repositories/user.repository.ts
import type { User, UserId } from '@/types/user';

export class UserRepository {
  async findById(id: UserId): Promise<User | null> {
    // Implementation
  }
}
```

### Validator Pattern

```typescript
// src/validators/user.validator.ts
import { z } from 'zod';

export const createUserSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
});

export type CreateUserInput = z.infer<typeof createUserSchema>;
```

## Testing Patterns

### Unit Test

```typescript
// tests/unit/user.service.test.ts
import { describe, it, expect } from 'vitest';
import { UserService } from '@/services/user.service';

describe('UserService', () => {
  it('should create user with valid input', async () => {
    const service = new UserService();
    const result = await service.create({
      email: 'user@test.com',
      password: 'password123',
    });
    
    expect(result.success).toBe(true);
  });
});
```

### Integration Test

```typescript
// tests/integration/api.test.ts
import { describe, it, expect } from 'vitest';
import { app } from '@/app';

describe('User API', () => {
  it('POST /users should create user', async () => {
    const response = await app.inject({
      method: 'POST',
      url: '/users',
      payload: {
        email: 'user@test.com',
        password: 'password123',
      },
    });
    
    expect(response.statusCode).toBe(201);
  });
});
```

## Troubleshooting

### Type Error

```bash
# Check exact error
tsc --noEmit

# Check specific file
tsc --noEmit src/services/user.service.ts
```

### Test Failure

```bash
# Run with verbose output
npm test -- --reporter=verbose

# Run specific test
npm test -- --grep "should create user"
```

### Build Error

```bash
# Clean build
rm -rf dist
npm run build
```

## Pre-Commit Checklist

- [ ] `npm run type-check` passes
- [ ] `npm run lint` passes  
- [ ] `npm test` passes
- [ ] No `any` types without validation
- [ ] All functions have return types
- [ ] Result types used for errors
- [ ] Tests written for new features

## Keep Handy

- **CLAUDE.md** - Coding standards reference
- **SUMMARY.md** - Workflow overview
- This file - Quick command lookup
