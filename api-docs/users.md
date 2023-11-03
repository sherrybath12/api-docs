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
