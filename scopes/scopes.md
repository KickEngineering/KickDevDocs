---
icon: telescope
---

# Scopes

Scopes enable an app to request a level of access to Kick and define the specific actions an application can perform.

These scopes are for apps using OAuth 2.1 authorization code grants for authorization. The title is displayed to the user on the consent screen during the authorization flow.

| Scope                            | Description                                                                        |
|----------------------------------|------------------------------------------------------------------------------------|
| `user:read`                      | View user information in Kick including username, streamer ID, etc.                |
| `channel:read`                   | View channel information in Kick including channel description, category, etc.     |
| `channel:write`                  | Update livestream metadata for a channel based on the channel ID                   |
| `chat:write`                     | Send chat messages and allow chat bots to post in your chat                        |
| `streamkey:read`                 | Read a user's stream URL and stream key                                            |
| `events:subscribe`               | Subscribe to all channel events on Kick e.g. chat messages, follows, subscriptions |
| `moderation:ban`                 | Execute ban/unban actions on users                                                 |
| `moderation:chat_message:manage` | Execute moderation actions on chat messages                                        |
| `kicks:read`                     | View KICKs related information in Kick e.g leaderboards, etc.                      |
