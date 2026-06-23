# Annex - Profile Management Evidence and Operational Gaps

## 1. Purpose

This annex summarizes the evidence currently available for profile management and identifies the missing evidence needed to fully support an ABC profile-management requirement.

This annex should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

## 2. Currently Available Evidence

The repository currently supports the following evidence:

### A. RBAC platform evidence

- Spatie Laravel Permission installed and configured.
- Dedicated role and permission tables.
- Role-to-permission mapping tables.
- Permission cache configuration.

### B. Role definition evidence

- `admin` profile with privileged permissions.
- `user` profile with minimal read-only permissions.
- Authoritative role-to-permission synchronization through `syncPermissions()`.

### C. User assignment evidence

- Explicit role assignment during provisioning.
- Distinct role allocation by job function.
- Environment-aware seeding for production and sandbox identities.

### D. Runtime enforcement evidence

- Permission gating through `$user->can()` checks.
- Restricted access to sensitive operations.
- Sensitive-access logging where applicable.

### E. Profile data structure evidence

- `UserRole` model with auditable CRUD-style capability flags.
- Validation rules for role/profile objects.
- Auditing enabled for profile records.

## 3. Missing Evidence for Full ABC Support

The following evidence is not clearly available in the repository:

- Dedicated routes for role/profile administration.
- Role/profile administration controllers.
- A visible UI or back-office module for managing profiles.
- Explicit runtime create/update/delete workflows for profile definitions.

## 4. Minimum Additional Evidence to Attach

If profile administration exists outside the currently verifiable repository surface, at least one of the following evidence sets should be attached:

### A. Application administration evidence

- Screenshot of role/profile administration screen.
- Screenshot of profile creation flow.
- Screenshot of profile edit flow.
- Screenshot of profile deactivation or deletion flow.

### B. Technical flow evidence

- Route definitions for role/profile management.
- Controller or service logic for profile CRUD.
- Audit logs showing profile changes.
- Approval workflow for profile changes.

### C. Governance evidence

- Procedure for access-profile creation and approval.
- Periodic access review records.
- Segregation-of-duties evidence for profile administration.

## 5. Suggested Evidence to Show the Auditor Now

For the controls already implemented and verifiable, the following can be shown to the auditor:

- Permission package configuration and permission-table migration.
- Seeder-based role and permission definitions.
- Seeder-based user role assignment.
- Runtime permission enforcement example in sensitive controllers.
- Security and PCI documentation referencing RBAC and least privilege.

## 6. Audit Note

Until an exposed or externally evidenced create/update/delete workflow for profiles is attached, this requirement should remain classified as **partially compliant**.
