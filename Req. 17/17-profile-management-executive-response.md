# SaaS / On-Prem Point 17 - Executive Response

This response should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

IGS Billing currently implements profile and permission management through role-based access control, authoritative role definitions, provisioning-time role assignment, and runtime permission enforcement.

These controls provide evidence that access profiles exist and are applied according to least-privilege principles. However, the current repository does not clearly expose a full in-application create, update, and delete workflow for profile administration.

Based on the current implementation evidence, this requirement should be stated as **partially compliant**. Full compliance would require evidence of an operational ABC workflow for profile administration or externally attached evidence showing how that process is executed.

Recommended questionnaire wording:

"The application currently implements profile management through role-based access control, permission mapping, provisioning-time role assignment, and runtime permission enforcement. These controls demonstrate how access profiles are defined and applied. However, no repository-verifiable in-application create/update/delete workflow for profile administration was clearly identified. Therefore, the requirement is currently considered partially compliant pending operational evidence of the profile administration lifecycle."
