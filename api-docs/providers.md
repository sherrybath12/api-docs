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
