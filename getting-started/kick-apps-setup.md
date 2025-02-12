---
icon: rocket-launch
description: Walkthrough on creating a Kick App
---

# App Setup

* To enable you to securely access our APIs via OAuth, you need to create an app with Kick (access instructions on App creation mentioned below).
* Creating this App assigns your app a unique \`ClientID\` and \`ClientSecret\` and a \`redirectURL\` specified by you.
* On successful authorization, Kick will redirect the control back to your \`redirectURL\` specified above with \`code\` to complete with OAuth2.0 Code Grant flow with PKCE.
