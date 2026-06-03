---
icon: rectangle-api
---

# Public API

Organizations can retrieve and update reward claims for their Drops campaigns using the Public API. Only OAuth apps associated with an organization can access these endpoints.

**Authorization:** Requires app access tokens from OAuth apps associated with the organization. See OAuth 2.1 for token generation.

### Retrieve Claims

**Endpoint:**

```
GET /public/v1/drops/claims
```

#### Query Parameters

| Name             | Type    | Required | Description                               |
| ---------------- | ------- | -------- | ----------------------------------------- |
| campaign\_id     | String  | No       | Filter by campaign\_id                    |
| limit            | Integer | No       | Number of results (default: 10), Max=1000 |
| cursor           | String  | No       | Pagination cursor – pass claim\_id        |
| user\_id         | Integer | No       | Filter by user ID                         |
| claim\_id        | String  | No       | Filter by claim ID                        |
| external\_status | String  | No       | Filter by external status                 |

#### Examples

```
GET /public/v1/drops/claims?campaign_id=01JAXK8N4QWRTY5PM7ZEBVJDS8S&limit=10&cursor=01K0TDDR08Q5ZNWXK92VRXD7GW&user_id=1234
GET /public/v1/drops/claims?claim_id=01JAXK8N4QWRTY5PM7ZEBVGH2S
```

#### Response: 200 OK

```json
{
  "data": {
    "claims": [
      {
        "claim_id": "string",
        "user_id": "integer",
        "campaign_id": "string",
        "reward_id": "string",
        "external_id": "string",
        "external_status": "string",
        "created_at": "datetime",
        "updated_at": "datetime"
      }
    ],
    "cursor": "01K0TDDR08Q5ZNWXK92SDH7SDH"
  },
  "message": "OK"
}
```

The `external_status` field is omitted when not set or null.

#### Error Responses

**401 Unauthorized**

```json
{
  "data": null,
  "message": "Unauthorized"
}
```

**500 Internal Server Error**

```json
{
  "data": null,
  "message": "Internal server error"
}
```

### Update Claims

Update `external_status` for one or more claims. Each item in the request must include only `claim_id` and `external_status`. A single request supports up to **100** claims.

**Endpoint:**

```
PATCH /public/v1/drops/claims
```

#### Request Body

| Field  | Type  | Required | Description                     |
| ------ | ----- | -------- | ------------------------------- |
| claims | Array | Yes      | List of claim updates (max 100) |

Each object in `claims`:

| Field            | Type   | Required | Description                           |
| ---------------- | ------ | -------- | ------------------------------------- |
| claim\_id        | String | Yes      | Claim ULID to update                  |
| external\_status | String | Yes      | Your fulfillment status for the claim |

#### Example

```
PATCH /public/v1/drops/claims
```

```json
{
  "claims": [
    {
      "claim_id": "01KAAFHJ2PNXS48NG8XXPGWKCZ",
      "external_status": "processed"
    },
    {
      "claim_id": "01KAAFHJ2PNXS48NG8XXPGWKCA",
      "external_status": "acknowledged"
    }
  ]
}
```

#### Response: 204 No Content

On success, the API returns **204 No Content** with an empty body.

#### Error Responses

**401 Unauthorized**

```json
{
  "data": null,
  "message": "Unauthorized"
}
```

**500 Internal Server Error**

```json
{
  "data": null,
  "message": "Internal server error"
}
```
