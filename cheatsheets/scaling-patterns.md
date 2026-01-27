# Scaling Patterns Cheatsheet

Quick reference for choosing the right scaling strategy.

## The Scaling Ladder

```
Users        Solution
─────        ────────
1-100        Single server
100-10K      Add caching, CDN
10K-100K     Load balancer, read replicas
100K-1M      Sharding, microservices
1M-10M       Multi-region, cell architecture
10M+         Custom solutions, specialized infrastructure
```

## Horizontal vs Vertical Scaling

| Vertical | Horizontal |
|----------|------------|
| Bigger machine | More machines |
| Limited by hardware | Theoretically unlimited |
| Simple | Complex |
| Single point of failure | Fault tolerant |
| Good for: databases | Good for: stateless services |

## Database Scaling

### Read Scaling

| Pattern | How | Use When |
|---------|-----|----------|
| **Caching** | Store hot data in memory | Read-heavy, tolerant of staleness |
| **Read replicas** | Replicate to read-only copies | Need fresh data |
| **CDN** | Edge cache for static content | Global users |

### Write Scaling

| Pattern | How | Use When |
|---------|-----|----------|
| **Sharding** | Split data across DBs | Single DB can't handle writes |
| **Async writes** | Queue and batch | Can tolerate delay |
| **CQRS** | Separate read/write models | Different read/write patterns |

### Sharding Strategies

| Strategy | Pros | Cons |
|----------|------|------|
| **Hash-based** | Even distribution | Cross-shard queries hard |
| **Range-based** | Range queries easy | Hot spots possible |
| **Geographic** | Low latency | Uneven distribution |
| **Tenant-based** | Isolation | Variable load |

## Caching Patterns

| Pattern | When | Trade-off |
|---------|------|-----------|
| **Cache-aside** | General purpose | Cache miss penalty |
| **Write-through** | Need consistency | Write latency |
| **Write-behind** | Write-heavy | Data loss risk |
| **Read-through** | Simplify app code | Initial latency |

## Load Balancing

| Algorithm | Best For |
|-----------|----------|
| **Round robin** | Equal servers, stateless |
| **Least connections** | Variable request times |
| **IP hash** | Session affinity needed |
| **Weighted** | Different server capacities |

## Async Processing

| Pattern | Use When |
|---------|----------|
| **Message queue** | Decouple services, handle spikes |
| **Event sourcing** | Audit trail, replay capability |
| **CQRS** | Different read/write patterns |
| **Saga** | Distributed transactions |

## Microservices Patterns

| Pattern | Purpose |
|---------|---------|
| **API Gateway** | Single entry point, auth, routing |
| **Service mesh** | Service-to-service communication |
| **Circuit breaker** | Prevent cascade failures |
| **Bulkhead** | Isolate failures |
| **Sidecar** | Cross-cutting concerns |

## Data Consistency

| Level | Guarantee | Use When |
|-------|-----------|----------|
| **Strong** | Latest data always | Financial transactions |
| **Eventual** | Eventually converges | Social feeds, analytics |
| **Causal** | Respects causality | Collaborative editing |

## High Availability Patterns

| Pattern | How |
|---------|-----|
| **Active-passive** | Standby takes over on failure |
| **Active-active** | Both serve traffic |
| **Multi-region** | Survive regional outages |
| **Cell-based** | Limit blast radius |

## CDN Strategy

| Content | TTL | Invalidation |
|---------|-----|--------------|
| Static assets | Long (1 year) | Version in URL |
| API responses | Short (1 min) | Cache-Control |
| User content | Medium (1 hour) | Purge API |

## Rate Limiting

| Algorithm | Allows Bursts | Smooth Output |
|-----------|---------------|---------------|
| Token bucket | Yes | No |
| Leaky bucket | No | Yes |
| Fixed window | Somewhat | No |
| Sliding window | No | Somewhat |

## Quick Decision Tree

```
Need to scale reads?
├── Can tolerate stale data? → Cache
├── Need fresh data? → Read replicas
└── Static content? → CDN

Need to scale writes?
├── Can batch? → Async queue
├── Can partition data? → Sharding
└── Independent services? → Microservices

Need high availability?
├── Single region? → Multi-AZ
├── Global users? → Multi-region
└── Limit failures? → Cell architecture
```

## Anti-Patterns

| Anti-Pattern | Problem | Solution |
|--------------|---------|----------|
| Premature optimization | Complexity without need | Start simple |
| Single point of failure | One component kills system | Redundancy |
| Synchronous everything | Cascading failures | Async where possible |
| Shared database | Tight coupling | Service owns its data |
| No caching | Database overload | Cache hot data |
| No rate limiting | Resource exhaustion | Protect endpoints |
