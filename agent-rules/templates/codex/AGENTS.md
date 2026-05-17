# Codex Agent Rules

You are an AI coding assistant configured to help write high-quality software following established patterns and best practices.

---

# Project Structure

## Directory Layout

```
/
├── src/                    # Application source code
│   ├── components/         # Reusable UI components
│   ├── pages/             # Page-level components/routes
│   ├── hooks/             # Custom React hooks
│   ├── services/          # API clients, external services
│   ├── utils/             # Pure utility functions
│   ├── types/             # TypeScript type definitions
│   └── stores/            # State management
├── tests/                 # Integration/E2E tests
├── __tests__/             # Unit tests (co-located)
├── docs/                  # Documentation
├── scripts/               # Build and deployment scripts
├── configs/               # Tool configurations
└── AGENTS.md              # This file
```

## File Naming

| Content Type | Convention | Example |
|-------------|------------|---------|
| Components | PascalCase | `UserProfile.tsx` |
| Utilities | camelCase | `formatDate.ts` |
| Services | camelCase | `apiClient.ts` |
| Types | PascalCase | `UserTypes.ts` |
| Hooks | camelCase, `use` prefix | `useAuth.ts` |
| Config files | camelCase or dotfile | `.eslintrc.js` |

---

# Code Style

## TypeScript Standards

```typescript
// ✅ CORRECT: Explicit types, async/await, const
const processUserData = async (data: UserInput): Promise<UserResult> => {
  const validated = validateInput(data);
  const result = await db.users.create(validated);
  return transformResult(result);
};

// ❌ INCORRECT: Implicit any, mutation, var
var processUser = async (data) => {
  var result = db.users.create(data);
  return result;
};
```

## Naming Standards

```typescript
// Variables and functions: camelCase
const userCount = 100;
const getUserById = (id: string) => { ... };

// Classes and types: PascalCase
class UserService { ... }
interface UserProfile { ... }
type ApiResponse<T> = { data: T; status: number };

// Constants: UPPER_SNAKE_CASE
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = 'https://api.example.com';
```

## Formatting

- Indentation: 2 spaces
- Max line length: 100 characters
- Semicolons: Required
- Single quotes for strings
- Trailing commas: Always

## Import Organization

```typescript
// Group 1: Node.js built-ins
import { join } from 'path';
import { readFile } from 'fs/promises';

// Group 2: External packages
import express from 'express';
import { z } from 'zod';

// Group 3: Internal absolute imports
import { helpers } from '@/utils/helpers';

// Group 4: Relative imports
import { Button } from './Button';
import { formatId } from '../utils/format';
```

---

# Prohibited

## Code Generation

- ❌ **Never generate `any` type** — Use `unknown` or specific types
- ❌ **Never use `!` non-null assertion** — Handle null explicitly
- ❌ **No `console.log` in code** — Use structured logging
- ❌ **No inline styles** — Use CSS classes or modules
- ❌ **No `setTimeout` loops** — Use proper async patterns
- ❌ **No magic numbers** — Define as constants
- ❌ **No string concatenation in SQL** — Use parameterized queries

## Git & Version Control

- ❌ **Never commit secrets, keys, credentials** — Use environment variables
- ❌ **No force push** — Use PRs and code review
- ❌ **No binary files over 5MB** — Use Git LFS
- ❌ **No direct main/master commits** — All changes via PR

## Architecture

- ❌ **No circular dependencies** — Use dependency injection
- ❌ **No God classes/files** — Single responsibility
- ❌ **No dead code** — Delete unused functions
- ❌ **No commented-out code** — Delete or feature-flag

---

# Testing Requirements

## Coverage Requirements

| Metric | Minimum | Target |
|--------|---------|--------|
| Line coverage | 80% | 90% |
| Branch coverage | 75% | 85% |
| Function coverage | 90% | 100% |

## Test File Naming

```
ComponentName.test.ts      # Unit tests
ComponentName.e2e.ts       # E2E tests
api.endpoint.spec.ts       # Integration tests
```

## Test Structure (AAA Pattern)

