# Intermediate Learning Path

> **Timeline**: 6-8 weeks | **Prerequisites**: [Beginner Path](./beginner.md) completed

This path deepens your understanding with real-world case studies and introduces distributed systems concepts.

---

## Week 1-2: Load Balancing & Traffic Management

Master how major platforms handle millions of requests.

### Core Reading
- [ ] [How Nginx Supports 1 Million Concurrent Connections](https://newsletter.systemdesign.one/p/how-does-nginx-work)
- [ ] [How Facebook Supports a Billion Users via Software Load Balancer](https://newsletter.systemdesign.one/p/facebook-load-balancer)

### Key Concepts
| Concept | Description |
|---------|-------------|
| **L4 Load Balancing** | Transport layer, based on IP/port |
| **L7 Load Balancing** | Application layer, content-aware |
| **Consistent Hashing** | Minimize redistribution when nodes change |
| **Health Checks** | Detect and route around failures |

### Deep Dive
- [ ] [Consistent Hashing Explained](https://systemdesign.one/consistent-hashing-explained/)

### Case Study
- [ ] [Stripe Rate Limiting for Scalable APIs](https://newsletter.systemdesign.one/p/rate-limiter)

---

## Week 3-4: Real-Time Systems

Learn patterns for live updates, streaming, and instant communication.

### Core Reading
- [ ] [Real-Time Presence Platform Design](https://systemdesign.one/real-time-presence-platform-system-design/)
- [ ] [Real-Time Live Comments](https://systemdesign.one/live-comment-system-design/)

### Case Studies
- [ ] [How Disney+ Hotstar Delivered 5 Billion Emojis in Real Time](https://newsletter.systemdesign.one/p/hotstar-architecture)
- [ ] [How Canva Supports Real-Time Collaboration for 135 Million Users](https://newsletter.systemdesign.one/p/rsocket)
- [ ] [How Facebook Scaled Live Video to a Billion Users](https://newsletter.systemdesign.one/p/live-streaming-architecture)

### Patterns to Master
- WebSockets vs Long Polling vs Server-Sent Events
- Pub/Sub architecture
- Event-driven design
- Backpressure handling

---

## Week 5-6: Database Scaling

Learn how companies scale databases to handle billions of rows.

### Core Reading
- [ ] [How YouTube Supports 2.49 Billion Users With MySQL](https://newsletter.systemdesign.one/p/vitess-mysql)
- [ ] [How Quora Shards MySQL to Handle 13+ Terabytes](https://newsletter.systemdesign.one/p/mysql-sharding)

### Key Concepts
| Strategy | Description | Use Case |
|----------|-------------|----------|
| **Replication** | Copy data to multiple nodes | Read scaling |
| **Sharding** | Split data across nodes | Write scaling |
| **Partitioning** | Divide tables logically | Query performance |

### Case Study
- [ ] [Tumblr's Database Migration With 60+ Billion Rows](https://newsletter.systemdesign.one/p/how-to-migrate-a-mysql-database)

### Deep Dive
- [ ] [How Cloudflare Supports 55M req/sec With 15 Postgres Clusters](https://newsletter.systemdesign.one/p/postgresql-scalability)

---

## Week 7-8: Microservices & Distributed Patterns

Understand how large systems are decomposed and coordinated.

### Core Reading
- [ ] [Microservices Lessons From Netflix](https://newsletter.systemdesign.one/p/netflix-microservices)
- [ ] [Amazon Prime Video Microservices Top Failure](https://newsletter.systemdesign.one/p/prime-video-microservices)

### Key Patterns
| Pattern | Purpose |
|---------|---------|
| **Service Discovery** | How services find each other |
| **Circuit Breaker** | Prevent cascade failures |
| **Saga Pattern** | Distributed transactions |
| **API Gateway** | Single entry point |

### Supporting Reading
- [ ] [Service Discovery](https://systemdesign.one/what-is-service-discovery/)
- [ ] [How Halo Scaled Using the Saga Pattern](https://newsletter.systemdesign.one/p/saga-design-pattern)

### Case Studies
- [ ] [Slack Architecture](https://systemdesign.one/slack-architecture/)
- [ ] [How Zapier Automates Billions of Tasks](https://newsletter.systemdesign.one/p/zapier-architecture)

---

## Milestone Projects

### Project 1: Design a Chat System
Using what you learned, design a system like Slack:
- Real-time messaging
- Presence indicators
- Message persistence
- Search functionality

Reference: [WeChat Architecture (1.67 Billion Users)](https://newsletter.systemdesign.one/p/chat-application-architecture)

### Project 2: Design a Feed System
Design a social media feed:
- Post creation and storage
- Feed generation
- Real-time updates

Reference: [How Hashnode Generates Feed at Scale](https://newsletter.systemdesign.one/p/feed-architecture)

---

## Completion Checklist

Before moving to Advanced:
- [ ] Understand L4 vs L7 load balancing
- [ ] Can explain consistent hashing
- [ ] Know when to use WebSockets vs polling
- [ ] Understand database sharding strategies
- [ ] Can articulate microservices tradeoffs
- [ ] Designed at least 2 systems end-to-end

---

**Previous**: [Beginner Path](./beginner.md) | **Next**: [Advanced Path](./advanced.md)
