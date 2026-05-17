# Project Context

You are working in a modern software project with the following characteristics:

## Project Type

- **Language**: [JavaScript/TypeScript/Python/etc.]
- **Framework**: [React/Node.js/Django/etc.]
- **Package Manager**: [npm/yarn/pnpm/pip]
- **Node Version**: [version from package.json-engines]

## Directory Structure

```
/
├── src/                    # Source code
├── tests/                  # Test files (co-located or unit/)
├── docs/                   # Documentation
├── scripts/                 # Build/dev scripts
├── configs/                # Configuration files
├── public/                  # Static assets
├── package.json
├── tsconfig.json            # or jsconfig.json
├── .eslintrc.js
├── .prettierrc
└── CLAUDE.md               # This file
```

## Code Organization

1. **Components** — Place in `src/components/` or `src/<feature>/`
2. **Utilities** — Pure functions in `src/utils/`
3. **Services** — External integrations in `src/services/`
4. **Types** — Shared types in `src/types/` or `*.d.ts`
5. **Tests** — Next to source files (`*.test.ts`) or in `tests/`

---

# Code Style

## TypeScript/JavaScript

```typescript
// ✅ DO: Use descriptive names, explicit types, const
const fetchUserData = async (userId: string): Promise<User> => {
  const response = await api.get(`/users/${userId}`);
  return response.data;
};

// ❌ DON'T: Use abbreviations, implicit any, let
const getUser = async (id) => {
  let r = await api.get('/users/' + id);
  return r.data;
};
```

## Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Files | kebab-case | `user-profile.tsx` |
| Classes | PascalCase | `UserService` |
| Functions | camelCase | `fetchUserData` |
| Constants | UPPER_SNAKE | `MAX_RETRIES` |
| Types/Interfaces | PascalCase | `UserProfile` |
| React Components | PascalCase | `UserCard` |
| CSS Classes | kebab-case | `.user-profile` |

## Formatting Rules

- **Indent**: 2 spaces (no tabs)
- **Line length**: 100 characters max
- **Semicolons**: Yes
- **Quotes**: Single for strings
- **Trailing commas**: Yes, in multiline
- **Trailing newline**: Yes

## Import Order

```typescript
// 1. Node built-ins
import { readFile } from 'fs/promises';

// 2. External packages
import React from 'react';
import { debounce } from 'lodash';

// 3. Internal packages (if applicable)
import { utils } from '@project/utils';

// 4. Relative imports (grouped)
import { UserCard } from '../components/UserCard';
import { formatDate } from '../utils/date';
```

---

# Prohibited

## Code

- **No `any`** — Use `unknown` or specific types
- **No `// TODO: fix later`** — Address immediately or create ticket
- **No commented-out code** — Delete or use feature flags
- **No `console.log`** — Use proper logging (debug/info/warn/error)
- **No hardcoded values** — Use environment variables or constants
- **No duplicate code** — Extract to shared utilities
- **No magic numbers** — Define as named constants

## Git

- **No force pushes** to main/master
- **No direct commits** to protected branches
- **No secrets in code** — Use .env files, never commit credentials
- **No large files in git** — Use Git LFS for binaries > 5MB

## Dependencies

- **No unverified packages** — Check maintainers and download counts
- **No outdated packages** — Keep dependencies current
- **No unused dependencies** — Remove promptly

---

# Testing Requirements

## Coverage Gates

| Metric | Minimum |
|--------|---------|
| Line coverage | 80% |
| Function coverage | 90% |
| Branch coverage | 75% |

## Test Structure

```typescript
describe('UserService', () => {
  describe('fetchUserData', () => {
    it('should return user data for valid ID', async () => {
      // Arrange
      const userId = '123';

      // Act
      const result = await userService.fetchUserData(userId);

      // Assert
      expect(result).toMatchObject({
        id: '123',
        name: expect.any(String),
      });
    });

    it('should throw NotFoundError for invalid ID', async () => {
      await expect(userService.fetchUserData('invalid')).rejects.toThrow(NotFoundError);
    });
  });
});
```

## Test Naming

`describe` → Feature name
`it` → Expected behavior: "should do X when Y"

## Required Test Types

1. **Unit tests** — All functions/classes
2. **Integration tests** — API endpoints, DB operations
3. **E2E tests** — Critical user flows (login, checkout, etc.)

---

# Commit Conventions

## Format

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

## Types

| Type | Description |
|------|-------------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Formatting, no code change |
| `refactor` | Code change, no feature/fix |
| `test` | Adding or updating tests |
| `chore` | Build, tooling, dependencies |

## Examples

```bash
feat(auth): add OAuth2 login flow

- Add Google and GitHub providers
- Implement token refresh logic
- Store refresh tokens in HttpOnly cookies

Closes #123
```

```bash
fix(api): handle null user in getProfile

The endpoint crashed when userId was valid but user
was deleted from database. Now returns 404 instead.
```

## Rules

- Subject line: 50 chars max, no period
- Use imperative mood: "add" not "added"
- Reference issues: `Closes #123`, `Fixes #456`

---

# Security

## Input Validation

- Validate all user input at API boundary
- Sanitize data before rendering
- Use parameterized queries for DB

## Authentication

- Never store passwords in plaintext
- Use bcrypt/argon2 for password hashing
- Implement rate limiting on auth endpoints
- Token expiry: access 15min, refresh 7d

## Secrets Management

- Use environment variables for secrets
- Never commit `.env` files
- Rotate secrets regularly
- Use vault for production secrets

## Dependency Security

- Run `npm audit` or `pip audit` before each deploy
- Update dependencies for security patches within 48h
- Use Snyk/Dependabot for automated updates

---

# Additional Context

## Build Commands

```bash
npm run dev      # Start development
npm run build     # Production build
npm run test      # Run tests
npm run lint      # Lint code
npm run format    # Format code
```

## Environment Variables

Required in `.env`:
- `DATABASE_URL` — Database connection
- `API_KEY` — External API key
- `SECRET_KEY` — Session/encryption key

See `.env.example` for all variables.

---

**Last updated**: [YYYY-MM-DD] — Edit this file to update project context.