# Annex - Authentication Evidence and Pending Federation Support

## 1. Purpose

This annex summarizes the evidence currently available for user authentication and identifies the missing implementation evidence required to satisfy the federation portion of the requirement.

This annex should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

## 2. Currently Available Authentication Evidence

The repository currently supports the following evidence:

### A. Web authentication evidence

- Laravel built-in authentication routes.
- Session-based login flow.
- Password reset functionality.
- Email verification requirement for protected routes.

### B. API authentication evidence

- `POST /api/v1/auth/login` for credential-based login.
- `POST /api/v1/auth/verify-otp` for MFA completion.
- `GET /api/v1/auth/me` for authenticated user retrieval.
- `POST /api/v1/auth/logout` for token invalidation.
- Sanctum bearer-token authentication for protected API routes.

### C. MFA evidence

- OTP generation for privileged users.
- Email delivery of OTP codes.
- OTP verification before token issuance.
- Admin-role-triggered MFA requirement.

### D. Access control evidence

- RBAC through Spatie Permission.
- `auth`, `auth:sanctum`, and `verified` middleware on protected routes.
- User role awareness in the authentication model.

## 3. Missing Federation Evidence

The following evidence is not currently available in the repository:

- SAML 2.0 login or SSO endpoints.
- SAML metadata, certificates, or assertion consumer service configuration.
- OAuth 2.0 authorization server or client integration for federated login.
- OIDC discovery configuration.
- External identity provider integration with Azure AD, Okta, Auth0, Google, or similar.

## 4. Minimum Evidence to Attach for Federation Compliance

If federation exists outside the repository, at least one of the following evidence sets should be attached:

### A. SAML 2.0 evidence

- Identity provider name.
- Service provider configuration.
- ACS URL.
- Entity ID.
- Metadata exchange evidence.
- Login flow screenshots.

### B. OAuth 2.0 or OIDC evidence

- Identity provider name.
- Authorization endpoint.
- Token endpoint.
- Client configuration.
- Redirect URI.
- Successful authentication flow screenshots.

### C. Production evidence

- Screenshot of SSO login page.
- Screenshot of identity provider application configuration.
- Screenshot or export showing successful federated sign-in.
- Operational document showing federation is active in production.

## 5. Suggested Authentication Flow Evidence for Audit

For the authentication portion already implemented in the repository, the following evidence can be shown to the auditor:

- API authentication documentation showing login and OTP verification.
- Web authentication route configuration.
- AuthController logic for login, token issuance, logout, and OTP verification.
- User model logic for MFA enforcement.
- Security assessment summary referencing MFA and authentication testing.

## 6. Audit Note

Until repository-verifiable or externally attached evidence of SAML 2.0 or OAuth 2.0 federation is provided, this requirement should remain classified as **partially compliant**.
