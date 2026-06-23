# SaaS / On-Prem Point 35 - Security Configuration and Hardening Guides

## 1. Objective

This document records the current evidence that IGS Billing maintains security hardening guides, applies them, and can provide them for verification.

This point should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Current Compliance Position

**Status:** Compliant.

The repository contains a formal security hardening guide explicitly intended to satisfy this control, and the same repository provides implementation evidence showing that key hardening measures are applied in the application. In addition, the security assessment confirms that configuration and hardening controls were reviewed and passed for the evaluated environment.

Although some hardening improvements remain open as maturity items, the current evidence is sufficient to show that security configuration guidance exists, is used as an operational verification baseline, and has been applied in the solution. Therefore, this requirement should be answered as **compliant**.

## 3. Scope of Verifiable Evidence

The following items are verifiable from the repository:

- A formal security hardening guide exists.
- The guide explicitly states that it is intended to satisfy Point 35.
- The guide includes configuration guidance for TLS, CSP, HSTS, X-Content-Type-Options, X-Frame-Options, Referrer-Policy, Permissions-Policy, CORS, secrets management, and WAF.
- The guide includes a deployment checklist for verification.
- The application middleware applies key HTTP security headers.
- The security assessment confirms that configuration and hardening controls passed.

## 4. Hardening Guide Evidence

### 4.1 Formal Guide Availability

The repository includes a formal hardening document:

- `docs/security-hardening-guide.md`

This document is customer- and auditor-facing and explicitly states that it is intended to satisfy **Point 35 — SaaS and On-Premises Security Hardening Guides**.

### 4.2 Hardening Topics Covered

The guide covers the following security-configuration domains:

- TLS / transport security.
- Content Security Policy (CSP).
- HTTP Strict Transport Security (HSTS).
- X-Content-Type-Options.
- X-Frame-Options.
- Referrer-Policy.
- Permissions-Policy.
- CORS configuration.
- Secrets management.
- Web Application Firewall (WAF).
- Deployment verification checklist.

This satisfies the requirement to provide configuration or security hardening guidance.

## 5. Evidence That the Guide Is Applied

### 5.1 Header and Hardening Implementation

The repository includes direct application-level implementation of key hardening controls in middleware.

Observed evidence in `app/Http/Middleware/AddCspHeaders.php`:

- `Content-Security-Policy` header applied.
- `Strict-Transport-Security` header applied for HTTPS requests.
- `X-Content-Type-Options: nosniff` applied.
- `X-Frame-Options: DENY` applied.
- `Referrer-Policy: strict-origin-when-cross-origin` applied.
- `Permissions-Policy` applied.

This demonstrates that the guide is not merely aspirational documentation; key controls are implemented in code.

### 5.2 Verification Checklist

The hardening guide includes a production deployment checklist covering:

- TLS verification.
- Security headers verification.
- CORS restrictions.
- Secrets-management checks.
- Application configuration checks.
- WAF checks.
- Logging and monitoring checks.

This provides a concrete verification mechanism showing how the guide should be applied before production release.

### 5.3 Security Assessment Confirmation

The security assessment provides supporting evidence that hardening controls were evaluated.

Observed evidence:

- `Configuration & Hardening`: HTTP security headers, CSP with nonces, secure cookies, and `.env` protection all pass.
- TLS is reported as strong and correctly configured.
- CSP and headers are reported as implemented with nonces.

This is strong evidence that the hardening guide is reflected in the evaluated implementation.

## 6. Current Hardening Position

The current repository supports the following compliance position:

- Security hardening guidance is formally documented.
- The guide is available for verification.
- Key hardening controls are implemented in application code.
- A deployment checklist exists for operational verification.
- The security assessment confirms the implemented hardening posture.

## 7. Open Hardening Improvements

The documentation also reflects some open improvement items, including:

- Removal of `unsafe-eval` from CSP once dependencies allow it.
- Further restriction of some CORS settings.

These items should be treated as ongoing hardening improvements, not as evidence that no hardening guide exists or that the guide is not applied.

## 8. Recommended Requirement Wording

IGS Billing maintains a formal security hardening guide and applies it as part of configuration and deployment verification. The guide covers transport security, HTTP security headers, CORS, secrets management, WAF recommendations, and a production deployment checklist. The repository also contains implementation evidence for key hardening controls, and the security assessment confirms that configuration and hardening controls passed in the evaluated environment.

Based on the currently available evidence, this requirement should be classified as **compliant**.

## 9. Evidence Matrix

| Requirement element | Current evidence | Status |
|---------|------------------|--------|
| Security hardening guide exists | `docs/security-hardening-guide.md` | Implemented |
| Guide available for verification | Auditor/customer-facing hardening guide | Implemented |
| Hardening controls documented | TLS, headers, CORS, secrets, WAF, checklist | Implemented |
| Hardening controls applied | Middleware and configuration evidence | Implemented |
| Hardening validation performed | Security assessment confirms pass status | Implemented |

## 10. Auditor-Facing Conclusion

The repository demonstrates that IGS Billing not only maintains formal security hardening guidance, but also applies those controls in the implementation and uses a deployment checklist and security assessment to verify them. Therefore, this point should be answered as **compliant**.

## 11. Additional Attachments That May Strengthen the Package

Although the current evidence is already sufficient, the package can be strengthened with:

- Header-validation screenshots from production.
- SSL Labs or securityheaders.com validation output.
- Deployment records showing checklist completion.

## 12. Verified Repository References

- `docs/security-hardening-guide.md`
- `app/Http/Middleware/AddCspHeaders.php`
- `docs/security-assessment.md`
- `docs/sdlc.md`

## 13. Conclusion

IGS Billing has formal security hardening guidance, applies core hardening controls in the implementation, and provides verification mechanisms through checklists and security assessment. The defensible answer for this requirement is therefore **compliant**.
