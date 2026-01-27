# Search & Discovery Case Studies

How companies help users find what they're looking for at massive scale.

## The Search Challenge

```
Query → Understand Intent → Search Index → Rank Results → Return Fast

All in < 200ms for billions of documents
```

## Case Studies

### Web Search

| Company | Scale | Key Innovation | Link |
|---------|-------|----------------|------|
| Google | The entire web | PageRank, distributed indexing | [Read](https://newsletter.systemdesign.one/p/search-engine-architecture) |

### Geospatial Search

| Company | Challenge | Solution | Link |
|---------|-----------|----------|------|
| Uber | Find nearby drivers | Geospatial indexing (1M req/sec) | [Read](https://newsletter.systemdesign.one/p/how-does-uber-find-nearby-drivers) |
| Uber | Calculate ETA | Graph algorithms (500K req/sec) | [Read](https://newsletter.systemdesign.one/p/uber-eta) |
| Tinder | Match nearby users | Location-based matching (1.6B swipes/day) | [Read](https://newsletter.systemdesign.one/p/tinder-architecture) |

### Content Discovery

| Company | Challenge | Solution | Link |
|---------|-----------|----------|------|
| Hashnode | Generate personalized feeds | Feed architecture | [Read](https://newsletter.systemdesign.one/p/feed-architecture) |
| Netflix | Content recommendations | ML-powered discovery | [Read](https://newsletter.systemdesign.one/p/how-does-netflix-work) |

## Generic Design Problems

| Problem | Key Concepts | Link |
|---------|--------------|------|
| Leaderboard | Sorted sets, real-time updates | [Read](https://systemdesign.one/leaderboard-system-design/) |
| Distributed Counter | Eventual consistency, aggregation | [Read](https://systemdesign.one/distributed-counter-system-design/) |

## Search Architecture Components

### Indexing Pipeline

```
Raw Data → Extract → Transform → Index → Serve
              ↓
         Tokenize
         Normalize
         Analyze
```

### Index Types

| Type | Use Case | Example |
|------|----------|---------|
| **Inverted index** | Full-text search | Elasticsearch |
| **Geospatial index** | Location queries | PostGIS, H3 |
| **Vector index** | Similarity search | Pinecone, Milvus |
| **Graph index** | Relationship queries | Neo4j |

### Ranking Factors

| Factor | Description |
|--------|-------------|
| **Relevance** | How well does result match query? |
| **Freshness** | How recent is the content? |
| **Popularity** | How many people engaged with it? |
| **Personalization** | User preferences and history |
| **Location** | Geographic relevance |

## Geospatial Systems

### Spatial Indexing

| Method | Description | Use Case |
|--------|-------------|----------|
| **Geohash** | Hierarchical grid | Proximity search |
| **H3** | Hexagonal grid | Uber's approach |
| **R-tree** | Bounding box tree | Range queries |
| **Quadtree** | Recursive subdivision | Sparse data |

### Uber's Driver Matching

1. **Index**: Drivers indexed by H3 cell
2. **Query**: Find cells near rider
3. **Filter**: Check availability, ETA
4. **Rank**: Score by distance, rating
5. **Match**: Dispatch to best driver

## Feed Generation

### Push vs Pull

| Model | How It Works | Best For |
|-------|--------------|----------|
| **Push (fan-out on write)** | Pre-compute feeds when content created | Small follower counts |
| **Pull (fan-out on read)** | Compute feed when user requests | Large follower counts |
| **Hybrid** | Push for active users, pull for inactive | Most social networks |

### Feed Ranking

- Chronological (simple, predictable)
- Engagement-based (more addictive)
- ML-ranked (personalized)

## Performance Optimization

### Caching Strategies
- Cache popular queries
- Cache user feeds
- Cache search suggestions

### Sharding Strategies
- By document ID (even distribution)
- By date (time-series data)
- By geography (location data)

## Questions to Consider

1. How fresh must results be?
2. What's the query latency budget?
3. How do you handle typos and synonyms?
4. How do you prevent gaming/spam?
5. How do you A/B test ranking changes?

## Design Exercise

Design a location-based search system that:
- Finds restaurants within 5km
- Handles 100K queries/second
- Returns results in < 100ms
- Supports filtering (cuisine, price, rating)
- Provides personalized ranking
