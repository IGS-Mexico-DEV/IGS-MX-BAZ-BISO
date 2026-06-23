# SaaS / On-Prem Point 22 - Executive Response

This response should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

IGS Billing currently implements centralized technical controls for user and access administration, including controlled provisioning, disabled self-registration, explicit role assignment, and runtime RBAC enforcement.

These controls improve internal control and reduce unauthorized access, fraud, and administrative errors. However, the current repository does not provide verifiable evidence that user and access administration has been formally delivered to CyAAL, the BAZ identity management area.

Based on the current implementation evidence, this requirement should be stated as **partially compliant**. Full compliance requires documentary or operational evidence proving CyAAL ownership of the identity and access administration lifecycle.

Recommended questionnaire wording:

"The application currently enforces centralized technical control over user and access administration through controlled provisioning, disabled self-registration, explicit role assignment, and runtime access enforcement. However, no repository-verifiable evidence has been identified showing that administration of users and access has been formally handed over to CyAAL, the BAZ identity management area. Therefore, the requirement is currently considered partially compliant pending formal ownership and operational evidence." 
