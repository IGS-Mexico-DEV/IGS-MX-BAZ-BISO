# SaaS / On-Prem Point 30 - Penetration Testing and Release Security Validation

## 1. Objective

This document records the currently verifiable evidence related to penetration testing, vulnerability scanning, and security validation in the release process of the IGS Billing application.

This point should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

## 2. Current Compliance Position

**Status:** Partially compliant.

The repository demonstrates that IGS Billing maintains a formal Secure Development Lifecycle, includes security testing activities in the release lifecycle, operates automated recurring vulnerability scans, and has recent scan evidence aligned with a recently achieved PCI DSS v4.0.1 certification context.

However, the same repository also states a key limitation: no external invasive penetration tests were executed against the sandbox environment in the referenced security assessment. In addition, the repository does not contain a recent standalone penetration-testing report, nor does it prove that each new application release is always gated by a completed penetration test before production deployment.

Accordingly, the most defensible response is **partially compliant**: the policy and supporting security-validation process are present, and recent scan evidence exists, but a recent pentest report tied directly to the release process is not verifiable from the repository.

## 3. Scope of Verifiable Evidence

The following items are verifiable from the repository:

- A formal SDLC includes security testing, vulnerability assessment, and penetration testing activities.
- Security testing approval by a pentester is defined as an SDLC gate.
- An external pentester role is identified in the SDLC.
- DAST is defined as manual / quarterly, not automated in CI.
- A GitHub Actions workflow performs recurring security scans on push, pull request, and weekly schedule.
- Snyk, Trivy, `composer audit`, and `npm audit` are used as recent scan mechanisms.
- A recent patch-management report dated 2026-05-15 records successful scan results.
- The security assessment records strong security results and PCI DSS v4.0.1 alignment.

The following items are **not** verifiable from the repository:

- A recent external penetration-testing report.
- Evidence that every release is blocked pending a completed pentest.
- A bug bounty or reward program.

## 4. Policy and Process Evidence

### 4.1 Secure Development Lifecycle Policy

The project has a formal SDLC document that includes security validation before release.

Observed evidence:

- Security testing includes SAST, DAST, and penetration testing.
- Vulnerability assessment is explicitly part of testing and validation.
- `Gate 4.2` requires security-testing approval by a pentester.
- The SDLC assigns an `External Pentester (quarterly)` role.
- DAST is defined as manual / quarterly execution with OWASP ZAP or Burp Suite and is not automated in CI.

This is the strongest policy-level evidence that penetration testing is part of the intended release-security model.

### 4.2 Release and Vulnerability Management Process

The patch and vulnerability management process reinforces ongoing security validation during update and release preparation.

Observed evidence:

- Weekly vulnerability scanning with Snyk and Dependabot.
- Trivy filesystem scanning integrated in CI/CD.
- Mandatory security tests and validation after changes.
- Post-deployment security validation required.

This supports a security-focused release discipline, although it does not by itself prove a pentest for every release.

## 5. Recent Security-Validation Evidence

### 5.1 CI/CD Security Scan Workflow

The repository contains an automated security-scan workflow with the following triggers:

- Weekly scheduled execution.
- Push to `main` and `develop`.
- Pull requests to `main` and `develop`.

Observed controls:

- PHPStan execution when available.
- Laravel Pint check.
- PHPUnit execution.
- Snyk scan.
- Trivy filesystem vulnerability scan with SARIF upload to GitHub Security.
- `composer audit` and `npm audit` advisory checks.
- Security report artifact generation.

### 5.2 Recent Scan Results Example

The repository includes a recent patch-management report dated **2026-05-15** with the following scan results:

| Scope | Tool | Result |
|-------|------|--------|
| PHP dependencies | `composer audit` | No security vulnerability advisories found |
| NPM dependencies | `npm audit` | 0 vulnerabilities found |

This is valid evidence of recent security scanning activity, although it is not equivalent to a full penetration-testing report.

### 5.3 Security Assessment Results

The security assessment documents recent security-validation outcomes, including:

- `Vulnerable Components: PASS (0 findings) — Dependabot and Snyk/Trivy integrated.`
- `Requirement 6 (Secure Development): SDLC gates, Dependabot, Snyk/Trivy — compliant.`

The same assessment also documents an important limitation:

- `No external invasive pentests were executed against sandbox.`

That limitation prevents this requirement from being answered as fully compliant based on repository evidence alone.

## 6. PCI DSS Context

According to the context provided for this response, the organization has recently achieved PCI DSS v4.0.1 certification. That context strengthens the overall credibility of the security-governance and validation program.

Even so, for this specific questionnaire item, the response should remain grounded in directly supportable evidence. The repository clearly supports recent scanning and security-validation practices, but it does not include a recent pentest report suitable to present as the requested example of penetration-test results.

## 7. Bug Bounty / Reward Program Position

No bug bounty or vulnerability reward program is evidenced in the repository.

For audit purposes, the defensible wording is:

- No repository evidence of a bug bounty / reward program was identified.

## 8. Recommended Requirement Wording

IGS Billing maintains a formal security-testing policy within its SDLC, including security testing, vulnerability assessment, pentester approval, and quarterly external pentester participation. The release-security process is reinforced by recurring CI/CD security scans using Snyk, Trivy, `composer audit`, and `npm audit`, and recent scan evidence is available from the 2026-05-15 patch-management report.

However, the current repository does not contain a recent external penetration-testing report, and the security assessment explicitly notes that no external invasive pentests were executed against the sandbox environment in that assessment cycle. Therefore, this requirement should currently be answered as **partially compliant** unless a recent pentest report can be attached from outside the repository.

## 9. Evidence Matrix

| Requirement element | Current evidence | Status |
|---------|------------------|--------|
| Penetration-testing policy | SDLC includes penetration testing and pentester approval gate | Implemented |
| External pentester role | SDLC identifies quarterly external pentester | Implemented |
| Release security scans | GitHub Actions workflow with Snyk, Trivy, audits | Implemented |
| Recent scan results | 2026-05-15 patch-management report | Implemented |
| Recent pentest results example | No standalone recent pentest report in repository | Not evidenced |
| Pentest tied to every release | Not verifiable from repository | Not evidenced |
| Bug bounty / reward program | No repository evidence identified | Not evidenced |

## 10. Auditor-Facing Conclusion

The repository supports a formal security-testing policy and recent automated security-scan evidence, both consistent with a mature PCI-aligned release process. However, it does not provide the specific artifact requested for full closure of this control: a recent penetration-testing report or equivalent pentest-results summary tied to the application release process.

Accordingly, this point should be answered as **partially compliant**.

## 11. Additional Evidence Needed for Full Compliance

To upgrade this point to full compliance in an audit package, attach one or more of the following:

- A recent external penetration-testing executive report.
- A sanitized findings summary showing scope, date, tester, severity, and remediation status.
- A release checklist proving pentest completion is mandatory before production promotion.
- Evidence of a bug bounty / responsible disclosure reward program, if one exists.

## 12. Verified Repository References

- `docs/sdlc.md`
- `.github/workflows/security-scan.yml`
- `docs/patch-management.md`
- `patch-report-20260515_083450.md`
- `docs/security-assessment.md`
- `README.md`

## 13. Conclusion

IGS Billing has a documented policy for security testing and strong evidence of recent automated security scans within its release and maintenance process. Nevertheless, the repository does not currently provide a recent penetration-testing report or direct proof that penetration testing is executed for each release. The defensible answer for this requirement is therefore **partially compliant**.
