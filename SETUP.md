# TypeScript Development Setup

Complete installation and configuration guide for the TypeScript development flow with Claude Code.

## Prerequisites

- Node.js 18+ installed
- npm, yarn, or pnpm
- Claude Code installed
- Git configured

## 1. Install OpenSpec

```bash
npm install -g @fission-ai/openspec@latest
```

Verify installation:

```bash
openspec --version
```

## 2. Install Superpowers Plugin

In Claude Code:

```bash
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

Verify installation:

```bash
/superpowers:list
```

## 3. Configure Claude Code

Copy the configuration file:

```bash
cp settings_local.json ~/.claude-code/settings_local.json
```

Or create manually at `~/.claude-code/settings_local.json`:

```json
{
  "permissions": {
    "allow": [
      "mcp__*",
      "Bash(npm *)",
      "Bash(yarn *)",
      "Bash(pnpm *)",
      "Bash(node *)",
      "Bash(cat *)",
      "Bash(ls *)",
      "Bash(pwd)",
      "Bash(echo *)",
      "Bash(grep *)",
      "Bash(find * -type *)",
      "Bash(find * -name *)",
      "Bash(head *)",
      "Bash(tail *)",
      "Bash(mkdir *)",
      "Bash(touch *)",
      "Bash(cp *.ts *.ts)",
      "Bash(cp *.js *.js)",
      "Bash(mv *.ts *.ts)",
      "Bash(mv *.js *.js)",
      "Bash(git status)",
      "Bash(git diff *)",
      "Bash(git log *)",
      "Bash(git branch *)",
      "Bash(git show *)",
      "Bash(test -* *)",
      "mcp__context7__resolve-library-id",
      "mcp__context7__get-library-docs"
    ],
    "deny": [
      "Bash(rm -rf /)",
      "Bash(rm -rf /*)",
      "Bash(curl * | bash)",
      "Bash(wget * | bash)",
      "Read(./.env)",
      "Read(./.env.*)"
    ]
  },
  "env": {
    "CLAUDE_CODE_ENABLE_TELEMETRY": "0"
  }
}
```

## 4. Initialize OpenSpec in Your Project

```bash
cd your-typescript-project
openspec init
```

This creates:

```
openspec/
├── changes/       # Active feature development
├── specs/         # Merged specifications
└── archive/       # Completed changes
```

## 5. Copy CLAUDE.md to Your Project

```bash
cp CLAUDE.md /path/to/your-project/
```

Place it at the project root for Claude to reference coding standards.

## 6. Configure TypeScript

Ensure your `tsconfig.json` has strict settings:

```json
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitOverride": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "target": "es2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "verbatimModuleSyntax": true,
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

## 7. Install Development Dependencies

```bash
npm install -D typescript @types/node
npm install -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
npm install -D prettier
npm install -D vitest # or jest
```

## 8. Configure ESLint

Create `.eslintrc.json`:

```json
{
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "rules": {
    "@typescript-eslint/no-explicit-any": "error",
    "@typescript-eslint/explicit-function-return-type": "warn"
  }
}
```

## 9. Configure Prettier

Create `.prettierrc`:

```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

## 10. Verify Setup

Start Claude Code in your project:

```bash
cd your-typescript-project
claude-code
```

Test the workflow:

```
/openspec:proposal test-feature
```

Should create proposal structure successfully.

## Project Structure Recommendation

```
your-project/
├── src/
│   ├── types/          # Shared type definitions
│   ├── services/       # Business logic
│   ├── utils/          # Helper functions
│   ├── validators/     # Runtime validation
│   └── index.ts
├── tests/
│   ├── unit/
│   └── integration/
├── openspec/
│   ├── changes/
│   ├── specs/
│   └── archive/
├── CLAUDE.md
├── tsconfig.json
├── package.json
└── README.md
```

## Runtime Validation Setup

Install validation library:

```bash
# Yup
npm install yup

# Or Zod
npm install zod
```

Example Yup schema:

```typescript
import * as yup from 'yup';

const userSchema = yup.object({
  email: yup.string().email().required(),
  age: yup.number().positive().integer().required(),
});

type User = yup.InferType<typeof userSchema>;
```

Example Zod schema:

```typescript
import { z } from 'zod';

const userSchema = z.object({
  email: z.string().email(),
  age: z.number().positive().int(),
});

type User = z.infer<typeof userSchema>;
```

## Testing Setup

### Vitest

```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    globals: true,
    environment: 'node',
  },
});
```

### Jest

```typescript
// jest.config.js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  roots: ['<rootDir>/tests'],
  testMatch: ['**/*.test.ts'],
};
```

## Troubleshooting

### OpenSpec not found

```bash
npm install -g @fission-ai/openspec@latest
```

### Superpowers not loading

Reinstall:

```bash
/plugin uninstall superpowers
/plugin install superpowers@superpowers-marketplace
```

### TypeScript errors in strict mode

Enable strict mode gradually:

```json
{
  "compilerOptions": {
    "strict": false,
    "noImplicitAny": true
  }
}
```

Then enable more flags one by one.

### Permission denied errors

Check `settings_local.json` is in correct location:

```bash
cat ~/.claude-code/settings_local.json
```

## Next Steps

1. Read through CLAUDE.md coding guidelines
2. Review QUICKREF.md for daily commands
3. Try creating your first feature with `/openspec:proposal`
4. Read SUMMARY.md to understand the full workflow

## Support

- [OpenSpec Documentation](https://github.com/fission-codes/openspec)
- [Superpowers Guide](https://github.com/obra/superpowers)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/)
