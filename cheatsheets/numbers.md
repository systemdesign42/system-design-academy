# Numbers Everyone Should Know

Essential numbers for back-of-envelope calculations in system design.

## Latency Numbers

| Operation | Time |
|-----------|------|
| L1 cache reference | 0.5 ns |
| L2 cache reference | 7 ns |
| Main memory reference | 100 ns |
| SSD random read | 150 μs |
| HDD seek | 10 ms |
| Network round trip (same datacenter) | 0.5 ms |
| Network round trip (cross-continent) | 150 ms |

### Memory Hierarchy

```
L1 Cache:     ~1 ns       ████
L2 Cache:     ~10 ns      ████████
RAM:          ~100 ns     ████████████████
SSD:          ~100 μs     ████████████████████████████████
HDD:          ~10 ms      ████████████████████████████████████████
```

## Time Conversions

| Unit | Seconds | Approximate |
|------|---------|-------------|
| 1 minute | 60 | 60 |
| 1 hour | 3,600 | ~4K |
| 1 day | 86,400 | ~100K |
| 1 week | 604,800 | ~600K |
| 1 month | 2,592,000 | ~2.5M |
| 1 year | 31,536,000 | ~30M |

**Quick trick**: 1 day ≈ 100K seconds

## Data Size

| Unit | Bytes | Use Case |
|------|-------|----------|
| 1 KB | 1,000 | Tweet, small JSON |
| 1 MB | 1,000,000 | High-res photo |
| 1 GB | 10^9 | Movie, 1 hour video |
| 1 TB | 10^12 | Large database |
| 1 PB | 10^15 | Enterprise data |

### Common Data Sizes

| Data | Size |
|------|------|
| UUID | 36 bytes |
| Timestamp | 8 bytes |
| Tweet (280 chars) | ~1 KB with metadata |
| Profile photo | ~200 KB |
| High-res image | ~2 MB |
| 1 min video (HD) | ~150 MB |

## Throughput

| System | Throughput |
|--------|------------|
| HDD | 100 MB/s sequential |
| SSD | 500 MB/s - 3 GB/s |
| 1 Gbps network | 125 MB/s |
| 10 Gbps network | 1.25 GB/s |
| RAM | 20+ GB/s |

## QPS Estimates

| Scale | Requests/Second |
|-------|-----------------|
| Small startup | 100 |
| Medium service | 10K |
| Large service | 100K |
| Major platform | 1M+ |

### Server Capacity (Rule of Thumb)

| Server Type | Capacity |
|-------------|----------|
| Web server | 1K-10K req/sec |
| Database (read) | 10K queries/sec |
| Database (write) | 1K writes/sec |
| Cache (Redis) | 100K+ ops/sec |

## Availability

| Availability | Downtime/Year | Downtime/Month |
|--------------|---------------|----------------|
| 99% (two 9s) | 3.65 days | 7.3 hours |
| 99.9% (three 9s) | 8.76 hours | 43.8 minutes |
| 99.99% (four 9s) | 52.6 minutes | 4.38 minutes |
| 99.999% (five 9s) | 5.26 minutes | 26.3 seconds |

## Quick Estimation Examples

### Twitter Storage

```
500M tweets/day × 1 KB = 500 GB/day
500 GB × 365 = ~180 TB/year
```

### Instagram Photo Storage

```
100M photos/day × 2 MB = 200 TB/day
With 3x replication = 600 TB/day
```

### Chat Application Bandwidth

```
1B messages/day × 1 KB = 1 TB/day
1 TB / 86,400 sec = ~12 MB/sec average
Peak (10x) = 120 MB/sec = ~1 Gbps
```

## Powers of 2

| Power | Value | Approximate |
|-------|-------|-------------|
| 2^10 | 1,024 | 1 Thousand (KB) |
| 2^20 | 1,048,576 | 1 Million (MB) |
| 2^30 | 1,073,741,824 | 1 Billion (GB) |
| 2^40 | | 1 Trillion (TB) |

## The "Rule of 72"

To estimate doubling time with growth rate:

```
Doubling time ≈ 72 / growth rate (%)

Example: 10% growth/month
Doubling time ≈ 72/10 = 7.2 months
```

## Interview Tips

1. **Round aggressively**: 86,400 → 100,000
2. **Use powers of 10**: Easier mental math
3. **State assumptions**: "Assuming 1KB per record..."
4. **Show your work**: Process matters
5. **Sanity check**: Does the answer make sense?
