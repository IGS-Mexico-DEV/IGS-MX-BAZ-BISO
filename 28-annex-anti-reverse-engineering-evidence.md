# Annex - Anti-Reverse-Engineering Evidence

## 1. Purpose

This annex summarizes the evidence supporting the anti-reverse-engineering control for a Laravel/PHP application, where the relevant safeguards are source-code protection, controlled deployment, hardening, and reduced client-side logic exposure.

This annex should be interpreted together with [01-assessment-context.md](./01-assessment-context.md).

## 2. Available Evidence

### A. Architecture evidence

- Backend logic resides in a Laravel/PHP server-side application.
- Backend source code is executed on the server rather than delivered to end users.

### B. Operational access-control evidence provided for this assessment

- The source-code repository is private.
- Access is invitation-based.
- Access is limited to specialized personnel.
- 2FA protects repository access.

### C. Hardening evidence

- The project includes a formal hardening guide.
- The guide covers TLS, CSP, HSTS, headers, secrets management, and WAF recommendations.

### D. Build-chain evidence

- `package.json` defines the production build command as `vite build`.
- `vite.config.js` enables `minify: 'terser'`.
- `vite.config.js` enables `drop_console: true`.
- `vite.config.js` enables `drop_debugger: true`.

### E. Build-output evidence

- `public/build/manifest.json` maps source entries to compiled hashed assets.
- `public/build/assets/app-3FUiPdkU.js` exists as a minified generated asset.

### F. Evidence sample

The generated JavaScript bundle is minified and significantly less readable than source form. This can be shown as limited evidence that client-side code is not distributed in raw development form.

## 3. Clarification About Obfuscation

The following evidence is not currently present in the repository:

- Dedicated obfuscation software.
- Backend PHP obfuscation.
- Anti-tamper tooling.
- Runtime self-protection.

For this requirement, those items are not the primary control basis for a Laravel server-side application. The principal control basis is that the source code is not publicly delivered, repository access is restricted, deployment is protected, and client-side exposure is minimized.

## 4. Audit Position

The current evidence supports a **compliant** answer when evaluated with the appropriate architecture-specific interpretation:

- The backend source code is server-side and not publicly delivered.
- Repository access is stated to be private, invitation-based, limited to specialized personnel, and protected with 2FA.
- Deployment hardening guidance is present.
- Frontend-delivered logic is compiled and minified.

## 5. Optional Strengthening Evidence

The answer could be further strengthened if the following external evidence exists:

- Screenshots or policy excerpts showing repository privacy and 2FA enforcement.
- Access-control records showing restricted code-repository membership.
- Deployment screenshots or runbooks for protected cloud environments.
- Secure SDLC or intellectual-property handling policies.
