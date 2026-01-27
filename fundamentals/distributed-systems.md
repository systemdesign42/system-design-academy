# Distributed Systems

Protocols, patterns, and data structures for building reliable distributed systems.

## Core Resources

| Resource | Description | Link |
|----------|-------------|------|
| Gossip Protocol | Decentralized communication | [Read](https://systemdesign.one/gossip-protocol/) |
| Hinted Handoff | Availability during failures | [Read](https://systemdesign.one/hinted-handoff/) |
| Consistent Hashing | Key distribution | [Read](https://systemdesign.one/consistent-hashing-explained/) |
| Service Discovery | How services find each other | [Read](https://systemdesign.one/what-is-service-discovery/) |

## White Papers

| System | Key Innovation | Link |
|--------|----------------|------|
| Amazon Dynamo | Eventual consistency at scale | [Read](https://newsletter.systemdesign.one/p/amazon-dynamo-architecture) |
| Google Spanner | Global transactions | [Read](https://newsletter.systemdesign.one/p/cloud-spanner-database) |

## Fundamental Challenges

### The Eight Fallacies

1. The network is reliable
2. Latency is zero
3. Bandwidth is infinite
4. The network is secure
5. Topology doesn't change
6. There is one administrator
7. Transport cost is zero
8. The network is homogeneous

**Reality**: Networks fail, latency varies, packets are lost.

## Communication Protocols

### Gossip Protocol

```
Node A knows X
    ↓ tells random node
Node B now knows X
    ↓ tells random nodes
Eventually everyone knows X
```

**Properties**:
- Decentralized (no leader)
- Eventually consistent
- Fault tolerant
- Scalable

**Use cases**: Membership, failure detection, data dissemination

[Deep dive](https://systemdesign.one/gossip-protocol/)

### Hinted Handoff

```
Normal: Client → Node A (owner)

During failure:
Client → Node B (stores hint for A)
         ↓
When A recovers, B hands off data
```

**Purpose**: Maintain availability when nodes fail temporarily.

[Deep dive](https://systemdesign.one/hinted-handoff/)

## Consensus

How multiple nodes agree on a value.

### Raft/Paxos (Leader-based)

```
1. Leader election
2. Leader proposes value
3. Followers accept
4. Committed when majority agrees
```

### Quorum

```
N = 5 nodes
W = 3 (write quorum)
R = 3 (read quorum)

W + R > N ensures overlap
```

| Configuration | Consistency | Availability |
|---------------|-------------|--------------|
| W=N, R=1 | Strong | Lower (all must be up for writes) |
| W=1, R=N | Weak writes | Lower (all must be up for reads) |
| W=Q, R=Q | Tunable | Balanced |

## Data Structures

### Bloom Filter

```
Question: "Is X in the set?"
Answer: "Definitely no" or "Probably yes"

False positives possible
False negatives impossible
```

**Properties**:
- Space efficient
- O(1) lookup
- No deletions (standard)

**Use cases**: Cache checks, duplicate detection, spell checking

[Deep dive](https://systemdesign.one/bloom-filters-explained/)

### Quotient Filter

Similar to Bloom filter but:
- Supports deletions
- More cache-friendly
- Can be resized

[Deep dive](https://systemdesign.one/quotient-filter-explained/)

### Consistent Hashing

```
Hash Ring:
        0°
        │
   270° ┼ 90°
        │
       180°

Nodes: A(30°), B(120°), C(240°)
Key "user:1" hashes to 100° → stored on B
```

**Property**: When nodes change, only K/n keys need to move.

[Deep dive](https://systemdesign.one/consistent-hashing-explained/)

### Vector Clocks

```
[A:1, B:0, C:0]  Event at A
[A:1, B:1, C:0]  Event at B
[A:1, B:0, C:1]  Event at C

Compare:
[A:2, B:1] > [A:1, B:1]  (A happened after)
[A:1, B:2] || [A:2, B:1]  (concurrent)
```

**Purpose**: Track causality in distributed systems.

## Service Discovery

How services find each other in dynamic environments.

### Patterns

| Pattern | How | Example |
|---------|-----|---------|
| **DNS-based** | Resolve service name | AWS Route 53 |
| **Registry** | Central service catalog | Consul, etcd |
| **Sidecar** | Local proxy | Envoy, Istio |

[Deep dive](https://systemdesign.one/what-is-service-discovery/)

## Failure Handling

### Circuit Breaker

```
Closed → (failures exceed threshold) → Open
   ↑                                      ↓
   └──── (success after timeout) ←── Half-Open
```

**Purpose**: Fail fast, prevent cascade failures.

### Bulkhead

```
Pool A (service X) ─── limited threads
Pool B (service Y) ─── limited threads

If A exhausted, B still works
```

**Purpose**: Isolate failures.

### Retry with Backoff

```
Attempt 1: wait 0s
Attempt 2: wait 1s
Attempt 3: wait 2s
Attempt 4: wait 4s (exponential)
```

**Add jitter** to prevent thundering herd.

## Architecture Patterns

### Cell-Based Architecture

```
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│   Cell 1    │ │   Cell 2    │ │   Cell 3    │
│ (Users 1-N) │ │ (Users N-M) │ │ (Users M-Z) │
│   [Full     │ │   [Full     │ │   [Full     │
│    Stack]   │ │    Stack]   │ │    Stack]   │
└─────────────┘ └─────────────┘ └─────────────┘
```

**Purpose**: Limit blast radius of failures.

[Deep dive](https://newsletter.systemdesign.one/p/cell-based-architecture)

### Actor Model

```
        ┌─────────┐
        │ Actor A │ ← messages only
        └────┬────┘
             │
    ┌────────┼────────┐
    ↓        ↓        ↓
┌─────┐  ┌─────┐  ┌─────┐
│  B  │  │  C  │  │  D  │
└─────┘  └─────┘  └─────┘
```

**Properties**:
- No shared state
- Communicate via messages
- Each actor processes sequentially

[Deep dive](https://newsletter.systemdesign.one/p/actor-model)

## Questions to Consider

1. What happens when a node fails?
2. How do you detect failures?
3. What's the consistency requirement?
4. How do you handle network partitions?
5. What's the recovery strategy?
