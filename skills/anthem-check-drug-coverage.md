---
name: anthem-check-drug-coverage
description: Determine whether a drug is on an Anthem Medicare, Medicaid or CHIP formulary, and at what tier, using the Anthem Drug Formulary FHIR API.
api: Anthem Drug Formulary FHIR API
generated: '2026-09-02'
method: generated
source: openapi/anthem-drug-formulary-api-openapi.yml (derived from Anthem's Interoperability API Endpoint Support Document IO105 v15.0)
operations:
  - searchFormularyInsurancePlan
  - searchFormularyBasic
  - searchFormularyMedicationKnowledge
  - readFormularyInsurancePlan
  - readFormularyBasic
  - readFormularyMedicationKnowledge
---

# Check Anthem drug coverage and tier

Base: `https://totalview.healthos.elevancehealth.com/resources/unregistered/api/v1/fhir/cms_mandate/frmlry`

Scope: **Medicare, Medicaid and CHIP plans only.** Anthem does not publish commercial-plan formularies through this API. Conforms to Da Vinci PDEX US Drug Formulary IG 2.0.1 STU2, where the resources are named unusually: a *FormularyItem* is a FHIR `Basic` and a *FormularyDrug* is a `MedicationKnowledge`.

## Before you start

OAuth 2.0 client-credentials, exactly as for the Provider Directory API — Anthem emails the token URL and credentials after approving the Formulary API Production Environment request form on https://www.anthem.com/developers. This server is stricter than its sibling: it returned **403 to an anonymous `/metadata` request**, so you cannot even read its capability statement without a token.

## Steps

1. **Find the formulary.** `searchFormularyInsurancePlan` — `GET /InsurancePlan?type=http://terminology.hl7.org/CodeSystem/v3ActCode|DRUGPOL`. Every formulary is an `InsurancePlan` of type `DRUGPOL`.
2. **Or go straight to a known formulary.** `GET /InsurancePlan?type=http://terminology.hl7.org/CodeSystem/v3ActCode|DRUGPOL&identifier=D1002`.
3. **Find which member plans use it.** `GET /InsurancePlan?formularycoverage=InsurancePlan/FormularyD1002` — this is the query that answers "if I pick this plan, which drug list do I get".
4. **Find the drug.** `searchFormularyMedicationKnowledge` — `GET /MedicationKnowledge?drug-name=<string>` or `?code=<system>|<code>` for an RxNorm/NDC code.
5. **Get tier and cost sharing.** `searchFormularyBasic` — `GET /Basic?code=formulary-item&formulary=InsurancePlan/<formulary-id>&subject=MedicationKnowledge/<drug-id>`. The FormularyItem is where `drug-tier` and `pharmacy-benefit-type` live, not the drug.
6. **Narrow by tier or pharmacy type** when comparing plans: `GET /Basic?formulary=InsurancePlan/<id>&drug-tier=<system>|<code>` and `&pharmacy-benefit-type=<system>|<code>`.
7. **Read the full record** with `readFormularyBasic` / `readFormularyMedicationKnowledge`.

## Getting it right

- Tier is a property of the *item on a formulary*, never of the drug. The same drug sits at different tiers on different Anthem formularies — answering from step 4 alone will be wrong for most members.
- Filter to `code=formulary-item` on every `Basic` search; `Basic` is a generic FHIR container.
- Prior-authorization and step-therapy flags travel on the FormularyItem too.

## Error handling

Same platform, same defects as the Provider Directory API: a bespoke `{status_code,status,error,error_description}` envelope instead of a FHIR `OperationOutcome`, 403 with an empty body when unauthenticated, no request id, no rate-limit headers, no documented limits. Do not treat a 4xx/5xx here as transient without first checking the token.

## Reversibility

Read-only. Nothing to undo.
