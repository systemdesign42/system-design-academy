# Conquering System Design

A comprehensive learning resource for mastering system design, from fundamentals to distributed systems at scale.

<p align="center">
  <a href="https://newsletter.systemdesign.one/">
    <img src="https://i.imgur.com/dea4G0P.png" alt="System Design Newsletter" />
  </a>
</p>

<p align="center">
  <a href="https://newsletter.systemdesign.one/">
    <b>Join the Newsletter for Weekly Deep Dives</b>
  </a>
</p>

---

## What's Inside

| Section | Description |
|---------|-------------|
| [Learning Paths](#learning-paths) | Structured curriculum from beginner to advanced |
| [Case Studies](#case-studies) | Real-world examples from 50+ companies |
| [Fundamentals](#fundamentals) | Core concepts and patterns |
| [Cheatsheets](#cheatsheets) | Quick reference guides for interviews |

---

## Learning Paths

Structured paths to master system design at your own pace.

| Path | Duration | For | Start Here |
|------|----------|-----|------------|
| [Beginner](./learning-paths/beginner.md) | 4-6 weeks | New to system design | Understanding the basics |
| [Intermediate](./learning-paths/intermediate.md) | 6-8 weeks | Ready for real-world patterns | Scaling and databases |
| [Advanced](./learning-paths/advanced.md) | 8-12 weeks | Targeting senior/staff roles | Distributed systems |

**How to use**: Follow paths in order. Each includes readings, exercises, and self-assessments.

---

## Case Studies

Learn from how the world's leading companies solve scaling challenges.

### By Theme

| Category | Focus | Companies |
|----------|-------|-----------|
| [Scaling](./case-studies/scaling/) | Growing to millions of users | Instagram, LinkedIn, Netflix, Disney+ |
| [Real-Time](./case-studies/real-time/) | Live updates and streaming | Slack, WhatsApp, Canva, Zoom |
| [Databases](./case-studies/databases/) | Data at scale | YouTube, Quora, Cloudflare |
| [Infrastructure](./case-studies/infrastructure/) | Core building blocks | AWS, Nginx, Facebook |
| [Payments](./case-studies/payments/) | Financial systems | Stripe, PayPal, Razorpay |
| [Search & Discovery](./case-studies/search-discovery/) | Finding and matching | Google, Uber, Tinder |

### Highlights

| Company | Achievement | Key Concept |
|---------|-------------|-------------|
| WhatsApp | 50B messages/day with 32 engineers | Erlang, efficiency |
| YouTube | 2.49B users on MySQL | Vitess, sharding |
| PayPal | 1B transactions/day with 8 VMs | Actor model |
| Meta | 99.99999999% cache consistency | Distributed caching |
| Uber | 1M requests/sec for nearby drivers | Geospatial indexing |

[Browse all 50+ case studies](./case-studies/)

---

## Fundamentals

Core concepts that underpin all large-scale systems.

| Topic | Key Concepts | Link |
|-------|--------------|------|
| Caching | Patterns, consistency, Redis | [Read](./fundamentals/caching.md) |
| Load Balancing | L4/L7, algorithms, health checks | [Read](./fundamentals/load-balancing.md) |
| Databases | CAP theorem, sharding, replication | [Read](./fundamentals/databases.md) |
| Distributed Systems | Gossip, consensus, data structures | [Read](./fundamentals/distributed-systems.md) |
| API Design | Rate limiting, idempotency, protocols | [Read](./fundamentals/api-design.md) |

[Explore all fundamentals](./fundamentals/)

---

## Cheatsheets

Quick reference guides for interviews and daily work.

| Cheatsheet | Use For |
|------------|---------|
| [Numbers Everyone Should Know](./cheatsheets/numbers.md) | Back-of-envelope calculations |
| [Scaling Patterns](./cheatsheets/scaling-patterns.md) | Choosing the right approach |
| [Interview Framework](./cheatsheets/interview-framework.md) | Structured interview approach |

---

## White Papers

Foundational papers that shaped modern distributed systems.

| Paper | Innovation | Link |
|-------|------------|------|
| Amazon Dynamo | Eventual consistency, consistent hashing | [Read](https://newsletter.systemdesign.one/p/amazon-dynamo-architecture) |
| Google Spanner | Global transactions, TrueTime | [Read](https://newsletter.systemdesign.one/p/cloud-spanner-database) |

---

## Quick Start

### New to System Design?
1. Start with [Beginner Learning Path](./learning-paths/beginner.md)
2. Read [What Happens When You Type a URL](https://systemdesign.one/what-happens-when-you-type-url-into-your-browser/)
3. Learn [Back of the Envelope](https://systemdesign.one/back-of-the-envelope/) calculations

### Preparing for Interviews?
1. Review the [Interview Framework](./cheatsheets/interview-framework.md)
2. Memorize [Numbers Everyone Should Know](./cheatsheets/numbers.md)
3. Practice with case studies

### Looking for Specific Topics?
- Browse [Case Studies by Theme](./case-studies/)
- Explore [Fundamentals](./fundamentals/)

---

## Repository Structure

```
conquering-system-design/
├── README.md                 # You are here
├── learning-paths/           # Structured learning curriculum
│   ├── beginner.md
│   ├── intermediate.md
│   └── advanced.md
├── case-studies/             # Real-world examples
│   ├── scaling/
│   ├── real-time/
│   ├── databases/
│   ├── infrastructure/
│   ├── payments/
│   └── search-discovery/
├── fundamentals/             # Core concepts
│   ├── caching.md
│   ├── load-balancing.md
│   ├── databases.md
│   ├── distributed-systems.md
│   └── api-design.md
└── cheatsheets/              # Quick references
    ├── numbers.md
    ├── scaling-patterns.md
    └── interview-framework.md
```

---

## Contributing

Found an issue or want to add content? Contributions are welcome!

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

---

## License

<p>Licensed under <a href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank" rel="license noopener noreferrer">CC BY-NC-ND 4.0</a></p>

---

<p align="center">
  <a href="https://newsletter.systemdesign.one/">
    <b>Subscribe to the Newsletter</b>
  </a>
  for weekly system design deep dives
</p>
