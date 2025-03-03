---
icon: tent-double-peak
---

# Introduction

The Events API allows you to subscribe to real-time updates and event notifications from Kick. With webhooks, you can receive instant data about actions like follows, subscriptions, gifted subscriptions, and chat messages directly to your application. This section guides you through setting up your webhook URL to start receiving these events.

To configure your webhook, head to your [Kick Developer tab](https://kick.com/settings/developer) located in your Account Settings. For an existing application, click "Edit" to access its settings. You’ll find a section labeled "Enable Webhooks" with a switch and a textbox below it:

- **Switch:** Toggle this to "On" to activate webhook event delivery.
- **Webhook URL:** Enter a publicly accessible URL in the textbox. This is where Kick will send POST requests containing event payloads.

**Important:** Your webhook URL must be accessible over the public internet. Localhost URLs (e.g. http://localhost:3000) won’t work unless you expose them using tools like Cloudflare Tunnel, ngrok, or similar services.

Once your webhook is enabled, you’re ready to receive events. Continue to the next section to learn how to verify event payloads using the public key, ensuring they come directly from Kick. Full payload structures and available events are detailed on the [Webhook Payloads](../events/event-types) page.