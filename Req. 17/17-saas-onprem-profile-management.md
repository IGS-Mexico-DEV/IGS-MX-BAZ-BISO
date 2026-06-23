# SaaS / On-Prem Point 17 - Profile Management and Role Administration

## 1. Objective

This document records the current evidence available in the IGS Billing project regarding profile management, role-based access control, and the management of user access profiles.

This point should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Current Compliance Position

**Status:** Partially compliant.

Repository evidence confirms that the project implements role-based access control, permission assignment, role provisioning, runtime permission enforcement, and least-privilege controls. However, the repository does not provide clear evidence of a fully exposed in-application ABC workflow for profile administration, understood as create, update, and delete management of access profiles through a dedicated operational module or controller surface.

Accordingly, the requirement should currently be classified as partially compliant.

## 3. Scope of Verifiable Evidence

The following controls are verifiable from the current repository state:

- RBAC implementation using Spatie Laravel Permission.
- Role and permission data structures at database level.
- Seeded role definitions and permission mapping.
- Provisioning-time role assignment for users.
- Runtime permission enforcement for sensitive operations.
- Least-privilege role design.
- Auditable custom `UserRole` model with CRUD-oriented fields.

The following items are not clearly evidenced as an exposed application management workflow:

- Dedicated routes or controllers for operational create/update/delete of roles.
- A visible UI module for profile administration.
- Clear runtime administration flows for modifying role definitions from the application interface.

## 4. Identified Profile Management Controls

### 4.1 RBAC Foundation

The project uses Spatie Laravel Permission as the core RBAC engine. The configuration defines role, permission, and pivot tables for assigning profiles and permissions to application users.

Verified controls:

- Spatie Permission package installed and configured.
- Dedicated `roles`, `permissions`, `model_has_roles`, `model_has_permissions`, and `role_has_permissions` tables.
- Gate-integrated permission check method enabled.
- Permission caching and automatic refresh support.

### 4.2 Role and Permission Definition

Role and permission definitions are created in an authoritative seeder. The current implementation defines at least two application profiles, `admin` and `user`, and associates each one with an explicit permission set.

Verified controls:

- Central role definition in `RolePermissionSeeder`.
- Explicit permission catalog including `view users`, `manage users`, `view reports`, and `manage system`.
- Authoritative `syncPermissions()` usage to prevent excess permissions.
- Minimal read-only permission set for the `user` role.

### 4.3 Role Assignment During Provisioning

Users are assigned a role at provisioning time in the default user seeder. The role assignment reflects the intended job function of the identity being created.

Verified controls:

- Explicit role assignment using `assignRole()`.
- Administrative users provisioned with the `admin` role.
- Business, sponsor, and non-administrative users provisioned with the `user` role.
- Environment-aware provisioning for production and sandbox users.

### 4.4 Runtime Enforcement of Role Permissions

Sensitive operations are protected through runtime permission checks. For example, Token Vault access is restricted to identities with the required permission before sensitive fields are exposed.

Verified controls:

- Permission enforcement through `$user->can()`.
- Sensitive data visibility gated by permission checks.
- Logging of sensitive access paths.
- Least-privilege enforcement at runtime.

### 4.5 Custom Profile Model Evidence

The repository also contains a custom `UserRole` model with auditable profile attributes such as create, read, update, delete, download, and decrypt capabilities. This shows that the domain includes explicit profile-management data structures.

Verified controls:

- `UserRole` model exists.
- Profile attributes include CRUD-level flags.
- Auditing enabled for role/profile records.
- Validation rules defined for profile objects.

## 5. Gap Analysis for ABC of Profiles

The repository demonstrates profile definition, permission mapping, provisioning assignment, and runtime enforcement. However, the requirement explicitly references profile management as an ABC process, which normally implies an exposed lifecycle for creating, updating, and removing profiles.

Observed findings:

- Role definitions are currently evidenced through seeders and configuration.
- Runtime use of profiles and permissions is clearly evidenced.
- A profile data model (`UserRole`) exists and is auditable.
- No dedicated route, controller, or visible administrative UI was identified for operational create/update/delete management of profiles.

Conclusion:

The project evidences strong RBAC and profile enforcement controls, but the repository does not clearly demonstrate a complete exposed ABC management workflow for profiles. This supports a partial compliance position.

## 6. Evidence Matrix

| Control | Current evidence | Status |
|---------|------------------|--------|
| Role-based access control | Spatie Permission integration and role-aware user model | Implemented |
| Role and permission persistence | Permission migration tables and configuration | Implemented |
| Authoritative profile definitions | `RolePermissionSeeder` role/permission mapping | Implemented |
| Role assignment to users | `UserDefaultSeeder` provisioning logic | Implemented |
| Runtime permission enforcement | `$user->can()` checks on sensitive operations | Implemented |
| Auditable profile data structure | `UserRole` model with CRUD-oriented attributes | Implemented |
| Exposed ABC workflow for profile administration | No clear route/controller/UI evidence identified | Partially evidenced |

## 7. Recommended Requirement Wording

IGS Billing currently implements profile and access management controls through role-based access control, explicit permission definitions, provisioning-time role assignment, and runtime permission enforcement. These controls reduce the risk of unauthorized access by assigning permissions according to role and limiting access to sensitive operations through least-privilege checks.

However, based on the current repository state, profile administration is primarily evidenced through technical configuration, seeders, and permission enforcement logic. No clearly exposed in-application ABC workflow for create, update, and delete management of profiles was identified in the repository. Therefore, this requirement should currently be classified as partially compliant.

## 8. Evidence Required for Full Compliance

To move this requirement from partial to full compliance, one or more of the following should be attached as evidence:

- Screenshots of a profile administration module.
- Routes, controllers, or service flows for creating, updating, and deleting roles or profiles.
- Operational documentation showing how profile changes are performed and approved.
- Audit evidence of role/profile changes performed through the application.
- Access review procedures demonstrating periodic governance of assigned profiles.

## 9. Verified Repository References

- `app/Models/User.php`
- `app/Models/UserRole.php`
- `app/Http/Controllers/TokenVaultController.php`
- `config/permission.php`
- `database/migrations/2026_01_10_043621_create_permission_tables.php`
- `database/seeders/RolePermissionSeeder.php`
- `database/seeders/UserDefaultSeeder.php`
- `docs/security-assessment.md`
- `docs/pci-dss/req-7.3.1-access-control-system.md`
- `docs/pci-dss/req-7.3.2-permissions-by-job-function.md`

## 10. Conclusion

Based on the evidence currently verifiable in the repository, IGS Billing implements profile and permission control through RBAC, seeded role definitions, provisioning-time role assignment, and runtime enforcement. These controls provide strong evidence of access-profile governance. However, because the repository does not clearly expose a full in-application ABC lifecycle for profile administration, the requirement should currently be answered as **partially compliant**.
