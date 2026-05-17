# Architecture Prompts

Battle-tested prompts for system design and technical decision-making.

## 1. System Design Review

```
Design a system architecture for: [describe the problem]

Requirements:
- Functional: [what it must do]
- Non-functional: [scale, latency, availability, etc.]

Provide:
1. **High-level architecture** - Components and their responsibilities
2. **Data flow** - How data moves through the system
3. **Technology choices** - Why each technology was selected
4. **Scalability approach** - How to handle growth
5. **Failure modes** - What can fail, how system degrades
6. **Trade-offs** - What was prioritized and why

Include diagrams (ASCII or Mermaid) showing:
- Component interactions
- Data storage layers
- API boundaries
- External service integrations

Consider: microservices vs monolith, sync vs async, shared DB vs per-service.
```

## 2. API Design

```
Design a REST API for: [describe the resource/domain]

Requirements:
1. **Resources** - What are the main entities?
2. **Operations** - What actions are needed?
3. **Constraints** - Any performance, security, or compatibility requirements?

Design output:
1. **Endpoint structure** - URL design following REST conventions
2. **HTTP methods** - Appropriate use of GET/POST/PUT/DELETE/PATCH
3. **Status codes** - Meaningful and consistent
4. **Request/response schemas** - JSON with examples
5. **Error handling** - Consistent error format
6. **Pagination** - For collection endpoints
7. **Versioning strategy** - How to evolve the API

Example format:
```
GET    /users          - List users (paginated)
POST   /users          - Create user
GET    /users/:id      - Get user
PUT    /users/:id      - Update user
DELETE /users/:id      - Delete user
```

For each endpoint: method, path, purpose, request, response, errors.
```

## 3. Database Schema Design

```
Design a database schema for: [describe the problem domain]

Design considerations:
1. **Normalization** - Reduce redundancy, ensure integrity
2. **Performance** - Indexes for frequent queries
3. **Evolution** - How to migrate without downtime
4. **Relationships** - One-to-many, many-to-many

Output for each table:
- Table name (singular, snake_case)
- Columns with types and constraints
- Primary key
- Indexes
- Foreign keys
- Relationships

Example:
\`\`\`sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_users_email ON users(email);
\`\`\`

Include:
- Entity relationship diagram
- Migration strategy
- Data retention policies
```

## 4. Microservices Decomposition

```
Decompose this monolithic application into microservices.

Current state: [describe current architecture]
Target: [what you want to achieve]

Decomposition criteria:
1. **Single responsibility** - Each service one bounded context
2. ** loose coupling** - Services communicate via contracts
3. **High cohesion** - Related functionality together
4. **Independent deployability** - Can deploy each service separately
5. **Team ownership** - Aligns with team structure

For each potential service:
- Name and bounded context
- Responsibility (what it owns/does)
- Data it manages
- APIs it exposes
- Dependencies (what it calls)
- How to communicate (sync REST, async events)

Also identify:
- Shared data (anti-pattern risk)
- Synchronization needs
- Transaction boundaries
- Migration path from current state
```

## 5. Technical Decision Record

```
Make a technical decision for: [describe the decision to make]

Options considered:
1. [Option A] - [description]
2. [Option B] - [description]
3. [Option C] - [description]

Decision criteria:
- [Criterion 1] - Weight: [high/medium/low]
- [Criterion 2] - Weight: [high/medium/low]

Analysis:
| Criterion | Option A | Option B | Option C |
|-----------|----------|----------|----------|
| [C1]      | rating   | rating   | rating   |
| [C2]      | rating   | rating   | rating   |

Recommendation: [Option X]

Justification:
- Why this option over others
- What risks are acceptable
- What trade-offs we're making

Implementation considerations:
- How to migrate
- Rollback plan
- Success metrics
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*