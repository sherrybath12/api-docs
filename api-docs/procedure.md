---
layout: default
title: Procedures
permalink: /procedure/
---

# Medical Procedures

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