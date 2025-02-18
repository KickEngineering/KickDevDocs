---
icon: unlock-keyhole
description: The Kick OAuth Flow.
---

# OAuth 2.1

## Token Types

There are 2 types of tokens that are available for the Kick Dev API: App Access Token and User Access Token. Each token has a unique OAuth flow to generate the token and are generally used in different scenarios.

### App Access Token (Not yet implemented)

App Access Tokens are generated through the Client Credentials flow. These server-to-server API tokens are the most basic form of token for accessing the API. They can access publicly available data and are ideal for use when user login is not required.

### User Access Token

User Access Tokens are generated through the Authorization Grant flow. These tokens give an application access to the user's information based on the scopes the App has requested. This gives more privileged information and access to an App and will often allow an App to act on the user's behalf.

## Kick OAuth Server

The Kick OAuth server is hosted on id.kick.com.

Information from creating an App will be required in these endpoints. Checkout the Kick Apps Setup page to get the information for your App.

{% hint style="info" %}
The host URL for our OAuth server is different from our API server.

The host URL is: _https://id.kick.com_
{% endhint %}

## Authorization Endpoint

<mark style="color:green;">`GET`</mark> `/oauth/authorize`

Directs the user to the authorization server where they can log in and approve the application's access request.

**Query Parameters**

| Name                    | Required            | Type   | Description                                                        |
| ----------------------- | ------------------- | ------ | ------------------------------------------------------------------ |
| `client_id`             | Yes                 | string | Your application's client ID                                       |
| `response_type`         | Yes                 | string | `code`                                                             |
| `redirect_uri`          | Yes                 | uri    | The URI to redirect users to after authorization                   |
| `state`                 | Yes (at the moment) | string | A random string to maintain state between the request and callback |
| `scope`                 | Yes                 | string | Scopes for request                                                 |
| `code_challenge`        | Yes                 | string | OAuth code challenge                                               |
| `code_challenge_method` | Yes                 | string | `S256`                                                             |

**Response**

{% tabs %}
{% tab title="200" %}
```json
https://yourapp.com/callback?code=<code>&state=random-state
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

#### Example Request

{% code overflow="wrap" %}
```uri
GET
https://id.kick.com/oauth/authorize?
    response_type=code&
    client_id=<your_client_id>&
    redirect_uri=<https://yourapp.com/callback>&
    scope=<scopes>&
    code_challenge=<code_challenge>&
    code_challenge_method=S256&
    state=<random_value>
```
{% endcode %}

#### Example Response

```uri
https://yourapp.com/callback?code=<code>&state=random-state
```

## Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/token`

Exchanges the code for a valid access token and a refresh token that can be used to make authorised requests to Kick's API.

**Body**

| Name            | Required | Type   | Description                                      |
| --------------- | -------- | ------ | ------------------------------------------------ |
| `code`          | Yes      | string | Code received during the Authorization Flow      |
| `client_id`     | Yes      | string | Your application's client ID                     |
| `client_secret` | Yes      | string | Your application's client secret                 |
| `redirect_uri`  | Yes      | string | The URI to redirect users to after authorization |
| `grant_type`    | Yes      | string | `authorization_code`                             |
| `code_verifier` | Yes      | string | To verify PKCE challenge code created            |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expiry": "",
  "scope": ""
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

#### Example Request

<pre><code>POST
https://id.kick.com/oauth/token

Request Form Body:
{
    grant_type=authorization_code
    client_id=&#x3C;client_id>
    client_secret=&#x3C;client_secret>
    redirect_uri=&#x3C;redirect_uri>
<strong>    code_verifier=&#x3C;code_verifier>
</strong>    code=&#x3C;CODE>
}
</code></pre>

#### Example Response

```
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expiry": "",
  "scope": ""
}
```

## Refresh Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/token`

Pass in refresh token and refresh both access and refresh codes.

**Body**

| Name            | Required | Type   | Description                                 |
| --------------- | -------- | ------ | ------------------------------------------- |
| `refresh_token` | Yes      | string | Code received during the Authorization Flow |
| `client_id`     | Yes      | string | Your application's client ID                |
| `client_secret` | Yes      | string | Your application's client secret            |
| `grant_type`    | Yes      | string | `refresh_token`                             |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expiry": "",
  "scope": ""
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

#### Example Request

```
POST
https://id.kick.com/oauth/token

Request Form Body:
{
    grant_type=refresh_token
    client_id=<client_id>
    client_secret=<client_secret>
    refresh_token=<refresh_token>
}
```

#### Example Response

```
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expiry": "",
  "scope": ""
}
```

## Revoke Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/revoke`

Pass in a token to revoke access to that token.

**Query**

| Name              | Required | Type   | Description                       |
|-------------------|----------|--------|-----------------------------------|
| `token`           | Yes      | string | The token to be revoked           |
| `token_hint_type` | No       | string | `access_token` or `refresh_token` |

**Response**

{% tabs %}
{% tab title="200" %}
OK
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

#### Example Request

```
POST
https://id.kick.com/oauth/revoke?token=<your_token>&token_hint_type=<token_type>
```

#### Example Response

```
OK
```
