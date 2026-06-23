# SaaS / On-Prem Point 14 - Executive Response

This response should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

IGS Billing currently implements user authentication through Laravel web sessions, Laravel Sanctum API tokens, email verification, role-based access control, and OTP-based MFA for privileged users.

These controls provide evidence of how users authenticate into the application and reduce the risk of unauthorized access. However, the current repository does not provide verifiable evidence of federated access control through SAML 2.0 or OAuth 2.0.

Based on the current implementation state, this requirement should be stated as **partially compliant**. Full compliance requires implementation evidence or externally provided operational evidence of active federation through SAML 2.0, OAuth 2.0, or OIDC with an identity provider.

Recommended questionnaire wording:

"The application currently implements user authentication through session-based web authentication, API token authentication, email verification, role-based access control, and OTP-based MFA for privileged users. These controls provide evidence of how user authentication is performed. However, no repository-verifiable evidence of federated access control through SAML 2.0 or OAuth 2.0 has been identified. Therefore, the requirement is currently considered partially compliant pending federation implementation evidence or external production evidence."
