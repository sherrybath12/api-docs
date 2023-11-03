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