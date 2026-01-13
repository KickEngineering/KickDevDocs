---
icon: ballot
---

# Changelog

## 19/12/2025

* Disabling webhooks for your app will now automatically unsubscribe it from all webhook events it is currently listening to.
* Updating custom tags via the [#patch-channels](apis/channels.md#patch-channels "mention") endpoint should now work correctly.
* The [#get-livestreams](apis/livestreams.md#get-livestreams "mention") endpoint now also returns the broadcaster's profile picture.

## 12/12/2025

* Apps that continually fail to process a webhook event for over a day will now have their app automatically be unsubscribed from receiving that webhook event. More info [here](events/webhook-security.md#disabling-of-webhooks)
* Endpoints returning profile pictures should now return the correct profile pictures
* Endpoints returning categories should now return the correct category details

## 03/12/2025

* Added [Channel Rewards APIs](apis/channel-rewards.md)
* Added [Channel Reward Redemption Updated webhook event](events/event-types.md#channel-reward-redemption-updated)

