---
name: anthem-find-in-network-provider
description: Find an in-network Anthem practitioner, facility or service for a given plan and location, using the CMS-mandated Anthem Provider Directory FHIR API.
api: Anthem Provider Directory FHIR API
generated: '2026-09-02'
method: generated
source: openapi/anthem-provider-directory-api-openapi.yml (derived from the live CapabilityStatement at https://totalview.healthos.elevancehealth.com/resources/unregistered/api/v1/fhir/cms_mandate/mcd/metadata)
operations:
  - getCapabilityStatement
  - searchInsurancePlan
  - searchOrganization
  - searchPractitioner
  - searchPractitionerRole
  - searchLocation
  - searchHealthcareService
  - readPractitioner
  - readOrganization
---

# Find an in-network Anthem provider

Base: `https://totalview.healthos.elevancehealth.com/resources/unregistered/api/v1/fhir/cms_mandate/mcd`

## Before you start

You need an OAuth 2.0 **client-credentials** token. Anthem does not publish a token endpoint — it emails you the access token URL, client id and client secret after approving the Provider Directory API Production Environment request form at https://www.anthem.com/developers/provider-directory-api-request. Budget several weeks; there is no self-service key.

```
POST <access token endpoint URL>
Content-Type: application/x-www-form-urlencoded
Authorization: Basic <base64 client_id:client_secret>

grant_type=client_credentials
```

Then send `Authorization: Bearer <token>` on every call below.

## Steps

1. **Confirm the surface.** `getCapabilityStatement` — `GET /metadata`. This is the only operation that answers without a token, so use it to check the server is up before you conclude your credentials are wrong.
2. **Find the plan.** `searchInsurancePlan` — `GET /InsurancePlan?name=...` or `GET /InsurancePlan?coverage-area=<2-letter state>`. Anthem's endpoint support document searches coverage area by two-letter state abbreviation. Keep the returned `InsurancePlan.id`.
3. **Find the network organization.** `searchOrganization` — `GET /Organization?name=...&address-state=XX`. In Plan-Net, a payer network is itself an `Organization`; `PractitionerRole.network` references it.
4. **Find candidate practitioners.** `searchPractitioner` — `GET /Practitioner?family=...&given=...` or `?name=...`. This returns the person, not their network participation.
5. **Establish that they are in network.** `searchPractitionerRole` — `GET /PractitionerRole?practitioner=Practitioner/<id>&network=Organization/<network-id>`. A `Practitioner` alone proves nothing about coverage; the `PractitionerRole` is what binds a person to a network, an organization, a location and a service. Never answer "in network" from step 4.
6. **Resolve the places and services in one round trip.** Add `_include`: `GET /PractitionerRole?practitioner=Practitioner/<id>&_include=PractitionerRole:location&_include=PractitionerRole:organization&_include=PractitionerRole:service`.
7. **Or search by service instead of by person.** `searchHealthcareService` — `GET /HealthcareService?specialty=<system>|<code>&location=Location/<id>`.
8. **Read individual records** with `readPractitioner` / `readOrganization` (`GET /{Resource}/{id}`) when you need the full resource.

## Paging

Follow `Bundle.link[relation=next]`. Use `_count` to size the page. There is no offset or cursor parameter.

## Error handling — read this before writing a retry loop

Anonymous or badly-credentialed calls to this host return **HTTP 500**, not 401:

```json
{"status_code":500,"status":"failed","error":"Internal server error","error_description":"An unexpected error occurred. Please try again"}
```

An unknown resource type and a non-existent id return the *same* body. So:

- Treat a 500 from this host as an authorization failure first. Re-check the bearer token before retrying.
- Do **not** retry a 500 with exponential backoff as if it were transient — an unauthenticated caller will get it forever.
- There is no request id or correlation id in any response, so you have nothing to quote to support. Log your own.
- Rate limits are undocumented and no `RateLimit-*` or `Retry-After` header is returned. Be conservative.

## What this API cannot do

It is read-only — search, read and vread. There is no write, so no idempotency key and nothing to reverse.
