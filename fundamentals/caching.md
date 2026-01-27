# Caching

Caching is one of the most important techniques for improving system performance. This guide covers patterns, strategies, and real-world applications.

## Why Cache?

```
Without Cache:  Client → Server → Database (100ms)
With Cache:     Client → Server → Cache (5ms) ✓
                              ↓ (cache miss)
                           Database
```

**Benefits**:
- Reduced latency (memory vs disk)
- Reduced database load
- Improved throughput
- Cost savings

## Core Resources

| Resource | Description | Link |
|----------|-------------|------|
| Top 5 Caching Patterns | Comprehensive pattern guide | [Read](https://newsletter.systemdesign.one/p/caching-patterns) |
| Cache Consistency | Meta's 10 nines approach | [Read](https://newsletter.systemdesign.one/p/cache-consistency) |
| Redis Use Cases | Practical Redis applications | [Read](https://newsletter.systemdesign.one/p/redis-use-cases) |

## Caching Patterns

### Cache-Aside (Lazy Loading)

```
Read:
1. Check cache
2. If miss, read from DB
3. Write to cache
4. Return data

Write:
1. Write to DB
2. Invalidate cache
```

**Pros**: Only caches what's needed, cache failures don't break the app
**Cons**: Cache miss penalty, potential for stale data

### Write-Through

```
Write:
1. Write to cache
2. Cache writes to DB (synchronous)
3. Return success

Read:
1. Always read from cache (always fresh)
```

**Pros**: Data always consistent
**Cons**: Write latency, cache may store unused data

### Write-Behind (Write-Back)

```
Write:
1. Write to cache
2. Return success immediately
3. Cache writes to DB asynchronously

Read:
1. Read from cache
```

**Pros**: Low write latency, batching possible
**Cons**: Data loss risk, complexity

### Read-Through

```
Read:
1. Request from cache
2. Cache fetches from DB if miss
3. Cache stores and returns data
```

**Pros**: Simpler application code
**Cons**: Initial request latency

### Refresh-Ahead

```
1. Track access patterns
2. Predictively refresh before expiry
3. Always serve from cache
```

**Pros**: No cache miss latency for hot data
**Cons**: Complexity, wasted refreshes

## Cache Invalidation

> "There are only two hard things in Computer Science: cache invalidation and naming things." — Phil Karlton

### Strategies

| Strategy | How | When |
|----------|-----|------|
| **TTL** | Expire after time | Tolerant of staleness |
| **Event-driven** | Invalidate on write | Need consistency |
| **Version-based** | New version = new key | Immutable data |

### Common Problems

| Problem | Cause | Solution |
|---------|-------|----------|
| **Thundering herd** | Many requests on cache miss | Locking, request coalescing |
| **Cache stampede** | Mass expiration | Staggered TTLs, warm-up |
| **Stale data** | Invalidation lag | Event-driven invalidation |

## Cache Levels

```
┌─────────────────────────────────────────────────────┐
│ Browser Cache (localStorage, sessionStorage)        │ ← Fastest
├─────────────────────────────────────────────────────┤
│ CDN Cache (Cloudflare, Fastly)                      │
├─────────────────────────────────────────────────────┤
│ Application Cache (Redis, Memcached)                │
├─────────────────────────────────────────────────────┤
│ Database Query Cache                                │
├─────────────────────────────────────────────────────┤
│ Database Buffer Pool                                │ ← Slowest
└─────────────────────────────────────────────────────┘
```

## Eviction Policies

| Policy | Description | Use When |
|--------|-------------|----------|
| **LRU** | Least Recently Used | General purpose |
| **LFU** | Least Frequently Used | Access frequency matters |
| **FIFO** | First In First Out | Simple, time-based |
| **Random** | Random eviction | Simple, low overhead |
| **TTL** | Time-based expiration | Data has natural lifetime |

## Redis Use Cases

| Use Case | Data Structure | Example |
|----------|----------------|---------|
| Session storage | String/Hash | User sessions |
| Rate limiting | String + INCR | API limits |
| Leaderboards | Sorted Set | Gaming ranks |
| Real-time analytics | HyperLogLog | Unique visitors |
| Pub/Sub | Pub/Sub | Real-time notifications |
| Distributed locks | String + NX | Mutex across services |

## Consistency at Scale

Meta achieves **99.99999999% cache consistency** through:
- Regional invalidation
- Version tracking
- Lease-based invalidation
- Monitoring and alerting

[Read the full case study](https://newsletter.systemdesign.one/p/cache-consistency)

## Questions to Consider

1. What's the read/write ratio?
2. Can you tolerate stale data? For how long?
3. What's the cache hit ratio target?
4. How will you handle cache failures?
5. What's the eviction strategy?
6. How will you warm the cache?
