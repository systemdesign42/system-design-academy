# Databases

Understanding database fundamentals: consistency models, scaling strategies, and when to use what.

## Core Resources

| Resource | Description | Link |
|----------|-------------|------|
| Consistency Patterns | Strong, eventual, causal | [Read](https://systemdesign.one/consistency-patterns/) |
| Password Storage | Security best practices | [Read](https://newsletter.systemdesign.one/p/how-to-store-passwords-in-database) |

## Case Studies

| Company | Challenge | Solution | Link |
|---------|-----------|----------|------|
| YouTube | 2.49B users | Vitess (MySQL sharding) | [Read](https://newsletter.systemdesign.one/p/vitess-mysql) |
| Quora | 13+ TB | MySQL sharding | [Read](https://newsletter.systemdesign.one/p/mysql-sharding) |
| Cloudflare | 55M req/sec | PostgreSQL | [Read](https://newsletter.systemdesign.one/p/postgresql-scalability) |
| Tumblr | 60B rows | Migration strategy | [Read](https://newsletter.systemdesign.one/p/how-to-migrate-a-mysql-database) |

## White Papers

| System | Innovation | Link |
|--------|------------|------|
| Amazon Dynamo | Eventual consistency at scale | [Read](https://newsletter.systemdesign.one/p/amazon-dynamo-architecture) |
| Google Spanner | Globally consistent transactions | [Read](https://newsletter.systemdesign.one/p/cloud-spanner-database) |

## SQL vs NoSQL

| Aspect | SQL | NoSQL |
|--------|-----|-------|
| **Schema** | Fixed, predefined | Flexible, dynamic |
| **Scaling** | Vertical (mostly) | Horizontal (designed for) |
| **Transactions** | ACID | BASE (usually) |
| **Joins** | Native support | Application-level |
| **Best for** | Complex queries, consistency | Scale, flexibility |

### When to Use SQL
- Complex relationships
- ACID transactions required
- Complex queries with joins
- Data integrity critical

### When to Use NoSQL
- High write throughput
- Flexible schema
- Horizontal scaling
- Simple query patterns

## CAP Theorem

```
       Consistency
           /\
          /  \
         /    \
        /  CA  \      ← Traditional RDBMS
       /________\
      /\        /\
     /  \  CP  /  \   ← MongoDB, HBase
    / AP \    /    \
   /______\  /______\

  Cassandra   Spanner
  DynamoDB
```

**You can only guarantee 2 of 3**:
- **Consistency**: Every read receives the most recent write
- **Availability**: Every request receives a response
- **Partition Tolerance**: System works despite network failures

In reality, partitions happen, so you choose between CP and AP.

## Consistency Models

| Model | Guarantee | Use When |
|-------|-----------|----------|
| **Strong** | Read sees latest write | Financial transactions |
| **Eventual** | Eventually converges | Social feeds, analytics |
| **Causal** | Respects causality | Collaborative apps |
| **Read-your-writes** | See your own writes | User-facing apps |

[Deep dive on consistency patterns](https://systemdesign.one/consistency-patterns/)

## Scaling Strategies

### Read Replicas

```
         Writes
            ↓
      ┌─────────┐
      │ Primary │
      └────┬────┘
           │ replication
    ┌──────┼──────┐
    ↓      ↓      ↓
┌───────┐┌───────┐┌───────┐
│Replica││Replica││Replica│ ← Reads
└───────┘└───────┘└───────┘
```

**Pros**: Scales reads, provides redundancy
**Cons**: Replication lag, doesn't scale writes

### Sharding

```
User ID 1-1M     → Shard 1
User ID 1M-2M    → Shard 2
User ID 2M-3M    → Shard 3
```

| Strategy | How | Pros | Cons |
|----------|-----|------|------|
| **Hash** | Hash key to shard | Even distribution | Range queries hard |
| **Range** | Key ranges | Range queries easy | Hot spots possible |
| **Directory** | Lookup table | Flexible | Single point of failure |

### Vertical Partitioning

```
Users Table:
┌────────────────────────────────┐
│ id │ name │ email │ bio │ ... │
└────────────────────────────────┘
                ↓
┌─────────────────┐  ┌─────────────────┐
│ id │ name │email│  │ id │ bio │ ... │
└─────────────────┘  └─────────────────┘
   Frequent access      Rare access
```

## Replication

### Single-Leader

```
Client writes → Leader → Followers
Client reads  ← Any node
```

Simple, but leader is bottleneck.

### Multi-Leader

```
Client → Leader A ←→ Leader B ← Client
```

Better availability, but conflict resolution needed.

### Leaderless

```
Client writes → Multiple nodes (quorum)
Client reads  ← Multiple nodes (quorum)
```

Highly available, but eventual consistency.

## Indexing

### B-Tree Index (Default)
- Good for: Range queries, equality
- Trade-off: Write overhead

### Hash Index
- Good for: Exact matches
- Trade-off: No range queries

### Composite Index
```sql
INDEX (a, b, c)
-- Supports: WHERE a=1, WHERE a=1 AND b=2
-- Not: WHERE b=1 (must use leftmost columns)
```

## Questions to Consider

1. What are the query patterns?
2. Read-heavy or write-heavy?
3. How important is consistency?
4. What's the data growth rate?
5. Do you need transactions across shards?
