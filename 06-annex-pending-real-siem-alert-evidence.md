# Annex - Pending Evidence for Real SIEM Alerts

## 1. Purpose

This annex defines the additional evidence that should be attached to complete SaaS Point 6 regarding monitoring, incidents, and alerting.

This annex should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

## 2. Current Situation

At the current project state, the repository demonstrates logging, health check, auditing, and observability capabilities, but it does not contain real SIEM alert samples or conclusive evidence of a centralized SIEM platform operating over production logs.

## 3. Minimum Evidence to Attach

At least three real samples, with sensitive data masked, should be attached from the following categories:

### A. Application Security Alerts

- Multiple failed authentication attempts.
- Permission- or role-based access denial.
- High-severity application error.
- Sensitive audited change on a critical entity.

### B. Infrastructure or Platform Alerts

- Abnormal CPU, memory, or disk utilization.
- Database, cache, or storage outage or degradation.
- Unexpected service restarts.
- Unauthorized modification of critical configuration.

### C. Perimeter or Network Alerts

- WAF blocked event.
- Scanning, brute-force, or web exploitation attempt.
- Anomalous connections from unexpected locations.
- Traffic patterns outside the established baseline.

## 4. Minimum Fields Required in Each Evidence Sample

Each real alert sample should include, at minimum:

- Date and time.
- Event source.
- Severity.
- Rule or use case that triggered the alert.
- Event summary.
- Handling or escalation status.
- Action taken or evidence of follow-up.

## 5. Acceptable Evidence Sources

Acceptable screenshots or exports may come from tools such as:

- Corporate SIEM.
- WAF integrated with a SIEM.
- CloudWatch, Datadog, ELK, Splunk, Sentinel, or an equivalent platform.
- An observability console that clearly shows active alerts and operational traceability.

## 6. Sanitization Criteria

Before attaching the evidence:

- Mask public IP addresses when the auditor does not require the full value.
- Hide tokens, secrets, personal email addresses, and customer data.
- Keep timestamps, severity, rule identifiers, and handling workflow visible.

## 7. Audit Note

Until real SIEM alerts are attached and verifiable evidence of centralized log correlation exists, this requirement should remain classified as **partially compliant**.
