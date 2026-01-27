# Payment Systems Case Studies

Building financial systems that never lose money and always work.

## Why Payments Are Different

```
Regular Systems          vs          Payment Systems
─────────────────                    ─────────────────
Eventual consistency OK              Must be strongly consistent
Duplicate messages OK                Duplicates = lost money
99.9% uptime acceptable              99.99%+ required
Retry freely                         Retry carefully (idempotency)
```

## Case Studies

### Transaction Processing

| Company | Achievement | Key Pattern | Link |
|---------|-------------|-------------|------|
| PayPal | 1B transactions/day with 8 VMs | Actor model | [Read](https://newsletter.systemdesign.one/p/actor-model) |
| Stripe | Prevents double payments | Idempotent APIs | [Read](https://newsletter.systemdesign.one/p/idempotent-api) |

### Rate Limiting & Protection

| Company | Context | Key Pattern | Link |
|---------|---------|-------------|------|
| Stripe | API scalability | Token bucket | [Read](https://newsletter.systemdesign.one/p/rate-limiter) |
| Razorpay | 1500 req/sec flash sales | Queue-based throttling | [Read](https://newsletter.systemdesign.one/p/payment-gateway-architecture) |

### High-Volume Commerce

| Company | Scale | Key Insight | Link |
|---------|-------|-------------|------|
| Shopify | 32M req/min flash sales | Pre-warming + queuing | [Read](https://newsletter.systemdesign.one/p/shopify-flash-sale) |
| McDonald's | 20K orders/sec | Event-driven architecture | [Read](https://newsletter.systemdesign.one/p/mcdonalds-architecture) |

## Critical Patterns

### Idempotency

**Problem**: Network failures cause retries. Retries can duplicate transactions.

**Solution**: Idempotency keys

```
Request 1: POST /charge {idempotency_key: "abc123", amount: 100}
  → Success, charged $100

Request 2: POST /charge {idempotency_key: "abc123", amount: 100}
  → Returns cached result, no duplicate charge
```

**Implementation**:
- Client generates unique key per logical operation
- Server stores key → result mapping
- On retry, return stored result

### Exactly-Once Semantics

| Approach | How It Works |
|----------|--------------|
| **Idempotency keys** | Deduplicate at API layer |
| **Transactional outbox** | Atomically write event + data |
| **Two-phase commit** | Coordinate across services |
| **Saga pattern** | Compensating transactions |

### Rate Limiting

| Algorithm | Description | Use Case |
|-----------|-------------|----------|
| **Token bucket** | Allows bursts | API rate limiting |
| **Leaky bucket** | Smooth output | Traffic shaping |
| **Fixed window** | Simple counting | Basic limiting |
| **Sliding window** | More accurate | Precise limiting |

## Reliability Requirements

### The Nines

| Availability | Downtime/Year | Downtime/Month |
|--------------|---------------|----------------|
| 99% | 3.65 days | 7.3 hours |
| 99.9% | 8.76 hours | 43.8 minutes |
| 99.99% | 52.6 minutes | 4.38 minutes |
| 99.999% | 5.26 minutes | 26.3 seconds |

### Achieving High Availability
- Active-active deployment
- Automatic failover
- No single points of failure
- Comprehensive monitoring

## Security Considerations

### Data Protection
- PCI DSS compliance
- Encryption at rest and in transit
- Tokenization of card data
- Key rotation

### Fraud Prevention
- Velocity checks
- Anomaly detection
- 3D Secure
- Address verification

## Questions to Consider

1. How do you handle network partitions during payment?
2. What happens if the database fails mid-transaction?
3. How do you reconcile at end of day?
4. How do you handle chargebacks?
5. What's your disaster recovery plan?

## Design Exercise

Design a payment system that handles:
- 10,000 transactions/second
- 99.99% availability
- Exactly-once semantics
- Multi-currency support
- Fraud detection
