# TypeScript Coding Rules

## Important Notes

- Use concise language
- Comments should be rare, code should be self-documenting
- Don't use emojis
- User runs npm commands, instruct and await
- npm run dev will normally already be running
- Local development environment
- Use Context7 MCP to read library documentation

## Type Safety Rules

- **No any**: Do not use `any` or `as any` unless data is truly runtime in nature. Use Yup schemas for runtime validation when unavoidable
- **Explicit function signatures**: All functions must have parameter types and return types
- **Use type over interface**: Use `type` for data shapes, `interface` only for actual contracts/services that may be implemented
- **Strict null checks**: Handle null/undefined cases explicitly
- **Type guards**: Use type predicates and guards for runtime type checking
- **Branded types**: Use branded types for domain-specific values

## Code Quality Rules

- **No code repetition**: Extract repeated logic into reusable functions
- **Descriptive naming**: Use clear, descriptive names for variables, functions, and types
- **Single responsibility**: Functions should handle single actions and be testable in isolation
- **No long functions**: Keep functions short and focused, break complex logic into smaller functions
- **Explicit returns**: Always explicitly return values from functions
- **Fail early**: Validate inputs and fail early with clear error messages

## Advanced Type Patterns

- **Conditional types**: Use for flexible, type-safe APIs
- **Mapped types**: Use for type transformations
- **Template literal types**: Use for string manipulation at type level
- **Discriminated unions**: Use for state machines and variants
- **Const assertions**: Use `as const` for literal types instead of manual definitions
- **Utility types**: Leverage built-in utilities (Pick, Omit, Partial, etc.) instead of manual definitions
- **Higher-kinded types**: Simulate when needed for advanced patterns
- **Recursive type definitions**: Use for nested data structures

## Project Structure Rules

- **Shared types separation**: Use separate folders/files for shared types across modules
- **Folder organization**: Structure using logical folders (utils/, shared/, types/, services/)
- **Layer separation**: Keep presentation separate from functional/business logic
- **Domain grouping**: Group related functionality together with clear boundaries
- **Import paths**: Use @ based imports with TypeScript path mapping in tsconfig

## Error Handling

- **Result types**: Use Result<T, E> patterns for expected errors
- **Never type**: Use for exhaustive checks
- **Type-safe errors**: Create typed error classes
- **Typed exceptions**: Functions that can fail should return Result types or throw typed errors

## Build Configuration

- **Strict mode**: Enable all strict compiler flags
- **Path mapping**: Configure @ imports in tsconfig paths
- **Source maps**: Enable for debugging
- **Type checking**: Pre-commit type checking
- **No emit on error**: Fail builds on type errors

## Testing

- **Type-safe tests**: Type test fixtures and mocks
- **Test utilities**: Create typed test helpers
- **Integration tests**: Type API responses
- **Type coverage**: Track type coverage metrics

---
