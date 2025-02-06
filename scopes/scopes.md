---
icon: telescope
---

# Scopes

Scopes enable an app to request a level of access to Kick and define the specific actions applications can perform.

These scopes are for apps using OAuth 2.1 authorization code grants for authorization. The title is displayed to the user on the consent screen during the authorization flow.

| Scope | Summary | Description |
|-------|---------|-------------|
| `user:read` | Read user info | View user information in Kick including username, StreamerID, etc. |
| `channel:read` | Read channel info | View channel information in Kick including Channel description, category, etc |
| `channel:write` | Update channel info | Update livestream metadata for a channel based on the channel ID. |
| `streamkey:read` | Read streamkey | Read a user's StreamURL and Stream key |
| `events:subscribe` | Subscribe to events | Subscribe to all channel events like chat messages, follows, subscribe and gifts on Kick |
