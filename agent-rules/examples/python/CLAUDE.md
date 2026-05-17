# Python Project Rules

> Template for Python applications using Claude Code.

---

## Project Structure

```
/
├── src/
│   ├── api/              # FastAPI routes
│   ├── models/          # Pydantic models, SQLAlchemy
│   ├── services/        # Business logic
│   ├── repositories/    # Data access layer
│   ├── middleware/      # Custom middleware
│   └── main.py          # Entry point
├── tests/
│   ├── unit/            # Unit tests
│   ├── integration/      # Integration tests
│   └── fixtures/        # Test fixtures
├── alembic/             # Database migrations
├── configs/             # Configuration files
└── pyproject.toml
```

## Architecture (Clean Architecture)

```
API Layer → Service Layer → Repository Layer → Database
     ↓
   Models
```

---

## Code Style

### FastAPI Route

```python
from fastapi import APIRouter, Depends, HTTPException, status
from pydantic import BaseModel, EmailStr, field_validator
from typing import Annotated

router = APIRouter(prefix="/users", tags=["users"])


class CreateUserRequest(BaseModel):
    name: str
    email: EmailStr
    password: str

    @field_validator("name")
    @classmethod
    def name_must_not_be_empty(cls, v: str) -> str:
        if not v or not v.strip():
            raise ValueError("Name cannot be empty")
        return v.strip()

    @field_validator("password")
    @classmethod
    def password_min_length(cls, v: str) -> str:
        if len(v) < 8:
            raise ValueError("Password must be at least 8 characters")
        return v


@router.post("/", status_code=status.HTTP_201_CREATED)
async def create_user(
    request: CreateUserRequest,
    user_service: Annotated[UserService, Depends(get_user_service)],
) -> UserResponse:
    try:
        user = await user_service.create(
            name=request.name,
            email=request.email,
            password=request.password,
        )
        return UserResponse.model_validate(user)
    except DuplicateEmailError as e:
        raise HTTPException(
            status_code=status.HTTP_409_CONFLICT,
            detail=str(e),
        )
```

### Service Layer

```python
from typing import Protocol
from abc import ABC, abstractmethod


class UserRepository(Protocol):
    async def find_by_email(self, email: str) -> User | None: ...
    async def create(self, user: User) -> User: ...


class UserService:
    def __init__(self, user_repo: UserRepository) -> None:
        self._user_repo = user_repo

    async def create(self, name: str, email: str, password: str) -> User:
        existing = await self._user_repo.find_by_email(email)
        if existing:
            raise DuplicateEmailError(f"Email {email} already registered")

        hashed = hash_password(password)
        user = User(name=name, email=email, password_hash=hashed)
        return await self._user_repo.create(user)
```

---

## Prohibited

- ❌ `except Exception:` (catch specific exceptions)
- ❌ `any` type hints (use `Unknown` or specific types)
- ❌ `print()` (use structured logging)
- ❌ String concatenation in SQL (use parameterized queries)
- ❌ Global mutable state
- ❌ Secrets in code (use environment variables)
- ❌ Synchronous DB operations in async endpoints

---

## Testing Requirements

### Pytest

```python
import pytest
from unittest.mock import AsyncMock, MagicMock
from src.services.user_service import UserService, DuplicateEmailError
from src.models.user import User


@pytest.fixture
def mock_repo() -> AsyncMock:
    return AsyncMock()


@pytest.fixture
def user_service(mock_repo: AsyncMock) -> UserService:
    return UserService(user_repo=mock_repo)


class TestUserService:
    @pytest.mark.asyncio
    async def test_create_user_success(
        self,
        user_service: UserService,
        mock_repo: AsyncMock,
    ) -> None:
        mock_repo.find_by_email.return_value = None
        mock_repo.create.return_value = User(
            id="1",
            name="Alice",
            email="alice@example.com",
            password_hash="hashed",
        )

        user = await user_service.create(
            name="Alice",
            email="alice@example.com",
            password="secure123",
        )

        assert user.id == "1"
        assert user.email == "alice@example.com"
        assert mock_repo.create.called

    @pytest.mark.asyncio
    async def test_create_user_duplicate_email(
        self,
        user_service: UserService,
        mock_repo: AsyncMock,
    ) -> None:
        mock_repo.find_by_email.return_value = User(
            id="existing",
            name="Bob",
            email="alice@example.com",
            password_hash="hash",
        )

        with pytest.raises(DuplicateEmailError):
            await user_service.create(
                name="Alice",
                email="alice@example.com",
                password="secure123",
            )
```

### Coverage

| Metric | Minimum |
|--------|---------|
| Line coverage | 80% |
| Branch coverage | 75% |
| Function coverage | 90% |

---

## Commit Conventions

```
feat(api): add user registration endpoint

POST /users accepts { name, email, password }
Returns 201 with user object (password excluded)
Validates email format and password strength

Closes #345
```

---

## Security

### Input Validation with Pydantic

```python
from pydantic import BaseModel, EmailStr, field_validator
from typing import Annotated

class UserInput(BaseModel):
    email: EmailStr  # Validates email format automatically
    name: str
    password: str

    @field_validator("password")
    @classmethod
    def password_strength(cls, v: str) -> str:
        if len(v) < 8:
            raise ValueError("Password must be at least 8 characters")
        if not re.search(r"[A-Z]", v):
            raise ValueError("Password must contain uppercase letter")
        return v
```

### SQL Injection Prevention

```python
# ❌ NEVER do this
query = f"SELECT * FROM users WHERE id = {user_id}"

# ✅ DO this with SQLAlchemy
result = session.execute(
    select(User).where(User.id == user_id)
)
```

### Secrets

```python
# ✅ Correct
import os
api_key = os.environ.get("API_KEY")

# ❌ Wrong
api_key = "sk-live-secret123"
```

---

## Commands

```bash
# Development
uv run uvicorn src.main:app --reload
python -m pytest tests/ -v

# Quality
python -m mypy src/
python -m ruff check .
python -m ruff format .

# Database
alembic upgrade head
alembic migrate -m "description"
```