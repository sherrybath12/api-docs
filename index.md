---
layout: default
title: API Documentation using Markdown
permalink: /
---

# Introduction

This section is intended to give the reader an overview of how to deliver a common search experience, medical cost and out of pocket cost lookup, as well as detailed provider information. This overview covers inputs and outputs for each endpoint, and relationships between the endpoints. For further detail on each endpoint, navigate to that specific endpoint's in-depth page.

## Table of contents

* [Authorization](#authorization)
* [Users](#users)
* [Plan Benefits](#plan-benefits)
* [Providers](#providers)
* [RXBrands](#rxbrands)
* [Medical Procedures](#medical-procedures)
* [Search](#search)


## Data Model

This section depicts the major model classes.

![alt text](/api-docs/images/model.png)

# Authorization

All API requests require the use of an Authenticated API key which should be provided in the header.

## Get Authorized User

Verify that the request includes a valid user.
```
GET /apip/auth/v2/token
```

## Request URL
```http
header 'x-authenticated-api-key: {api_key}'
```

| Parameter | Type | Required |
| :--- | :--- | :--- |
| `x-authenticated-api-key` | `string`| `true` |

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | OK | Success |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

# Users

The Users endpoints allow for retrieval and update of registered members including dependents.

## Get User

- Get information on a member resource with a given user key (external id).
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /members
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/members \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
  "id": "",
  "type": "members",
  "name": "John Doe",
  "gender": "F",
  "addresses": [
    {
      "id": "156",
      "type": "member_addresses",
      "label": null,
      "address1": "Death Star #5",
      "address2": "8th Floor Sunnyside",
      "city": "Nashville",
      "state": "TN",
      "zipcode": "37205",
      "latitude": 34.921356,
      "longitude": -85.142191,
      "default": true
    }
  ],
  "emails": [
    {
      "id": "834",
      "type": "member_emails",
      "label": null,
      "email": "temp_email@gmail.com",
      "default": true
    }
  ],
  "preferences": [
    {
      "id": "459",
      "type": "member_preferences",
      "medDistance": 25,
      "rxDistance": 25,
      "notifyWaysToSaveEmail": true,
      "notifyWaysToSaveSms": false,
      "targetedAlertEmail": true,
      "medMinSavingAmount": 75,
      "rxMinSavingAmount": 75
    }
  ],
  "orgUnitId": "482",
  "firstName": "",
  "lastName": "",
  "birthDate": "1993-06-30",
  "phoneNumber": "5556667777",
  "profileCompleted": true,
  "termsAccepted": true,
  "role": "primary"
}
```

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |


## Get Dependents

- Get dependent members for a given user key (external id).
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /members/dependents
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/members/dependents \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
  "dependent_list": [
    {
      "id": "3149819",
      "type": "members",
      "gender": "M",
      "age": "43",
      "orgUnitId": "420",
      "firstName": "Jack",
      "lastName": "Sonofjohn",
      "birthDate": "1975-05-18",
      "email": "bananapancakes@gmail.com.com",
      "hipaaStatus": "pending_approval",
      "isUnderage": false
    }
  ],
  "age_limit": "25"
}
```

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

# Plan Benefits

Plan Benefits returns benefit data for individual and family.

## Get Plan Benefits

- Get plan benefits data for single user or family. Returns current deductible amount, maximum out of pocket costs, and coinsurance.
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /plan_benfits
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/plan_benefits \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
  "memberId": {
    "userKey": "E123456789",
    "individual": {
      "deductible": 1000,
      "max_oop": 12000,
      "coinsurance": 0.5,
      "remainder": {
        "deductible": 20,
        "max_oop": 8000
      }
    },
    "family": {
      "coinsurance": 0.5,
      "deductible": 8000,
      "max_oop": 12000,
      "remainder": {
        "deductible": 1000,
        "max_oop": 8000
      }
    }
  }
}
```

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |


---
layout: default
title: Providers
permalink: /providers/
---

# Providers

The Providers endpoints provide routes for finding information on providers.

## Get_Provider

- Gets information for a specific provider resource.
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /providers/{provider_id}
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/providers/7794 \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `provider_id` | `path` | `string`| `true` |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
  "id": "7794",
  "type": "providers",
  "suffix": "",
  "name": "Marshall Tufts Schreeder",
  "gender": "M",
  "pharmacyChainId": null,
  "providerType": "Physician",
  "firstName": "Marshall Tufts Schreeder",
  "lastName": "",
  "facilityName": "Marshall Tufts Schreeder",
  "phoneNumber": "2565516546",
  "website": "www.drschreeder.yourmd.com",
  "fax": "2565342605",
  "providerGroupName": "Medical Oncology",
  "summaryQualityRating": 0,
  "maxSummaryQualityRating": 100,
  "qualitySummary": {
    "ratingSummary": {
      "id": 2000,
      "type": "provider_summary_rating",
      "score": "4",
      "display_type": "Circles"
    },
    "reviewSummary": {
      "id": 2000,
      "type": "provider_summary_rating",
      "score": "4",
      "count": 47,
      "display_type": "Circles"
    }
  },
  "acceptingNewPatients": false,
  "description": null,
  "designationLabels": [
    null
  ],
  "designationLogos": [
    null
  ],
  "spokenLanguages": [
    "English"
  ],
  "networks": [
    null
  ],
  "boardCertifications": [
    null
  ],
  "specialties": [
    "Internal Medicine"
  ],
  "affiliations": [
    {
      "description": "SOUTHWEST WASHINGTON MEDICAL CENTER",
      "affiliation_type": "Hospital"
    }
  ]
}
```

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

# Rx Brand

The RX Brands endpoints provide routes for finding information about various prescriptions, dosages, and costs

## Get Rx Brand

Get information about a specific RX brand.

```
GET /rx_brands/{rx_brand_id}
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/rx_brands/11813 \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `rx_brand_id` | `path` | `integer`| `true` |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
  "id": "11813",
  "type": "rx_brands",
  "maintenence": false,
  "generic": false,
  "name": "NEOSPORIN",
  "ingredient": "NEOMYCIN/BACITRACIN/POLYMYXIN - TOPICAL (nee-oh-MY-sin/paw-lee-MIX-in/bass-eh-TRAY-sin)",
  "alternatives": [
    null
  ],
  "sideEffects": "SIDE EFFECTS:  This medication is usually well tolerated.    Rarely, use of this medication may result in other types of skin infections (e.g., fungal or other bacterial infections).  Call your doctor for medical advice about side effects. You may report side effects to FDA at 1-800-FDA-1088.",
  "commonUses": "USES:  This medication is used to prevent and treat minor skin infections caused by small cuts, scrapes, or burns. It is available without a prescription for self-medication. Do not use this product over large areas of the body. Ask your doctor first before using this product for serious skin injuries or infections.",
  "rxBrandDosages": [
    {
      "id": "5718",
      "type": "rx_brand_dosages",
      "strength": "3.5 mg-400 unit-5,000 unit/gram",
      "form": "OINT PACK",
      "alternatives": [
        null
      ],
      "frequencies": [
        {
          "name": "episodic",
          "label": "episodic",
          "default": false
        }
      ],
      "quantities": [
        {
          "quantity": 28.3,
          "default": false
        }
      ]
    }
  ]
}
```

## Responses

The following status codes in its API:

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

## Get_RX_Expected_Cost

- Get nearby Rx costs for a given Rx common cost ID.
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /costs/rx/{rx_cost_id}
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/costs/rx/rx_chain_costs-648967 \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `rx_cost_id` | `path` | `integer`| `true` |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
[
  {
    "id": "L-rx_chain_costs-648967-8225685-30",
    "type": "rx_expected_costs",
    "preferred": false,
    "provider": {
      "id": "746495",
      "type": "providers",
      "name": "WAL-MART",
      "npi": "1295046977",
      "locationAgnostic": false,
      "serviceLocation": {
        "id": "994732",
        "type": "provider_addresses",
        "address1": "7044 CHARLOTTE PIKE",
        "address2": null,
        "city": "NASHVILLE",
        "state": "TN",
        "zipcode": "37209",
        "latitude": 36.131348,
        "longitude": -86.90706,
        "distance": 0.7,
        "externalId": null
      },
      "qualityRating": {
        "score": 78,
        "max_score": 100
      },
      "qualitySummary": {
        "ratingSummary": null,
        "reviewSummary": null
      }
    },
    "commonCostId": "rx_chain_costs-648967",
    "costType": "rx_chain_cost",
    "expectedCost": 2.6,
    "dispensingFee": 1.1,
    "totalUnits": 30,
    "extendedDaySupply": false,
    "pharmacyChainId": "7",
    "otherProviders": [
      "6974224"
    ]
  }
]
```

## Responses

The following status codes in its API:

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

## Response Schema

| Name | Type | 
| :--- | :--- |
| `array` | `[RXExpectedCost]` |

## Get_RX_Expected_Cost (MOP)

- Get nearby Rx costs for a given Rx common cost ID.
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /costs/rx/{rx_cost_id}/mop
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/costs/rx/L-rx_chain_costs-100-200-30/mop \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `rx_cost_id` | `path` | `integer`| `true` |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
  "id": "L-rx_chain_costs-100-200-30",
  "type": "rx_expected_costs",
  "expectedCost": 70,
  "memberCost": 14,
  "planCost": 56,
  "effectiveDate": "2015-11-04"
}
```

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

## Response Schema

| Name | Type | 
| :--- | :--- |
| `array` | `[RXExpectedCost]` |

# Procedures

The Medical Procedure endpoints provide routes for finding information about various services and costs.

## Get_Procedure

- Get information on a particular procedure.
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /procedure/{procedure_id}
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/provider_service_groups/string \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `procedure_id` | `path` | `string`| `false` |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
  "id": "30",
  "type": "provider_service_group",
  "name": "Mental health office visit - 75-80 minutes",
  "description": "A mental health office visit (often called psychotherapy)  refers to an interaction with a mental health provider to discuss a patient's current mental health concerns. The problems addressed in these visits are psychological in nature and vary from patient to patient.",
  "educationalInfo": ""
}
```

## Responses

The following status codes in its API:

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

## Get_Med_Expected_Cost

- Get information about a specific procedure cost.
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /costs/med/{med_cost_id}
```

## Request URL
```http
curl --request GET \
  --url https://dummy.example.com/api/v1/costs/med/L-41568205-2973616- \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `med_cost_id` | `path` | `string`| `true` |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
  "id": "L-41568205-2973616-",
  "type": "med_expected_costs",
  "preferred": true,
  "expectedCost": 49.09,
  "specialtyName": "Psychologist",
  "provider": {
    "id": "746495",
    "type": "providers",
    "name": "WAL-MART",
    "npi": "1295046977",
    "locationAgnostic": false,
    "serviceLocation": {
      "id": "994732",
      "type": "provider_addresses",
      "address1": "7044 CHARLOTTE PIKE",
      "address2": null,
      "city": "NASHVILLE",
      "state": "TN",
      "zipcode": "37209",
      "latitude": 36.131348,
      "longitude": -86.90706,
      "distance": 0.7,
      "externalId": null
    },
    "qualityRating": {
      "score": 78,
      "max_score": 100
    },
    "qualitySummary": {
      "ratingSummary": null,
      "reviewSummary": null
    }
  },
  "secondaryProvider": null,
  "details": [
    {
      "id": "48151623",
      "cost": 815.42,
      "specialtyName": "Psychologist",
      "networkIdentifier": null,
      "providerId": "6986928",
      "serviceType": {
        "id": "9051",
        "type": "provider_service_codes",
        "description": "Existing Patient Office Visit (15 min)"
      },
      "serviceTypeCode": {
        "description": "Professional (Physician) Visit-Office",
        "codeValue": "98"
      }
    }
  ]
}
```

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

# Search

The Search endpoints allow for geographic searching for prescriptions, providers, and services.

## Search_Procedures

- Get information on a particular procedure.
- In addition the endpoint requires the [Authorization](auth.md) `x-authenticated-api-key` in the header.

```
GET /search/procedures
```

## Request URL
```http
curl --request GET \
  --url 'https://dummy.example.com/api/v1/search/procedures?long=-94.476097&lat=39.233299&page=0&query=knee' \
  --header 'accept: application/json' \
  --header 'x-authenticated-api-key: API_KEY' \
  --header 'x-user-key: x2319'
```

| Parameter | In | Type | Required |
| :--- | :--- | :--- |:--- |
| `query` | `query` | `string`| `true` |
| `page` | `query` | `integer`| `true` |
| `lat` | `query` | `number`| `true` |
| `long` | `query` | `number`| `true` |
| `x-authenticated-api-key` | `header` | `string`| `true` |
| `x-user-key` | `header` | `string`| `true` |

## Successful Response

```javascript
{
{
  "indexName": "providerservicegroups",
  "hits": [
    {
      "id": 437,
      "extraTerms": "X-ray and imaging, x-ray & imaging, imaging, surgery/surgical procedures, surgery",
      "name": "Diagnostic Knee Arthroscopy",
      "description": "Knee arthroscopy is surgery that is done by making small cuts on your knee and looking inside using a tiny camera."
    }
  ],
  "query": "knee",
  "totalHits": 6,
  "totalPages": 0
}
}
```

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |

## ResponseSchema

| Name | Type |
| :--- | :--- |
| `indexName` | `string` | `Success` |
| `hits` | `[SearchedProcedures]` |
