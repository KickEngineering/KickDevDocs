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

User Access Tokens are generated through the Authorization Grant Flow. These token give an application access to the users information based on the scopes the App has requested. This give more privileged information and access to an App and will often allow an App to act on the users behalf.



## Kick OAuth Server

The Kick OAuth server is hosted on id.kick.com.

Information from creating an App will be required in these endpoints. Checkout the Kick Apps Setup page to get the information for your App.

Available endpoints are below.



{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/oauth/authorize" method="get" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/oauth/token" method="post" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}

{% swagger src="https://api.kick.com/swagger/v1/doc.json" path="/oauth/revoke" method="post" %}
[https://api.kick.com/swagger/v1/doc.json](https://api.kick.com/swagger/v1/doc.json)
{% endswagger %}
