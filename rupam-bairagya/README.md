# 🖥️ LedgerGuard: Enterprise Multi-Tenant Billing Dashboard

**Maintainer:** Rupam Bairagya  
**Role:** Team Lead & Frontend Architect  
**Branch:** `rupam-bairagya`  

---

## 🎯 Domain Overview

The Enterprise Frontend provides a responsive, high-fidelity administrative portal for managing multi-tenant SaaS billing, inspecting financial transaction ledgers, triggering live ACID rollback demonstrations, and cryptographically signing payloads with RSA-256 in the browser.

### Key Capabilities:
1. `TenantSwitcher`: Dropdown allowing administrators to switch between isolated tenant namespaces (`acme_corp`, `globex_corp`, `soylent_corp`).
2. `RollbackVisualizerModal`: 5-step live chaos injection simulator demonstrating how mid-flight network drops automatically abort MongoDB ACID transactions and release Redis Redlocks without double-charging.
3. `BillingLedgerView`: Filterable financial ledger stream with status tracking (`COMMITTED`, `ROLLED_BACK`, `PENDING`).
4. `TenantsManagementView`: Directory of provisioned tenants, tier quotas, and database namespaces.
5. `SecurityAuditView`: In-browser 2048-bit RSA key generation and zero-knowledge signature verification tool.

---

## 🏃 Running the Dashboard

```bash
npm run dev
```
Starts the Vite development server on `http://localhost:5173`.



### Day 11 Audit (Nov 20, 2026)
- Profiled and memoized TenantSwitcher dropdown and ledger filter renders (re-render latency under 1.2ms).

### Day 12 Audit (Nov 21, 2026)
- Verified CSV audit export formatting with RFC-4180 escaping and GST SAC 998313 tax split columns.

### Day 13 Audit (Nov 22, 2026)
- Calibrated enterprise slate dark-mode contrast ratios to WCAG 2.1 AA (4.5 to 1 minimum) across card badges.

### Day 14 Audit (Nov 23, 2026)
- Hardened active view tab synchronization with window.history.pushState and popstate event listeners.

### Day 15 Audit (Nov 24, 2026)
- Added automated test specs for Union Territory GST (Delhi, Ladakh, Jammu and Kashmir) and Base64 PEM RSA edge cases.
