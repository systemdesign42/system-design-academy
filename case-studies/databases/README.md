# Database Case Studies

How companies scale databases to handle petabytes of data and millions of queries per second.

## The Database Scaling Challenge

```
Problem: Single database can't handle the load

Solutions:
├── Read Replicas (scale reads)
├── Sharding (scale writes)
├── Caching (reduce load)
└── NewSQL (distributed SQL)
```

## Case Studies

### Sharding Strategies

| Company | Scale | Approach | Link |
|---------|-------|----------|------|
| Quora | 13+ TB MySQL | Functional + horizontal sharding | [Read](https://newsletter.systemdesign.one/p/mysql-sharding) |
| YouTube | 2.49B users | Vitess (MySQL clustering) | [Read](https://newsletter.systemdesign.one/p/vitess-mysql) |

### Migrations

| Company | Challenge | Link |
|---------|-----------|------|
| Tumblr | 60+ billion rows migration | [Read](https://newsletter.systemdesign.one/p/how-to-migrate-a-mysql-database) |

### PostgreSQL at Scale

| Company | Achievement | Link |
|---------|-------------|------|
| Cloudflare | 55M req/sec with 15 clusters | [Read](https://newsletter.systemdesign.one/p/postgresql-scalability) |

### Distributed Databases (White Papers)

| System | Innovation | Link |
|--------|------------|------|
| Amazon Dynamo | Eventual consistency, consistent hashing | [Read](https://newsletter.systemdesign.one/p/amazon-dynamo-architecture) |
| Google Spanner | Global transactions with TrueTime | [Read](https://newsletter.systemdesign.one/p/cloud-spanner-database) |

### Storage Systems

| Company | Achievement | Link |
|---------|-------------|------|
| Amazon S3 | 99.999999999% durability | [Read](https://newsletter.systemdesign.one/p/amazon-s3-durability) |
| Amazon S3 | Architecture deep dive | [Read](https://newsletter.systemdesign.one/p/s3-architecture) |

## Caching for Databases

| Company | Achievement | Link |
|---------|-------------|------|
| Meta | 99.99999999% cache consistency | [Read](https://newsletter.systemdesign.one/p/cache-consistency) |

## Key Patterns

### Sharding Strategies

| Strategy | Description | Best For |
|----------|-------------|----------|
| **Hash-based** | Hash key to determine shard | Even distribution |
| **Range-based** | Ranges of keys per shard | Range queries |
| **Geographic** | Shard by region | Locality |
| **Tenant-based** | Shard per customer | Multi-tenant SaaS |

### Replication Patterns

| Pattern | Consistency | Availability | Use Case |
|---------|-------------|--------------|----------|
| **Single leader** | Strong | Medium | OLTP |
| **Multi-leader** | Eventual | High | Multi-region |
| **Leaderless** | Tunable | High | AP systems |

### Migration Strategies

| Strategy | Risk | Downtime |
|----------|------|----------|
| **Big bang** | High | Long |
| **Dual write** | Medium | None |
| **Shadow traffic** | Low | None |
| **Strangler fig** | Low | None |

## Consistency Patterns

| Pattern | Description | Link |
|---------|-------------|------|
| Strong | Read sees latest write | [Read](https://systemdesign.one/consistency-patterns/) |
| Eventual | Read may see stale data | [Read](https://systemdesign.one/consistency-patterns/) |
| Causal | Respects causality | [Read](https://systemdesign.one/consistency-patterns/) |

## Questions to Consider

1. What's your read/write ratio?
2. Can you tolerate eventual consistency?
3. What are your query patterns?
4. How will you handle schema changes?
5. What's your backup and recovery strategy?
