# React Project Rules

> Template for React applications using Claude Code.

---

## Project Structure

```
src/
├── components/
│   ├── ui/              # Base components (Button, Input, Card)
│   ├── layout/          # Layout components (Header, Footer, Sidebar)
│   └── feature/         # Feature-specific components
├── hooks/               # Custom React hooks
├── services/            # API clients (React Query, SWR)
├── utils/              # Pure utility functions
├── types/               # TypeScript type definitions
├── stores/             # State management (Zustand/Redux)
└── pages/              # Page components (if not using App Router)
```

## Component Structure

```tsx
// Component file structure
import React, { useState, useCallback } from 'react';
import { cn } from '@/lib/utils';

interface ComponentProps {
  title: string;
  onAction: (value: string) => void;
  className?: string;
}

export function Component({ title, onAction, className }: ComponentProps) {
  const [value, setValue] = useState('');

  const handleSubmit = useCallback(() => {
    onAction(value);
    setValue('');
  }, [value, onAction]);

  return (
    <div className={cn('component', className)}>
      <h2>{title}</h2>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}
```

---

## Code Style

### Hooks

```typescript
// Custom hook structure
export function useUserData(userId: string) {
  const [data, setData] = useState<User | null>(null);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);

  useEffect(() => {
    let cancelled = false;

    async function fetchUser() {
      try {
        setIsLoading(true);
        const result = await userApi.getUser(userId);
        if (!cancelled) setData(result);
      } catch (err) {
        if (!cancelled) setError(err as Error);
      } finally {
        if (!cancelled) setIsLoading(false);
      }
    }

    fetchUser();
    return () => { cancelled = true; };
  }, [userId]);

  return { data, isLoading, error };
}
```

### State Management

```typescript
// Zustand store example
import { create } from 'zustand';

interface UserStore {
  user: User | null;
  isLoading: boolean;
  setUser: (user: User | null) => void;
  clearUser: () => void;
}

export const useUserStore = create<UserStore>((set) => ({
  user: null,
  isLoading: false,
  setUser: (user) => set({ user }),
  clearUser: () => set({ user: null }),
}));
```

---

## Prohibited

- ❌ Class components (use functional components)
- ❌ `any` type (use `unknown` or specific types)
- ❌ `console.log` (use logger)
- ❌ Inline styles (use Tailwind or CSS modules)
- ❌ Prop drilling (use Context or state management)
- ❌ Default exports (named exports only)

---

## Testing Requirements

### Test Library

```typescript
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import { userEvent } from '@testing-library/user-event';

describe('UserCard', () => {
  it('should display user name', async () => {
    render(<UserCard user={{ id: '1', name: 'Alice' }} />);
    expect(screen.getByText('Alice')).toBeInTheDocument();
  });

  it('should call onClick when clicked', async () => {
    const handleClick = vi.fn();
    render(<UserCard user={{ id: '1' }} onClick={handleClick} />);
    await userEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledOnce();
  });
});
```

### Coverage

- Component coverage: 90%
- Hook coverage: 100%
- Critical paths: 100%

---

## Commit Conventions

```
feat(component): add UserCard with avatar support

- Display user avatar or initials fallback
- Show name and email
- Add loading skeleton state
- Include click handler prop

Closes #123
```

---

## Security

### XSS Prevention

```tsx
// ❌ Never do this
<div dangerouslySetInnerHTML={{ __html: userInput }} />

// ✅ Use sanitization
import DOMPurify from 'dompurify';
<div>{DOMPurify.sanitize(userInput)}</div>
```

### Input Validation

```typescript
import { z } from 'zod';

const UserFormSchema = z.object({
  email: z.string().email(),
  name: z.string().min(1).max(100),
  age: z.number().int().min(0).max(150).optional(),
});
```

---

## Commands

```bash
npm run dev        # Start development
npm run build      # Production build
npm run preview    # Preview production build
npm test           # Run tests
npm run lint       # Lint code
npm run format     # Format code
```