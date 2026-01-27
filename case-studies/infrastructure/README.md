# Infrastructure Case Studies

Building blocks of large-scale systems: load balancers, serverless, and core infrastructure.

## Case Studies

### Load Balancing

| Company | Achievement | Key Insight | Link |
|---------|-------------|-------------|------|
| Facebook | Billion users | Software L4 load balancer | [Read](https://newsletter.systemdesign.one/p/facebook-load-balancer) |
| Nginx | 1M concurrent connections | Event-driven architecture | [Read](https://newsletter.systemdesign.one/p/how-does-nginx-work) |

### Serverless & Compute

| Company | System | Key Insight | Link |
|---------|--------|-------------|------|
| Amazon | Lambda | Cold starts, execution model | [Read](https://newsletter.systemdesign.one/p/how-does-aws-lambda-work) |

### Storage

| Company | Achievement | Key Insight | Link |
|---------|-------------|-------------|------|
| Amazon S3 | 11 nines durability | Replication + checksums | [Read](https://newsletter.systemdesign.one/p/amazon-s3-durability) |
| Amazon S3 | Architecture | Object storage design | [Read](https://newsletter.systemdesign.one/p/s3-architecture) |

### Content Delivery

| Company | Scale | Key Insight | Link |
|---------|-------|-------------|------|
| Giphy | 10B GIFs/day | CDN architecture | [Read](https://newsletter.systemdesign.one/p/cdn-explained) |

### Cost Optimization

| Company | Savings | How | Link |
|---------|---------|-----|------|
| Airbnb | $84 million | HTTP streaming | [Read](https://newsletter.systemdesign.one/p/what-is-critical-rendering-path) |

## Load Balancing Deep Dive

### L4 vs L7 Load Balancing

| Layer | Operates On | Pros | Cons |
|-------|-------------|------|------|
| **L4 (Transport)** | IP + Port | Fast, simple | No content awareness |
| **L7 (Application)** | HTTP headers, URL | Content-based routing | More overhead |

### Load Balancing Algorithms

| Algorithm | Description | Use When |
|-----------|-------------|----------|
| **Round Robin** | Rotate through servers | Equal capacity servers |
| **Least Connections** | Send to least busy | Varying request times |
| **Weighted** | Proportional to capacity | Different server sizes |
| **IP Hash** | Consistent by client IP | Session affinity needed |

## Serverless Architecture

### When to Use Serverless

| Good For | Bad For |
|----------|---------|
| Variable traffic | Predictable high traffic |
| Event-driven workloads | Long-running processes |
| Rapid development | Low-latency requirements |
| Cost optimization at low scale | High-throughput systems |

### Cold Start Mitigation
- Provisioned concurrency
- Keep-alive pings
- Optimize package size
- Choose faster runtimes

## CDN Architecture

### CDN Benefits
- Reduced latency (edge locations)
- Reduced origin load
- DDoS protection
- SSL termination

### Cache Invalidation Strategies
| Strategy | Speed | Complexity |
|----------|-------|------------|
| TTL-based | Slow | Simple |
| Purge API | Fast | Medium |
| Versioned URLs | Instant | Higher |

## Key Infrastructure Patterns

### High Availability
- Multi-AZ deployment
- Health checks + auto-recovery
- Graceful degradation
- Circuit breakers

### Resilience
- Chaos engineering (Netflix)
- Blast radius reduction
- Bulkhead pattern
- Timeout + retry with backoff

## Questions to Consider

1. What's the expected traffic pattern?
2. Do you need content-based routing?
3. What's the latency budget?
4. How do you handle failures?
5. What's the cost model at scale?
