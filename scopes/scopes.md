---
icon: telescope
---

# Scopes

Scopes enable an app to request a level of access to Kick and define the specific actions an application can perform.

These scopes are for apps using OAuth 2.1 authorization code grants for authorization. The title is displayed to the user on the consent screen during the authorization flow.

| Scope              | Summary             | Description                                                                        |
|--------------------|---------------------|------------------------------------------------------------------------------------|
| `user:read`        | Read user info      | View user information in Kick including username, streamer ID, etc.                |
| `channel:read`     | Read channel info   | View channel information in Kick including channel description, category, etc.     |
| `channel:write`    | Update channel info | Update livestream metadata for a channel based on the channel ID                   |
| `chat:write`       | Write to chat       | Send chat messages and allow chat bots to post in your chat                        |
| `streamkey:read`   | Read stream key     | Read a user's stream URL and stream key                                            |
| `events:subscribe` | Subscribe to events | Subscribe to all channel events on Kick e.g. chat messages, follows, subscriptions |
