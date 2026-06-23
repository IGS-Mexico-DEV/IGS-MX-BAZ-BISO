# Annex - Guides and Manuals Evidence

## 1. Purpose

This annex summarizes the documentation currently available for implementation, administration, and use of IGS Billing.

This annex should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Available Documentation

### A. Implementation documentation

- `README.md` installation steps.
- Environment configuration guidance.
- Database setup instructions.
- Frontend build instructions.
- Production optimization steps.
- Deployment and hardening checklist.

### B. Administration documentation

- `docs/security-hardening-guide.md`.
- `docs/patch-management.md`.
- `docs/sdlc.md`.
- `docs/api/health-check.md`.

### C. User / usage documentation

- `docs/api/api-documentation.md`.
- `docs/api/auth/auth.md`.
- API usage examples in `README.md`.

## 3. Operational Context Included in This Response

The following service-delivery context was provided for this assessment and is relevant to how the manuals should be interpreted:

- The solution lives in IGS infrastructure.
- GS accesses the solution via web.
- Access is protected by VPN.
- Access uses a controlled URL.
- Access is restricted by IP whitelist controls.

## 4. Audit Position

The current evidence supports a **compliant** response:

- Implementation guidance exists.
- Administration guidance exists.
- Usage guidance exists.
- The managed access model reduces customer-side implementation and administration risk.

## 5. Optional Additional Attachments

The audit package can be strengthened with the following operational documents, if maintained outside the repository:

- VPN access runbook.
- IP allowlist onboarding procedure.
- URL publication / service access authorization note.
- End-user quick guide for business operators.
