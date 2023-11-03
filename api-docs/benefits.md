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
