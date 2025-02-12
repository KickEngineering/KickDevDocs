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
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel"
  },
  "sender": {
    "user_id": 987654321,
    "username": "sender_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "sender_channel"
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
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel"
  },
  "follower": {
    "user_id": 987654321,
    "username": "follower_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "follower_channel"
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
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel"
  },
  "subscriber": {
    "user_id": 987654321,
    "username": "subscriber_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "subscriber_channel"
  },
  "duration": 3.
  "created_at": "2025-01-14T16:08:06Z"
}
```

## Channel Subscription Gifts

```json
Headers
- Kick-Event-Type: “channel.subscription.gifts”
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel"
  },
  "gifter": {
    "user_id": 987654321,
    "username": "gifter_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "gifter_channel"
  },
  "giftees": 
  [
    {
      "user_id": 561654654,
      "username": "giftee_name",
      "is_verified": true,
      "profile_picture": "https://example.com/broadcaster_avatar.jpg",
      "channel_slug": "giftee_channel"
    }
  ],
  "created_at": "2025-01-14T16:08:06Z"
}
```

## Channel Subscription Created

```json
Headers
- Kick-Event-Type: “channel.subscription.new”
- Kick-Event-Version: “1”

{
  "broadcaster": {
    "user_id": 123456789,
    "username": "broadcaster_name",
    "is_verified": true,
    "profile_picture": "https://example.com/broadcaster_avatar.jpg",
    "channel_slug": "broadcaster_channel"
  },
  "subscriber": {
    "user_id": 987654321,
    "username": "subscriber_name",
    "is_verified": false,
    "profile_picture": "https://example.com/sender_avatar.jpg",
    "channel_slug": "subscriber_channel"
  },
  "duration": 1.
  "created_at": "2025-01-14T16:08:06Z"
}
```
