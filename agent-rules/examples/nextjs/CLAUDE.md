# Next.js Project Rules

> Template for Next.js applications using Claude Code.

---

## Project Structure (App Router)

```
/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── (routes)/          # Route groups
│   │   │   ├── page.tsx       # Page component
│   │   │   └── loading.tsx    # Loading state
│   │   ├── api/               # API routes
│   │   ├── layout.tsx         # Root layout
│   │   └── globals.css        # Global styles
│   ├── components/
│   │   ├── ui/                # Base components
│   │   ├── feature/           # Feature components
│   │   └── layout/            # Layout components
│   ├── hooks/                  # Custom hooks
│   ├── lib/                    # Utilities (db, auth, utils)
│   ├── services/               # Business logic
│   └── types/                  # TypeScript types
├── public/                     # Static assets
├── next.config.ts
├── tailwind.config.ts
└── tsconfig.json
```

## Component Types

### Server Components (default)

```tsx
// app/users/page.tsx
// This is a Server Component by default

import { db } from '@/lib/db';
import { UserCard } from '@/components/feature/UserCard';

// Server Components can:
// - Fetch data directly
// - Access backend resources
// - Use async/await

export default async function UsersPage() {
  const users = await db.user.findMany();

  return (
    <main className="container mx-auto py-8">
      <h1 className="text-3xl font-bold mb-6">Users</h1>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        {users.map((user) => (
          <UserCard key={user.id} user={user} />
        ))}
      </div>
    </main>
  );
}
```

### Client Components

```tsx
// components/feature/SearchInput.tsx
'use client';

import { useState, useCallback } from 'react';
import { useDebouncedCallback } from '@/hooks/useDebounce';

interface SearchInputProps {
  onSearch: (query: string) => void;
  className?: string;
}

export function SearchInput({ onSearch, className }: SearchInputProps) {
  const [value, setValue] = useState('');

  const debouncedSearch = useDebouncedCallback(
    (query: string) => onSearch(query),
    300
  );

  return (
    <input
      type="search"
      value={value}
      onChange={(e) => {
        setValue(e.target.value);
        debouncedSearch(e.target.value);
      }}
      className={className}
      placeholder="Search..."
    />
  );
}
```

---

## Prohibited

- ❌ `any` type (use `unknown` or specific types)
- ❌ `console.log` (use structured logger)
- ❌ Inline styles (use Tailwind)
- ❌ `.js` files (use `.ts`/`.tsx`)
- ❌ `use client` without need (default to Server Components)
- ❌ `getServerSideProps` (use App Router patterns)
- ❌ Secrets in code (use environment variables)
- ❌ Default exports (named exports only)

---

## Testing Requirements

### Jest + React Testing Library

```typescript
import { render, screen, waitFor } from '@testing-library/react';
import { userEvent } from '@testing-library/user-event';
import { SearchInput } from './SearchInput';

describe('SearchInput', () => {
  it('should debounce search calls', async () => {
    const handleSearch = vi.fn();
    render(<SearchInput onSearch={handleSearch} />);

    const input = screen.getByRole('searchbox');
    await userEvent.type(input, 'query');

    await waitFor(() => {
      expect(handleSearch).toHaveBeenCalledTimes(1);
    }, { timeout: 400 });
  });
});
```

### Coverage

- Line coverage: >= 80%
- Branch coverage: >= 75%
- Component coverage: >= 90%

---

## Commit Conventions

```
feat(app): add user profile page

- Server component fetches user data
- Suspense boundaries for loading states
- Client component for search functionality
- Incremental static regeneration enabled

Closes #456
```

---

## Security

### Server Actions

```typescript
'use server';

import { z } from 'zod';
import { revalidatePath } from 'next/cache';
import { db } from '@/lib/db';

const CreateUserSchema = z.object({
  name: z.string().min(1).max(100),
  email: z.string().email(),
});

export async function createUser(formData: FormData) {
  const validated = CreateUserSchema.parse(Object.fromEntries(formData));
  await db.user.create({ data: validated });
  revalidatePath('/users');
}
```

### Input Validation

```typescript
// Always validate on server, even if client validates
import { z } from 'zod';

const UserSchema = z.object({
  email: z.string().email('Invalid email'),
  name: z.string().min(1).max(100).trim(),
  age: z.coerce.number().int().min(0).max(150).optional(),
});
```

---

## Data Fetching Patterns

### Server Component Data Fetching

```typescript
// In Server Components - use fetch with cache tags
const users = await fetch('https://api.example.com/users', {
  next: { tags: ['users'], revalidate: 3600 },
  headers: { Authorization: `Bearer ${process.env.API_KEY}` },
});
```

### Route Handler

```typescript
// app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { db } from '@/lib/db';

export async function GET(request: NextRequest) {
  const users = await db.user.findMany();
  return NextResponse.json({ data: users });
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  const user = await db.user.create({ data: body });
  return NextResponse.json({ data: user }, { status: 201 });
}
```

---

## Commands

```bash
npm run dev           # Start development
npm run build         # Production build
npm run start         # Production server
npm lint              # Lint code
npm run format        # Format code
npm test              # Run tests
npm run test:watch    # Watch mode
```