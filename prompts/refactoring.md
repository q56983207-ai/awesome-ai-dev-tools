# Refactoring Prompts

Battle-tested prompts for code quality improvement and architectural enhancements.

## 1. General Refactoring

```
Act as an expert refactoring specialist. Transform the following code while preserving all existing behavior.

Refactoring goals:
1. **Eliminate code smells** - Duplication, long methods, dead code
2. **Improve readability** - Clear naming, logical structure
3. **Enhance maintainability** - Loose coupling, high cohesion
4. **Prepare for extension** - Open for modification, closed for changes

Process:
1. Analyze current structure and identify issues
2. List specific refactorings to apply (with rationale)
3. Show before/after code for each change
4. Verify behavior preservation through explanation

Important constraints:
- No functional changes, only structural
- All tests must continue to pass
- Keep changes atomic and reversible
- Document the "why" behind each decision

End with a summary of what was changed and why.
```

## 2. Extract Method Refactoring

```
Given the following code section, identify and extract logical units into well-named functions.

Target extraction patterns:
- Functions exceeding 20 lines
- Blocks with a single responsibility
- Repeated code sequences
- Complex conditional logic
- Nested loops that could be separate operations

For each extraction:
1. **What**: Name the new function
2. **Why**: Specific refactoring motivation
3. **Before**: Original code
4. **After**: Extracted code with call site
5. **Contract**: Parameters and return value

Ensure:
- New functions have single responsibility
- Parameters are at appropriate abstraction level
- Return types are clear and useful
- Side effects are documented
```

## 3. Design Pattern Application

```
Analyze this code and identify opportunities to apply appropriate design patterns.

Available patterns to consider:
- **Creational**: Factory, Builder, Singleton, Prototype
- **Structural**: Adapter, Decorator, Facade, Proxy
- **Behavioral**: Strategy, Observer, Command, State, Template Method

For each pattern opportunity:
1. **Current problem**: Specific code smell or architectural issue
2. **Pattern recommendation**: Why this pattern fits
3. **Application approach**: Step-by-step implementation plan
4. **Code transformation**: Before → After
5. **Benefits**: What improvement this delivers

Also note:
- Patterns that could work but may be over-engineering (flag as "avoid")
- Anti-patterns currently in use
- Migration risks and mitigation

End with a prioritized recommendation list.
```

## 4. Legacy Code Refactoring

```
You are helping refactor legacy code. The goal is to make it testable and maintainable without breaking existing functionality.

Challenge: Code that is difficult to test usually has:
- Hidden dependencies (global state, singletons)
- Tight coupling to infrastructure
- Missing interfaces
- Unclear responsibilities

Refactoring strategy (Michael Feathers approach):
1. **Seam identification** - Find points where behavior can vary
2. **Targeted modification** - Introduce change without breaking tests
3. **Characterization tests** - Lock down current behavior before changing
4. **Interdependency breaking** - Introduce testability (parameterize, extract interfaces)
5. **Incremental improvement** - Small, safe steps toward better design

For this code:
- Identify the seams
- Propose minimal changes to enable testing
- Suggest a phased migration path
- Highlight risks and how to mitigate them

Prioritize changes that reduce risk while maximizing future flexibility.
```

## 5. API Refactoring

```
Refactor this code's API to be cleaner, more intuitive, and more maintainable.

Consider:
1. **Naming**: Do names clearly express intent?
2. **Signature**: Are parameters at the right abstraction level?
3. **Defaults**: Can sensible defaults reduce cognitive load?
4. **Consistency**: Does API follow uniform conventions?
5. ** discoverability**: Can users understand usage without reading internals?

For each issue:
- Current state and problem
- Refactored proposal with code
- Migration path for existing callers
- Breaking change considerations (if any)

API quality checklist:
- [ ] Purpose is obvious from name
- [ ] Required vs optional params are clear
- [ ] Return type is predictable
- [ ] Error cases are handled gracefully
- [ ] Behavior is consistent with similar APIs in codebase

Provide before/after for each significant change.
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*