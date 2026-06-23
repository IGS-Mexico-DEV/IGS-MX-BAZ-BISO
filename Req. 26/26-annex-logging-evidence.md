# Annex - Logging Evidence and Forensic Support

## 1. Purpose

This annex summarizes the evidence currently available for transaction logging, error logging, and forensic traceability.

This annex should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

## 2. Currently Available Logging Evidence

The repository currently supports the following evidence:

### A. Error logging evidence

- Unhandled exception logging.
- Unhandled database exception logging.
- Error detail retention in server-side logs.
- Sanitized client-facing error messages.

### B. Security logging evidence

- Dedicated `security` log channel.
- Daily rotation of security logs.
- 30-day local retention.
- Standard application log channel configuration.

### C. Transaction and audit evidence

- Audit logging for create, update, delete, and restore events.
- Audit storage in a dedicated database table.
- Audit trails available for multiple business entities.
- Audit endpoints exposed for authorized review.

### D. Forensic metadata evidence

- Authenticated user capture.
- IP address capture.
- Request URL capture.
- User-Agent capture.

### E. Sensitive-operation logging evidence

- Sensitive token-data access logging.
- Sensitive token-list access logging.
- Unauthorized access-attempt logging.

## 3. Suggested Evidence to Show the Auditor

The following evidence can be shown now from the current repository state:

- Logging configuration showing application and security channels.
- Audit configuration showing metadata capture.
- Audit model showing forensic purpose.
- API and controller code showing exception logging and sensitive-access logging.
- API documentation exposing audit retrieval endpoints.

## 4. Optional Additional Evidence

The following evidence may strengthen the audit response but is not strictly required to support the current implementation claim:

- Sanitized copies of real application log lines.
- Sanitized copies of real security log lines.
- Screenshots of audit endpoint responses.
- Evidence of log review procedures.

## 5. Audit Note

Centralized SIEM integration remains a separate maturity improvement item. It does not invalidate the existence of transaction, error, and forensic logging already implemented in the application. This requirement should therefore remain classified as **compliant** based on the current repository evidence.
