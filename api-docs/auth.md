# Authorization

All API requests require the use of an Authenticated API key which should be provided in the header.

## Get Authorized User

Verify that the request includes a valid user.

```
GET /apip/auth/v2/token
```

## Request URL
```http
--header 'x-authenticated-api-key: {api_key}'
```

| Parameter | Type | Required |
| :--- | :--- | :--- |
| `x-authenticated-api-key` | `string`| `true` |

## Responses

| Status Code | Meaning | Description | 
| :--- | :--- |:--- |
| 200 | `OK` | `Success` |
| 401 | `UNAUTHORIZED` | `Api Key is missing or invalid`|
| 500 | `INTERNAL SERVER ERROR` | `Something went wrong` |


