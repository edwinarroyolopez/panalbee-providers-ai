# Project Discovery Question Bank

## How to use this bank

This is a reservoir of possible questions. It is not a mandatory form.

Rules:

- pick only unresolved, high-impact questions
- prefer fewer questions with clear decision value
- skip any question already answered by the user

## Categories and candidate questions

### 1) Product identity

- What is the product name (working name is fine)?
- What outcome must this product guarantee in v1?
- What is explicitly out of scope for v1?

### 2) Users and actors

- Who are the primary users?
- Are there internal operators/admins distinct from end users?
- Which actor decisions must be enforceable by role/capability?

### 3) Surfaces and channels

- Which clients ship in v1 (web, app, backend-only, mixed)?
- Which actions are allowed per surface?
- Is any flow surface-exclusive?

### 4) Domain and bounded contexts

- What are the top domain entities (3-10)?
- Which entity is the operational root of daily work?
- Which bounded contexts should be separate from day one?

### 5) Auth model

- How do users authenticate (OTP, password, SSO, hybrid)?
- What session model is expected (token, refresh token, short session)?
- Any compliance/security constraints for auth?

### 6) Tenancy and scope

- Is the product single-tenant or multi-tenant?
- What is the active scope in runtime (account, workspace, org, branch)?
- Can users belong to multiple scopes?

### 7) Capabilities and gating

- Which features are gated by capability or plan?
- Is gating backend-enforced, frontend-only, or both?
- Do we need upgrade prompts and limit warnings in v1?

### 8) Billing and plans

- Is there paid billing from v1?
- Which billing concepts exist (tier, billingPlan, usage limits)?
- What events can change plan/entitlements?

### 9) Core workflows

- What are the top 3-5 operational flows?
- Which flow is the first production-critical flow?
- What failure states must be visible to users?

### 10) Data, offline, and sync

- Is offline behavior required on app?
- What data must remain consistent across reconnects?
- Are there local-first or queue/retry constraints?

### 11) Integrations

- Which external systems are required in v1?
- Which integrations are blocking vs optional?
- Any webhook/event-driven contracts expected?

### 12) Metrics and traceability

- What must be measurable from day one?
- Which events need immutable audit traceability?
- Which KPIs drive product decisions?

### 13) Starter inheritance decisions

- Which starter examples are kept, quarantined, or removed?
- Any legacy vocabulary that must be forbidden in this project?
- Which existing agents/skills are definitely reusable here?

## Priority guidance

Ask in this order unless user context already resolves it:

1. identity + users + surfaces
2. domain + auth + tenancy
3. capabilities + billing
4. workflows + integrations + metrics
5. inheritance cleanup details
