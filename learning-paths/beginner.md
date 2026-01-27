# Beginner Learning Path

> **Timeline**: 4-6 weeks | **Prerequisites**: Basic programming knowledge

This path builds your foundation in system design from the ground up. Focus on understanding *why* systems are designed certain ways, not just *how*.

---

## Week 1: How the Internet Works

Before designing systems, understand how they communicate.

### Core Reading
- [ ] [What Happens When You Type a URL Into Your Browser?](https://systemdesign.one/what-happens-when-you-type-url-into-your-browser/)
- [ ] [How to Troubleshoot if You Can't Access a Website](https://systemdesign.one/how-to-troubleshoot-if-you-cannot-access-a-website/)

### Key Concepts to Master
- DNS resolution
- TCP/IP basics
- HTTP request/response cycle
- Client-server model

### Self-Check Questions
1. What are the steps between typing a URL and seeing a webpage?
2. What's the difference between HTTP and HTTPS?
3. How does DNS work?

---

## Week 2: Estimations & Back-of-Envelope Math

Learn to quickly estimate system requirements - a critical interview skill.

### Core Reading
- [ ] [Back of the Envelope](https://systemdesign.one/back-of-the-envelope/)
- [ ] [System Design Interview Cheat Sheet](https://systemdesign.one/system-design-interview-cheatsheet/)

### Numbers You Must Know
| Unit | Value |
|------|-------|
| 1 KB | 1,000 bytes |
| 1 MB | 1,000 KB |
| 1 GB | 1,000 MB |
| 1 TB | 1,000 GB |
| Seconds in a day | 86,400 (~100K) |
| Seconds in a year | ~31 million |

### Practice Exercise
Estimate Twitter's daily storage needs:
- 500M tweets/day
- Average tweet: 280 chars + metadata (~1KB)
- How much storage per day? Per year?

---

## Week 3: Scaling Fundamentals

Understand how systems grow from hundreds to millions of users.

### Core Reading
- [ ] [How to Scale an App to 10 Million Users on AWS](https://newsletter.systemdesign.one/p/aws-scale)
- [ ] [How Dropbox Scaled to 100 Thousand Users](https://newsletter.systemdesign.one/p/dropbox-architecture)

### Key Concepts
| Concept | Description |
|---------|-------------|
| **Vertical Scaling** | Bigger machine (more CPU/RAM) |
| **Horizontal Scaling** | More machines |
| **Load Balancer** | Distributes traffic across servers |
| **Database Replication** | Copies of data for redundancy |
| **Caching** | Store frequently accessed data in memory |

### Milestone Project
Draw a diagram showing how you'd scale a simple web app from 1 to 1M users.

---

## Week 4: Databases & Storage

Learn how data is stored, retrieved, and kept consistent.

### Core Reading
- [ ] [How Databases Keep Passwords Securely](https://newsletter.systemdesign.one/p/how-to-store-passwords-in-database)
- [ ] [Consistency Patterns](https://systemdesign.one/consistency-patterns/)

### Key Concepts
- SQL vs NoSQL tradeoffs
- ACID properties
- CAP theorem basics
- Indexing

### Case Study
- [ ] [How Amazon S3 Achieves 99.999999999% Durability](https://newsletter.systemdesign.one/p/amazon-s3-durability)

---

## Week 5: Caching

One of the most important performance optimization techniques.

### Core Reading
- [ ] [Top 5 Caching Patterns](https://newsletter.systemdesign.one/p/caching-patterns)
- [ ] [Redis Use Cases](https://newsletter.systemdesign.one/p/redis-use-cases)

### Caching Patterns Summary
| Pattern | Use When |
|---------|----------|
| **Cache-Aside** | Read-heavy, can tolerate stale data |
| **Write-Through** | Need consistency, can tolerate write latency |
| **Write-Behind** | Write-heavy, can tolerate eventual consistency |

### Case Study
- [ ] [How Meta Achieves 99.99999999% Cache Consistency](https://newsletter.systemdesign.one/p/cache-consistency)

---

## Week 6: Your First System Design

Put it all together with a classic problem.

### Design Exercise: URL Shortener
- [ ] [Bitly URL Shortener Architecture](https://systemdesign.one/url-shortening-system-design/)

### Requirements to Consider
1. How to generate short URLs?
2. How to handle redirects efficiently?
3. How to store billions of URLs?
4. How to handle high read traffic?

### Framework for Interviews
- [ ] [7 Simple Ways to Fail System Design Interview](https://newsletter.systemdesign.one/p/design-system-newsletter)

---

## Completion Checklist

Before moving to Intermediate:
- [ ] Can explain what happens when you type a URL
- [ ] Can do back-of-envelope calculations
- [ ] Understand vertical vs horizontal scaling
- [ ] Know the 5 caching patterns
- [ ] Can design a basic URL shortener
- [ ] Comfortable with estimation numbers

---

**Next**: [Intermediate Path](./intermediate.md)
