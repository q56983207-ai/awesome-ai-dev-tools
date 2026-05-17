# Performance Prompts

Battle-tested prompts for optimization and efficiency improvements.

## 1. Performance Audit

```
Perform a comprehensive performance audit of this code.

Audit dimensions:
1. **CPU** - Computation complexity, algorithmic efficiency
2. **Memory** - Allocation patterns, garbage collection pressure
3. **I/O** - Disk operations, network calls, buffer sizes
4. **Concurrency** - Parallelization opportunities, lock contention

For each finding:
- Location and code snippet
- Performance impact (quantified if possible)
- Root cause
- Optimization approach
- Expected improvement

Deliverables:
1. **Hotspots list** - Top 5 performance issues ranked by impact
2. **Quick wins** - Easy fixes with big impact
3. **Architectural concerns** - Fundamental issues needing redesign
4. **Optimization roadmap** - Prioritized list with effort estimates

Include before/after benchmark estimates.
```

## 2. Query Optimization

```
Optimize these database queries.

Current query: [SQL or ORM code]
Execution context: [table sizes, indexes, frequency]

Analysis:
1. **EXPLAIN output** - How is the query executed?
2. **Index usage** - Are indexes being used effectively?
3. **Data volume** - How many rows are processed?
4. **N+1 problems** - Are there hidden loops?

For each issue:
- Problem description
- Why it causes slowdown
- Optimization approach
- Improved query

Alternative approaches:
- Denormalization
- Materialized views
- Query caching
- Pagination
- Batch operations

Provide optimized version with explanation of changes.
```

## 3. Caching Strategy

```
Design a caching strategy for: [describe the system/use case]

Caching layers to consider:
1. **Browser cache** - Static assets, API responses
2. **CDN** - Edge caching for static content
3. **Application cache** - In-memory (Redis, Memcached)
4. **Database cache** - Query results, computed values

For each cache layer:
- What to cache
- TTL strategy
- Invalidation approach
- Hit rate target

Cache patterns:
- **Cache-aside** (lazy loading)
- **Write-through** (eager update)
- **Read-through** (transparent)
- **Refresh-ahead** (proactive refresh)

Implementation checklist:
- [ ] Cache key strategy
- [ ] Serialization format
- [ ] Eviction policy (LRU, TTL, etc.)
- [ ] Failure handling (cache miss → DB)
- [ ] Monitoring and alerts

Provide configuration and code examples.
```

## 4. Algorithm Optimization

```
Optimize the algorithm in this code.

Current implementation: [code]
Constraints: [time/space limits, data sizes]

Analysis:
1. **Current complexity** - Big-O notation
2. **Bottleneck type** - CPU-bound, I/O-bound, memory-bound
3. **Data characteristics** - Size, distribution, patterns

Optimization techniques:
1. **Algorithmic** - Better data structure or approach
2. **Data-oriented** - Cache-friendly access patterns
3. **Parallelization** - Divide work across cores/threads
4. **Approximation** - Trading accuracy for speed (if acceptable)

For each optimization:
- Original vs optimized approach
- Complexity improvement
- Code implementation
- Trade-off analysis

Benchmark results:
| Operation | Before | After | Improvement |
|-----------|--------|-------|-------------|
| [op1]     | time   | time  | %           |
```

## 5. Memory Optimization

```
Optimize memory usage in this code.

Current behavior: [describe what's happening]
Memory constraints: [available RAM, per-request limits]

Memory issues to address:
1. **Allocation patterns** - Too many allocations, premature allocation
2. **Data structure efficiency** - Over-allocated or under-utilized
3. **Leak sources** - Unreleased resources, retained references
4. **Copy overhead** - Unnecessary data copying

Optimization strategies:
- Object pooling / reuse
- Lazy initialization
- Weak references where appropriate
- Compact data structures
- Streaming / lazy evaluation

For each fix:
- Problem: What causes memory bloat
- Solution: Specific change to make
- Impact: Estimated memory reduction
- Trade-off: What might get slower/more complex

Provide code changes with memory before/after estimates.
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*