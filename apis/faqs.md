---
description: Frequently asked questions about Kick Public API and Kick Apps.
icon: clipboard-question
---

# FAQs

<details>

<summary>What Is App Verification?</summary>

App Verification confirms that an application built on Kick is legitimate and trustworthy.\
Verified apps receive:

* Verified badge on bot account to help distinguish them from impersonators or misleading copycats.
* Increased chat subscription limits (from 1,000 → 10,000 subscriptions)

</details>

<details>

<summary>How do I request verification for my app/bot?</summary>

To request verification, email the Kick Developer Team at developers@kick.com and include:

* Client ID
* App Name
* Whether the bot also requires verification
* Reason for verification request (e.g., large/fast-growing user base, documented impersonation issues, need for expanded subscription capacity)
* Supporting evidence (e.g., public website/Chrome extension, active user metrics, impersonation examples, summary of the legitimate use case)

</details>

<details>

<summary>Can I test the APIs without hosting an app?</summary>

You can test the APIs directly from this UI.&#x20;

To do so:

* You will need your OAuth 2.1 credentials (client ID + secret) found in your Kick Developer settings
* Go to any API endpoint page (example, [V2 Categories](categories.md#get-public-v2-categories)) and click the "Test it" button.
* In the modal that opens, select the Auth Type by clicking the expandable on the top right of the "Authentication" section.

**UserAccessToken**

* Ensure you set your app's "Redirect URL" in your Kick Developer settings to `https://docs.kick.com`
* Fill in your `Client ID`, `Client Secret`
* Set `Use PKCE` to `SHA-256`
* Select the necessary scope for the operation, if needed.
* Click the "Authorize" button on the bottom right of the "Authentication" section.

**AppAccessToken**

* Fill in your `Client ID`, `Client Secret`
* Click the "Authorize" button on the bottom right of the "Authentication" section.

After following the above steps, you should be able to send requests by clicking the "Send" button on the top of the modal.

</details>
