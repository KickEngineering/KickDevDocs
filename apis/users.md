---
icon: user
---

# Users

User APIs allow apps to interact with user information. Scopes will vary and sensitive data will be available to User Access Tokens with the required scopes.

{% openapi-operation spec="kick-dev-api" path="/public/v1/users" method="get" %}
[OpenAPI kick-dev-api](https://api.kick.com/swagger/doc.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="kick-dev-api" path="/public/v1/token/introspect" method="post" %}
[OpenAPI kick-dev-api](https://api.kick.com/swagger/doc.yaml)
{% endopenapi-operation %}
