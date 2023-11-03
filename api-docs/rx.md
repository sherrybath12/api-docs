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