```typescript
describe('UserService', () => {
  describe('createUser', () => {
    it('should create user with valid data', async () => {
      // Arrange
      const input: CreateUserInput = {
        name: 'Test User',
        email: 'test@example.com',
      };

      // Act
      const result = await userService.createUser(input);

      // Assert
      expect(result).toMatchObject({
        id: expect.any(String),
        name: 'Test User',
        createdAt: expect.any(Date),
      });
    });

    it('should reject duplicate email', async () => {
      // Arrange
      await userService.createUser({ name: 'First', email: 'dup@example.com' });

      // Act & Assert
      await expect(
        userService.createUser({ name: 'Second', email: 'dup@example.com' })
      ).rejects.toThrow(DuplicateEmailError);
    });
  });
});
```

## Required Test Scenarios

1. Happy path — Valid input produces expected output
2. Error cases — Invalid input handled gracefully
3. Edge cases — Null, undefined, empty, boundary values
4. Async behavior — Promises resolve/reject correctly
5. External dependencies — Mocks behave as expected

---

# Commit Message Format

## Structure

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

## Type Reference

| Type | Use When |
|------|----------|
| `feat` | Adding new functionality |
| `fix` | Bug fix |
| `docs` | Documentation changes |
| `style` | Formatting, no logic change |
| `refactor` | Code restructure, no feature change |
| `test` | Adding/updating tests |
| `chore` | Build, dependencies, tooling |
| `perf` | Performance improvement |

## Examples

```
feat(auth): add JWT refresh token rotation

- Implement sliding window token refresh
- Add token rotation on each use
- Invalidate old tokens after refresh

Closes: #456
```

```
fix(api): handle race condition in connection pool

The pool could deadlock when max connections reached
during high-load scenarios. Added connection timeout
and proper cleanup on error.

Fixes: #789
```

## Rules

- Subject: 50 chars max, lowercase start, no period
- Body: Wrap at 72 chars, explain what and why
- Footer: Reference issues with `Closes #N` or `Fixes #N`

---

# Security Requirements

## Input Validation

```typescript
// ✅ CORRECT: Validate all external input
import { z } from 'zod';

const UserSchema = z.object({
  email: z.string().email(),
  age: z.number().int().positive().max(150),
  name: z.string().min(1).max(100),
});

const validated = UserSchema.parse(untrustedInput);
```

## Secrets Management

```typescript
// ❌ NEVER DO THIS
const apiKey = 'sk-live-abc123xyz';

// ✅ DO THIS
const apiKey = process.env.API_KEY;
```

## Dependency Security

```bash
# Audit dependencies
npm audit

# Update vulnerable packages immediately
npm audit fix

# Use lock file for reproducible installs
npm ci  # not npm install in CI
```

## SQL Injection Prevention

```typescript
// ❌ NEVER: String concatenation
const query = `SELECT * FROM users WHERE id = ${userId}`;

// ✅ ALWAYS: Parameterized queries
const query = 'SELECT * FROM users WHERE id = $1';
const result = await db.query(query, [userId]);
```

---

# Development Workflow

## Commands

```bash
# Development
npm run dev          # Start dev server
npm run dev:debug    # Start with debugger

# Quality
npm run lint          # Run linter
npm run format        # Format code
npm run typecheck     # TypeScript check

# Testing
npm test              # Run tests
npm run test:watch    # Watch mode
npm run test:coverage # Coverage report

# Build
npm run build         # Production build
npm run preview       # Preview production build
```

## Environment Setup

Required `.env` variables:
- `DATABASE_URL` — PostgreSQL connection string
- `REDIS_URL` — Redis connection string
- `API_SECRET` — JWT signing secret
- `LOG_LEVEL` — debug|info|warn|error

Never commit `.env` files. Use `.env.example` as template.

---

# Configuration Files

This project uses:
- **ESLint** — Code linting (`.eslintrc.js`)
- **Prettier** — Code formatting (`.prettierrc`)
- **TypeScript** — Type checking (`tsconfig.json`)
- **Husky** — Git hooks (`.husky/`)

Run `npm run setup` after clone to install pre-commit hooks.

---

**End of rules. Follow these guidelines strictly.**