# IGS Mexico / BAZ BISO - Common Assessment Context

## Purpose

This document defines the common context that must be used when interpreting the compliance points documented in this folder. It is intended to keep the evidence package consistent as new documents, annexes, and executive responses are added or updated.

## Current Development State

- The solution is in an active development and controlled release state.
- The repository evidences ongoing security, hardening, testing, and patch-management work.
- Compliance conclusions in this folder must reflect the current documented implementation state, not an ideal or assumed future state.

## Technology Context

- Backend: Laravel 12.x on PHP 8.2+.
- Authentication: Laravel Sanctum.
- Frontend: Blade, Livewire, Alpine.js, Tailwind CSS 4.x, Vite 6.x.
- Auditing: OwenIt Laravel Auditing.
- Authorization: Spatie Permission.
- Observability / monitoring support: Laravel Nightwatch and application logging.

This technology context is relevant because some controls must be interpreted according to a server-side Laravel web-application model rather than a desktop, mobile, or client-installed binary model.

## Service Delivery Model

- The solution is deployed in IGS (Integral Group Solution) infrastructure.
- The service is made available to GS (Grupo Salinas) via web access.
- Access is protected by VPN.
- Access is exposed through controlled URLs.
- Access is restricted through IP allowlisting / whitelist controls.

This service model must be considered when evaluating requirements related to implementation, administration, hardening, reverse engineering, and operational access.

## Interpretation Rule

- Do not assess the solution as if GS installs and operates a standalone customer-side software package unless the point explicitly requires that model.
- Evaluate controls according to the actual managed-service model evidenced and provided in operational context.
- Distinguish clearly between repository-verifiable evidence and operational context provided for the assessment.

## Maintenance Rule

- Update this context document whenever the development state, architecture, deployment model, or access-control delivery model changes materially.
- When a point document depends on this context, it should reference this file rather than restating the full model inconsistently.
