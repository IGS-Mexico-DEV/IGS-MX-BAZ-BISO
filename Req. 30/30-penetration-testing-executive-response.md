# SaaS / On-Prem Point 30 - Executive Response

This response should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

IGS Billing maintains a formal security-testing policy in its SDLC, including penetration testing, pentester approval, vulnerability assessment, and quarterly external pentester participation. The release and maintenance process is supported by recurring security scans in CI/CD and recent scan evidence, including 2026-05-15 results showing no security advisories in `composer audit` and 0 vulnerabilities in `npm audit`.

However, the repository does not currently include a recent external penetration-testing report, and the security assessment explicitly notes that no external invasive pentests were executed against the sandbox environment in that assessment cycle.

For that reason, the most defensible response is **partially compliant**.

Recommended questionnaire wording:

"The application has a formal security-testing policy that includes penetration testing and pentester approval within the SDLC, and it is reinforced by recurring automated security scans and recent vulnerability-scan results. However, a recent external penetration-testing report was not identified in the current evidence repository. Therefore, this requirement is currently considered partially compliant." 
