# Annex - Security Hardening Evidence

## 1. Purpose

This annex summarizes the evidence that security configuration and hardening guides exist and are applied in IGS Billing.

This annex should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Available Evidence

### A. Formal guide evidence

- `docs/security-hardening-guide.md` exists.
- The document explicitly states it is intended to satisfy Point 35.
- The guide is written for customer and auditor review.

### B. Hardening topics covered

- TLS.
- CSP.
- HSTS.
- X-Content-Type-Options.
- X-Frame-Options.
- Referrer-Policy.
- Permissions-Policy.
- CORS.
- Secrets management.
- WAF.
- Deployment checklist.

### C. Applied implementation evidence

- `app/Http/Middleware/AddCspHeaders.php` applies CSP.
- `app/Http/Middleware/AddCspHeaders.php` applies HSTS for HTTPS.
- `app/Http/Middleware/AddCspHeaders.php` applies `nosniff`.
- `app/Http/Middleware/AddCspHeaders.php` applies `DENY` framing protection.
- `app/Http/Middleware/AddCspHeaders.php` applies `Referrer-Policy`.
- `app/Http/Middleware/AddCspHeaders.php` applies `Permissions-Policy`.

### D. Verification evidence

- The hardening guide includes a deployment checklist.
- The security assessment states that configuration and hardening controls pass.

## 3. Audit Position

The current evidence supports a **compliant** response:

- Security hardening guidance exists.
- The guide can be provided for verification.
- Core hardening controls are applied in the implementation.
- Verification guidance and assessment evidence are available.

## 4. Open Improvements

The following items remain as hardening improvements:

- CSP `unsafe-eval` removal.
- Additional CORS tightening.

These do not negate the existence or application of the hardening guide.
