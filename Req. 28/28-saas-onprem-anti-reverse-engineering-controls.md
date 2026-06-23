# SaaS / On-Prem Point 28 - Anti-Reverse-Engineering Controls

## 1. Objective

This document records the technical and operational evidence used to address the reverse-engineering control for the IGS Billing application, considering the nature of a Laravel/PHP server-side stack.

This point should be interpreted together with [01-assessment-context.md](../01-assessment-context.md).

## 2. Current Compliance Position

**Status:** Compliant.

For a Laravel application, reverse-engineering risk must be evaluated differently from desktop or mobile applications distributed as binaries. In this architecture, the backend PHP source code is executed on the server and is not delivered to end users. The appropriate control objective is therefore to ensure that the source code is not publicly accessible, the deployment is protected, the platform is hardened, frontend-delivered logic is minimized, and access to the codebase is operationally restricted.

Based on the current repository evidence and the provided operational context, this control is satisfied through a combination of server-side architecture, protected deployment and hardening measures, frontend asset minimization, and restricted access to the private source-code repository. The repository is stated to be private, invitation-based, limited to specialized personnel, and protected by 2FA. Under this control model, dedicated code obfuscation is not the primary or necessary mechanism for a Laravel application.

## 3. Scope of Verifiable Evidence

The following items are verifiable from the repository:

- Backend application logic is implemented in Laravel/PHP and executed server-side.
- Frontend build uses Vite.
- Frontend build is configured to minify assets with Terser.
- Terser removes `console` statements and `debugger` instructions during build.
- Production build manifest references compiled frontend assets.
- Production build JavaScript asset is minified.
- Security hardening guidance exists for TLS, CSP, HSTS, headers, secrets management, and WAF recommendations.

The following items are treated as operational controls provided as context for this response:

- Source-code repository access is private.
- Repository membership is invitation-based.
- Access is limited to specialized personnel.
- Access is protected with 2FA.

## 4. Technical and Operational Evidence

### 4.1 Server-Side Execution Model

The application is implemented on Laravel/PHP, which means the backend source code is processed on the server and is not distributed to the browser or exposed as a client-installable binary. This materially reduces the classic reverse-engineering scenario associated with desktop or mobile packaged software.

Control implication:

- Users interact with rendered responses and API outputs, not with the backend source tree.
- Reverse-engineering exposure is concentrated on the client-side assets, not on the server-side PHP codebase.

### 4.2 Protected Source-Code Access

According to the operational context provided for this assessment, access to the source-code repository is controlled as follows:

- The repository is private.
- Access is granted by invitation.
- Access is limited to specialized personnel.
- 2FA is required for repository access.

These controls are directly relevant to preventing unauthorized acquisition of the source code.

### 4.3 Deployment Protection and Hardening

The project contains a formal hardening guide covering security controls that reduce the practical risk of unauthorized access, interception, misuse, and exposure in deployed environments such as managed cloud or AWS-style infrastructure.

Observed evidence:

- TLS 1.2 / 1.3 enforcement guidance.
- CSP implementation guidance.
- HSTS enforcement guidance.
- X-Content-Type-Options, X-Frame-Options, Referrer-Policy, and Permissions-Policy guidance.
- Secrets-management guidance.
- WAF recommendations.

These are relevant because preventing reverse engineering in a server-side web application depends primarily on restricting access to code, servers, and exposed logic, not on binary obfuscation.

### 4.4 Frontend Build Minification

The frontend pipeline uses Vite with Terser minification.

Observed evidence:

- Build command defined as `vite build`.
- `minify: 'terser'` enabled in the Vite build configuration.
- `drop_console: true` enabled.
- `drop_debugger: true` enabled.

This reduces readability of delivered browser-side JavaScript and removes common debugging artifacts from compiled assets.

### 4.5 Compiled Asset Delivery

The build manifest confirms that the application publishes compiled assets into the production build output.

Observed evidence:

- `public/build/manifest.json` references hashed asset files.
- `public/build/assets/app-3FUiPdkU.js` exists as a compiled frontend artifact.

### 4.6 Example of Minified Delivered Code

