# Node.js Project Rules

> Template for Node.js applications using Claude Code.

---

## Project Structure

```
/
├── src/
│   ├── routes/           # Express/Fastify routes
│   ├── controllers/      # Request handlers
│   ├── services/         # Business logic
│   ├── models/          # Data models
│   ├── middleware/       # Express middleware
│   ├── utils/            # Utility functions
│   ├── types/            # TypeScript types
│   └── index.ts          # Entry point
├── tests/
│   ├── unit/             # Unit tests
│   ├── integration/      # Integration tests
│   └── fixtures/        # Test fixtures
├── configs/              # Configuration files
├── scripts/              # Build scripts
└── package.json
```

## Architecture

```
Request → Middleware → Controller → Service → Model → Database
                ↓
           Error Handler
```

---

## Code Style

### Express/Fastify Handler

```typescript
// Handler structure
import { Request, Response, NextFunction } from 'express';

interface UserControllerDeps {
  userService: UserService;
}

export function createUserController(deps: UserControllerDeps) {
  return {
    async create(req: Request, res: Response, next: NextFunction) {
      try {
        const { name, email } = req.body;
        const user = await deps.userService.create({ name, email });
        res.status(201).json({ data: user });
      } catch (error) {
        next(error);
      }
    },

    async getById(req: Request, res: Response, next: NextFunction) {
      try {
        const { id } = req.params;
        const user = await deps.userService.findById(id);
        if (!user) {
          return res.status(404).json({ error: 'User not found' });
        }
        res.json({ data: user });
      } catch (error) {
        next(error);
      }
    },
  };
}
```

### Service Layer

```typescript
// Service structure
export class UserService {
  constructor(
    private readonly userRepo: UserRepository,
    private readonly emailService: EmailService,
  ) {}

  async create(data: CreateUserInput): Promise<User> {
    const existing = await this.userRepo.findByEmail(data.email);
    if (existing) {
      throw new ConflictError('Email already in use');
    }

    const hashedPassword = await bcrypt.hash(data.password, 12);
    const user = await this.userRepo.create({
      ...data,
      password: hashedPassword,
    });

    await this.emailService.sendWelcome(user);
    return user;
  }
}
```

---

## Prohibited

- ❌ `any` type (use `unknown` or specific types)
- ❌ `console.log` (use structured logger)
- ❌ Callback-style code (use async/await)
- ❌ String concatenation in SQL (use parameterized queries)
- ❌ Synchronous file I/O in request handlers
- ❌ Global mutable state
- ❌ Secrets in code (use environment variables)

---

## Testing Requirements

### Unit Test

```typescript
import { describe, it, expect, vi, beforeEach } from 'vitest';
import { UserService } from '@/services/userService';

describe('UserService', () => {
  let userRepo: MockRepository;
  let emailService: MockEmailService;
  let service: UserService;

  beforeEach(() => {
    userRepo = createMockRepository();
    emailService = createMockEmailService();
    service = new UserService(userRepo, emailService);
  });

  describe('create', () => {
    it('should create user with hashed password', async () => {
      userRepo.findByEmail.mockResolvedValue(null);
      userRepo.create.mockImplementation(async (data) => ({ id: '1', ...data }));
      emailService.sendWelcome.mockResolvedValue(undefined);

      const user = await service.create({
        name: 'Alice',
        email: 'alice@example.com',
        password: 'plain123',
      });

      expect(user.password).not.toBe('plain123');
      expect(bcrypt.compare('plain123', user.password)).resolves.toBe(true);
    });

    it('should throw ConflictError for duplicate email', async () => {
      userRepo.findByEmail.mockResolvedValue({ id: 'existing' });

      await expect(
        service.create({ name: 'Alice', email: 'existing@example.com', password: '123' })
      ).rejects.toThrow(ConflictError);
    });
  });
});
```

### Integration Test

```typescript
import request from 'supertest';
import { app } from '@/app';
import { createTestDb, cleanTestDb } from '@/tests/fixtures';

describe('POST /users', () => {
  beforeEach(() => cleanTestDb());
  afterAll(() => createTestDb().destroy());

  it('should create user and return 201', async () => {
    const response = await request(app)
      .post('/users')
      .send({ name: 'Alice', email: 'alice@example.com', password: 'password123' })
      .expect(201);

    expect(response.body.data).toMatchObject({
      id: expect.any(String),
      name: 'Alice',
      email: 'alice@example.com',
    });
    expect(response.body.data.password).toBeUndefined();
  });
});
```

---

## Commit Conventions

```
feat(api): add user registration endpoint

POST /users accepts { name, email, password }
Returns 201 with user object (password excluded)
Sends welcome email on success

Closes #234
```

---

## Security

### Input Validation

```typescript
import { z } from 'zod';

const CreateUserSchema = z.object({
  name: z.string().min(1).max(100),
  email: z.string().email(),
  password: z.string().min(8).regex(/[A-Z]/, 'Password must contain uppercase'),
});

export function validateUserInput(body: unknown) {
  return CreateUserSchema.parse(body);
}
```

### Rate Limiting

```typescript
import rateLimit from 'express-rate-limit';

const authLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 5, // 5 attempts per window
  message: { error: 'Too many attempts, please try again later' },
  standardHeaders: true,
  legacyHeaders: false,
});

app.use('/auth/login', authLimiter);
app.use('/auth/register', authLimiter);
```

---

## Commands

```bash
npm run dev           # Development server
npm run build         # Production build
npm run start         # Production server
npm test              # Run tests
npm run test:watch    # Watch mode
npm run lint          # Lint code
npm run format        # Format code
```