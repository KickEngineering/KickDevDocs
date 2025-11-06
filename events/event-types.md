---
description: Request body payloads for Webhook API requests
icon: brackets-curly
---

# Webhook Payloads

## Events

| Event                                                                       | Name                           | Version | Description                                                                                        |
| --------------------------------------------------------------------------- | ------------------------------ | ------- | -------------------------------------------------------------------------------------------------- |
| [Chat Message](event-types.md#chat-message)                                 | `chat.message.sent`            | 1       | Fired when a message has been sent in a stream's chat.                                             |
| [Channel Follow](event-types.md#channel-follow)                             | `channel.followed`             | 1       | Fired when a user follows a channel.                                                               |
| [Channel Subscription Renewal](event-types.md#channel-subscription-renewal) | `channel.subscription.renewal` | 1       | Fired when a user's subscription to a channel is renewed.                                          |
| [Channel Subscription Gifts](event-types.md#channel-subscription-gifts)     | `channel.subscription.gifts`   | 1       | Fired when a user gifts subscriptions to a channel.                                                |
| [Channel Subscription Created](event-types.md#channel-subscription-created) | `channel.subscription.new`     | 1       | Fired when a user first subscribes to a channel.                                                   |
| [Livestream Status Updated](event-types.md#livestream-status-updated)       | `livestream.status.updated`    | 1       | Fired when a stream's status has been updated. For example, a stream could have started or ended   |
| [Livestream Metadata Updated](event-types.md#livestream-metadata-updated)   | `livestream.metadata.updated`  | 1       | Fired when a stream's metadata has been updated. For example, a stream's title could have changed. |
| [Moderation Banned](event-types.md#moderation-banned)                       | `moderation.banned`            | 1       | Fired when a user has been banned from a channel.                                                  |
| [Kicks Gifted](event-types.md#kicks-gifted)                                 | `kicks.gifted`                 | 1       | Fired when a user gifts kicks to a channel.                                                        |

### Chat Message

```json
Headers
- Kick-Event-Type: “chat.message.sent”
- Kick-Event-Version: “1”

{
  "message_id": "unique_message_id_123",
  "replies_to": {
    "message_id": "unique_message_id_456",
    "content": "This is the parent message!",
    "sender": {
      "is_anonymous": false,
      "user_id": 12345,
      "username": "parent_sender_name",
      "is_verified": false,
      "profile_picture": "https://example.com/parent_sender_avatar.jpg",
      "channel_slug": "parent_sender_channel",
      "identity": null // no identity for sender in replies_to at the moment
    },
  },
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null // no identity for broadcasters at the moment
  },
  "sender": {
    "is_anonymous": false,
    "user_id": 987654321,
    "username": "sender_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "sender_channel",
    "identity": {
      "username_color": "#FF5733",
      "badges": [
        {
          "text": "Moderator",
          "type": "moderator",
        },
        {
          "text": "Sub Gifter",
          "type": "sub_gifter",
          "count": 5,
        },
        {
          "text": "Subscriber",
          "type": "subscriber",
          "count": 3,
        }
      ]
    }
  },
  "content": "This is a test message with emotes!",
  "emotes": [
    {
      "emote_id": "12345",
      "positions": [
        { "s": 0, "e": 7 }
      ]
    },
    {
      "emote_id": "67890",
      "positions": [
        { "s": 20, "e": 25 }
      ]
    }
  ],
  "created_at": "2025-01-14T16:08:06Z"
}
```

### Channel Follow

```json
Headers
- Kick-Event-Type: “channel.followed”
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null
  },
  "follower": {
    "is_anonymous": false,
    "user_id": 987654321,
    "username": "follower_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "follower_channel",
    "identity": null
  }
}
```

### Channel Subscription Renewal

```json
Headers
- Kick-Event-Type: “channel.subscription.renewal”
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null
  },
  "subscriber": {
    "is_anonymous": false,
    "user_id": 987654321,
    "username": "subscriber_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "subscriber_channel",
    "identity": null
  },
  "duration": 3,
  "created_at": "2025-01-14T16:08:06Z",
  "expires_at": "2025-02-14T16:08:06Z"
}
```

### Channel Subscription Gifts

```json
Headers
- Kick-Event-Type: “channel.subscription.gifts”
- Kick-Event-Version: “1”

Public Gift Structure
{
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,    
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null
  },
  "gifter": {
    "is_anonymous": false,
    "user_id": 987654321, // null if is_anonymous=true
    "username": "gifter_name", // null if is_anonymous=true
    "is_verified": false, // null if is_anonymous=true
    "profile_picture": "https://example.com/sender_avatar.jpg", // null if is_anonymous=true
    "channel_slug": "gifter_channel", // null if is_anonymous=true
    "identity": null // null if is_anonymous=true
  },
  "giftees": 
  [
    {
      "is_anonymous": false,
      "user_id": 561654654,
      "username": "giftee_name",
      "is_verified": true,
      "profile_picture": "https://example.com/broadcaster_avatar.jpg",
      "channel_slug": "giftee_channel",
      "identity": null
    }
  ],
  "created_at": "2025-01-14T16:08:06Z",
  "expires_at": "2025-02-14T16:08:06Z"
}
```

### Channel Subscription Created

```json
Headers
- Kick-Event-Type: “channel.subscription.new”
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null
  },
  "subscriber": {
    "is_anonymous": false,
    "user_id": 987654321,
    "username": "subscriber_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "subscriber_channel",
    "identity": null
  },
  "duration": 1,
  "created_at": "2025-01-14T16:08:06Z",
  "expires_at": "2025-02-14T16:08:06Z"
}
```

### Livestream Status Updated

#### Stream started

```json
Headers
- Kick-Event-Type: "livestream.status.updated"
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null
  },
  "is_live": true,
  "title": "Stream Title",
  "started_at": "2025-01-01T11:00:00+11:00",
  "ended_at": null
}
```

#### Stream ended

```json
Headers
- Kick-Event-Type: "livestream.status.updated"
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null
  },
  "is_live": false,
  "title": "Stream Title",
  "started_at": "2025-01-01T11:00:00+11:00",
  "ended_at": "2025-01-01T15:00:00+11:00"
}
```

### Livestream Metadata Updated

```json
Headers
- Kick-Event-Type: "livestream.metadata.updated"
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null
  },
  "metadata": {
    "title": "Stream Title",
    "language": "en",
    "has_mature_content": true,
    "category": {
      "id": 123,
      "name": "Category name",
      "thumbnail": "http://example.com/image123"
    }
  }
}
```

### Moderation Banned

```json
Headers
- Kick-Event-Type: "moderation.banned"
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "is_anonymous": false,
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel",
    "identity": null
  },
  "moderator": {
    "is_anonymous": false,
    "user_id": 987654321,
    "username": "moderator_name",
    "is_verified": false,
    "profile_picture": "https://example.com/moderator_avatar.jpg",
    "channel_slug": "moderator_channel",
    "identity": null
  },
  "banned_user": {
    "is_anonymous": false,
    "user_id": 135790135,
    "username": "banned_user_name",
    "is_verified": false,
    "profile_picture": "https://example.com/banned_user_avatar.jpg",
    "channel_slug": "banned_user_channel",
    "identity": null
  },
  "metadata": {
    "reason": "banned reason",
    "created_at": "2025-01-14T16:08:05Z",
    "expires_at": "2025-01-14T16:10:06Z", // null for permanent bans
  }
}
```

### Kicks Gifted

```json
Headers
- Kick-Event-Type: "kicks.gifted"
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel"
  },
  "sender": {
    "user_id": 987654321,
    "username": "gift_sender",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "gift_sender_channel"
  },
  "gift": {
    "amount": 100,
    "name": "Full Send",
    "type": "BASIC",
    "tier": "BASIC",
    "message": "w"
  },
  "created_at": "2025-10-20T04:00:08.634Z"
}
```
