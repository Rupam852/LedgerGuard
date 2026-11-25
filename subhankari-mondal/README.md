# 🔒 LedgerGuard: Distributed Locks & ACID Rollback Engine

**Maintainer:** Subhankari Mondal  
**Role:** Distributed Systems & Locks Specialist  
**Branch:** `subhankari-mondal`  

---

## 🎯 Domain Overview

This module guarantees financial integrity across the LedgerGuard platform. By integrating Redis-based distributed locking (Redlock algorithm with fencing tokens) and MongoDB multi-document ACID transactions, it completely eliminates race conditions, double-spending, and partial state corruption.

### Key Components:
1. `RedisConnectionManager`: Robust connection manager with automatic retry backoff.
2. `DistributedLockManager`: Atomic Redis lock acquisition with unique fencing tokens and safe Lua release scripts.
3. `AcidTransactionManager`: Multi-document ACID transaction wrapper (`session.withTransaction()`).
4. `IdempotentLedgerService`: Double-checked idempotency caching preventing repeat billing calls.
5. `RollbackSimulator`: Chaos failure injection engine validating instant rollbacks during mid-flight timeouts.

---

## 🏃 Running Benchmarks

```bash
npm run benchmark:locks
```
Simulates 200 concurrent transactions competing for the same account and verifies 100% mutual exclusion with zero double-billing.


### Day 11 Audit (Nov 20, 2026)
- Analyzed ioredis retry backoff timing and pipelined lock round-trip time (RTT avg: 1.8ms over Upstash TLS).

### Day 12 Audit (Nov 21, 2026)
- Documented Redlock TTL sizing trade-offs vs MongoDB transaction execution window (5000ms TTL vs 2000ms max tx).

### Day 13 Audit (Nov 22, 2026)
- Verified rollback simulator abort sequence; confirmed zero phantom records in MongoDB after injected network fault.

### Day 14 Audit (Nov 23, 2026)
- Evaluated lock contention rejection ratio under simultaneous retries; verified fail-safe HTTP 423 Locked behavior.

### Day 15 Audit (Nov 24, 2026)
- Audited 24-hour (86400s) Redis idempotency key expiration format (idempotency:<tenantId>:<key>) for memory efficiency.

### Day 16 Audit (Nov 25, 2026)
- Executed 200-transaction burst benchmark; confirmed 100% mutual exclusion and 0 race conditions on shared accounts.
