# IGS Mexico / BAZ BISO - Compliance Checklist

## Purpose

This checklist consolidates the current compliance position of each verified point documented in this folder. It is intended to serve both as a living control register and as the executive traffic-light summary for management or committee review. It must be updated whenever the related evidence package, annexes, executive responses, or supporting repository evidence are expanded, corrected, or superseded.

This checklist must be read together with [01-assessment-context.md](./01-assessment-context.md), which defines the common development, technology, and service-delivery context for the full evidence package.

## Executive Snapshot

- Total verified points: 10
- Green: 5
- Yellow: 5
- Red: 0
- Overall executive reading: controlled but still pending closure of material evidence gaps in selected security and governance-related points.

## Executive Position

The current package shows a stable baseline for secure implementation guidance, logging, hardening, implementation guidance, and reverse-engineering protection under the actual managed-service model deployed in IGS infrastructure.

The main residual exposure is concentrated in five yellow points where the repository supports part of the requirement but does not yet prove the full control outcome expected for committee-level closure.

## Maintenance Rule

- Update this checklist whenever any point document, annex, executive response, or supporting evidence changes.
- Keep the status aligned with the latest documented conclusion in the main point document.
- Update the justification summary if new evidence changes the compliance position.
- Use the `Last Reviewed` column to reflect the latest checklist synchronization date.

## Status Legend

- `Compliant`: current evidence supports the requirement.
- `Partially compliant`: current evidence supports part of the requirement, but one or more material gaps remain.
- `Not evidenced`: no sufficient evidence currently available.

## Traffic Light Legend

- `Green`: requirement supported by current evidence.
- `Yellow`: requirement partially supported; material evidence or implementation gaps remain.
- `Red`: requirement not evidenced or currently unsupported.

## Executive Traffic Light Summary

| Point | Topic | Traffic Light | Executive Reading | Primary Gap for Closure | Recommended Committee Follow-up |
|------:|-------|---------------|-------------------|-------------------------|---------------------------------|
| 33 | Secure ecosystem implementation | Green | Security modules and secure implementation practices are explicitly documented and evidenced in code, configuration, and governance artifacts. | No material repository gap identified for this point. | Maintain the security-module inventory and keep implementation evidence synchronized as the platform evolves. |
| 06 | Security monitoring and alerting | Yellow | Monitoring, observability, logging, and auditing are present, but centralized SIEM correlation and real alert evidence are not yet demonstrated. | Verifiable SIEM integration and alert evidence. | Confirm whether centralized SIEM onboarding and alert evidence will be provided by IGS operations or must be documented externally. |
| 14 | Authentication and federated access control | Yellow | Core authentication controls are implemented, including sessions, Sanctum, OTP MFA, email verification, and RBAC, but federation is not evidenced. | SAML 2.0, OAuth 2.0, or OIDC federation evidence. | Decide whether federated access is in scope for this service or whether an exception or compensating-control position is required. |
| 17 | Profile management and role administration | Yellow | Role and permission controls exist, but the end-to-end administrative workflow for profile lifecycle management is not fully evidenced. | Clear create, update, and delete profile-management workflow evidence. | Define whether current RBAC evidence is sufficient or whether a documented administrative workflow must be added. |
| 22 | User and access administration handover to CyAAL | Yellow | Technical control exists, but formal ownership by CyAAL is not evidenced. | Operational handover or governance evidence naming CyAAL as owner. | Confirm governance owner and attach formal handover, RACI, or operating procedure evidence. |
| 26 | Transaction, error, and audit logging | Green | Logging and auditability are sufficiently evidenced for the current requirement. | No material repository gap identified for this point. | Maintain evidence currency as implementation evolves. |
| 28 | Anti-reverse-engineering controls | Green | The control is adequately covered under the actual Laravel server-side and IGS-hosted delivery model. | No material repository gap identified for this point. | Preserve current deployment, repository access, and hardening controls. |
| 30 | Penetration testing and release security validation | Yellow | Security validation activities and scan evidence exist, but a recent external pentest report tied to release closure is not evidenced. | Recent external pentest report and release-gate traceability. | Decide whether to provide a current pentest report, attach external evidence, or maintain a partial-compliance position. |
| 34 | Implementation, administration, and user guides | Green | Documentation coverage is sufficient for the managed-service delivery model. | No material repository gap identified for this point. | Keep documentation synchronized with operational changes. |
| 35 | Security configuration and hardening guides | Green | Hardening guidance and implementation evidence are sufficient for the current assessed model. | No material repository gap identified for this point. | Keep the guide and evidence aligned with future infrastructure or architecture changes. |

## Checklist

