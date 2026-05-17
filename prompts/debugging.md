# Debugging Prompts

Battle-tested prompts for systematic issue diagnosis and resolution.

## 1. Systematic Debugging

```
Debug the following issue systematically. Apply the scientific method:

1. **Reproduce** - Create minimal reproduction steps
2. **Hypothesize** - What's causing this based on symptoms?
3. **Test** - Verify or eliminate the hypothesis
4. **Analyze** - Dig deeper into root cause
5. **Fix** - Implement and validate the solution

For each step:
- What you did
- What you observed
- What you concluded

Issue context:
- Error message: [What is shown]
- Expected behavior: [What should happen]
- Actual behavior: [What happens instead]
- Environment: [Versions, config, OS]

Provide:
- Root cause analysis
- Fix implementation
- Verification steps
- Prevention measures
```

## 2. Memory Leak Detection

```
Analyze this code for potential memory leaks.

Memory leak patterns to identify:
1. **Unreleased resources** - Files, handles, connections not closed
2. **Cached items** - unbounded caches growing indefinitely
3. **Event listener leaks** - listeners added but never removed
4. **Closure retention** - closures capturing large objects
5. **Circular references** - objects referencing each other

For each potential leak:
- Location in code
- Why it's a problem
- Memory impact assessment
- Fix recommendation
- Detection method (profiler output, heap snapshot)

Include:
- heap analysis approach
- profiling tools to use
- Expected memory growth pattern
```

## 3. Race Condition Finder

```
Analyze this concurrent code for race conditions and thread safety issues.

Concurrency patterns to check:
1. **Read-modify-write** - non-atomic compound operations
2. **Check-then-act** - time-of-check to time-of-use bugs
3. **Double-checked locking** - improper synchronization
4. **Deadlock potential** - lock ordering issues
5. **Starvation** - threads unable to progress

For each issue:
- Location and code snippet
- Race condition type
- Trigger scenario
- Impact (data corruption, crash, deadlock)
- Fix with corrected code

Also identify:
- Missing synchronization
- Incorrect lock granularity
- Potential deadlocks
- Thread-safe alternatives

Provide corrected implementation with explanation.
```

## 4. Performance Bug Investigation

```
Investigate this performance issue. Symptoms and context:

[Describe performance problem - slow response, high latency, etc.]

Investigation approach:
1. **Baseline** - Establish current performance metrics
2. **Profile** - Identify hotspots (CPU, memory, I/O)
3. **Isolate** - Find the specific code path causing issue
4. **Quantify** - Measure impact of each contributing factor
5. **Optimize** - Apply targeted fix
6. **Verify** - Confirm improvement and no regressions

For each bottleneck identified:
- Location and code
- Call frequency and impact
- Why it's slow (algorithm, I/O, allocation, etc.)
- Optimization approach
- Expected improvement

Provide:
- Root cause summary
- Specific fix recommendations
- Benchmark results before/after
```

## 5. Exception Stack Trace Analysis

```
Analyze this stack trace to understand the failure chain.

Stack trace:
[Provide stack trace]

Analysis approach:
1. **Entry point** - Where did execution start?
2. **Call chain** - What sequence led to the error?
3. **Error origin** - Where was the exception thrown?
4. **Failure point** - Which line caused the actual failure?

For each relevant frame:
- File:Line
- Method signature
- Local variable state (if visible)
- What it was trying to accomplish

Identify:
- Whether the exception propagated or was caught
- If there are nested exceptions (cause chain)
- What null/undefined values triggered the issue
- Whether this is a first occurrence or recurring

Provide:
- Root cause (the actual issue, not just the symptom)
- Fix recommendation
- Prevention (null checks, validation, etc.)
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*