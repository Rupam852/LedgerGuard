# 🌐 LedgerGuard: API Gateway & Cryptographic Routing

**Maintainer:** Anish Das  
**Role:** Backend & API Gateway Lead  
**Branch:** `anish-das`  

---

## 🎯 Domain Overview

The API Gateway is the central entry point for all tenant interactions in LedgerGuard. It handles asymmetric JWT decoding, extracts organization and tenant claims, establishes execution context isolation using Node.js `AsyncLocalStorage`, and verifies RSA-256 payload signatures before dispatching financial operations.

### Key Modules:
1. `tenantContextMiddleware`: Binds `tenantId` and `organizationId` to execution context preventing cross-request pollution.
2. `jwtTenantAuthMiddleware`: Validates asymmetric JWT signatures and enforces strict tenant scope matching.
3. `cryptoVerifierMiddleware`: RSA-256 zero-knowledge signature verification guarding billing endpoints.
4. `billingRouter`: Idempotent billing endpoints with distributed lock orchestration.
5. `tenantsRouter`: Automated enterprise tenant provisioning.

---

## 🏃 Running the Gateway

```bash
npm run dev
```
Starts the API gateway on `http://localhost:5000`.


### Day 11 Audit (Nov 20, 2026)
- Profiled JSON rawBody capture and Helmet security header middleware stack; overhead under 0.15ms per request.

### Day 12 Audit (Nov 21, 2026)
- Hardened 2000-calls/month quota boundary checks in billing route; verified 429 quota exceeded response.

### Day 13 Audit (Nov 22, 2026)
- Tightened express.json schema validation with strict RFC-7807 problem details error responses.

### Day 14 Audit (Nov 23, 2026)
- Audited CORS exposedHeaders (X-Request-ID, X-Tenant-ID, X-Crypto-Verified) and 15-minute onboarding token TTL.

### Day 15 Audit (Nov 24, 2026)
- Tested SPKI PEM and Base64 X-Public-Key public header decoding edge cases across node:crypto verifiers.

### Day 16 Audit (Nov 25, 2026)
- Stress-tested AsyncLocalStorage context propagation under 500 concurrent async operations with 0 context bleed.
