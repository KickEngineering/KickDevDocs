---
icon: ballot
---

# Changelog

## 15/01/2025

* Added new [Categories V2 endpoint](apis/categories.md#get-public-v2-categories) which includes improvements like more explicit filters and pagination.
  * As a result, the V1 endpoints for Categories are now deprecated and will be removed in due time.
* The existing [Token introspect endpoint](apis/users.md#post-public-v1-token-introspect) is now deprecated, the [new endpoint](getting-started/generating-tokens-oauth2-flow.md#token-introspect-endpoint) has moved under `/oauth` instead of `/public`&#x20;
* You can now test APIs directly via the Kick Dev Docs UI. See [here](apis/faqs.md#can-i-test-the-apis-without-hosting-an-app) for more information.
* Added [Channel Reward Redemptions APIs](apis/channel-rewards.md#get-public-v1-channels-rewards-redemptions), including:
  * Fetching redemptions by ID, by a particular status and by specific reward
  * Accepting pending redemptions
  * Rejecting pending redemptions

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

