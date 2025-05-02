---
icon: font-case
description: Request body payloads for Webhook API requests
---

# Webhook Payloads

## Chat Message

```json
Headers
- Kick-Event-Type: “chat.message.sent”
- Kick-Event-Version: “1”

{
  "message_id": "unique_message_id_123",
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
  ]
}
```

## Channel Follow

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

## Channel Subscription Renewal

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

## Channel Subscription Gifts

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

## Channel Subscription Created

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

## Livestream Status Updated

#### Livestream Status Updated - Stream started
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

#### Livestream Status Updated - Stream ended
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

## Livestream Metadata Updated

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