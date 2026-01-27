# Advanced Learning Path

> **Timeline**: 8-12 weeks | **Prerequisites**: [Intermediate Path](./intermediate.md) completed

This path covers distributed systems theory, white papers, and architecture patterns used at massive scale.

---

## Week 1-2: Distributed Systems Fundamentals

Master the theoretical foundations that underpin large-scale systems.

### Core Reading
- [ ] [Gossip Protocol](https://systemdesign.one/gossip-protocol/)
- [ ] [Hinted Handoff](https://systemdesign.one/hinted-handoff/)

### Key Concepts
| Concept | Description |
|---------|-------------|
| **CAP Theorem** | Consistency, Availability, Partition tolerance tradeoffs |
| **Gossip Protocol** | Decentralized information dissemination |
| **Vector Clocks** | Ordering events in distributed systems |
| **Quorum** | Consensus mechanism for reads/writes |

### Probabilistic Data Structures
- [ ] [Bloom Filter](https://systemdesign.one/bloom-filters-explained/)
- [ ] [Quotient Filter](https://systemdesign.one/quotient-filter-explained/)

---

## Week 3-4: White Papers Deep Dive

Study the foundational papers that shaped modern distributed systems.

### Amazon Dynamo
- [ ] [Amazon Dynamo Architecture](https://newsletter.systemdesign.one/p/amazon-dynamo-architecture)

**Key Innovations:**
- Consistent hashing with virtual nodes
- Vector clocks for conflict resolution
- Sloppy quorum and hinted handoff
- Anti-entropy with Merkle trees

### Google Spanner
- [ ] [Google Spanner](https://newsletter.systemdesign.one/p/cloud-spanner-database)

**Key Innovations:**
- TrueTime API for global consistency
- Globally distributed transactions
- Automatic sharding and replication

---

## Week 5-6: Architecture Patterns at Scale

Learn patterns used by companies serving billions of users.

### Cell-Based Architecture
- [ ] [Cell Based Architecture](https://newsletter.systemdesign.one/p/cell-based-architecture)

**When to Use:**
- Blast radius reduction
- Independent scaling
- Regional isolation

### Actor Model
- [ ] [Actor Model (PayPal's Billion Transactions/Day)](https://newsletter.systemdesign.one/p/actor-model)

**When to Use:**
- Concurrent processing
- State isolation
- Message-driven systems

### Micro Frontends
- [ ] [Micro Frontends](https://newsletter.systemdesign.one/p/micro-frontends)
- [ ] [How Discord Boosts Performance With Code-Splitting](https://newsletter.systemdesign.one/p/what-is-code-splitting-in-react)

---

## Week 7-8: Resilience Engineering

Learn how to build systems that survive failures.

### Chaos Engineering
- [ ] [How Netflix Uses Chaos Engineering](https://newsletter.systemdesign.one/p/chaos-engineering)

### Key Principles
| Principle | Implementation |
|-----------|----------------|
| **Expect Failure** | Design for it, don't prevent it |
| **Blast Radius** | Limit impact of failures |
| **Graceful Degradation** | Partial functionality > total outage |
| **Circuit Breakers** | Fail fast, recover fast |

### Case Studies in Resilience
- [ ] [5 Reasons Zoom Supports 300 Million Video Calls/Day](https://newsletter.systemdesign.one/p/zoom-architecture)
- [ ] [How Disney+ Scaled to 11 Million Users on Launch Day](https://newsletter.systemdesign.one/p/disney-architecture)

---

## Week 9-10: Payments & Financial Systems

Financial systems require the highest levels of consistency and reliability.

### Core Reading
- [ ] [Stripe Idempotent API (Prevents Double Payment)](https://newsletter.systemdesign.one/p/idempotent-api)
- [ ] [Razorpay Flash Sales at 1500 req/sec](https://newsletter.systemdesign.one/p/payment-gateway-architecture)

### Key Requirements
| Requirement | Why It Matters |
|-------------|----------------|
| **Idempotency** | Prevent duplicate charges |
| **Exactly-once delivery** | Critical for money movement |
| **Audit trails** | Regulatory compliance |
| **Strong consistency** | Account balances must be accurate |

### Case Study
- [ ] [PayPal: Billion Transactions/Day with 8 VMs](https://newsletter.systemdesign.one/p/actor-model)

---

## Week 11-12: Massive Scale Case Studies

Study how the largest systems in the world are built.

### Billion-User Systems
- [ ] [How Instagram Scaled to 2.5 Billion Users](https://newsletter.systemdesign.one/p/instagram-infrastructure)
- [ ] [8 Reasons WhatsApp Supports 50 Billion Messages/Day with 32 Engineers](https://newsletter.systemdesign.one/p/whatsapp-engineering)
- [ ] [How LinkedIn Scaled to 930 Million Users](https://newsletter.systemdesign.one/p/scalable-software-architecture)

### Content Delivery at Scale
- [ ] [How Giphy Delivers 10 Billion GIFs/Day](https://newsletter.systemdesign.one/p/cdn-explained)
- [ ] [YouTube: 11 Reasons for 100 Million Views/Day with 9 Engineers](https://newsletter.systemdesign.one/p/youtube-scalability)

### Search & Discovery
- [ ] [How Google Search Works](https://newsletter.systemdesign.one/p/search-engine-architecture)
- [ ] [How Uber Finds Nearby Drivers at 1 Million req/sec](https://newsletter.systemdesign.one/p/how-does-uber-find-nearby-drivers)
- [ ] [How Uber Computes ETA at Half Million req/sec](https://newsletter.systemdesign.one/p/uber-eta)

---

## Capstone Projects

### Project 1: Design a Global Payment System
Requirements:
- Multi-region deployment
- Exactly-once semantics
- Sub-second latency
- 99.999% availability

### Project 2: Design a Video Streaming Platform
Requirements:
- Live and on-demand streaming
- Global CDN strategy
- Adaptive bitrate
- Millions of concurrent viewers

### Project 3: Design a Real-Time Collaboration Tool
Requirements:
- Operational transformation or CRDTs
- Conflict resolution
- Offline support
- Multi-device sync

---

## Completion Checklist

You've mastered system design when you can:
- [ ] Read and understand distributed systems white papers
- [ ] Apply CAP theorem to real design decisions
- [ ] Design for failure from the start
- [ ] Make informed tradeoffs at scale
- [ ] Articulate why companies made specific architectural choices
- [ ] Design systems serving billions of users

---

## What's Next?

- Contribute to open-source distributed systems
- Read more white papers (Kafka, Cassandra, Raft)
- Practice with mock interviews
- Build your own distributed system

---

**Previous**: [Intermediate Path](./intermediate.md)
