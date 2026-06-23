# SaaS / On-Prem Point 14 - User Authentication and Federated Access Control

## 1. Objective

This document records the current user authentication methods and access control evidence available in the IGS Billing project, with specific attention to the requirement for federation-based access control through SAML 2.0 and OAuth 2.0.

This point should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Current Compliance Position

**Status:** Partially compliant.

Repository evidence confirms that the application implements user authentication controls, including web session authentication, API token authentication, email verification, role-based access control, and MFA by OTP for critical users. However, the repository does not provide verifiable implementation evidence of federated authentication or access control through SAML 2.0 or OAuth 2.0.

Accordingly, the requirement can only be classified as partially compliant based on the current implementation state.

## 3. Scope of Verifiable Evidence

The following controls are verifiable from the current repository state:

- Web authentication through Laravel session-based authentication.
- API authentication through Laravel Sanctum personal access tokens.
- MFA through email-delivered OTP for privileged users.
- Email verification for protected routes.
- Role-based access control through Spatie Permission.
- Protected routes enforced through authentication and verification middleware.

The following items are not verifiable from the repository and therefore remain unsupported as implementation evidence:

- SAML 2.0 identity provider or service provider integration.
- OAuth 2.0 federation, delegated identity, or external identity provider login.
- OIDC-based single sign-on implementation.
- Federation metadata, SSO endpoints, assertion consumer service configuration, or OAuth client/authorization server flows.

## 4. Identified Authentication and Access Controls

### 4.1 Web Authentication

The application uses Laravel's built-in session-based authentication for the web interface. Web routes are protected with `auth` and `verified` middleware, and the application uses standard Laravel authentication flows for login, password reset, and email verification.

Verified controls:

- Session-based web authentication.
- Built-in Laravel authentication routes.
- Password reset flow.
- Email verification for sensitive web areas.

### 4.2 API Authentication

The API uses Laravel Sanctum to issue personal access tokens after successful authentication. Protected API routes require `auth:sanctum`, and many business routes also require `verified` middleware.

Verified controls:

- Token-based API authentication using Sanctum.
- Protected routes enforced with `auth:sanctum`.
- Token issuance after successful login.
- Token revocation on logout.
- Token expiration logic based on user profile.

### 4.3 Multi-Factor Authentication

The login flow requires MFA for critical users, such as users with the `admin` role. In those cases, the application generates a six-digit OTP, sends it through email, and requires successful OTP verification before issuing the final access token.

Verified controls:

- MFA requirement for privileged users.
- OTP generation and validation flow.
- Email notification for OTP delivery.
- Time-limited OTP usage.

### 4.4 Access Control and Authorization

The project uses role-based access control through Spatie Permission. The `User` model includes role-aware logic and route protection is applied to sensitive endpoints. The repository also documents authentication, authorization, and session testing in the security assessment.

Verified controls:

- RBAC through Spatie Permission.
- Role-aware MFA enforcement.
- Verified-user requirement for protected functionality.
- Authentication and authorization controls documented in the security assessment.

## 5. Gap Analysis for SAML 2.0 and OAuth 2.0 Federation

The current repository does not contain verifiable evidence of federated access control through SAML 2.0 or OAuth 2.0.

Observed findings:

- No SAML libraries, configuration, metadata, or federation endpoints were identified.
- No Laravel Passport, Socialite, OIDC, or equivalent OAuth 2.0 federation implementation was identified.
- Laravel Sanctum is present, but Sanctum provides first-party/session or personal access token authentication and should not be treated as evidence of OAuth 2.0 federation.
- No evidence was found of external identity provider integration such as Azure AD, Okta, Google Workspace, ADFS, Auth0, or a custom SAML/OAuth broker.

Conclusion:

The project demonstrates strong local authentication controls, but it does not currently provide repository-verifiable evidence of the required federation protocols.

## 6. Evidence Matrix

| Control | Current evidence | Status |
|---------|------------------|--------|
| Web user authentication | Laravel session authentication routes and `auth` middleware | Implemented |
| API user authentication | Sanctum-based token authentication and protected routes | Implemented |
| MFA for critical users | OTP generation, delivery, and verification flow | Implemented |
| Email verification | `verified` middleware on sensitive routes | Implemented |
| Role-based access control | Spatie Permission integration and role-aware logic | Implemented |
| SAML 2.0 federation | No implementation evidence identified in the repository | Not implemented / not evidenced |
| OAuth 2.0 federation | No implementation evidence identified in the repository | Not implemented / not evidenced |

## 7. Recommended Requirement Wording

IGS Billing currently implements user authentication controls through Laravel session-based web authentication, Laravel Sanctum API token authentication, email verification, role-based access control, and OTP-based MFA for privileged users. These controls reduce the risk of unauthorized access and provide evidence of how user authentication is performed within the application.

However, based on the current repository state, no verifiable implementation evidence was identified for federated access control through SAML 2.0 or OAuth 2.0. Therefore, this requirement should currently be classified as partially compliant until federation-based access control is implemented or external operational evidence is provided.

## 8. Evidence Required for Full Compliance

To move this requirement from partial to full compliance, one or more of the following should be attached as evidence:

- SAML 2.0 configuration and integration evidence.
- OAuth 2.0 or OIDC federation flow evidence.
- Identity provider integration evidence, such as Azure AD, Okta, Auth0, or Google Workspace.
- Screenshots or exported configuration showing SSO endpoints, federation metadata, or authorization flows.
- Architecture or operational documentation demonstrating the active federated authentication model in production.

## 9. Verified Repository References

- `app/Http/Controllers/AuthController.php`
- `app/Models/User.php`
- `app/Notifications/OtpNotification.php`
- `routes/api.php`
- `routes/web.php`
- `config/auth.php`
- `config/sanctum.php`
- `composer.json`
- `docs/api/auth/auth.md`
- `README.md`
- `docs/security-assessment.md`

## 10. Conclusion

Based on the evidence currently verifiable in the repository, IGS Billing supports authenticated access through web sessions, API tokens, email verification, RBAC, and MFA. These controls provide meaningful evidence of user authentication. However, the repository does not presently demonstrate federated access control through SAML 2.0 or OAuth 2.0, so the requirement should be answered as **partially compliant**.
