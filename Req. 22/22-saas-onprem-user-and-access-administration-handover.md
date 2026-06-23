# SaaS / On-Prem Point 22 - User and Access Administration Handover to CyAAL

## 1. Objective

This document records the current evidence available in the IGS Billing project regarding user and access administration, with specific attention to the requirement that administration of users and access must be delivered to CyAAL, the BAZ identity management area.

This point should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Current Compliance Position

**Status:** Partially compliant.

Repository evidence confirms that user and access administration is centrally controlled at the technical level: self-registration is disabled, users are provisioned through controlled processes, roles are assigned explicitly, and access is enforced through RBAC and approval-oriented provisioning boundaries. However, the repository does not provide verifiable evidence that responsibility for user and access administration has been formally transferred to CyAAL or that CyAAL is the active operational owner of the identity lifecycle.

Accordingly, the requirement should currently be classified as partially compliant.

## 3. Scope of Verifiable Evidence

The following controls are verifiable from the current repository state:

- Self-service user registration is disabled.
- User provisioning is centrally controlled.
- Roles and permissions are assigned explicitly.
- Access is enforced through RBAC and least-privilege checks.
- Privileged identities are explicitly enumerated and provisioned.
- Sensitive access requires approved role assignment and MFA.

The following items are not verifiable from the repository and therefore remain unsupported as implementation evidence:

- Formal ownership transfer of user/access administration to CyAAL.
- Operational handoff procedures between IGS and BAZ CyAAL.
- CyAAL-managed approval workflow, ticketing, or identity-governance process.
- Evidence that CyAAL is the system-of-record owner for joiner/mover/leaver operations.

## 4. Identified User and Access Administration Controls

### 4.1 Centralized User Provisioning

The repository shows that user creation and role assignment are centrally controlled rather than self-service. Default accounts are provisioned through seeding logic and role assignment occurs explicitly at provisioning time.

Verified controls:

- Centralized provisioning through `UserDefaultSeeder`.
- Explicit role assignment using `assignRole()`.
- Named administrative identities provisioned individually.
- Environment-aware provisioning for production and sandbox accounts.

### 4.2 Self-Registration Disabled

The web application disables public self-registration. This prevents users from creating their own accounts and supports centralized control over identity creation.

Verified controls:

- Laravel authentication routes configured with `register => false`.
- No public self-service onboarding path evidenced in the repository.
- No runtime self-elevation path to privileged roles identified.

### 4.3 Role-Based Access Administration

Access permissions are managed through role and permission definitions implemented with Spatie Laravel Permission. The repository evidences central permission catalogs and explicit mapping of permissions to roles.

Verified controls:

- `admin` and `user` roles defined centrally.
- Explicit permission catalog including `view users` and `manage users`.
- Authoritative `syncPermissions()` usage.
- Runtime permission enforcement on sensitive operations.

### 4.4 Management-Gated Privileged Access

Privileged users are provisioned as explicitly named identities, and sensitive permissions are attached only to those approved identities. The documentation also evidences MFA for admin users and logging of sensitive access paths.

Verified controls:

- Named administrative identities in provisioning logic.
- `admin` role required for privileged operations.
- MFA required for privileged users.
- Sensitive access logging and audit evidence.

## 5. Gap Analysis for CyAAL Handover

The current repository demonstrates that user and access administration is controlled, centralized, and not self-service. However, the requirement is not only about technical control; it explicitly requires that administration be delivered to CyAAL, the BAZ identity-management area.

Observed findings:

- The repository evidences centralized provisioning and access restriction.
- The repository evidences approval-style boundaries for privileged identities.
- The repository does not identify CyAAL as owner, operator, or approval authority.
- No ticketing, workflow, API integration, RACI, or operating procedure referencing CyAAL was identified.
- No technical integration with a BAZ identity administration platform was identified.

Conclusion:

The repository supports the existence of centralized user and access administration controls, but it does not provide verifiable evidence that such administration has been formally handed over to CyAAL. This supports a partial compliance position.

## 6. Evidence Matrix

| Control | Current evidence | Status |
|---------|------------------|--------|
| Centralized user provisioning | `UserDefaultSeeder` provisions users and assigns roles | Implemented |
| Self-service registration disabled | `register => false` in Laravel auth routes | Implemented |
| Role and permission administration | `RolePermissionSeeder` and Spatie Permission configuration | Implemented |
| Privileged access approval boundary | Named admin identities and explicit privileged role assignment | Implemented |
| Runtime enforcement of access controls | RBAC checks and protected routes | Implemented |
| Formal handover to CyAAL | No repository-verifiable evidence identified | Not evidenced |
| CyAAL operational ownership of IAM lifecycle | No repository-verifiable evidence identified | Not evidenced |

## 7. Recommended Requirement Wording

IGS Billing currently implements centralized technical controls for user and access administration, including controlled user provisioning, disabled self-registration, explicit role assignment, and runtime RBAC enforcement. These controls support internal control objectives and reduce the risk of unauthorized access, fraud, and administrative errors.

However, based on the current repository state, no verifiable evidence was identified showing that user and access administration has been formally delivered to CyAAL, the BAZ identity management area. Therefore, this requirement should currently be classified as partially compliant until organizational handover evidence and CyAAL operating ownership are formally documented.

## 8. Evidence Required for Full Compliance

To move this requirement from partial to full compliance, one or more of the following should be attached as evidence:

- Formal RACI or responsibility matrix assigning IAM ownership to CyAAL.
- Procedure or SOP showing CyAAL as the operating owner for user provisioning and access changes.
- Ticketing or workflow evidence demonstrating CyAAL approval and execution of joiner/mover/leaver requests.
- Screenshots from the CyAAL-managed IAM platform or administration console.
- Governance documentation showing CyAAL ownership of access reviews and privileged account administration.

## 9. Verified Repository References

- `routes/web.php`
- `database/seeders/UserDefaultSeeder.php`
- `database/seeders/RolePermissionSeeder.php`
- `config/permission.php`
- `app/Models/User.php`
- `docs/pci-dss/req-7.3.1-access-control-system.md`
- `docs/pci-dss/req-7.3.2-permissions-by-job-function.md`
- `docs/pci-dss/req-7.3.3-deny-all-by-default.md`
- `docs/pci-dss/req-9.4.4.b-management-approval-media-movement.md`

## 10. Conclusion

Based on the evidence currently verifiable in the repository, IGS Billing enforces centralized and controlled user/access administration at the technical layer. However, the repository does not demonstrate that administration of users and access has been formally handed over to CyAAL. For that reason, the requirement should be answered as **partially compliant**.
