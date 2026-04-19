# Anthem (anthem)
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