The generated JavaScript bundle is clearly minified. Example excerpt from the built asset:

```js
var t=function(){function t(t,e){void 0===e&&(e=[]),this._eventType=t,this._eventFunctions=e}return t.prototype.init=function(){var t=this;this._eventFunctions.forEach(function(e){"undefined"!=typeof window&&window.addEventListener(t._eventType,e)})},t}(),e=new(function(){function t(){this._instances={Accordion:{},Carousel:{},Collapse:{},Dial:{},Dismiss:{},Drawer:{},Dropdown:{},Modal:{},Popover:{},Tabs:{},Tooltip:{},InputCounter:{},CopyClipboard:{},Datepicker:{}}}
```

This is acceptable as evidence that browser-delivered logic is minimized and not served in raw development form.

## 5. Control Assessment

### 5.1 What the Current Implementation Does Provide

- Server-side execution of backend business logic, with no backend source code delivered to the client.
- Private repository access restricted to specialized personnel by invitation and protected with 2FA.
- Deployment-hardening guidance covering transport, headers, CSP, secrets, and WAF posture.
- Basic reduction of frontend code readability through minification.
- Removal of debugging-oriented statements from distributed JavaScript.
- Hashed compiled asset delivery rather than raw source files.

### 5.2 What the Current Implementation Does Not Require to Satisfy This Control

- For a Laravel/PHP web application, a dedicated binary obfuscation product is not the primary control mechanism.
- Because backend code is not distributed to the client, application-wide source obfuscation is not the main basis for compliance.
- The control is better satisfied by restricting code access, protecting deployment environments, and minimizing client-side logic exposure.

## 6. Recommended Requirement Wording

IGS Billing currently includes a limited technical measure to reduce reverse-engineering exposure on the client-side delivery layer: frontend assets are compiled and minified with Vite and Terser, and debugging artifacts are removed from the generated JavaScript bundle. This provides a basic deterrent against casual inspection of browser-delivered code.

For the Laravel/PHP backend, the main protection model is different: source code remains on the server, is not publicly delivered to end users, and is further protected by restricted repository access, controlled deployment, and hardening measures. Based on the provided operational context that repository access is private, invitation-based, limited to specialized personnel, and protected with 2FA, this requirement should be classified as **compliant**.

## 7. Evidence Matrix

| Requirement element | Current evidence | Status |
|---------|------------------|--------|
| Backend source not publicly delivered | Laravel server-side execution model | Implemented |
| Repository access restriction | Private, invitation-based, specialized-personnel access with 2FA (operational context provided) | Implemented |
| Deployment protection | Hardening guide covering TLS, CSP, HSTS, headers, secrets, WAF | Implemented |
| Frontend compiled delivery | Vite build pipeline and hashed manifest output | Implemented |
| Frontend minification | Terser enabled in build configuration | Implemented |
| Removal of debug artifacts | `drop_console` and `drop_debugger` enabled | Implemented |
| Frontend exposure reduction | Minified frontend bundle available | Implemented |

## 8. Auditor-Facing Conclusion

The repository supports evidence that the application addresses reverse-engineering risk using the control model appropriate for Laravel: backend source code is server-side, frontend-delivered logic is minimized through compiled/minified assets, and the deployment is supported by hardening guidance. In addition, this assessment incorporates the provided operational control that repository access is private, invitation-based, limited to specialized personnel, and protected by 2FA.

Accordingly, this point should be answered as **compliant**. A dedicated code-obfuscation platform may be optional as a strengthening control, but it is not required to justify compliance for this server-side architecture.

## 9. Verified Repository References

- `app/`
- `package.json`
- `vite.config.js`
- `public/build/manifest.json`
- `public/build/assets/app-3FUiPdkU.js`
- `docs/security-hardening-guide.md`

## 10. Conclusion

For this Laravel application, anti-reverse-engineering control is primarily achieved by keeping backend source code on the server, restricting access to the private repository, protecting deployment environments, applying hardening measures, and minimizing browser-delivered logic through compiled and minified frontend assets. Under that control model, this requirement is **compliant**.
