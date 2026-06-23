# SaaS / On-Prem Point 28 - Executive Response

This response should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

For a Laravel application, the anti-reverse-engineering control is addressed primarily by preventing unauthorized access to the source code and protecting the deployment environment, rather than by distributing obfuscated binaries.

In IGS Billing, the backend source code is executed server-side and is not publicly delivered to end users. In addition, the source-code repository is stated to be private, invitation-based, limited to specialized personnel, and protected with 2FA. The project also includes deployment-hardening guidance, and the frontend assets delivered to browsers are compiled and minified through Vite with Terser.

For that reason, the most defensible response is **compliant**.

Recommended questionnaire wording:

"For this Laravel-based application, reverse-engineering risk is mitigated primarily by ensuring that backend source code is not publicly accessible, repository access is private and restricted to authorized specialized personnel with 2FA, deployment environments are hardened, and frontend-delivered logic is compiled and minified. Under this control model, the requirement is currently considered compliant." 
