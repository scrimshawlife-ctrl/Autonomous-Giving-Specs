---
id: SPEC-020
title: Reference Deployment Profiles
version: 1.1.0
status: accepted
authority: informative
owner: Platform Architecture
related_specs:
- SPEC-002A
- SPEC-006
- SPEC-011
- SPEC-013
related_adrs:
- ADR-001
- ADR-010
- ADR-012
related_contracts: []
---

# SPEC-020: Reference Deployment Profiles

## Purpose and authority

Publish **informative** deployment profiles. They are examples, not conformance requirements: implementations MAY choose another topology that preserves the platform capabilities, contracts, lifecycle, and security boundaries.

## Profile A — Demo

| Element | Choice |
| --- | --- |
| Frontend | Static host or equivalent |
| Data | Static fixtures |
| Backend | None required |
| Secrets | None |

Use for narrative demos and deterministic replay without operational systems.

## Profile B — MVP (recommended)

```text
Static/Web Frontend
        ↓
Edge Application Runtime (optional, request-driven)
        ↓
Modular Platform Capabilities
        ↓
PostgreSQL + Object Storage
```

| Characteristic | Value |
| --- | --- |
| Frontend | Static-first web application |
| Edge runtime | Optional; request-driven only when a runtime boundary is needed |
| Database | One primary PostgreSQL |
| Storage | Object storage for evidence binaries |
| Authentication | OIDC-compatible and implementation-selected |
| Background work | Managed function or worker only when required |
| Architecture | Modular monolith first; capabilities remain distinct in code |
| Orchestration / broker / service mesh | Not required |

### Informative Autonomous Giving reference implementation

The present Autonomous Giving implementation uses GitHub for source and CI, Cloudflare Workers Static Assets for public edge delivery, and Supabase for Auth, PostgreSQL, RLS, Storage, and data-centric Edge Functions. This is a practical reference, not a vendor requirement. Its current AGI public surface is a static export; Worker APIs and runtime projections remain future work.

## Profile C — Production

Optional horizontal scaling, separate managed background work, or an edge runtime can be introduced with operational justification while retaining the same modular logical system.

## Profile D — Enterprise

Optional extraction, streaming, Kubernetes, and multi-region operation. Adopt only when the extraction criteria in [SPEC-002A](SPEC-002A-architectural-principles.md) are met.

## Non-goals

This document does not prescribe cloud vendors, IaC tools, D1, a second database, a full Next.js runtime, or distributed infrastructure. It does not make Profile D the reference shape.
