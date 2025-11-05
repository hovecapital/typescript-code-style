# How It All Works

Understanding the TypeScript development flow with Claude Code.

## The Big Picture

This setup combines three powerful tools to create a predictable, high-quality development workflow:

1. **OpenSpec** - Spec-driven development framework
2. **Superpowers** - Proven development workflows
3. **Context7 MCP** - Up-to-date library documentation

Together they enable Claude to help you build TypeScript applications systematically with built-in quality assurance.

## The Flow

```
Idea → Proposal → Refinement → Implementation → Verification → Archive
  ↓        ↓           ↓              ↓              ↓            ↓
Think  Capture    Iterate       Build+Test      Check       Preserve
```

### 1. Idea → Proposal

You have an idea for a feature.

```
/openspec:proposal add-user-authentication
```

OpenSpec creates a structured proposal:

```
openspec/changes/add-user-authentication/
├── proposal.md      # What and why
├── tasks.md         # Implementation steps
└── specs/
    └── auth/
        └── spec.md  # Technical specification
```

**What happens:**

- Claude captures your intent in proposal.md
- Breaks down work into tasks.md
- Creates spec deltas showing what will change

### 2. Proposal → Refinement

Review and iterate on the proposal.

```
openspec show add-user-authentication
```

**What happens:**

- You see the full proposal
- Request changes if needed
- Claude updates the proposal
- Repeat until specs are clear

**Why this matters:**

- Agree on requirements before code
- Catch issues early
- Clear expectations for both you and Claude

### 3. Refinement → Implementation

Implement the approved proposal.

```
/openspec:apply add-user-authentication
```

**What happens:**

- Superpowers TDD skill activates
- Claude works through tasks systematically
- Tests written first (red)
- Implementation follows (green)
- Refactoring as needed (refactor)

**Tools used during implementation:**

#### Context7 MCP

```
"Get Zod validation examples"
```

Fetches current documentation for libraries you're using.

#### CLAUDE.md Rules

- Strict typing enforced
- No `any` without validation
- Result types for errors
- Type guards for runtime checks

#### Superpowers Workflows

- TDD: Systematic red-green-refactor
- Debug: 4-phase root cause analysis
- Verify: Completion criteria checking

### 4. Implementation → Verification

Check that work is complete and correct.

```
/superpowers:verify
```

**What happens:**

- All tasks marked complete
- Tests passing
- Type checking passing
- Linting passing
- No `any` types without validation
- Result types used appropriately
- Code follows CLAUDE.md standards

### 5. Verification → Archive

Preserve the completed work.

```
/openspec:archive add-user-authentication --yes
```

**What happens:**

- Specs merged from changes/ to specs/
- Change moved to archive/
- Ready for next feature

## Why This Works

### Deterministic Development

Traditional approach:

```
"Add user authentication" → [unpredictable implementation]
```

This approach:

```
"Add user authentication" 
  → Proposal (clear intent)
  → Tasks (clear steps)
  → Specs (clear expectations)
  → TDD (systematic implementation)
  → Verification (quality gates)
  → Archive (preserved knowledge)
```

### Built-in Quality

Quality isn't checked at the end - it's built in:

1. **Specs first** - Clear requirements prevent rework
2. **TDD** - Tests drive implementation
3. **Type safety** - Compiler catches errors
4. **Standards** - CLAUDE.md enforces patterns
5. **Verification** - Checklist before done

### Knowledge Preservation

Every feature leaves behind:

- **Specs** - What the system does
- **Tests** - How it should behave  
- **Code** - Implementation details
- **Archive** - Decision history

New team members can understand the system by reading specs and tests.

## The Tools

### OpenSpec

**Purpose:** Structure and preserve specifications

**Key concepts:**

- Changes: Active feature development
- Specs: Merged, authoritative documentation
- Archive: Historical record

**Commands:**

- `openspec init` - Initialize in project
- `openspec list` - View changes
- `openspec show <name>` - View specific change

### Superpowers

**Purpose:** Proven development workflows

**Key workflows:**

- **TDD**: Red-green-refactor cycle
- **Debug**: Systematic problem solving
- **Verify**: Completion checking
- **Plan**: Breaking down complex work

**How it works:**

- Skills activate automatically based on context
- Claude follows proven patterns
- Quality built into the process

**Commands:**

- `/superpowers:list` - Available skills
- `/superpowers:brainstorm` - Design refinement
- `/superpowers:debug` - Problem solving
- `/superpowers:verify` - Check completion

### Context7 MCP

**Purpose:** Current library documentation

**What it provides:**

- Up-to-date API docs
- Usage examples
- Type definitions
- Best practices

**How to use:**
Ask Claude to get docs:

```
"Get Zod object schema examples"
"Show TypeScript utility types"
"Get tRPC router configuration"
```

Claude fetches and uses the documentation.

## The Standards

### CLAUDE.md

**Purpose:** Coding guidelines and patterns

**Key rules:**

- Strict TypeScript configuration
- No `any` without runtime validation
- Type over interface
- Result types for errors
- Branded types for domain values
- @ based imports

**When referenced:**

- During implementation
- During code review
- When making decisions

### TypeScript Configuration

**Key settings:**

