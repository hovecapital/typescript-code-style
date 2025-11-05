# TypeScript Development Flow for Claude Code

Spec-driven development workflow combining OpenSpec, Superpowers, and MCPs for predictable, high-quality TypeScript applications.

## Quick Start

```bash
# Install OpenSpec
npm install -g @fission-ai/openspec@latest

# Initialize in your project
cd your-typescript-project
openspec init

# Install Superpowers in Claude Code
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace

# Copy configuration
cp settings_local.json ~/.claude-code/settings_local.json
cp CLAUDE.md /path/to/your-project/

# Start building
/openspec:proposal <your-feature-name>
```

## What You Get

✅ Spec-driven workflow - Agree on requirements before coding
✅ Automatic TDD - Test-first development built-in
✅ Systematic debugging - 4-phase root cause process
✅ Current documentation - Up-to-date library docs via Context7
✅ Strict TypeScript - Full type safety, no any
✅ Safe permissions - Work efficiently without constant prompts

## The Files

| File | Purpose | When to Use |
|------|---------|-------------|
| SETUP.md | Installation guide | Once per project setup |
| CLAUDE.md | Coding guidelines | Reference during development |
| QUICKREF.md | Daily commands | Keep open while coding |
| SUMMARY.md | How it all works | Understanding the flow |
| settings_local.json | Claude Code config | Copy to ~/.claude-code/ |

## The Workflow

### 1. Propose

```
/openspec:proposal Add user authentication
```

Creates structured proposal with specs and tasks.

### 2. Refine

```
openspec show add-user-authentication
```

Review and iterate until specs are clear.

### 3. Implement

```
/openspec:apply add-user-authentication
```

Superpowers guides TDD automatically. Context7 provides docs.

### 4. Archive

```
/openspec:archive add-user-authentication --yes
```

Merges approved specs, archives change.

## Core Technologies

### OpenSpec

Spec-driven development - agree on requirements before code.

- Proposals capture intent
- Tasks break down work
- Spec deltas show changes
- Archive maintains history

### Superpowers

Proven workflows activate automatically:

- TDD - Red-green-refactor cycle
- Debugging - Systematic root cause analysis
- Verification - Ensure work is complete
- Planning - Break down complex features

### Context7 MCP

Up-to-date library documentation:

```
"Get TypeScript utility types docs"
"Show Zod validation examples"
"Get tRPC router setup guide"
```

## Development Standards

### TypeScript Strict Mode

```typescript
// Type-safe data models
type User = {
  readonly id: string;
  email: string;
  status: UserStatus;
};

// Discriminated unions
type Result<T, E> = 
  | { success: true; data: T }
  | { success: false; error: E };

// Branded types
type UserId = string & { readonly __brand: 'UserId' };

// Type guards
function isUser(value: unknown): value is User {
  return (
    typeof value === 'object' &&
    value !== null &&
    'id' in value &&
    'email' in value
  );
}
```

### Architecture Pattern

```
Controllers/Routes → Services → Repositories → Data Layer
        ↓               ↓
    Validators       DTOs/Types
```

- Controllers/Routes: Thin, delegate to services
- Services: Business logic
- Repositories: Data access layer
- Validators: Runtime validation (Yup/Zod)
- DTOs: Type-safe data transfer
- Types: Shared type definitions

### Testing

```typescript
// Focus on meaningful integration tests
describe('User Registration', () => {
  it('should create user with valid data', async () => {
    const result = await userService.register({
      email: 'user@test.com',
      password: 'password123',
    });

    expect(result.success).toBe(true);
    if (result.success) {
      expect(result.data.email).toBe('user@test.com');
    }
  });
});
```

Focus on meaningful tests, not coverage percentages.

## Example Session

**Developer:** Create a feature for user profile editing

**Claude:** I'll create an OpenSpec proposal for user profile editing.

```
/openspec:proposal add-profile-editing

✓ Created openspec/changes/add-profile-editing/
✓ proposal.md - Intent and approach
✓ tasks.md - Implementation checklist  
✓ specs/users/spec.md - Profile spec delta

Ready to review. Use: openspec show add-profile-editing
```

**Developer:** Looks good, let's implement

**Claude:** Starting implementation for add-profile-editing.
Superpowers TDD skill activated.

```
[Gets documentation via Context7]
"Get Zod validation schema examples"

[Implements following CLAUDE.md standards]
✓ Task 1.1: Create profile types
✓ Task 1.2: Add ProfileService with Result types
✓ Task 1.3: Create validation schemas
✓ Task 2.1: Write unit tests
✓ Task 2.2: Create API routes

All tasks complete. Tests passing.
```

**Developer:** Archive the change

**Claude:**

```
/openspec:archive add-profile-editing --yes

✓ Specs merged to openspec/specs/users/
✓ Change archived
✓ Ready for next feature
```

## Safety Features

### Allowed Operations

✅ npm/yarn/pnpm commands
✅ Git operations (status, diff, commit)
✅ File viewing (cat, ls, grep)
✅ Package management
✅ Code quality tools (eslint, prettier)

### Blocked Operations

❌ System-wide deletions (rm -rf /)
❌ Destructive disk ops (dd, mkfs)
❌ Piped execution (curl | bash)
❌ Environment access (.env files)

## Pre-Completion Checklist

Before marking work done:

- [ ] Strict mode enabled in tsconfig.json
- [ ] No `any` types without Yup/Zod validation
- [ ] Type hints on all functions
- [ ] Runtime validation for external data
- [ ] Tests written for business logic
- [ ] Result types for error handling
- [ ] OpenSpec change archived
- [ ] Superpowers verification passed

## Common Commands

### Daily Workflow

```bash
/openspec:proposal <feature>      # Start feature
openspec show <feature>            # Review specs
/openspec:apply <feature>          # Implement
/openspec:archive <feature> --yes  # Complete
```

### Superpowers

```bash
/superpowers:brainstorm    # Design refinement
/superpowers:write-plan    # Create plan
/superpowers:execute-plan  # Batch execution
```

### Development

```bash
npm run dev          # Start dev server
npm run test         # Run tests
npm run build        # Production build
npm run type-check   # TypeScript checking
```

## Documentation

- **SETUP.md** - Complete installation and configuration
- **CLAUDE.md** - Full coding guidelines and patterns
- **QUICKREF.md** - Daily command reference
- **SUMMARY.md** - How everything works together

## Philosophy

- Write specs before code
- Follow proven workflows
- Enforce quality systematically

This setup embodies:

- Deterministic over unpredictable
- Systematic over ad-hoc
- Typed over dynamic
- Tested over hoped
- Documented over assumed

## Resources

- [OpenSpec](https://github.com/fission-codes/openspec)
- [Superpowers](https://github.com/obra/superpowers)
- [Context7 MCP](https://github.com/context7/mcp)
- [TypeScript Docs](https://www.typescriptlang.org/docs/)

## License

MIT
