# Real-Time Systems Case Studies

Building systems that deliver instant updates to millions of users.

## What Makes Real-Time Hard?

```
Challenge: Deliver updates to millions of users in milliseconds

Traditional Request/Response     vs     Real-Time
        Client → Server                 Server → Client
        (pull model)                    (push model)
```

## Case Studies

### Messaging & Chat

| Company | Scale | Key Pattern | Link |
|---------|-------|-------------|------|
| WhatsApp | 50B messages/day | Erlang + BEAM VM | [Read](https://newsletter.systemdesign.one/p/whatsapp-engineering) |
| WeChat | 1.67B monthly users | Microservices | [Read](https://newsletter.systemdesign.one/p/chat-application-architecture) |
| Slack | Enterprise messaging | WebSockets + channels | [Read](https://systemdesign.one/slack-architecture/) |

### Live Streaming & Video

| Company | Scale | Key Pattern | Link |
|---------|-------|-------------|------|
| Facebook | Billion-user live video | Adaptive bitrate | [Read](https://newsletter.systemdesign.one/p/live-streaming-architecture) |
| Zoom | 300M video calls/day | Media servers | [Read](https://newsletter.systemdesign.one/p/zoom-architecture) |

### Collaboration

| Company | Scale | Key Pattern | Link |
|---------|-------|-------------|------|
| Google Docs | Real-time editing | Operational Transform (OT) | [Read](http://newsletter.systemdesign.one/p/how-does-google-docs-work) |
| Canva | 135M users real-time | RSocket protocol | [Read](https://newsletter.systemdesign.one/p/rsocket) |

### Live Events

| Company | Scale | Key Pattern | Link |
|---------|-------|-------------|------|
| Disney+ Hotstar | 5B emojis real-time | Pub/sub + aggregation | [Read](https://newsletter.systemdesign.one/p/hotstar-architecture) |
| SeatGeek | High-demand ticket sales | Virtual waiting room | [Read](https://newsletter.systemdesign.one/p/virtual-waiting-room) |

## Generic Patterns

| Problem | Pattern | Link |
|---------|---------|------|
| Presence (online/offline) | Heartbeat + timeout | [Read](https://systemdesign.one/real-time-presence-platform-system-design/) |
| Live comments | Fan-out on write | [Read](https://systemdesign.one/live-comment-system-design/) |
| Leaderboards | Sorted sets + pub/sub | [Read](https://systemdesign.one/leaderboard-system-design/) |

## Key Technologies

### Connection Protocols

| Protocol | Use Case | Pros | Cons |
|----------|----------|------|------|
| **WebSocket** | Bidirectional real-time | Full duplex, low latency | Connection overhead |
| **Server-Sent Events** | Server → client only | Simple, auto-reconnect | One direction only |
| **Long Polling** | Fallback option | Works everywhere | Higher latency |
| **RSocket** | Reactive streams | Backpressure support | Less mature |

### Message Delivery Patterns

| Pattern | Description | Use When |
|---------|-------------|----------|
| **Fan-out on write** | Pre-compute and push to all followers | Read-heavy, small fan-out |
| **Fan-out on read** | Compute feed at read time | Write-heavy, large fan-out |
| **Hybrid** | Hot users: write, Cold users: read | Best of both worlds |

## Design Considerations

### Presence System
- How often to send heartbeats?
- How long before marking offline?
- How to handle network partitions?

### Message Ordering
- Total ordering vs causal ordering
- Vector clocks for conflict resolution
- Last-write-wins vs merge

### Scaling WebSockets
- Connection limits per server
- Sticky sessions vs stateless
- Horizontal scaling strategies

## Questions to Consider

1. What's acceptable latency for your use case?
2. Can you tolerate message loss?
3. How do you handle reconnection?
4. What happens during network partitions?
