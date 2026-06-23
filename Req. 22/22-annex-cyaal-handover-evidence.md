# Annex - CyAAL Handover Evidence and Operational Gaps

## 1. Purpose

This annex summarizes the evidence currently available for centralized user and access administration and identifies the additional evidence required to prove handover to CyAAL.

This annex should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Currently Available Technical Evidence

The repository currently supports the following evidence:

### A. Centralized account provisioning evidence

- User accounts provisioned through controlled seeding logic.
- Explicit role assignment at provisioning time.
- Named administrative identities.
- Environment-aware segregation of user creation.

### B. Registration control evidence

- Self-registration disabled.
- No public account-creation path exposed.
- No runtime privilege-elevation path identified.

### C. Access control evidence

- Central role and permission catalog.
- `admin` and `user` roles defined explicitly.
- `view users` and `manage users` permissions defined.
- Runtime permission checks on sensitive operations.

### D. Governance-style technical boundaries

- Privileged users require explicit provisioning.
- Privileged users require MFA.
- Sensitive-access logging and auditability exist.

## 3. Missing Evidence for CyAAL Ownership

The following evidence is not currently available in the repository:

- CyAAL listed as operating owner of user/access administration.
- Formal handover documentation to CyAAL.
- CyAAL-managed workflow for account creation, modification, or revocation.
- CyAAL-managed access review process.
- Integration with a BAZ identity-management platform.

## 4. Minimum Additional Evidence to Attach

If CyAAL already operates the process outside the repository, at least one of the following evidence sets should be attached:

### A. Governance evidence

- Signed responsibility matrix.
- IAM operating procedure naming CyAAL as owner.
- Joiner/mover/leaver policy naming CyAAL as executor or approver.

### B. Workflow evidence

- Access request ticket handled by CyAAL.
- Access modification approval ticket handled by CyAAL.
- Account deprovisioning record executed by CyAAL.

### C. Platform evidence

- Screenshot of CyAAL administration console.
- Screenshot of CyAAL-controlled user lifecycle workflow.
- Screenshot of CyAAL-driven approval or recertification process.

## 5. Suggested Evidence to Show the Auditor Now

For the controls already implemented and verifiable, the following can be shown now:

- Self-registration disabled in web auth routes.
- Seeder-based controlled provisioning.
- Seeder-based role and permission assignment.
- RBAC configuration and permission-table migration.
- Documentation showing approval-gated privileged identities and least privilege.

## 6. Audit Note

Until documentary or operational evidence shows that CyAAL is the effective owner of user and access administration, this requirement should remain classified as **partially compliant**.
