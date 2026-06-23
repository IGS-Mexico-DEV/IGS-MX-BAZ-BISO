# SaaS / On-Prem Point 26 - Transaction, Error, and Audit Logging

## 1. Objective

This document records the current evidence available in the IGS Billing project regarding application logging, transaction traceability, error recording, and forensic support.

This point should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

## 2. Current Compliance Position

**Status:** Compliant.

Repository evidence confirms that the application generates logs and trace records for errors, sensitive access events, and auditable business transactions. The project includes application log channels, security log retention, structured exception logging, model-level audit trails, and protected audit retrieval endpoints.

While the repository also documents that centralized SIEM integration remains an open improvement, that gap relates to log centralization and monitoring maturity, not to the existence of transaction and error logging itself. Based on the current repository evidence, the requirement for generating logs of transactions, errors, and related activity is satisfied.

## 3. Scope of Verifiable Evidence

The following controls are verifiable from the current repository state:

- Application error logging.
- Dedicated security logging channel.
- Daily log rotation and retention settings.
- Model-level audit trail generation for sensitive business entities.
- Audit capture of user, IP, URL, and user-agent metadata.
- Logging of sensitive-access events.
- Audit retrieval endpoints for multiple business resources.

## 4. Identified Logging and Traceability Controls

### 4.1 Application Error Logging

The application logs unexpected exceptions and unhandled database errors through Laravel logging. Error details are preserved in the log layer while user-facing API responses remain generic.

Verified controls:

- Unhandled database errors logged with code, message, file, and line.
- Unhandled exceptions logged with type, code, message, file, and line.
- User-facing error messages sanitized while preserving server-side traceability.

### 4.2 Security Log Channel and Retention

The logging configuration includes a dedicated `security` channel implemented with daily rotation and 30-day retention. Standard application logs are also configured with daily or single-file modes.

Verified controls:

- `security.log` channel defined.
- Daily log rotation enabled.
- 30-day retention configured for security logs.
- Standard Laravel application logging also configured.

### 4.3 Transaction and Business Audit Logging

The project uses OwenIt Laravel Auditing to record create, update, delete, and restore events for sensitive business entities. This provides durable traceability for transaction-related record changes and administrative activity.

Verified controls:

- Auditing enabled by default.
- Audited lifecycle events: `created`, `updated`, `deleted`, `restored`.
- Audit records stored in the `audits` table.
- Auditing active across multiple sensitive models.

### 4.4 Forensic Metadata Capture

Audit records capture contextual forensic metadata, including the acting user, IP address, request URL, and user agent. This supports post-incident review and investigation of administrative or business record changes.

Verified controls:

- User resolver configured for `web`, `api`, and `sanctum` guards.
- IP resolver configured.
- URL resolver configured.
- User-Agent resolver configured.

### 4.5 Sensitive Access Logging

The application explicitly logs access to sensitive token data. This creates an additional forensic record when protected information is exposed to an authorized identity.

Verified controls:

- `Log::info` entries when sensitive token data is accessed.
- `Log::info` entries when sensitive token lists are accessed.
- `Log::warning` entries for unauthorized access attempts.
- Logged metadata includes user identity and source IP.

### 4.6 Audit Retrieval and Operational Visibility

Multiple business routes expose audit endpoints, allowing authorized users or operators to review historical record changes. This provides an operational way to inspect what occurred over time.

Verified controls:

- Audit endpoints available for multiple resources.
- Audit capability documented in API documentation.
- Audit model intended for monitoring, compliance, and forensic analysis.

## 5. Evidence Matrix

| Control | Current evidence | Status |
|---------|------------------|--------|
| Application error logging | Structured exception and database-error logging | Implemented |
| Security log generation | Dedicated `security` channel in logging configuration | Implemented |
| Log retention | 30-day retention for security logs | Implemented |
| Transaction and record audit trail | OwenIt audit driver and audit-enabled models | Implemented |
| Forensic metadata capture | User, IP, URL, and User-Agent resolvers | Implemented |
| Sensitive-access logging | Explicit `Log::info` / `Log::warning` entries in sensitive flows | Implemented |
| Audit retrieval capability | `/audits` endpoints on multiple protected resources | Implemented |

## 6. Recommended Requirement Wording

IGS Billing currently generates logs and trace records for application errors, sensitive-access events, and auditable business transactions. The implementation includes standard application logging, a dedicated security log channel, model-level audit trails, forensic metadata capture, and protected audit retrieval endpoints. These controls support operational monitoring, detection of anomalous activity, and post-event forensic investigation.

The current security assessment notes that log centralization into a SIEM remains an open improvement item. However, that finding does not negate the existence of transaction, error, and audit logging within the application. Based on the current repository evidence, this requirement should be classified as compliant.

## 7. Additional Evidence That May Strengthen the Response

Although the requirement is satisfied by the current implementation, the following evidence could be attached to strengthen the audit package:

- Sanitized samples of `laravel.log` and `security.log`.
- Screenshots or exports of audit records from protected endpoints.
- Operational screenshots showing log review procedures.
- SIEM forwarding evidence, if later available.

## 8. Verified Repository References

- `config/logging.php`
- `config/audit.php`
- `app/Models/Audit.php`
- `app/Helpers/ApiResponseHelper.php`
- `app/Http/Controllers/TokenVaultController.php`
- `routes/api.php`
- `docs/api/token-vaults.md`
- `docs/security-assessment.md`
- `docs/security-hardening-guide.md`

## 9. Conclusion

Based on the evidence currently verifiable in the repository, IGS Billing generates logs for errors, sensitive operations, and auditable business activity in a way that supports monitoring and forensic investigation. Therefore, this requirement should be answered as **compliant**.
