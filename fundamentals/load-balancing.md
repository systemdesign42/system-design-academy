# Load Balancing

Distributing traffic across servers to improve reliability, scalability, and performance.

## Why Load Balance?

```
Without Load Balancer:          With Load Balancer:

Client → Server (overloaded)    Client → LB → Server 1
                                         ↘ → Server 2
                                         ↘ → Server 3
```

**Benefits**:
- Horizontal scaling
- High availability
- SSL termination
- Health monitoring

## Core Resources

| Resource | Description | Link |
|----------|-------------|------|
| Nginx Architecture | 1M concurrent connections | [Read](https://newsletter.systemdesign.one/p/how-does-nginx-work) |
| Facebook Load Balancer | Billion-user scale | [Read](https://newsletter.systemdesign.one/p/facebook-load-balancer) |
| Consistent Hashing | Key distribution | [Read](https://systemdesign.one/consistent-hashing-explained/) |

## L4 vs L7 Load Balancing

### Layer 4 (Transport)

```
Operates on: IP address + Port
Sees: TCP/UDP packets
Cannot see: HTTP headers, URLs, cookies
```

**Pros**: Fast, simple, low overhead
**Cons**: No content-based routing

**Use when**: Raw performance matters, simple routing

### Layer 7 (Application)

```
Operates on: HTTP/HTTPS
Sees: URLs, headers, cookies, body
Can do: Path-based routing, header modification
```

**Pros**: Smart routing, SSL termination, caching
**Cons**: More overhead, more complex

**Use when**: Need content-based decisions

## Load Balancing Algorithms

| Algorithm | How It Works | Best For |
|-----------|--------------|----------|
| **Round Robin** | Rotate through servers | Equal capacity, stateless |
| **Weighted Round Robin** | Proportional to weight | Different server sizes |
| **Least Connections** | Send to least busy | Variable request times |
| **Least Response Time** | Fastest server first | Heterogeneous servers |
| **IP Hash** | Hash client IP | Session affinity |
| **Consistent Hash** | Minimize redistribution | Caching, stateful |

### Round Robin

```
Request 1 → Server A
Request 2 → Server B
Request 3 → Server C
Request 4 → Server A (repeat)
```

Simple but doesn't account for server load or capacity.

### Least Connections

```
Server A: 10 connections
Server B: 5 connections
Server C: 8 connections

Next request → Server B (least busy)
```

Better for requests with varying duration.

### Consistent Hashing

```
Hash Ring:
    ┌───────────────────┐
    │   Server A (0°)   │
    │                   │
Server C (240°)     Server B (120°)
    │                   │
    └───────────────────┘

key "user:123" hashes to 100° → Server B
```

When servers change, only K/n keys need remapping (not all keys).

## Health Checks

### Types

| Type | How | Detects |
|------|-----|---------|
| **TCP** | Open connection | Server up/down |
| **HTTP** | GET /health | App responsiveness |
| **Deep** | Check dependencies | Full system health |

### Configuration

```
health_check:
  interval: 10s      # How often to check
  timeout: 5s        # How long to wait
  unhealthy: 3       # Failures before marking down
  healthy: 2         # Successes before marking up
```

## Session Persistence

When requests from same user must go to same server:

| Method | How | Trade-off |
|--------|-----|-----------|
| **Sticky sessions** | Cookie/IP affinity | Uneven load |
| **Session replication** | Share across servers | Complexity |
| **External session store** | Redis/Memcached | Additional hop |
| **Stateless design** | JWT/signed tokens | Best approach |

## High Availability

### Active-Passive

```
        ┌──────────┐
        │ Active   │ ← All traffic
        │ LB       │
        └────┬─────┘
             │ heartbeat
        ┌────▼─────┐
        │ Passive  │ ← Takes over on failure
        │ LB       │
        └──────────┘
```

### Active-Active

```
        ┌──────────┐     ┌──────────┐
        │ LB 1     │     │ LB 2     │
        └────┬─────┘     └────┬─────┘
             │                │
        DNS / Anycast routes to both
```

## Global Load Balancing

```
User (US) ─────→ DNS ─────→ US Data Center
User (EU) ─────→ DNS ─────→ EU Data Center
User (Asia) ───→ DNS ─────→ Asia Data Center
```

**Methods**:
- GeoDNS (route by location)
- Anycast (route to nearest)
- Latency-based routing

## Facebook's Approach

Facebook built a software L4 load balancer that:
- Handles billion+ users
- Runs on commodity hardware
- Uses consistent hashing
- Provides health checking

[Read the full case study](https://newsletter.systemdesign.one/p/facebook-load-balancer)

## Questions to Consider

1. L4 or L7? (Performance vs features)
2. Do you need session affinity?
3. What's the health check strategy?
4. How do you handle load balancer failure?
5. Do you need global load balancing?
