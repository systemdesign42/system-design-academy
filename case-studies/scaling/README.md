# Scaling Case Studies

How companies grew from startups to serving billions of users.

## The Scaling Journey

```
Thousands → Millions → Billions
    ↓           ↓          ↓
 Single      Horizontal  Global
 Server      Scaling     Distribution
```

## Case Studies

### Growth Stories

| Company | Journey | Key Insight | Link |
|---------|---------|-------------|------|
| Dropbox | 100K → millions in 1 year | Product-market fit + viral growth | [Read](https://newsletter.systemdesign.one/p/dropbox-architecture) |
| Instagram | Startup → 2.5B users | Simplicity at scale | [Read](https://newsletter.systemdesign.one/p/instagram-infrastructure) |
| LinkedIn | Launch → 930M users | Incremental evolution | [Read](https://newsletter.systemdesign.one/p/scalable-software-architecture) |
| Khan Academy | Education → 30M users | Mission-driven scaling | [Read](https://newsletter.systemdesign.one/p/khan-academy-architecture) |

### Cloud Scaling Blueprints

| Platform | Target Scale | Key Patterns | Link |
|----------|--------------|--------------|------|
| AWS | 10 million users | Auto-scaling, multi-AZ | [Read](https://newsletter.systemdesign.one/p/aws-scale) |
| GCP | 100 million users | Global load balancing | [Read](https://newsletter.systemdesign.one/p/google-cloud-scalability) |

### Launch Day Scaling

| Company | Challenge | Solution | Link |
|---------|-----------|----------|------|
| Disney+ | 11M users day one | Pre-scaling + graceful degradation | [Read](https://newsletter.systemdesign.one/p/disney-architecture) |
| Disney+ Hotstar | 25M concurrent | Cell-based architecture | [Read](https://newsletter.systemdesign.one/p/hotstar-scaling) |

### Microservices at Scale

| Company | Lesson | Link |
|---------|--------|------|
| Netflix | How to do microservices right | [Read](https://newsletter.systemdesign.one/p/netflix-microservices) |
| Prime Video | When microservices are wrong | [Read](https://newsletter.systemdesign.one/p/prime-video-microservices) |

## Key Patterns

### Horizontal Scaling
- Add more machines instead of bigger machines
- Requires stateless services
- Load balancer distributes traffic

### Caching Layers
- CDN for static assets
- Application cache (Redis/Memcached)
- Database query cache

### Database Scaling
- Read replicas for read-heavy workloads
- Sharding for write scaling
- Denormalization for performance

### Async Processing
- Message queues for background work
- Event-driven architecture
- Eventual consistency where acceptable

## Questions to Consider

1. What's the bottleneck at each scale?
2. When do you need to re-architect vs optimize?
3. How do you maintain development velocity while scaling?
4. What's the cost vs performance tradeoff?