```json
{
  "strict": true,
  "noUncheckedIndexedAccess": true,
  "noImplicitOverride": true
}
```

**Why:**

- Catch errors at compile time
- Enforce type safety
- Prevent runtime surprises

### Architecture Pattern

```
Entry Points → Services → Repositories → Data
      ↓           ↓
  Validators   Types
```

**Why:**

- Clear separation of concerns
- Testable components
- Type-safe data flow

## Common Scenarios

### Starting a New Feature

```
You: "Add email verification"

Claude: /openspec:proposal add-email-verification
        Created proposal structure.
        Review: openspec show add-email-verification

You: [Reviews and approves]

Claude: /openspec:apply add-email-verification
        [Implements with TDD]
        ✓ All tasks complete
        
You: "Looks good"

Claude: /openspec:archive add-email-verification --yes
        ✓ Archived
```

### Debugging an Issue

```
You: "Users can't login"

Claude: /superpowers:debug
        
        Phase 1: Gather information
        - Reviewing login flow
        - Checking recent changes
        - Reading error logs
        
        Phase 2: Form hypothesis
        - Token validation may be failing
        
        Phase 3: Test hypothesis
        - Writing test case
        - Confirms token issue
        
        Phase 4: Fix
        - Updated token validation
        - Tests passing
```

### Refactoring Code

```
You: "This UserService is too complex"

Claude: /superpowers:brainstorm
        
        Analyzing UserService...
        
        Suggestions:
        1. Extract email sending to EmailService
        2. Extract validation to UserValidator
        3. Extract queries to UserRepository
        
        Should I create a refactoring proposal?

You: "Yes"

Claude: /openspec:proposal refactor-user-service
        [Creates detailed refactoring plan]
```

## Benefits

### For You

- **Predictable outcomes** - Know what to expect
- **Less back-and-forth** - Clear specs up front
- **Quality assurance** - Built into workflow
- **Knowledge retention** - Everything documented

### For Your Team

- **Clear history** - Why decisions were made
- **Onboarding** - New members read specs
- **Consistency** - Same patterns everywhere
- **Maintainability** - Easy to modify later

### For Your Codebase

- **Type safety** - Compiler catches errors
- **Test coverage** - TDD ensures tests exist
- **Clear structure** - Patterns enforced
- **Documentation** - Specs stay current

## Advanced Usage

### Multiple Features

Work on multiple features simultaneously:

```bash
/openspec:proposal feature-a
/openspec:proposal feature-b

# Implement first
/openspec:apply feature-a
/openspec:archive feature-a --yes

# Then second
/openspec:apply feature-b
/openspec:archive feature-b --yes
```

### Complex Features

For large features, create sub-proposals:

```
/openspec:proposal user-management
# Break into smaller proposals
/openspec:proposal user-registration
/openspec:proposal user-profile
/openspec:proposal user-permissions
```

### Integration Points

When features interact:

```
/openspec:proposal feature-c
# In proposal.md, reference related specs:
# "Integrates with user-authentication (see specs/auth/)"
```

## Troubleshooting

### "Claude isn't following standards"

Check CLAUDE.md is in project root:

```bash
ls -la CLAUDE.md
```

### "Tests aren't being written"

Ensure Superpowers is installed:

```bash
/superpowers:list
```

### "Type errors everywhere"

Enable strict mode gradually:

```json
{
  "strict": false,
  "noImplicitAny": true
}
```

Add more strict flags incrementally.

## Best Practices

### Write Good Proposals

Bad:

```
"Make the app better"
```

Good:

```
"Add email verification to prevent fake accounts.
Users should verify email within 24 hours of registration."
```

### Keep Tasks Small

Bad:

```
Task 1: Build entire authentication system
```

Good:

```
Task 1.1: Create User type
Task 1.2: Add UserService.register
Task 1.3: Add email validation
Task 1.4: Add password hashing
```

### Use Descriptive Names

Bad:

```
/openspec:proposal thing
```

Good:

```
/openspec:proposal add-user-email-verification
```

### Review Before Applying

Always run:

```bash
openspec show <feature-name>
```

Before:

```bash
/openspec:apply <feature-name>
```

### Archive Completed Work

Don't leave changes in the changes/ directory:

```bash
/openspec:archive <feature-name> --yes
```

## Philosophy

This workflow embodies several principles:

### Specification-Driven

Code should match specifications. Specifications should be clear, reviewed, and preserved.

### Test-Driven

Tests define behavior. Implementation fulfills tests. Refactoring preserves behavior.

### Type-Driven

Types define contracts. Runtime validates types. Compiler enforces contracts.

### Quality-Driven

Quality isn't checked at the end. Quality is built into every step.

### Knowledge-Driven

Every decision documented. Every change explained. Every spec preserved.

## Next Steps

1. Try the workflow with a small feature
2. Review generated proposals and refine
3. Watch TDD in action during implementation
4. Examine archived changes to see knowledge preservation
5. Adapt the workflow to your needs

## Resources

- [OpenSpec Documentation](https://github.com/fission-codes/openspec)
- [Superpowers Guide](https://github.com/obra/superpowers)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/)
- CLAUDE.md - Project coding standards
- QUICKREF.md - Daily command reference
