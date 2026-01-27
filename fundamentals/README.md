# System Design Fundamentals

Core concepts and patterns that underpin all large-scale systems.

## Quick Navigation

| Topic | Description |
|-------|-------------|
| [Caching](./caching.md) | Patterns, consistency, and Redis use cases |
| [Load Balancing](./load-balancing.md) | L4/L7, algorithms, and health checks |
| [Databases](./databases.md) | Consistency, sharding, and replication |
| [Distributed Systems](./distributed-systems.md) | Protocols, consensus, and data structures |
| [API Design](./api-design.md) | Rate limiting, idempotency, and protocols |

## Foundational Resources

### Getting Started
- [What Happens When You Type a URL?](https://systemdesign.one/what-happens-when-you-type-url-into-your-browser/)
- [How to Troubleshoot Website Access](https://systemdesign.one/how-to-troubleshoot-if-you-cannot-access-a-website/)
- [Back of the Envelope Calculations](https://systemdesign.one/back-of-the-envelope/)

### Interview Preparation
- [System Design Interview Cheat Sheet](https://systemdesign.one/system-design-interview-cheatsheet/)
- [7 Ways to Fail System Design Interview](https://newsletter.systemdesign.one/p/design-system-newsletter)
- [Software Engineer Interview Resources](https://systemdesign.one/software-engineer-interview-learning-resources/)

### Architecture Principles
- [Amazon Frugal Architecture](https://newsletter.systemdesign.one/p/frugal-architecture)

## Concept Map

```
                    ┌─────────────────┐
                    │   Client        │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │   CDN / Cache   │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │  Load Balancer  │
                    └────────┬────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
┌───────▼───────┐   ┌───────▼───────┐   ┌───────▼───────┐
│   Service A   │   │   Service B   │   │   Service C   │
└───────┬───────┘   └───────┬───────┘   └───────┬───────┘
        │                    │                    │
        └────────────────────┼────────────────────┘
                             │
                    ┌────────▼────────┐
                    │  Cache (Redis)  │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │    Database     │
                    └─────────────────┘
```

## By Category

### Caching
| Concept | Description | Link |
|---------|-------------|------|
| Caching Patterns | Cache-aside, write-through, etc. | [Read](https://newsletter.systemdesign.one/p/caching-patterns) |
| Cache Consistency | How Meta achieves 10 nines | [Read](https://newsletter.systemdesign.one/p/cache-consistency) |
| Redis Use Cases | When and how to use Redis | [Read](https://newsletter.systemdesign.one/p/redis-use-cases) |

### Data Structures
| Concept | Description | Link |
|---------|-------------|------|
| Bloom Filter | Probabilistic membership testing | [Read](https://systemdesign.one/bloom-filters-explained/) |
| Quotient Filter | Space-efficient alternative | [Read](https://systemdesign.one/quotient-filter-explained/) |
| Consistent Hashing | Distributed key mapping | [Read](https://systemdesign.one/consistent-hashing-explained/) |

### Distributed Systems
| Concept | Description | Link |
|---------|-------------|------|
| Gossip Protocol | Decentralized communication | [Read](https://systemdesign.one/gossip-protocol/) |
| Hinted Handoff | Availability during failures | [Read](https://systemdesign.one/hinted-handoff/) |
| Consistency Patterns | Strong, eventual, causal | [Read](https://systemdesign.one/consistency-patterns/) |

### Architecture Patterns
| Concept | Description | Link |
|---------|-------------|------|
| Actor Model | Concurrent computation | [Read](https://newsletter.systemdesign.one/p/actor-model) |
| Cell Architecture | Blast radius reduction | [Read](https://newsletter.systemdesign.one/p/cell-based-architecture) |
| Microservices | Service decomposition | [Read](https://newsletter.systemdesign.one/p/netflix-microservices) |
| Micro Frontends | Frontend decomposition | [Read](https://newsletter.systemdesign.one/p/micro-frontends) |

### Infrastructure
| Concept | Description | Link |
|---------|-------------|------|
| Service Discovery | How services find each other | [Read](https://systemdesign.one/what-is-service-discovery/) |
| Nginx Architecture | Event-driven model | [Read](https://newsletter.systemdesign.one/p/how-does-nginx-work) |
| Code Splitting | Frontend performance | [Read](https://newsletter.systemdesign.one/p/what-is-code-splitting-in-react) |

### Security
| Concept | Description | Link |
|---------|-------------|------|
| Password Storage | How databases secure passwords | [Read](https://newsletter.systemdesign.one/p/how-to-store-passwords-in-database) |
