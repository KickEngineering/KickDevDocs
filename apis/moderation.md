---
icon: icons
---

# Moderation

Moderation APIs enable you to restrict user participation in chat rooms through temporary timeouts or permanent bans, as well as reverse these actions by removing timeouts or unbanning specific users.

{% openapi-operation spec="kick-dev-api" path="/public/v1/moderation/bans" method="post" %}
[OpenAPI kick-dev-api](https://api.kick.com/swagger/doc.yaml)
{% endopenapi-operation %}

{% openapi-operation spec="kick-dev-api" path="/public/v1/moderation/bans" method="delete" %}
[OpenAPI kick-dev-api](https://api.kick.com/swagger/doc.yaml)
{% endopenapi-operation %}
