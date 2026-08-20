# Topic 04 — Azure Managed Redis (Cache & Vector Search)

> **Domain A (25–30%)** — official skill A3  
> **Module:** [`../02-language-conversational.md`](../02-language-conversational.md)

---

## In one sentence

**Azure Managed Redis** provides **low-latency caching** (TTL, invalidation) and **vector indexing** for similarity search on hot corpora — not a replacement for authoritative document storage.

---

## Why it exists on the exam

AI-200 explicitly lists Redis **caching/expiration/invalidation** and **vector indexing**. Trap: thinking Redis is "only a key-value cache."

---

## How it works in Azure

### Caching patterns for AI APIs

| Cache what | Key pattern | TTL |
|------------|-------------|-----|
| Embedding for unchanged text | `emb:{sha256(text)}` | Long (hours/days) |
| Full RAG answer | `ans:{tenant}:{query_hash}` | Short (minutes) |
| Rate limit counters | `rl:{client_id}:{minute}` | 60s |

```python
import redis
import json
import hashlib

r = redis.Redis(host="<cache>.redis.cache.windows.net", port=6380, ssl=True, password="<key>")

def get_or_embed(text: str, embed_fn):
    key = "emb:" + hashlib.sha256(text.encode()).hexdigest()
    cached = r.get(key)
    if cached:
        return json.loads(cached)
    vector = embed_fn(text)
    r.setex(key, 86400, json.dumps(vector))  # 24h TTL
    return vector
```

### Invalidation

When source document changes:

```python
def invalidate_document(tenant_id: str, document_id: str):
    # Delete known answer keys for doc (maintain index set on write)
    for key in r.smembers(f"dockeys:{tenant_id}:{document_id}"):
        r.delete(key)
    r.delete(f"dockeys:{tenant_id}:{document_id}")
```

**Exam point:** Cache without invalidation → **stale AI answers**.

### Vector indexing (Redis vector search)

Redis supports vector fields in indices (RediSearch/Redis Stack capabilities — verify GA on Azure Managed Redis docs):

```text
  HOT corpus (frequently queried SKUs, FAQs)
        │
        ▼
  Redis vector index (HNSW/FLAT)
        │
        ▼
  Sub-millisecond top-k for retrieval layer
        │
        ▼
  Optional: fall back to PostgreSQL/Cosmos for cold/full corpus
```

**Tiered retrieval architecture:**

1. Redis — hot, low-latency vectors + cache
2. PostgreSQL/Cosmos — source of truth, full corpus
3. On cache miss → query authoritative store → warm Redis

---

## When to use / avoid

| Use Redis | Don't use Redis alone |
|-----------|----------------------|
| Hot path latency SLAs | Sole copy of embeddings with no backup |
| Session/cache layers | Complex governance/audit as primary store |
| Ephemeral rate limiting | Long-term document archive |

---

## ⚠️ Exam traps

1. **Redis as only vector DB** with no persistence strategy — wrong for compliance scenarios.
2. **No TTL/invalidation** — stale cached answers after doc update.
3. **Caching PII-heavy responses** without encryption/TTL policy.
4. **Same secret forever** — rotate access keys via Key Vault (prefer MI where available).

---

## Checkpoint questions

**Q1.** FAQ bot; 500 questions served 1000x/day. Optimization?  
<details><summary>Answer</summary>Cache embeddings and/or retrieval results with TTL; invalidate on FAQ update.</details>

**Q2.** Exam asks about "vector indexing" on Azure Managed Redis. Meaning?  
<details><summary>Answer</summary>Store vectors in Redis index for similarity search — not only string caching.</details>

**Q3.** Document updated; users still get old cached answer. Fix?  
<details><summary>Answer</summary>Invalidation on write event (Event Grid/change feed → purge cache keys).</details>

---

## Skills checklist (official A3)

- [ ] Caching, expiration, invalidation
- [ ] Vector indexing for similarity search

---

## Next topic

[05 — RAG & vector retrieval design](./05-rag-vector-retrieval.md)
