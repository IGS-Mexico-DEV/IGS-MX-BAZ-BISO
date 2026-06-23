# Annex - Penetration Testing and Recent Scan Evidence

## 1. Purpose

This annex summarizes the evidence currently available for penetration-testing policy, recent security-scan execution, and the current evidence gap for a recent pentest report.

This annex should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Available Evidence

### A. Policy evidence

- The SDLC includes `Security Testing: SAST, DAST, penetration testing`.
- `Gate 4.2` requires security-testing approval by a pentester.
- The SDLC identifies an `External Pentester (quarterly)` role.
- DAST is defined as manual / quarterly and not automated in CI.

### B. Automated scan evidence

- GitHub Actions security workflow runs on schedule, push, and pull request.
- Snyk is executed.
- Trivy is executed.
- `composer audit` is executed.
- `npm audit` is executed.
- A security report artifact is generated.

### C. Recent results evidence

Recent patch-management report dated 2026-05-15:

- `composer audit`: no security vulnerability advisories found.
- `npm audit`: 0 vulnerabilities found.

Security assessment evidence:

- `Vulnerable Components: PASS (0 findings) — Dependabot and Snyk/Trivy integrated.`
- `Requirement 6 (Secure Development): SDLC gates, Dependabot, Snyk/Trivy — compliant.`

## 3. Current Evidence Gap

The repository also states:

- `No external invasive pentests were executed against sandbox.`

Therefore, the following requested evidence is currently missing from the repository:

- Recent penetration-testing report.
- Sanitized penetration-testing findings summary.
- Release artifact proving pentest completion for the last release.
- Bug bounty / reward program evidence.

## 4. Audit Position

The current evidence supports a **partial** response:

- Yes, there is a formal testing policy and recent security-scan evidence.
- No, a recent pentest-results document is not currently evidenced in the repository.

## 5. Best Attachment to Add Next

The strongest next attachment would be:

- A recent external pentest executive summary with date, scope, tester, methodology, severity summary, and remediation status.
