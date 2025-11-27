---
description: Request body payloads for Webhook API requests
icon: brackets-curly
---

# Webhook Payloads

## Events

<table data-full-width="true"><thead><tr><th>Event</th><th>Name</th><th>Version</th><th>Description</th></tr></thead><tbody><tr><td><a href="event-types.md#chat-message">Chat Message</a></td><td><code>chat.message.sent</code></td><td>1</td><td>Fired when a message has been sent in a stream's chat.</td></tr><tr><td><a href="event-types.md#channel-follow">Channel Follow</a></td><td><code>channel.followed</code></td><td>1</td><td>Fired when a user follows a channel.</td></tr><tr><td><a href="event-types.md#channel-subscription-renewal">Channel Subscription Renewal</a></td><td><code>channel.subscription.renewal</code></td><td>1</td><td>Fired when a user's subscription to a channel is renewed.</td></tr><tr><td><a href="event-types.md#channel-subscription-gifts">Channel Subscription Gifts</a></td><td><code>channel.subscription.gifts</code></td><td>1</td><td>Fired when a user gifts subscriptions to a channel.</td></tr><tr><td><a href="event-types.md#channel-subscription-created">Channel Subscription Created</a></td><td><code>channel.subscription.new</code></td><td>1</td><td>Fired when a user first subscribes to a channel.</td></tr><tr><td><a href="event-types.md#livestream-status-updated">Livestream Status Updated</a></td><td><code>livestream.status.updated</code></td><td>1</td><td>Fired when a stream's status has been updated. For example, a stream could have started or ended</td></tr><tr><td><a href="event-types.md#livestream-metadata-updated">Livestream Metadata Updated</a></td><td><code>livestream.metadata.updated</code></td><td>1</td><td>Fired when a stream's metadata has been updated. For example, a stream's title could have changed.</td></tr><tr><td><a href="event-types.md#moderation-banned">Moderation Banned</a></td><td><code>moderation.banned</code></td><td>1</td><td>Fired when a user has been banned from a channel.</td></tr><tr><td><a href="event-types.md#kicks-gifted">Kicks Gifted</a></td><td><code>kicks.gifted</code></td><td>1</td><td>Fired when a user gifts kicks to a channel.</td></tr></tbody></table>

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
  "content": "Hello [emote:4148074:HYPERCLAP] [emote:4148074:HYPERCLAP] [emote:37226:KEKW]",
  "emotes": [
    {
      "emote_id": "4148074",
      "positions": [
        { "s": 6, "e": 30 },
        { "s": 32, "e": 56 }
      ]
    },
    {
      "emote_id": "37226",
      "positions": [
        { "s": 58, "e": 75 }
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
