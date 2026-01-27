# API Design

Building robust, scalable APIs that handle real-world challenges.

## Core Resources

| Resource | Description | Link |
|----------|-------------|------|
| Rate Limiting | Stripe's approach | [Read](https://newsletter.systemdesign.one/p/rate-limiter) |
| Idempotent APIs | Prevent duplicate operations | [Read](https://newsletter.systemdesign.one/p/idempotent-api) |
| Protocol Buffers | LinkedIn's 60% latency reduction | [Read](https://newsletter.systemdesign.one/p/protocol-buffers-vs-json) |

## Rate Limiting

### Why Rate Limit?

- Prevent abuse
- Ensure fair usage
- Protect backend services
- Control costs

### Algorithms

| Algorithm | Description | Best For |
|-----------|-------------|----------|
| **Token Bucket** | Tokens added at fixed rate, consumed per request | Allows bursts |
| **Leaky Bucket** | Requests processed at fixed rate | Smooth output |
| **Fixed Window** | Count requests per time window | Simple |
| **Sliding Window** | Rolling time window | More accurate |

### Token Bucket

```
Bucket capacity: 10 tokens
Refill rate: 1 token/second

Request 1: 10 tokens → 9 tokens (allowed)
Request 2: 9 tokens → 8 tokens (allowed)
...
Request 11: 0 tokens → rejected (429 Too Many Requests)
Wait 1 second: 1 token added
Request 12: 1 token → 0 tokens (allowed)
```

### Implementation Considerations

```
Where to limit:
├── Client-side (advisory)
├── Load balancer (network protection)
├── API Gateway (per-API limits)
└── Application (business logic limits)

What to limit by:
├── IP address
├── API key
├── User ID
└── Endpoint
```

[Stripe's rate limiting deep dive](https://newsletter.systemdesign.one/p/rate-limiter)

## Idempotency

### The Problem

```
Client: POST /charge {amount: 100}
Server: Process... (success)
Network: Response lost
Client: POST /charge {amount: 100} (retry)
Server: Process... (charges twice!)
```

### The Solution

```
Client: POST /charge {amount: 100, idempotency_key: "abc123"}
Server: Process, store result with key
Network: Response lost
Client: POST /charge {amount: 100, idempotency_key: "abc123"} (retry)
Server: Return cached result (no duplicate charge)
```

### Implementation

```
1. Client generates unique key per logical operation
2. Server stores: idempotency_key → {status, response}
3. On retry, return stored response
4. Keys expire after reasonable TTL (24-48 hours)
```

[Stripe's idempotency implementation](https://newsletter.systemdesign.one/p/idempotent-api)

## API Protocols

### REST

```
GET    /users/123      # Read
POST   /users          # Create
PUT    /users/123      # Update (full)
PATCH  /users/123      # Update (partial)
DELETE /users/123      # Delete
```

**Pros**: Simple, cacheable, widely understood
**Cons**: Multiple round trips, over-fetching

### GraphQL

```graphql
query {
  user(id: "123") {
    name
    posts(limit: 10) {
      title
    }
  }
}
```

**Pros**: Single request, client specifies data
**Cons**: Complexity, caching harder

### gRPC

```protobuf
service UserService {
  rpc GetUser(UserRequest) returns (User);
  rpc StreamUsers(Empty) returns (stream User);
}
```

**Pros**: Fast (binary), streaming, code generation
**Cons**: Not browser-native, less human-readable

### Comparison

| Aspect | REST | GraphQL | gRPC |
|--------|------|---------|------|
| **Format** | JSON | JSON | Protobuf |
| **Speed** | Medium | Medium | Fast |
| **Flexibility** | Low | High | Medium |
| **Browser support** | Native | Native | Via proxy |
| **Learning curve** | Low | Medium | High |

## Protocol Buffers

LinkedIn reduced latency by 60% switching from JSON to Protocol Buffers.

### Why Faster?

| JSON | Protobuf |
|------|----------|
| Text-based | Binary |
| Self-describing | Schema required |
| ~100 bytes | ~50 bytes |
| Parse: slow | Parse: fast |

[LinkedIn case study](https://newsletter.systemdesign.one/p/protocol-buffers-vs-json)

## Versioning

### Strategies

| Strategy | Example | Pros | Cons |
|----------|---------|------|------|
| **URL path** | `/v1/users` | Clear, cacheable | URL pollution |
| **Query param** | `/users?version=1` | Optional | Easy to miss |
| **Header** | `Accept: application/vnd.api.v1+json` | Clean URLs | Hidden |

### Breaking vs Non-Breaking Changes

**Non-breaking** (usually safe):
- Adding optional fields
- Adding new endpoints
- Adding new enum values

**Breaking** (requires new version):
- Removing fields
- Changing field types
- Changing required/optional
- Changing semantics

## Error Handling

### HTTP Status Codes

| Code | Meaning | When |
|------|---------|------|
| 200 | OK | Success |
| 201 | Created | Resource created |
| 400 | Bad Request | Client error |
| 401 | Unauthorized | Auth required |
| 403 | Forbidden | Auth insufficient |
| 404 | Not Found | Resource missing |
| 429 | Too Many Requests | Rate limited |
| 500 | Server Error | Our fault |
| 503 | Service Unavailable | Temporarily down |

### Error Response Format

```json
{
  "error": {
    "code": "RATE_LIMITED",
    "message": "Too many requests",
    "details": {
      "retry_after": 60,
      "limit": 100,
      "remaining": 0
    }
  }
}
```

## Pagination

### Offset-based

```
GET /users?offset=20&limit=10
```

**Pros**: Simple, random access
**Cons**: Inconsistent with changes, slow for large offsets

### Cursor-based

```
GET /users?cursor=eyJpZCI6MTAwfQ&limit=10
```

**Pros**: Consistent, efficient
**Cons**: No random access

## Questions to Consider

1. Who are your API consumers?
2. What's the expected request rate?
3. How will you version?
4. What's the error contract?
5. How will you document?
