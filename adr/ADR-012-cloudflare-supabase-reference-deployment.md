---
id: ADR-012
version: 1.0.0
authority: informative
owner: Platform Architecture
date: "2026-08-12"
title: Cloudflare and Supabase Reference Deployment
status: proposed
related_specs:
- SPEC-002A
- SPEC-006
- SPEC-020
---

# ADR-012: Cloudflare and Supabase Reference Deployment

## Context

The Autonomous Giving implementation previously described Vercel and GitHub Pages as public hosting while Supabase already supplied platform state. The platform specification must preserve vendor-neutral conformance while recording a material implementation deployment decision.

## Decision

For the current Autonomous Giving reference implementation: GitHub owns source and CI; Cloudflare Workers owns edge delivery and optional lightweight edge compute; Supabase owns persistent state and identity. The present AGI public site remains a static export delivered by Workers Static Assets.

## Consequences

Positive: fewer infrastructure roles, globally distributed static delivery, no persistent application server, retained PostgreSQL/Auth investment, and an incremental Worker API path.

Negative: Cloudflare deployment tooling; later dynamic code needs Worker-runtime compatibility testing; OpenNext requires separate evaluation when static export no longer fits.

## Rejected alternatives

- Keep Vercel: no longer the chosen public-delivery owner.
- Render plus Supabase: adds a long-running server without a current need.
- Replace Supabase with Cloudflare D1: creates an unnecessary state migration and abandons existing Auth/RLS/PostgreSQL boundaries.
- Immediate OpenNext: no verified SSR or other runtime requirement.
- Distributed or microservice deployment: adds operational complexity before demonstrated need.

This ADR is informative and does not change platform conformance or require a vendor.
