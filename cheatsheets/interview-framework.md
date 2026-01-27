# System Design Interview Framework

A structured approach to system design interviews.

## The 45-Minute Framework

| Phase | Time | Focus |
|-------|------|-------|
| 1. Requirements | 5 min | Understand the problem |
| 2. Estimation | 5 min | Scale and constraints |
| 3. High-Level Design | 15 min | Core architecture |
| 4. Deep Dive | 15 min | Detailed components |
| 5. Wrap Up | 5 min | Trade-offs and extensions |

---

## Phase 1: Requirements (5 min)

### Clarifying Questions

**Functional Requirements**
- What are the core features?
- Who are the users?
- What actions can users take?

**Non-Functional Requirements**
- How many users? (Scale)
- What's acceptable latency?
- What's the availability target?
- Is consistency or availability more important?

### Example: Design Twitter

```
Functional:
- Post tweets
- Follow users
- View timeline
- Search tweets

Non-Functional:
- 500M users, 200M daily active
- Timeline loads < 200ms
- 99.9% availability
- Eventual consistency OK for timeline
```

---

## Phase 2: Estimation (5 min)

### Calculate Key Metrics

```
Users:       500M total, 200M DAU
Tweets/day:  200M users × 2 tweets = 400M tweets
Reads/day:   200M users × 100 reads = 20B reads
Read:Write:  50:1

Storage:
- 400M tweets × 1KB = 400GB/day
- 400GB × 365 × 5 years = 730TB

QPS:
- Writes: 400M / 86400 ≈ 5K tweets/sec
- Reads: 20B / 86400 ≈ 230K reads/sec
- Peak (3x): 700K reads/sec
```

### Capacity Estimation Template

```
1. Users (total, daily active)
2. Actions per user per day
3. Total actions per day
4. Data size per action
5. Storage per day/year
6. QPS (average and peak)
7. Bandwidth requirements
```

---

## Phase 3: High-Level Design (15 min)

### Draw the Architecture

```
┌─────────┐     ┌──────────┐     ┌──────────────┐
│ Clients │────▶│   CDN    │────▶│ Load Balancer│
└─────────┘     └──────────┘     └──────┬───────┘
                                        │
                    ┌───────────────────┼───────────────────┐
                    ▼                   ▼                   ▼
              ┌──────────┐       ┌──────────┐       ┌──────────┐
              │ Service  │       │ Service  │       │ Service  │
              └────┬─────┘       └────┬─────┘       └────┬─────┘
                   │                  │                  │
                   └──────────────────┼──────────────────┘
                                      ▼
                               ┌──────────┐
                               │  Cache   │
                               └────┬─────┘
                                    ▼
                               ┌──────────┐
                               │ Database │
                               └──────────┘
```

### Core Components to Consider

| Component | Purpose |
|-----------|---------|
| Load Balancer | Distribute traffic |
| Web Servers | Handle requests |
| Application Servers | Business logic |
| Cache | Reduce database load |
| Database | Persistent storage |
| Message Queue | Async processing |
| CDN | Static content delivery |

---

## Phase 4: Deep Dive (15 min)

### Pick 2-3 Areas to Explore

**Options:**
- Data model and schema
- API design
- Caching strategy
- Database scaling
- Specific algorithms
- Failure handling

### Deep Dive Template

```
Component: [Name]

Purpose: Why do we need this?

Design choices:
- Option A: [pros/cons]
- Option B: [pros/cons]
- Chosen: [which and why]

Data flow:
1. Step 1
2. Step 2
3. Step 3

Edge cases:
- What if X fails?
- How do we handle Y?
```

### Example: Timeline Generation

```
Approach 1: Fan-out on write (push)
- On tweet: write to all followers' timelines
- Pros: Fast read
- Cons: Celebrity problem, write amplification

Approach 2: Fan-out on read (pull)
- On read: query all followees' tweets
- Pros: Simple writes
- Cons: Slow reads, heavy database load

Chosen: Hybrid
- Normal users: push
- Celebrities (>1M followers): pull
- Combine at read time
```

---

## Phase 5: Wrap Up (5 min)

### Discuss Trade-offs

| Decision | Trade-off |
|----------|-----------|
| Eventual consistency | Faster but may show stale data |
| Caching | Speed vs complexity |
| Microservices | Scalability vs operational overhead |

### Mention Extensions

- How would you add feature X?
- How would you scale 10x?
- How would you handle regional expansion?

### Address Bottlenecks

- What's the weakest point?
- How would you monitor it?
- What's the failover strategy?

---

## Common Mistakes

| Mistake | Better Approach |
|---------|-----------------|
| Jumping to solution | Ask clarifying questions first |
| Over-engineering | Start simple, add complexity as needed |
| Ignoring scale | Always estimate and design for scale |
| One-way monologue | Engage interviewer, ask for feedback |
| No trade-offs | Every decision has pros and cons |
| Skipping estimation | Numbers drive design decisions |

---

## Quick Reference: What to Draw

```
For any system, consider:

1. Entry points
   - DNS → CDN → Load Balancer

2. Compute layer
   - Web servers → App servers
   - API Gateway → Microservices

3. Data layer
   - Cache → Database
   - Read replicas, sharding

4. Async processing
   - Message queues
   - Background workers

5. Supporting services
   - Monitoring
   - Logging
   - Service discovery
```

---

## Practice Problems

### Beginner
- URL Shortener
- Pastebin
- Rate Limiter

### Intermediate
- Twitter/News Feed
- Chat System
- Search Autocomplete

### Advanced
- YouTube/Netflix
- Uber/Lyft
- Distributed Cache

---

## Final Checklist

Before finishing, verify:
- [ ] Addressed all functional requirements
- [ ] System handles estimated scale
- [ ] Explained key trade-offs
- [ ] Discussed failure scenarios
- [ ] Mentioned monitoring/observability
