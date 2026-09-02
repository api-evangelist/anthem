---
name: anthem-member-patient-access
description: Obtain a member's authorization through SMART on FHIR and read their Anthem claims and clinical history under the CMS Patient Access rule.
api: Anthem Patient Access API / Anthem Patient360 Member FHIR API
generated: '2026-09-02'
method: generated
source: >-
  authentication/anthem-authentication.yml, scopes/anthem-scopes.yml,
  openapi/anthem-patient360-member-fhir-api-openapi.yml,
  https://www.anthem.com/content/dam/digital/developers-portal/Anthem-IOProviderDirectoryAndFormulary-API-Documentation.pdf
operations:
  - getP360Conformance
  - p360ReadPatient
  - p360SearchClaim
  - p360SearchCoverage
  - p360SearchCondition
  - p360SearchObservation
  - p360SearchMedicationOrder
  - p360SearchImmunization
  - p360SearchAllergyIntolerance
---

# Read an Anthem member's own health data with their consent

This is a **member-authorized** flow. You are never acting on your own credentials; you are acting on a consent the member granted, and they can withdraw it.

## Two surfaces, do not confuse them

- **Patient Access API (R4)** — the CMS-mandate surface Anthem documents. Up to five years of medical, dental, vision and pharmacy claims plus clinical data. FHIR R4 4.0.1, CARIN IG for Blue Button STU 2.1.0, US Core 6.1.0, SMART App Launch 2.2.0. Thirteen brand-specific production bases under `https://totalview.healthos.elevancehealth.com/resources/registered/<Brand>/api/v1/fhir` — pick the base for the member's brand (Amerigroup, Anthem Blue Cross, Anthem Blue Cross Blue Shield, Blue Medicare Advantage, Clear Health Alliance, Dell Children Health Plan, Healthy Blue, Healthy Blue Blue Choice, Healthy Blue NC, Simply HealthCare, Summit, Unicare, Wellpoint). Register at https://www.anthem.com/developers/request-anthem-io.
- **Patient360 member FHIR (DSTU2)** — a separate, older, live Anthem server at `https://patient360c.anthem.com/P360Member/api/fhir` running FHIR **1.0.2**. Its conformance statement and its SMART/OpenID discovery document are both public, so it is the surface you can actually inspect before you have credentials. The `p360*` operationIds above belong to this server.

## Steps

1. **Start in the sandbox.** Anthem runs a public Patient Access sandbox with synthetic data, open on developer self-registration, supporting SMART authorization and SMART client registration. Do all functional testing there — production approval "can take several weeks".
2. **Read the discovery documents.** `GET https://patient360c.anthem.com/P360Member/identityserver/.well-known/openid-configuration` (anonymous, HTTP 200) gives you `authorization_endpoint`, `token_endpoint`, `jwks_uri`, PKCE support (`S256`) and all 1,048 supported scopes. `getP360Conformance` — `GET /metadata?_format=json` — gives you the resource set. Default response format on this server is XML; pass `_format=json`.
3. **Request the narrowest scopes that answer your question.** The grammar is `patient/<Resource>.read`. Ask for `patient/Claim.read patient/Coverage.read patient/Condition.read` — not `patient/*.read`. A member reviewing a consent screen sees what you asked for.
4. **Run authorization_code with PKCE.** Send the member to `authorization_endpoint` with `code_challenge_method=S256`; exchange at `token_endpoint` (`client_secret_post` or `client_secret_basic`).
5. **Identify the member.** The `fhirUser` claim and the `patientidentifier` claim come back on the id token. `p360ReadPatient` — `GET /Patient/{id}`.
6. **Pull the history.** `p360SearchClaim`, `p360SearchCoverage`, `p360SearchCondition`, `p360SearchObservation`, `p360SearchMedicationOrder`, `p360SearchImmunization`, `p360SearchAllergyIntolerance` — `GET /{Resource}?patient=...&_lastUpdated=gt<date>`. Follow `Bundle.link.next` to page.
7. **Respect the 90-day clock.** Anthem states a Patient Access production token is valid for **90 days** and that continued access requires **renewed member consent**. Schedule re-consent before expiry; do not silently keep refreshing.
8. **Honour withdrawal.** The member can revoke. The identity server exposes `connect/revocation` and `connect/endsession`. Delete or stop refreshing cached data when consent ends.

## Handling and privacy

This is protected health information under HIPAA. Store the minimum, encrypt at rest, log access, and never widen the scope set beyond what the member approved. Anthem contacts for interoperability questions: interoperabilityworkgroup@anthem.com.

## Known gaps

Anthem publishes no rate limits, no changelog, no status page and no error reference for these endpoints. Prior-authorization data is committed to the Patient Access API by 2027-01-01 under CMS-0057-F but is not there today.
