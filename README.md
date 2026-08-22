# Anthem (anthem)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Anthem, Inc. (now operating as Elevance Health) is one of the largest health benefits companies in the United States, serving members through affiliated Blue Cross and Blue Shield health plans. Under CMS interoperability rules (CMS-9115-F), Anthem offers FHIR-based Patient Access, Provider Directory, and Drug Formulary APIs.

**URL:** [Visit APIs.json](https://raw.githubusercontent.com/api-evangelist/anthem/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Blue Cross Blue Shield, FHIR, Health Benefits, Health Insurance, Healthcare, Interoperability

## Timestamps

- **Created:** 2026-03-23
- **Modified:** 2026-04-19

## APIs

### Anthem Patient Access API
The Anthem Patient Access API provides members access to their personal health data via HL7 FHIR R4, as required by the CMS Interoperability and Patient Access Final Rule (CMS-9115-F). Implements SMART on FHIR for authorization.

**Human URL:** [https://www.anthem.com/developer/](https://www.anthem.com/developer/)

#### Tags:

 - FHIR, Health Insurance, Healthcare, Interoperability, Patient Access, SMART on FHIR

#### Properties

- [Documentation](https://www.anthem.com/developer/)
- [Authentication](https://www.anthem.com/developer/authentication/)

### Anthem Provider Directory API
The Anthem Provider Directory API provides public access to provider directory information via HL7 FHIR R4, enabling search for in-network providers, facilities, and insurance plans.

**Human URL:** [https://www.anthem.com/developer/](https://www.anthem.com/developer/)

#### Tags:

 - FHIR, Healthcare, Interoperability, Provider Directory

#### Properties

- [Documentation](https://www.anthem.com/developer/)

### Anthem Drug Formulary API
The Anthem Drug Formulary API provides access to prescription drug formulary data via HL7 FHIR R4, including covered medications, cost tiers, prior authorization requirements, and quantity limits.

**Human URL:** [https://www.anthem.com/developer/](https://www.anthem.com/developer/)

#### Tags:

 - Drug Formulary, FHIR, Healthcare, Pharmacy

#### Properties

- [Documentation](https://www.anthem.com/developer/)

## Common Properties

- [Portal](https://www.anthem.com)
- [SignUp](https://www.anthem.com/developer/register/)
- [TermsOfService](https://www.anthem.com/legal/terms-and-conditions/)
- [PrivacyPolicy](https://www.anthem.com/legal/privacy-policy/)

## Features

| Name | Description |
|------|-------------|
| FHIR R4 Compliance | All Anthem interoperability APIs implement HL7 FHIR Release 4 standards with USCDI-conformant resource profiles. |
| SMART on FHIR Authorization | Patient Access APIs use SMART on FHIR for secure OAuth2-based authorization allowing members to grant third-party app access. |
| Claims and Clinical Data | Members can access their claims history, clinical notes, lab results, immunizations, and medication history. |
| Provider Directory Search | Search for in-network providers by specialty, location, name, and plan type. |

## Use Cases

| Name | Description |
|------|-------------|
| Member Health Apps | Enable member-authorized third-party health apps to aggregate claims, clinical, and formulary data from Anthem plans. |
| Care Coordination | Allow care coordinators and providers to access member health history with member authorization. |
| Provider Lookup | Enable applications to search Anthem's provider directory for in-network physicians, hospitals, and specialists. |

## Integrations

| Name | Description |
|------|-------------|
| CommonWell Health Alliance | Anthem participates in the CommonWell Health Alliance for cross-organizational clinical data exchange. |
| Carequality Framework | Anthem participates in the Carequality interoperability framework for health data exchange between networks. |

## Maintainers

**FN:** Kin Lane

**Email:** info@apievangelist.com
