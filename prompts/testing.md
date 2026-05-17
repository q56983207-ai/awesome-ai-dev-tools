# Testing Prompts

Battle-tested prompts for comprehensive test generation and testing strategy.

## 1. Unit Test Generation

```
Generate comprehensive unit tests for the following code.

Requirements:
1. **Arrange-Act-Assert** pattern for each test
2. **Descriptive test names**: GivenWhenThen format
3. **Edge case coverage**: Null, empty, boundary values, exceptions
4. **Mock external dependencies**: Use appropriate mocking framework
5. **Single assertion focus**: Each test one logical assertion

For each test:
- Test name (describes the scenario being tested)
- Input values
- Expected behavior
- Edge cases covered

Testing checklist:
- [ ] Happy path works
- [ ] Null/undefined inputs handled
- [ ] Empty collections handled
- [ ] Boundary conditions tested
- [ ] Exception paths covered
- [ ] Mock expectations verified

Use [Jest/Vitest/Pytest/JUnit] format and include imports.
```

## 2. Integration Test Design

```
Design integration tests for this module/component.

Integration tests verify that components work together correctly.

Coverage areas:
1. **API endpoints** - Request/response contracts, status codes
2. **Database operations** - CRUD, transactions, migrations
3. **External services** - API calls, message queues, caches
4. **Authentication/Authorization** - Permission flows
5. **Error propagation** - How errors bubble up and are handled

For each test scenario:
1. **Setup**: Preconditions and test data
2. **Action**: The operation being tested
3. **Verification**: Expected outcomes
4. **Cleanup**: Reset state (use fixtures/teardown)

Important:
- Tests should be independent (no order dependency)
- Use real infrastructure where possible (or realistic mocks)
- Include both positive and negative cases
- Verify side effects (logs, events, state changes)

Provide the test structure and key scenarios.
```

## 3. Property-Based Testing

```
Generate property-based tests for this function/class.

Property-based testing validates invariants across many random inputs.

Identify:
1. **Properties** - Statements that should always be true
   - Symmetry (round-trip conversions)
   - Invariants (output always valid regardless of input)
   - Idempotence (calling twice = calling once)
   - Monotonicity (increasing input → increasing output)

2. **Generators** - How to produce random valid inputs
   - Primitives (int, string, bool)
   - Collections (non-empty, specific sizes)
   - Edge cases (min/max values, special characters)

3. **Shrinking** - How to simplify failing inputs to minimal reproductions

For each property:
- Property description
- Test implementation
- Why this property matters
- How it would catch real bugs

Use [Hypothesis/Property-Based Testing library] format.
```

## 4. Test-Driven Development (TDD) Session

```
Let's practice TDD. Given the following requirements, we'll work in red-green-refactor cycles.

Requirements:
[Insert functional requirements here]

Process:
1. **Red**: Write a failing test that describes the next piece of functionality
2. **Green**: Write minimal code to make the test pass
3. **Refactor**: Improve code while keeping tests green

Constraints:
- Never write production code without a failing test
- Never write more of a test than needed to fail
- Never write more production code than needed to pass

For this session:
1. Identify the first test case (simplest behavior)
2. Write the test
3. Implement the minimum to pass
4. Verify all tests pass
5. Refactor if needed
6. Move to next test case

Track: tests written, tests passing, refactoring opportunities.
```

## 5. Mock & Stub Strategy

```
Create a comprehensive mocking strategy for testing this component.

Mocking philosophy:
- Mock external dependencies (databases, APIs, services)
- Don't mock value objects or simple data structures
- Verify mock interactions (not just return values)
- Keep mocks close to reality (avoid over-specifying)

For each dependency to mock:
1. **What**: Dependency name and interface
2. **Why mocked**: External, non-deterministic, or slow
3. **How**: Mock setup (stubs, spies, expectations)
4. **Verification**: What interactions to verify

Test double types:
- **Dummy**: Passed but never used
- **Fake**: Working implementation (in-memory DB)
- **Stub**: Returns canned responses
- **Spy**: Records how it was called
- **Mock**: Pre-programmed expectations

Provide implementation for each mock with verification calls.
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*