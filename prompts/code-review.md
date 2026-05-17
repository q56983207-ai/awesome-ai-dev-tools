# Code Review Prompts

Battle-tested prompts for systematic code analysis and improvement.

## 1. Comprehensive Code Review

```
Act as a senior code reviewer with 15+ years of experience. Perform a thorough review of the following code:

Focus areas:
1. **Correctness** - Logic errors, off-by-one bugs, edge cases
2. **Performance** - Algorithmic efficiency, unnecessary iterations, memory issues
3. **Security** - Injection vulnerabilities, input validation, authentication/authorization flaws
4. **Maintainability** - Code clarity, naming conventions, comments adequacy
5. **Testing** - Coverage gaps, missing edge case tests

Output format:
- Severity: [Critical/High/Medium/Low]
- Location: [File:Line]
- Issue description
- Recommended fix with code example

Provide a summary with the top 3 priorities for immediate action.
```

## 2. Security-First Review

```
Perform a security-focused code review. Treat this code as potentially hostile (user input, network data, etc.).

Check for:
1. Injection attacks (SQL, XSS, Command, LDAP, XML, ORM)
2. Authentication/authorization bypass
3. Cryptographic failures (weak algorithms, hardcoded secrets, insecure RNG)
4. Data exposure (logging sensitive info, insecure storage)
5. Race conditions and concurrency issues

For each finding:
- Attack vector
- Impact assessment
- Exploitation scenario
- Remediation priority (1-3)
- Secure code sample

End with a risk summary: [Critical/High/Medium/Low] overall rating.
```

## 3. Performance Review

```
Analyze the following code for performance issues. Consider both runtime efficiency and resource usage.

Examine:
1. Algorithmic complexity (O(n), O(n²), etc.)
2. Database query efficiency (N+1 problems, missing indexes, full scans)
3. Memory allocation patterns (unnecessary copies, leaks, excessive allocation)
4. I/O operations (blocking calls, sequential vs parallel)
5. Caching opportunities

For each issue:
- Current bottleneck
- Benchmark data (if applicable)
- Optimization approach
- Expected improvement
- Trade-offs to consider

Include a prioritized optimization roadmap.
```

## 4. Test Coverage Review

```
Review this code's test coverage. Assume you have full access to the test suite and codebase.

Evaluate:
1. **Boundary coverage** - All edge cases tested
2. **Error path coverage** - Exception handling tested
3. **Integration points** - External dependencies mocked appropriately
4. **State transitions** - Stateful code paths tested
5. **Regression risk** - Critical paths have regression protection

For each gap:
- Missing test scenario
- Why it matters (defect probability × impact)
- Test template showing what to add

Provide a coverage score (0-100%) with top 5 gaps to fix.
```

## 5. PR Review Summary

```
You are reviewing a Pull Request. The branch contains new code changes that need thorough review.

Context:
- [What this PR does]
- [Why this change is needed]
- [Related issues/tickets]

Review checklist:
1. Does the implementation match the stated requirements?
2. Are there any unintended side effects?
3. Is the code maintainable for the team?
4. Do tests adequately cover new behavior?
5. Is documentation updated where needed?

Format your review as:
- **Summary**: One paragraph overview
- **Approve/Conditional-Approve/Request Changes**
- **Required Changes** (if any): Must be addressed before merge
- **Suggestions** (if any): Optional improvements
- **Questions**: Things that need clarification

Be constructive and specific. Every comment should include actionable guidance.
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*