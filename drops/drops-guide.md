---
icon: gift
description: Guide to setting up and running Drops campaigns on Kick for game developers and organizations.
---

# Kick Drops Guide

## Introduction
Kick Drops let you reward viewers for watching streams, driving engagement for Kick, game developers, and viewers alike. Drops campaigns are a win-win-win for everyone involved.

## Who Can Use Drops?
Only organization owners can create and manage Drops campaigns.

## How Drops Work
- Campaigns are created under your organization's dashboard on [dev.kick.com](https://dev.kick.com)
- Each campaign has one or more rewards (created separately)
- Viewers earn rewards by watching participating streams for a set amount of time ("watch to redeem")
- Viewers claim rewards via their Inventory page after linking their Kick and game accounts

## Setting Up a Campaign
1. **Create rewards** (before campaign):
   - Name, image, category, optional external ID
2. **Create campaign**:
   - Name, category, campaign info URL, start/end date
   - Rule: watch to redeem (set minutes required per reward)
   - Grace period: days after campaign ends for late claims
   - Announcement period: days before the start_at
   - Whitelisted channels (for allowlist campaigns) or leave empty for global
   - Attach up to 12 rewards
3. **Test mode**: Optionally run campaign in test mode (only org members can participate/claim)

## Account Linking
- Orgs create OAuth apps and a landing page for account linking
- Recommended flow: connect game account first, then Kick account
- Provide Kick with your connect URL for redirect

## Claiming Rewards
- Users claim via their Inventory page after meeting watch requirements and linking accounts
- Claim button is enabled once both accounts are linked

## Fulfillment
- Kick sends a synchronous webhook POST to your provided URL when a reward is claimed
- Webhook payload includes claim details (see below)
- Respond with 200 OK immediately (idempotent on claim_id)
- Optionally, use the [public API](#public-api-retrieve-claims) to fetch claims

### Webhook Example
```
POST https://your.webhook.endpoint/
```
```json
{
  "claim_id": "string",      // ULID
  "user_id": "integer",      // uint64
  "campaign_id": "string",   // ULID
  "reward_id": "string",     // ULID
  "external_id": "string"    // Optional - external reward reference
}
```
### Expectations
- You must return **200 OK** if processed successfully.
- The webhook is **idempotent**: if `claim_id` already exists, still return 200 OK.

### Security
- All webhook payloads are signed by Kick.
- You must verify the signature to ensure authenticity using the provided public key.
- The public key is available at: https://api.kick.com/public/v1/public-key.

## Public API: Retrieve Claims

Organizations can retrieve claims for a campaign using the Drops Public API. Only OAuth apps associated with an organization can access this endpoint.

**Authorization:** Requires app access tokens from OAuth apps associated with the organization.

**Endpoint:**
```
GET /public/v1/drops/claims
```

#### Query Parameters
| Name            | Type    | Required | Description                                 |
|-----------------|---------|----------|---------------------------------------------|
| campaign_id     | String  | No       | Filter by campaign_id                       |
| limit           | Integer | No       | Number of results (default: 10), Max=1000   |
| cursor          | String  | No       | Pagination cursor – pass claim_id           |
| user_id         | Integer | No       | Filter by user ID                           |
| claim_id        | String  | No       | Filter by claim ID                          |

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
        "created_at": "datetime",
        "updated_at": "datetime"
      }
    ],
    "cursor": "01K0TDDR08Q5ZNWXK92SDH7SDH"
  },
  "message": "OK"
}
```

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


## Campaign Limits & Analytics
- Up to 12 rewards per campaign
- Unlimited campaigns per org
- Campaign overview shows watched minutes, claimed rewards, unique users watched

## Streamer Participation
- Streamers can opt out of global Drops campaigns (disable Drops in their settings)
- If a streamer is whitelisted for a campaign, they cannot opt out of that campaign

## Best Practices
- Double-check campaign start/end times
- Respond to webhook calls with 200 OK before timeout
- Use claim_id as an idempotency key

## FAQ / Troubleshooting
- For support, email developers@kick.com

## References
- [Organization Management Public API](../organizations/organization-management.md#api-endpoints)
- [Webhook Security](../events/webhook-security.md)