| Point | Topic | Status | Comment / Justification | Primary Evidence | Last Reviewed |
|------:|-------|--------|-------------------------|------------------|---------------|
| 33 | Secure ecosystem implementation | Compliant | The current repository explicitly identifies security modules in the application stack and documents secure implementation practices through the SDLC, hardening guide, patch-management process, security assessment, and code-level controls. Under the managed-service model, this is sufficient evidence that the provider can present the security capabilities included in the solution and the good practices used to implement them. | [33-saas-onprem-secure-ecosystem-implementation.md](./Req.%2033/33-saas-onprem-secure-ecosystem-implementation.md) | 2026-07-17 |
| 06 | Security monitoring and alerting | Partially compliant | In the current Laravel-based, IGS-hosted service model, application monitoring, health checks, logging, auditing, and observability are implemented, but centralized SIEM correlation and real alert evidence are still not evidenced from the repository. | [06-saas-security-monitoring-and-alerting.md](./Req.%2006/06-saas-security-monitoring-and-alerting.md) | 2026-05-21 |
| 14 | Authentication and federated access control | Partially compliant | In the current managed web-application model, web authentication, Sanctum API auth, OTP MFA, email verification, and RBAC are implemented, but no verifiable SAML 2.0, OAuth 2.0, or OIDC federation evidence was found. | [14-saas-onprem-authentication-and-federation.md](./Req.%2014/14-saas-onprem-authentication-and-federation.md) | 2026-05-21 |
| 17 | Profile management and role administration | Partially compliant | In the current Laravel/Spatie RBAC implementation, permission assignment, role provisioning, and least-privilege controls are evidenced, but a clear in-application create/update/delete workflow for profile administration is not fully evidenced. | [17-saas-onprem-profile-management.md](./Req.%2017/17-saas-onprem-profile-management.md) | 2026-05-21 |
| 22 | User and access administration handover to CyAAL | Partially compliant | In the current IGS-operated service model, user and access administration is technically centralized and controlled, but no verifiable evidence shows that CyAAL is the formal operational owner of the process. | [22-saas-onprem-user-and-access-administration-handover.md](./Req.%2022/22-saas-onprem-user-and-access-administration-handover.md) | 2026-05-21 |
| 26 | Transaction, error, and audit logging | Compliant | In the current deployed application state, the platform generates logs for errors, sensitive-access events, and auditable business activity, with logging channels, audit trails, and forensic metadata capture. SIEM centralization remains a separate improvement, not a blocker for this point. | [26-saas-onprem-transaction-error-and-audit-logging.md](./Req.%2026/26-saas-onprem-transaction-error-and-audit-logging.md) | 2026-05-21 |
| 28 | Anti-reverse-engineering controls | Compliant | For the Laravel server-side model deployed in IGS infrastructure, the control is satisfied through non-public backend source code, protected deployment, hardening measures, minimized frontend exposure, and restricted private repository access with 2FA, as provided in operational context. | [28-saas-onprem-anti-reverse-engineering-controls.md](./Req.%2028/28-saas-onprem-anti-reverse-engineering-controls.md) | 2026-05-21 |
| 30 | Penetration testing and release security validation | Partially compliant | In the current development and release state, the SDLC and release process include security testing policy and recent security scans, but the repository does not contain a recent external pentest report or direct evidence that every release is gated by completed penetration testing. | [30-saas-onprem-penetration-testing-and-release-security-validation.md](./Req.%2030/30-saas-onprem-penetration-testing-and-release-security-validation.md) | 2026-05-21 |
| 34 | Implementation, administration, and user guides | Compliant | The repository provides implementation, administration, and usage documentation appropriate to the managed-service model, complemented by the operational context of IGS-hosted delivery via web, VPN, controlled URL, and IP allowlisting. | [34-saas-onprem-implementation-administration-and-user-guides.md](./Req.%2034/34-saas-onprem-implementation-administration-and-user-guides.md) | 2026-05-21 |
| 35 | Security configuration and hardening guides | Compliant | A formal hardening guide exists, is explicitly intended for this requirement, and is supported by implementation evidence and security-assessment validation of applied hardening controls in the current IGS-hosted deployment model. | [35-saas-onprem-security-hardening-guides.md](./Req.%2035/35-saas-onprem-security-hardening-guides.md) | 2026-05-21 |

## Committee-Oriented Priorities

### Priority 1: Governance and operating-model closure

- Point 22 requires a formal decision on ownership and administrative accountability.
- Point 14 requires a scope decision on whether federation is mandatory for closure.

### Priority 2: Security-evidence closure

- Point 06 requires a decision on SIEM evidence ownership and expected supporting artifacts.
- Point 30 requires a decision on whether a current external pentest report will be produced or attached.

### Priority 3: Process formalization

- Point 17 would benefit from explicit workflow evidence for profile lifecycle administration.

## Recommended Executive Message

The current compliance package shows a controlled technical baseline with no red points among the verified items. However, five yellow points remain open due to evidence or governance gaps rather than a complete absence of control implementation. Committee attention should focus on closing ownership, federation scope, SIEM evidence, pentest evidence, and profile-administration workflow definition.

## Update Notes

- If a point changes from `Partially compliant` to `Compliant`, update this checklist only after the main point document and supporting annex clearly document the new evidence.
- If external evidence is attached outside the repository, reflect that in the justification summary and, when possible, note it in the corresponding point document first.
- Do not update this checklist independently of the evidence package; it must remain synchronized with the detailed documents.

## Suggested Update Workflow

1. Update the detailed point document.
2. Update the annex if the evidence set changed.
3. Update the executive response if the status or wording changed.
4. Update this checklist to reflect the new compliance position.

## Last Reviewed

2026-07-17
