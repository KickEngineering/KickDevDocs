---
description: The Kick OAuth Flow.
icon: unlock-keyhole
---

# OAuth 2.1

## Token Types

There are 2 types of tokens that are available for the Kick Dev API: App Access Token and User Access Token. Each token has a unique OAuth flow to generate the token and are generally used in different scenarios.

### App Access Token

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

| Name                    | Required            | Type   | Description                                                                                                                                                                                  |
| ----------------------- | ------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `client_id`             | Yes                 | string | Your application's client ID                                                                                                                                                                 |
| `response_type`         | Yes                 | string | `code`                                                                                                                                                                                       |
| `redirect_uri`          | Yes                 | uri    | The URI to redirect users to after authorization. If your redirect URI host is 127.0.0.1, see this [workaround](generating-tokens-oauth2-flow.md#workaround-for-127.0.0.1-host-redirect-uri) |
| `state`                 | Yes (at the moment) | string | A random string to maintain state between the request and callback                                                                                                                           |
| `scope`                 | Yes                 | string | Scopes for request                                                                                                                                                                           |
| `code_challenge`        | Yes                 | string | OAuth code challenge                                                                                                                                                                         |
| `code_challenge_method` | Yes                 | string | `S256`                                                                                                                                                                                       |

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

**Headers**

| Name         | Required | Type   | Value                             |
| ------------ | -------- | ------ | --------------------------------- |
| Content-Type | true     | string | application/x-www-form-urlencoded |

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
  "expires_in": "",
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

Headers: 
Content-Type: application/x-www-form-urlencoded

Body:
{
    grant_type=authorization_code
    client_id=<client_id>
    client_secret=<client_secret>
    redirect_uri=<redirect_uri>
    code_verifier=<code_verifier>
    code=<CODE>
}
```

#### Example Response

```
{
  "access_token": "",
  "token_type": "",
  "refresh_token": "",
  "expires_in": "",
  "scope": ""
}
```

## App Access Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/token`

Uses a client\_id and client\_secret to generate an app access token which can be used to obtain public data on Kick.

**Headers**

| Name         | Required | Type   | Value                             |
| ------------ | -------- | ------ | --------------------------------- |
| Content-Type | true     | string | application/x-www-form-urlencoded |

**Body**

| Name            | Required | Type   | Description                      |
| --------------- | -------- | ------ | -------------------------------- |
| `client_id`     | Yes      | string | Your application's client ID     |
| `client_secret` | Yes      | string | Your application's client secret |
| `grant_type`    | Yes      | string | `client_credentials`             |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "access_token": "",
  "token_type": "",
  "expires_in": "",
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

Headers:
Content-Type: application/x-www-form-urlencoded

Body:
{
    grant_type=client_credentials
    client_id=<client_id>
    client_secret=<client_secret>
}
```

#### Example Response

```
{
  "access_token": "",
  "expires_in": "",
  "token_type": "",
}
```

## Refresh Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/token`

Pass in refresh token and refresh both access and refresh codes.

**Headers**

| Name         | Required | Type   | Value                             |
| ------------ | -------- | ------ | --------------------------------- |
| Content-Type | true     | string | application/x-www-form-urlencoded |

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
  "expires_in": "",
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

Headers: 
Content-Type: application/x-www-form-urlencoded

Body:
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
  "expires_in": "",
  "scope": ""
}
```

## Revoke Token Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/revoke`

Pass in a token to revoke access to that token.

**Headers**

| Name         | Required | Type   | Value                             |
| ------------ | -------- | ------ | --------------------------------- |
| Content-Type | true     | string | application/x-www-form-urlencoded |

**Query**

| Name              | Required | Type   | Description                       |
| ----------------- | -------- | ------ | --------------------------------- |
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

Headers: 
Content-Type: application/x-www-form-urlencoded
```

#### Example Response

```
OK
```

## Token introspect Endpoint

<mark style="color:green;">`POST`</mark> `/oauth/token/introspect`

Checks if an access token is valid and returns information about it.

## Notes

#### Workaround for 127.0.0.1 Host Redirect URI

If developing your authorization to only happen on an app running locally, we recommend using `localhost` as your redirect URI/callback URL e.g. `http://localhost/auth/callback`. But if you're unable to change your callback URL to use `localhost`  instead of `127.0.0.1`, you will need to perform a workaround due to a [bug in our frontend framework, NextJS](https://github.com/vercel/next.js/issues/79182).

NextJS will change the first occurrence of `127.0.0.1` in a URL to `localhost`, and as the redirect URI needs to match exactly to your callback URL specified in your app settings, this will cause authorization to fail.

When performing the Authorize GET request, you will need to add a sacrificial query parameter that sits before the `redirect_uri` parameter that contains "127.0.0.1". This parameter can be named anything but from testing it's best to call it `redirect`.  This will cause NextJS to change that first parameter and leave the second parameter untouched. See an example request below:

```
GET
https://id.kick.com/oauth/authorize?
    response_type=code&
    client_id=<your_client_id>&
    redirect=127.0.0.1
    redirect_uri=<http://127.0.0.1/callback>&
    scope=<scopes>&
    code_challenge=<code_challenge>&
    code_challenge_method=S256&
    state=<random_value>
```
